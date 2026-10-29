---
name: suprimentos-asana-base
description: >-
  Regras do projeto Asana de Suprimentos (Base Empreendimentos / URBANIT / MIRAGE)
  e da SOLICITAÇÃO DE COMPRA feita na conversa: toda SC nasce nos dois lados — card
  no projeto Suprimentos da obra certa no Asana E solicitação no Sienge na obra
  certa, amarrados pelo número. Use ao pedir uma compra ("abre uma SC", "precisa
  comprar", "solicita material"), e ao criar ou atualizar tarefas de contratos,
  notas fiscais, recibos, medições ou listas de materiais no Asana da Base.
---

# Suprimentos no Asana — Base Empreendimentos

## Solicitação de compra: nasce nos dois lados, na mesma conversa

Regra do Vitor (29/10/2026): **toda solicitação de compra vira card no Asana E
solicitação no Sienge**, na mesma conversa. Card sem SC no Sienge fica fora da
cotação, do pedido e do custo por nível. Não é "depois", não é "quando der".

### Qual obra é qual

| Obra | Projeto no Asana (workspace BASE) | Obra no Sienge (`empreendimento_id`) |
|---|---|---|
| Urbanit Garden | **URBANIT - Suprimentos** `1213779123366734` | **125** — Urbanit Garden |
| Mirage Sky Houses | **MIRAGE - Suprimentos** `1211756343941559` | **181** — Mirage Sky Houses - Obra |

Conferido em 29/10/2026 pelas SCs que já existem (SC 38 → 125, SC 33 → 181).
**Não use** os empreendimentos-irmãos (126/127 "Urbanit Garden - Obra/Indiretos",
182/183 "Mirage - Diretos/Indiretos"): têm o nome parecido e não são onde a compra
nasce. Obra fora desta tabela (Business Hub, pós-obra, Base): **pergunte** antes —
não chute o par.

### Antes de gravar, junte (pergunte só o que faltar)

- **Obra** — decide o par da tabela.
- **Itens**: o que, quantidade, unidade, e a especificação ("2 × 5 L, ref. tal ou
  equivalente").
- **Apropriação de cada item** (planilha e item de último nível do orçamento).
  É **de quem pede, nunca escolhida por mim**. Ajude a achar
  (`planilhas_orcamento`, `itens_planilha`), mas a escolha é da pessoa.
- **Data de necessidade** e o **porquê** (quem pediu no campo, para que serve).

### A ordem

1. **Insumo existe na obra?** `insumos_da_obra(empreendimento_id, busca=...)`.
   Não está → `buscar_insumo_no_cadastro` (pode existir com outro nome) →
   `incluir_insumo_na_obra` (prévia, sim, confirmo). Insumo que não existe nem no
   cadastro geral é cadastro na tela, por uma pessoa — avise e pare esse item.
2. **Mostre UMA prévia com os dois lados juntos**: o card (projeto, título,
   responsável, descrição) e a SC (`criar_solicitacao_de_compra` sem `confirmo`,
   que confere item por item contra o orçamento). Um "sim" só vale para os dois.
3. **Crie o card no Asana** (`criar_tarefa`) — primeiro, porque é dele o link que
   vai na SC. Título `SC - <o que> - <Obra>`; responsável Duana (abaixo).
4. **Crie a SC no Sienge** (`criar_solicitacao_de_compra`, `confirmo=True`), com
   `solicitante` = o código Sienge de quem pede (o do Vitor é `VZP`) e a
   `observacao` levando o porquê **e o link do card**
   (`https://app.asana.com/0/<projeto>/<tarefa>`), não só o nome do card — nome
   muda, link não.
5. **Volte ao card e grave o número**: título passa a `SC <nº> - <o que> - <Obra>`
   (`atualizar_tarefa`) e a descrição ganha a linha `Sienge: SC <nº>, obra <id>`.
   Se o projeto tiver o campo personalizado `SC Sienge` (`campos_do_projeto`),
   preencha também (`definir_campos`).
6. **Confira e diga em uma linha**: número da SC, obra, itens gravados (a tool
   relê), link do card. Itens nascem **pendentes de autorização**
   (`nascer_autorizado=False`) — só `True` se quem pede é quem autoriza e disse.

### Se um lado falhar

- **Card criado, SC recusada** (insumo fora da obra, apropriação inválida):
  não apague o card. Corrija e tente de novo; se não der na conversa, comente no
  card o que falta ("SC no Sienge pendente: <motivo>") para não parecer pronto.
- **SC criada sem itens** (cabeçalho foi, itens não): a resposta da tool traz o
  número; complete com `incluir_itens_na_solicitacao` e grave o número no card
  do mesmo jeito.
- Nunca deixe uma SC solta no Sienge sem card, nem um card que diga ter SC sem ter.

### SC que já existe

Card no Asana sem SC no Sienge (aberto antes da regra, ou pela tela): mesma ordem
a partir do passo 4. SC no Sienge sem card: crie o card e grave o número nele.
Para não duplicar, procure antes: `solicitacoes_de_compra(empreendimento_id=...)`
e `buscar_tarefas` pelo assunto.

## Responsável

Toda tarefa de **contrato, NF, recibo, medição, lista de materiais ou solicitação de
compra** tem como responsável a **Duana Fernanda Hanauer Machado** (Suprimentos).

- `assignee` = Asana user GID `1207878814282741`
- E-mail: `suprimentos.baseemp@gmail.com`
- Vale para URBANIT e MIRAGE.

## Automação do projeto (importante)

No projeto **URBANIT - Suprimentos** (GID `1213779123366734`, workspace BASE
Empreendimentos, Time OBRAS) há uma automação: toda tarefa recém-criada é movida
para a seção **Solicitações de Compras** e tem a descrição sobrescrita por um
template de compra.

**Como contornar ao criar via API/conector:**

1. Ao criar o card, `section_id` e `html_notes` são **ignorados** na criação.
2. Logo depois, corrija:
   - `mover_para_secao` para a seção desejada (ex.: **Fechamento**, GID
     `1213779709755721`);
   - `atualizar_tarefa` reenviando a descrição.
3. A automação **não re-dispara** na edição, então a correção fica.

Para SC, a seção **Solicitações de Compras** é a certa — só a descrição precisa
ser reenviada no passo 5, junto com o número da SC.

## Anexos

O conector do Asana anexa: `anexar_arquivo` (um) e `anexar_varios`, com o arquivo
no SharePoint (`sharepoint_item_id`). Arquivo só no disco → suba antes ao
SharePoint da obra. Confira com `listar_anexos`.
