---
name: fluxo-desembolso-base
description: "Montar a previsão de desembolso do que ainda NÃO foi contratado em cada obra da Base Empreendimentos (Mirage Sky Houses, Urbanit Garden), uma pasta Excel por unidade construtiva, com o valor do Sienge e a curva do Prevision, sem nenhum download. Use quando pedirem \"fluxo de desembolso\", \"quanto vai sair por mês\", \"curva de desembolso\", \"manda o fluxo pra Amanda\" ou para atualizar o fluxo depois de mudança de orçamento, de contratação ou de cronograma. Não usar para fluxo de caixa consolidado (com receita) nem para o módulo de Gestão Financeira do Prevision, que está descontratado."
---

# Fluxo de desembolso: Base Empreendimentos

Motor próprio. A Base **não** usa o módulo de Gestão Financeira do Prevision: auditado no
Mirage em 28/08/2026, ele não lê os vínculos da obra, roda sobre orçamento velho e chegou a
pôr R$ 950 mil em dez/2050.

Desde 30/09/2026 não há mais export manual. As três planilhas baixadas do Prevision, o
`montar_fluxo.py`, o `montar_xlsx.py` e o `rodar_local.py` morreram. Se alguém pedir "manda
os exports", a resposta é que não precisa mais.

## As regras que não se negociam

1. **Peso e data vêm do Prevision. Valor vem do Sienge.**
2. **A Amanda recebe a previsão do não contratado**: orçado − comprometido, item a item. O
   comprometido do Sienge já inclui o pago e o adiantamento. O que já foi contratado sai da
   curva, porque a data dele está no contrato e não no cronograma.
3. **Cada unidade construtiva tem seu fluxo**, com curva própria e o mesmo motor. O relatório
   de revisão junta tudo. A Amanda recebe as pastas separadas.
4. **Nominal e corrigido saem lado a lado.**
5. **O prazo de pagamento é por pacote de trabalho**, e quem define é o Vitor.
6. **Relatório e painel consomem este motor, nunca um cálculo paralelo.**
7. **O envio à Amanda é ato do Vitor.** Monta, mostra, e só manda depois do "pode mandar".

## Onde roda

No **Claude Code do notebook do Vitor**. O motor precisa de disco, do token REST do Prevision
(`projetos\construbase\.env`) e da rota `dashboards/cff`, que o conector do Prevision não
expõe. No claude.ai sem o notebook, diga isso e não improvise o fluxo pelos conectores: sairia
exatamente o cálculo paralelo que a regra 6 proíbe.

```
python C:\claude\scripts\fluxo-desembolso\fluxo_desembolso.py --obra mirage|urbanit|todas
```

Leva uns 40 s por obra, porque são uma chamada ao Prevision por serviço (145 no Mirage).

## De onde vem cada número

- **Valor:** a foto diária do robô do Sienge no Supabase (`custo_por_nivel` corrigido pelo CUB
  e `custo_por_nivel_nominal`). As duas fotos precisam ser do mesmo dia, senão o script para.
- **Curva:** `construction-schedule/api/v1/project/{id}/dashboards/cff?reportId=<orçamento>&serviceIds=<serviço>`
  do Prevision. Dá, por item e por pacote, a fração de cada mês na curva prevista. Tem que ser
  **todos** os serviços de `/activities`, porque o `cost` das atividades vem incompleto e deixa
  item de fora.
- **Código:** Prevision usa 2 dígitos por segmento, Sienge 3 (`01.01.00.01` = `01.001.000.001`).

| Obra | Sienge | Prevision | Unidades (Sienge) | CUB |
|---|---|---|---|---|
| Mirage Sky Houses (`MIR`) | 181 | 35782 | 1 Obra (orç. 85446), 3 Condomínio (81357), 2 Indiretos | R16-A |
| Urbanit Garden (`UG`) | 125 | 41750 | 5 Obra E01 (84493), 6 Obra E02 (84494), 2 e 4 Indiretos, 7 e 8 Condomínio | R16-N |

Unidade sem orçamento no Prevision (Indiretos, Condomínio do Urbanit) usa curva própria
linear, que termina quando a etapa atinge 99% do custo. O Condomínio usa os 6 últimos meses.
Isso é premissa, e a planilha diz que é.

## Como o fluxo se forma

- O fluxo começa no mês corrente, ou no seguinte se já passou do dia 15.
- O previsto para o passado que ainda não foi realizado cai no mês de início, como atraso.
- Item com comprometido acima do orçado fica em zero e não tira verba de outro item.
- Serviço concluído com verba sem contratar fica **fora da curva**, como provável sobra, e
  aparece na conferência.
- O prazo desloca a parcela: prazo de 45 dias leva cerca de metade do mês para 1 mês depois e o resto
  para 2.

## O prazo por pacote

Fica em `C:\claude\trabalho\fluxo-desembolso\prazos-<obra>.csv` (`;`, abre no Excel), colunas
`unidade;pacote;prazo_dias;observacao`. O arquivo sobrevive entre rodadas. Pacote novo entra
com o padrão e a observação `padrao - definir`, e o script avisa. Em 30/09/2026 o Vitor deixou
**todos em 0**, de propósito, para o primeiro momento.

Existe uma Matriz de Condição de Pagamento do Urbanit de 28/08
(`260828-UG-PLAN-MatrizCondicaoPagamento-R00.xlsx`, prazo −30, entrada 10%, retenção 10%).
Não está em uso. Só vira prazo se o Vitor mandar.

## A conferência

**Trava**, e aí não se entrega número novo:
- item com verba a contratar e sem vínculo no Prevision (verba fora da curva);
- rateio que não fecha 100% entre os pacotes de um item.

**Avisa:** orçamento do Prevision diferente do Sienge (o Sienge manda), comprometido acima do
orçado, atraso levado ao mês de início, serviço concluído com verba sobrando e prazo padrão a
definir.

O `--forcar` gera mesmo travado. Só com decisão do Vitor, e com o motivo escrito na entrega.

## O que sai

Em `C:\claude\trabalho\fluxo-desembolso\saida\`:
- `AAMMDD-<MIR|UG>-PLAN-FluxoDesembolso-<Unidade>-RXX.xlsx`, uma por unidade. A revisão sobe
  uma a cada dia de rodada (R00, R01...). Rodar de novo no mesmo dia mantém o número e
  substitui a emissão do dia. Abas Leia-me,
  Fluxo mensal (com gráfico), Premissas (amarelo é editável: CUB futuro % a.a. e prazo por
  pacote), A incorrer, A pagar e Itens. As fórmulas são vivas: a Amanda simula prazo sem nós.
- `AAMMDD-BASE-PLAN-FluxoDesembolso-Revisao-R00.html`, o relatório de revisão do Vitor, com
  as duas obras, o gráfico por unidade, a conferência e o que mudou. **Não vai para a Amanda.**
- `trabalho\fluxo-desembolso\rodadas\AAMMDD-<obra>.json`, que a rodada seguinte usa para
  dizer o que mudou.

Unidade sem nada a contratar não gera pasta.

## Arquivar e entregar

O fluxo é documento recorrente, e o histórico entre as emissões é obrigatório. Depois de o
Vitor conferir, rode `C:\claude\scripts\fluxo-desembolso\arquivar-sharepoint.ps1`. Para ver
antes o que ele vai fazer, rode com `-Ensaio`. Ele segue o costume das pastas de planejamento:
- A emissão em vigor fica na raiz de `10-Plan/Fin` da obra:
  - Mirage: `Base Empreendimentos/11-Ob em Andam/Ob-MIR-BASE-Sorriso-MT/10-Plan/FIN`
  - Urbanit: `Base Empreendimentos/11-Ob em Andam/Ob-UG-BASE-Sorriso-MT/10-Plan/Fin`
- Toda emissão anterior da mesma unidade é **movida** para `_Obsoletos/`, nunca apagada. O
  item leva junto o histórico de versões do SharePoint.

O script sobe a emissão nova antes de mover a antiga, então uma falha no meio não deixa a pasta
sem a emissão em vigor. Se já existir em `_Obsoletos` um arquivo com o mesmo nome, ele para:
não sobrescreve evidência.

Ao mostrar ao Vitor, uma linha para cada: a contratar nominal e corrigido por unidade; o pico
e o mês; o que a conferência acusou; o que mudou desde a última rodada; e que a curva do não
contratado é premissa sobre o cronograma, não dado de contrato.

Só depois do "pode mandar" o e-mail sai para a Amanda, uma pasta por unidade.

## O que ainda falta

- **Contratado a pagar pelo vencimento.** Hoje o motor entrega só a faixa do não contratado.
  O contratado e não pago viria dos títulos a pagar do Sienge, pela data de vencimento.
- **Conferir contra o `#desembolso` do ConstruBASE**, que é detector (saídas − títulos a
  pagar) e deveria bater com este motor.
