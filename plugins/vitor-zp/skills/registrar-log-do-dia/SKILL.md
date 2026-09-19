---
name: "registrar-log-do-dia"
description: "Registrar no cartão Asana \"📊 Log do dia\" o que foi trabalhado numa sessão do Claude (VZP, Base, VLA ou pessoal). Use SEMPRE ao encerrar uma sessão em que houve trabalho real — decisão, entrega, análise, documento, cotação, aprovação, travamento — e também quando o Vitor pedir \"registra no log do dia\". É o único canal que a rotina diária das 18h enxerga."
---

# Registrar no Log do Dia

## Por que esta skill existe

A rotina automática das 18h ("relatorio-diario-produtividade") fecha o dia do Vitor com um cartão no Asana. Ela lê Asana, Zara, WhatsApp e e-mail — mas **NÃO enxerga o trabalho feito dentro do Claude**.

Limitação testada em 15/09/2026, não redescubra:
- `list_sessions` só alcança sessões do modo agente/Cowork com pasta própria.
- **Conversas dentro de um Projeto** (ex.: "Perguntas principais", "Mirage payment and disbursement flow") são **invisíveis**.
- Sessões no claude.ai (web ou celular) são **invisíveis**.
- `read_transcript` não devolve timestamps.
- A pasta de dados do app **não pode ser montada** — bloqueio de design, rota fechada.

Consequência real: em 15/09/2026 a maior entrega do dia (SIOP com todas as notas técnicas prontas, a primeira em execução, e o bloqueio do add-in do Excel) não apareceu em nenhuma fonte automática. Só entrou no log porque o Vitor avisou na mão.

**Por isso: comentar no cartão do dia é o único canal confiável. Esta skill é o que fecha esse buraco.**

## Quando aplicar

Ao ENCERRAR uma sessão em que houve trabalho real, ou quando o Vitor pedir "registra no log do dia".

Conta como trabalho real: decisão tomada, documento ou planilha gerada, análise concluída, cotação montada ou comparada, aprovação dada, contrato redigido ou revisado, projeto compatibilizado, orçamento ou cronograma mexido, travamento identificado, pendência descoberta.

NÃO registrar: pergunta pontual respondida sem entrega, conversa exploratória que não gerou nada, teste de ferramenta.

Na dúvida, registre — o custo de um registro a mais é zero; o de um a menos é o dia ficar sem rastro.

## Como fazer

### 1. Carregue o conector do Asana

ToolSearch: `select:mcp__041aa7e0-a6b3-4dde-a314-66c50d91da3c__buscar_tarefas,mcp__041aa7e0-a6b3-4dde-a314-66c50d91da3c__criar_tarefa,mcp__041aa7e0-a6b3-4dde-a314-66c50d91da3c__comentar_tarefa`

Os nomes curtos (`mcp__Asana__*`) NÃO existem. Workspace = `"Base"`.

### 2. Descubra a data

Bash: `TZ=America/Cuiaba date +"%d/%m/%Y"` e o dia da semana. Cuiabá é UTC−4.

### 3. Ache o cartão do dia

`buscar_tarefas` com texto `"Log do dia"` (traz os concluídos também). Procure `📊 Log do dia — DD/MM/AAAA` de hoje.

Se **não existir**, crie:
- `criar_tarefa` workspace `"Base"`, `projeto_id` `1214320646060633` ("Assistente Claude — Vitor"), `responsavel` `"me"`, `vencimento` = hoje
- nome: `📊 Log do dia — DD/MM/AAAA (dia da semana)`

Se o cartão **já estiver concluído**, comente nele do mesmo jeito — não reabra, não crie um segundo.

### 4. Poste o comentário

`comentar_tarefa` no cartão, neste formato:

```
🧾 Registro de sessão — [assunto] — DD/MM/AAAA HH:MM

✅ O QUE FOI FEITO
• [entregas concretas, com nomes e números reais]

⛔ O QUE TRAVOU
• [o que impediu, e por quê. Omita a seção se nada travou.]

🔴 PRECISA DO VITOR
• [decisões, aprovações, assinaturas pendentes. Omita se não houver.]

🟡 AGUARDANDO TERCEIROS
• [quem, o quê, prazo. Omita se não houver.]

📎 ONDE FICOU
• [arquivos gerados, links, tarefas criadas. Omita se não houver.]
```

## Regras de conteúdo

**Seja específico.** Nomes reais de obra (URBANIT/UG, MIRAGE, VISION, ECOVILLE), fornecedor, contrato, nº de NF, nº de PD, valores, prazos, revisão de projeto (R00, R01, R02). "Avancei no orçamento" não serve. "Fechei o comparativo de hidrossanitário do UG com Chacon, Agnello e RA — falta a RA responder" serve.

**Nunca invente número.** Se não apurou, escreva "não apurado".

**Seja curto.** O cartão recebe vários registros por dia. Bullets, sem parágrafo longo.

## Classificação profissional × pessoal — OBRIGATÓRIA

Regra do Vitor (15/09/2026): o log captura **tudo** que ele fez, inclusive o pessoal. Não omita nem censure assunto pessoal. O que muda é a **marcação**, para que no fechamento (semanal, mensal, trimestral) dê para filtrar e entregar só o profissional.

- Todo item de origem pessoal leva o prefixo literal `[PESSOAL]` no início da linha.
- Itens pessoais vão agrupados **no fim** de cada seção, nunca misturados.

**PROFISSIONAL:** Base Empreendimentos, URBANIT/UG, MIRAGE, VISION, ECOVILLE, VZP Engenharia, VLA (Engenharia, Imobiliária, Patrimonial), Sienge, SIOP/CAIXA, ConstruBASE, Construpoint, Prevision, Asana, fornecedores, contratos, medições, projetos, obra.

**PESSOAL:** família (Vitória, Luciana, bebê), saúde e treino, finanças pessoais (Nubank pessoal, Airbnb, contas da casa), reforma residencial, Canil Lucini, Animalle Pet Care, viagens, processo LATAM, imóveis próprios, carteiras pessoais do PayingLess.

**Na dúvida:** classifique como profissional e marque `[PESSOAL?]`. Não chute.

## Ao terminar

Uma linha ao Vitor dizendo que registrou e em qual cartão. Não repita o conteúdo do comentário — ele já está no Asana.

## Constantes

| item | valor |
|---|---|
| Workspace Asana | `Base` |
| Projeto "Assistente Claude — Vitor" | `1214320646060633` |
| Seção "Concluídas" | `1214320646110297` |
| Fuso | America/Cuiaba (UTC−4) |

Observação: este conector do Asana **não expõe campos personalizados** — "Percentual Executado" não pode ser setado por ferramenta. Não tente.

