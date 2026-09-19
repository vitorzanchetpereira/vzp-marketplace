---
name: fechamento-trimestral-base
description: "Gerar o Dossiê de Evidências e o Anexo de Entregas Fora do Escopo a cada virada de trimestre do contrato de gestão de obras VZP × Base Empreendimentos. Use em fechamento trimestral, apuração de success fee, revisão dos marcos M1–M5 ou quando pedirem o dossiê do trimestre."
---

# Fechamento trimestral — contrato Base Empreendimentos

O contrato de gestão de obras prevê remuneração variável por sucesso, apurada ao fim de cada
trimestre. A apuração se sustenta em dois documentos: o **Dossiê de Evidências** (marcos M1–M5) e o
**Anexo de Entregas Fora do Escopo Contratado**.

## Calendário dos ciclos

| Ciclo | Período |
|---|---|
| T3/2026 | encerrou em 30/08/2026 |
| T4/2026 | até 30/11/2026 |
| T1/2027 | 01/12/2026 a 28/02/2027 |

O inciso III da Cláusula 3ª vale **por trimestre**, não pelo semestre — cada trimestre tem seu
próprio teto.

## Passo 1 — Confirmar antes de produzir

Pergunte, se não estiver claro: qual trimestre, e se o documento sai com layout **Base**
(endereçado ao contratante) ou **VZP** (interno). Nunca aplique o layout de uma empresa em documento
de outra. O *Dossiê de Renegociação de Contrato* é sempre interno da VZP — nunca anexar no Asana nem
enviar à Base.

## Passo 2 — Coletar a série de logs diários

Os cartões `📊 Log do dia — DD/MM/AAAA` vivem no projeto Asana **"Assistente Claude — Vitor"**
(workspace *BASE Empreendimentos*, conta "Base"). A série começou em **22/07/2026**.

```
mcp__asana__buscar_tarefas  texto="Log do dia"  workspace="BASE"  limite=60
```

Armadilhas conhecidas, todas já custaram tempo:

- **O conector cai de sessão a cada poucas chamadas** (`session expired`). Recarregue com
  `ToolSearch select:mcp__asana__listar_comentarios,mcp__asana__obter_tarefa` e siga. Não é falha real.
- **O conteúdo do log fica ora em comentário, ora nas notas.** Depende de qual conector rodou naquele
  dia. **Sempre chame as duas** — `listar_comentarios` e `obter_tarefa` — por cartão. `total: 0` em
  comentários não significa cartão vazio.
- **Cartões duplicados.** Em 31/07/2026 a rotina rodou 4×, com divergências factuais entre as versões.
  Adote o cartão mais detalhado como base e trate os demais como corroboração.
- **Dias sem cartão.** Confira os buracos e declare-os. Em T3/2026 faltaram 23, 24 e 26/07; 02, 03,
  06, 07, 10, 18 e 23/08.
- **Volume.** São ~35 cartões longos por trimestre. Paralelize em 4 subagentes por faixa de datas,
  cada um com instrução de recarregar o conector sozinho.

## Passo 3 — Avaliar os marcos M1–M5

Para cada marco, cruze a tarefa-mãe no Asana com o que os logs registram. A distinção que decide o
nível é sempre a mesma: **a entrega existe e não foi registrada como tarefa**, ou **não existe**?

Quando uma Super Meta depender de terceiro (BPO, projetista, sócio), registre como **dependência
externa formal** em vez de aceitar o desvio na conta do prestador. Quando depender de aprovação
nunca agendada, aponte o gate sem responsável e sem data.

**Não infle.** Um marco que o próprio prestador rebaixa compra credibilidade para os outros quatro;
uma autoavaliação em que tudo sobe é descontada por inteiro. Percentual acima de 100% costuma ser
aparado pelo avaliador e queima o capital do rebaixamento honesto — o excedente de escopo pertence ao
Anexo, não ao percentual.

## Passo 4 — Montar o Anexo em DOIS blocos

Nunca misture os dois: provam coisas diferentes, e juntos derrubam um ao outro.

- **Bloco A — executado.** Atividade realizada, com data, hora e citação literal.
- **Bloco B — atribuído.** Responsabilidade endereçada ao prestador fora do escopo, executada ou não
  (tipicamente a seção "🔴 Precisa de você" dos logs). Prova como a função foi desenhada na prática:
  alçada de compra, atos de RH, assinatura de contrato, emissão de ART.

Categorias do Bloco A: contratação e gestão de pessoal · contratos · projeto (produção, revisão,
decisão) · compras e suprimentos com decisão de valor · condução direta de frente de obra ·
processo e governança · captação e prospecção.

### Regras de honestidade — inegociáveis

1. **Sem citação literal, o item não entra.** Nada de inferência, extrapolação ou agregação de itens
   parecidos.
2. Marque como **ambíguo** o que fica entre auditoria (dentro) e execução (fora) — e diga por quê.
3. **Exclua o que não é Base.** Os logs misturam VZP, VLA, Canil Lucini e assuntos pessoais. O anexo
   cobre apenas Base, Urbanit Garden, MIRAGE e VISION.
4. Rotina de planejamento, cronograma, orçamento e medição é **dentro** do escopo — vira evidência de
   M1/M2, não linha de scope creep.

### Ressalvas obrigatórias no rodapé do anexo

Janela coberta × trimestre real · dias sem cartão · indisponibilidade declarada de conectores nas
apurações (os números são piso, não total) · **a fonte é autodeclaração**, gerada por rotina sob a
conta do próprio prestador, não atestado da contratante — a prova primária (e-mail, mensagem, arquivo
emitido) precisa ser anexada item a item se a apuração for contestada.

Omitir essas ressalvas é o que transforma um anexo forte em um anexo contestável.

## Passo 5 — Identidade visual

**Base Empreendimentos** — vermelho `#BE1E2D`, cinza `#726E67`, carvão `#22201E`, fonte
`'Helvetica Neue', Arial`. O logo está em:

```
Base Empreendimentos/09-Mark e Prop/Assinatura de Email/logo_base_assinatura.png
```

O wordmark é cinza-claro — use sobre faixa escura, não sobre branco. Embuta como data URI.

**VZP Engenharia** — navy `#1F3864`, laranja `#E8610A`, creme `#FFF4EC`.
**VLA** — azul `#1C77BE`, laranja `#FD7606`.

Entregue em HTML autocontido, com `@media print` e tabelas em `overflow-x:auto`.

## Passo 6 — Nomear e arquivar

Padrão: `AAMMDD-SIGLA-CATEGORIA-Descricao.ext`

```
260901-BASE-CONTR-AnexoEntregasForaEscopo-T3-2026.html
```

Destino do contrato de gestão prestado (a Base compra o serviço, logo é Compras):

```
Base Empreendimentos/01-Compras/05-Contratos/VZP Engenharia/
```

Entregue com `SendUserFile` **e** grave na pasta com `device_commit_files`.

## Passo 7 — Registrar

Salve o estado do fechamento em doc do projeto (`project_write`) para o trimestre seguinte partir
daí: percentuais defendidos, evidências usadas, gates travados e o que ficou para o próximo ciclo.

## Ponto em aberto que vale levantar

O dossiê não calcula prêmio — a conversão de nível em valor é regra interna do contratante. Sem
conhecer essa curva, otimizar décimos de nível é trabalho às cegas. Vale perguntar ao responsável
contratual qual é a regra antes de investir horas no dossiê.