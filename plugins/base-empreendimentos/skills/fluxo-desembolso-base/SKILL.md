---
name: fluxo-desembolso-base
description: "Montar a previsão de desembolso do que ainda NÃO está lançado no Sienge em cada obra da Base Empreendimentos (Mirage Sky Houses, Urbanit Garden): o que falta executar no cronograma do Prevision menos os títulos em aberto e o adiantamento, uma pasta Excel por unidade construtiva, sem nenhum download. Use quando pedirem \"fluxo de desembolso\", \"quanto vai sair por mês\", \"curva de desembolso\", \"manda o fluxo pra Amanda\" ou para atualizar o fluxo depois de mudança de orçamento, de contratação ou de cronograma. Não usar para fluxo de caixa consolidado (com receita) nem para o módulo de Gestão Financeira do Prevision, que está descontratado."
---

# Fluxo de desembolso: Base Empreendimentos

Motor próprio. A Base **não** usa o módulo de Gestão Financeira do Prevision: auditado no
Mirage em 28/08/2026, ele não lê os vínculos da obra, roda sobre orçamento velho e chegou a
pôr R$ 950 mil em dez/2050.

Desde 30/09/2026 não há mais export manual. As três planilhas baixadas do Prevision, o
`montar_fluxo.py`, o `montar_xlsx.py` e o `rodar_local.py` morreram. Se alguém pedir "manda
os exports", a resposta é que não precisa mais.

## As regras que não se negociam

1. **A base é o cronograma atualizado do Prevision**, que já vem com valor. Por item:
   **falta executar** = valor no cronograma × (100% − realizado).
2. **A Amanda recebe o que falta lançar**: falta executar − títulos em aberto − adiantamento a
   abater, item a item, sem ficar negativo. O que tem título (nota, boleto, provisão de contrato
   ou de pedido) já está no contas a pagar dela. **Contrato sem título lançado entra**, porque
   não aparece em lugar nenhum do fluxo do financeiro. Regra do Vitor em 01/10/2026; o pago do
   passado **não** se subtrai, porque já é do serviço que o cronograma deu como executado (só o
   adiantamento cobre serviço futuro).
3. **Cada unidade construtiva tem seu fluxo**, com curva própria e o mesmo motor. O relatório
   de revisão junta tudo. A Amanda recebe as pastas separadas.
4. **Nominal e corrigido saem lado a lado.**
5. **O prazo de pagamento é por pacote de trabalho**, e quem define é o Vitor.
6. **Relatório e painel consomem este motor, nunca um cálculo paralelo.**
7. **O envio à Amanda é ato do Vitor.** Monta, mostra, e só manda depois do "pode mandar".

## Onde roda

No **Claude Code do notebook do Vitor**. O motor precisa de disco, do token REST do Prevision e da
credencial de API do Sienge (os dois no `projetos\construbase\.env`), do `bulk-data` do Sienge e da rota `dashboards/cff`, que o conector do Prevision não
expõe. No claude.ai sem o notebook, diga isso e não improvise o fluxo pelos conectores: sairia
exatamente o cálculo paralelo que a regra 6 proíbe.

```
python C:\claude\scripts\fluxo-desembolso\fluxo_desembolso.py --obra mirage|urbanit|todas
```

Leva uns 40 s por obra: uma chamada ao Prevision por serviço (145 no Mirage) e uma ao Sienge.

## Por que mudou em 01/10/2026

Até 30/09 a base era a verba não contratada (orçado − comprometido). Errava nos dois sentidos,
e o Vitor viu na revisão: punha saída em **fundação**, concluída, só porque sobrou verba; e
tirava a **estrutura**, contratada mas sem título lançado. No Mirage, pela regra nova, a
Infraestrutura vai a zero e a Supraestrutura volta com R$ 1,0 mi (2,2 a executar − 1,2 lançado).

## De onde vem cada número

- **Quanto falta executar:** valor e realizado do item no cronograma do Prevision (abaixo).
- **Já lançado:** o saldo em aberto das parcelas a pagar da obra, no
  `bulk-data/v1/outcome` do Sienge, **uma chamada por obra**, rateado por unidade e item pelo
  `buildingsCosts`. Previsões (PCT, PPC, PRV…) contam: estão no contas a pagar. Credencial
  `SIENGE_*` do `projetos\construbase\.env`. E o adiantamento a abater
  (`upfrontPayment − upfrontPaymentCompensation`) da foto do Custo por Nível.
- **Corrigido:** o falta executar vezes o fator do item (orçado corrigido ÷ nominal) da foto
  diária do robô do Sienge no Supabase (`custo_por_nivel` e `custo_por_nivel_nominal`, do
  mesmo dia, senão o script para). O título já está em reais de hoje e sai igual nos dois.
- **Curva:** `construction-schedule/api/v1/project/{id}/dashboards/cff?reportId=<orçamento>&serviceIds=<serviço>`
  do Prevision. Dá, por item e por pacote, a fração de cada mês na curva prevista. Tem que ser
  **todos** os serviços de `/activities`, porque o `cost` das atividades vem incompleto e deixa
  item de fora.
- **Código:** Prevision usa 2 dígitos por segmento, Sienge 3 (`01.01.00.01` = `01.001.000.001`).

| Obra | Sienge | Prevision | Unidades (Sienge) | CUB |
|---|---|---|---|---|
| Mirage Sky Houses (`MIR`) | 181 | 35782 | 1 Obra (orç. 85446), 3 Condomínio (81357), 2 Indiretos | R16-A |
| Urbanit Garden (`UG`) | 125 | 41750 | 5 Obra E01 (84493), 6 Obra E02 (84494), 2 e 4 Indiretos, 7 e 8 Condomínio | R16-N |

Unidade sem orçamento no Prevision (Indiretos, Condomínio do Urbanit) usa **verba − pago −
títulos em aberto** (decisão do Vitor, 01/10) e curva própria linear, que termina quando a etapa
atinge 99% do custo. O Condomínio usa os 6 últimos meses. Isso é premissa, e a planilha diz que é.

## Como o fluxo se forma

- O fluxo começa no mês corrente, ou no seguinte se já passou do dia 15.
- O previsto para o passado que ainda não foi realizado cai no mês de início, como atraso.
- O já lançado cobre a execução **mais próxima** da curva; o que falta lançar é o fim dela.
- Item com lançado acima do que falta executar fica em zero e não tira de outro item.
- Serviço concluído não gera saída, sobre verba ou não.
- O prazo desloca a parcela: prazo de 45 dias leva cerca de metade do mês para 1 mês depois e o resto
  para 2.

## O prazo por pacote

Fica em `C:\claude\trabalho\fluxo-desembolso\prazos-<obra>.csv` (`;`, abre no Excel), colunas
`unidade;pacote;prazo_dias;observacao`. O arquivo sobrevive entre rodadas. Pacote novo entra
com o padrão (0) e a observação `padrao - definir`, e o script avisa. Em 30/09/2026 o Vitor deixou
**todos em 0**, de propósito, para o primeiro momento.

Existe uma Matriz de Condição de Pagamento do Urbanit de 28/08
(`260828-UG-PLAN-MatrizCondicaoPagamento-R00.xlsx`, prazo −30, entrada 10%, retenção 10%).
Não está em uso. Só vira prazo se o Vitor mandar.

## A conferência

**Trava**, e aí não se entrega número novo:
- item do Sienge sem vínculo no Prevision e com verba ainda não paga nem lançada;
- rateio que não fecha 100% entre os pacotes de um item.

**Avisa:** valor do cronograma diferente da verba do Sienge (o cronograma manda), lançado acima
do que falta executar, **título vencido em aberto** (costuma ser provisão esquecida), atraso
levado ao mês de início e prazo padrão a definir.

O `--forcar` gera mesmo travado. Só com decisão do Vitor, e com o motivo escrito na entrega.

## O que sai

Em `C:\claude\trabalho\fluxo-desembolso\saida\`:
- `AAMMDD-<MIR|UG>-PLAN-FluxoDesembolso<Unidade>-RXX.xlsx` (ex.: `260930-UG-PLAN-FluxoDesembolsoObraE01-R00.xlsx`), uma por unidade. A revisão sobe
  uma a cada dia de rodada (R00, R01...). Rodar de novo no mesmo dia mantém o número e
  substitui a emissão do dia. Abas Leia-me,
  Fluxo mensal (com gráfico), Premissas (amarelo é editável: CUB futuro % a.a. e prazo por
  pacote), A incorrer, A pagar e Itens. As fórmulas são vivas: a Amanda simula prazo sem nós.
- `AAMMDD-BASE-PLAN-FluxoDesembolsoRevisao-R00.html`, o relatório de revisão do Vitor, com
  as duas obras, o gráfico por unidade, a conferência e o que mudou. **Não vai para a Amanda.**
- `trabalho\fluxo-desembolso\rodadas\AAMMDD-<obra>.json`, que a rodada seguinte usa para
  dizer o que mudou.

Unidade sem nada a lançar não gera pasta.

## Arquivar e entregar

O fluxo é documento recorrente, e o histórico entre as emissões é obrigatório. Depois de o
Vitor conferir, rode `C:\claude\scripts\fluxo-desembolso\arquivar-sharepoint.ps1`. Para ver
antes o que ele vai fazer, rode com `-Ensaio`. Ele segue o POP-04.00 da Base, R09 (§4.3.2 e §6.8):
- A emissão em vigor fica na raiz de `10-Plan/03-Fluxo Desembolso` da obra:
  - Mirage: `Base Empreendimentos/11-Ob em Andam/Ob-MIR-BASE-Sorriso-MT/10-Plan/03-Fluxo Desembolso`
  - Urbanit: `Base Empreendimentos/11-Ob em Andam/Ob-UG-BASE-Sorriso-MT/10-Plan/03-Fluxo Desembolso`
- Toda emissão anterior da mesma unidade é **movida** para `_Obsoletos/`, nunca apagada. O
  item leva junto o histórico de versões do SharePoint.

O script sobe a emissão nova antes de mover a antiga, então uma falha no meio não deixa a pasta
sem a emissão em vigor. Se já existir em `_Obsoletos` um arquivo com o mesmo nome, ele para:
não sobrescreve evidência.

Ao mostrar ao Vitor, uma linha para cada: falta executar, já lançado e a lançar (nominal e
corrigido) por unidade; o pico e o mês; o que a conferência acusou (título vencido em aberto
sobretudo); o que mudou desde a última rodada; e que a curva é a do cronograma, não a do contrato.

Só depois do "pode mandar" o e-mail sai para a Amanda, uma pasta por unidade.

## O que ainda falta

- **Prazo por pacote.** Todos em 0 até o Vitor definir; pacote novo também nasce em 0.
- **Conferir contra o `#desembolso` do ConstruBASE**, que é detector (saídas − títulos a
  pagar) e deveria bater com este motor.
