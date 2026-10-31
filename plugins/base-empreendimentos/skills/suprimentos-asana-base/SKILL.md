---
name: suprimentos-asana-base
description: >-
  Regras do projeto Asana de Suprimentos (Base Empreendimentos / URBANIT / MIRAGE)
  e da SOLICITAÇÃO DE COMPRA feita na conversa: toda SC nasce nos dois lados — card
  no projeto Suprimentos da obra certa no Asana E solicitação no Sienge na obra
  certa, amarrados pelo número — e da COTAÇÃO que vem depois (propostas e
  vencedor no Sienge, mapa em PDF no card). Use ao pedir uma compra ("abre uma
  SC", "precisa comprar", "solicita material"), ao cotar ("lança as propostas",
  "faz a cotação", "quem ganhou"), e ao criar ou atualizar tarefas de contratos,
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
   cadastro geral (POP §4): `cadastrar_insumo` com descrição, unidade (o
   símbolo do Sienge), grupo de último nível e conta financeira analítica. O
   **grupo e a conta são de quem pede**: a prévia mostra os insumos parecidos
   e o grupo e a conta que eles usam. Use isso para perguntar, não para
   escolher. Prévia, sim, confirmo. O código que voltar vai para
   `incluir_insumo_na_obra`.
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

## Cotação: no Sienge pelo conector, mapa em PDF no card

Depois da SC, a cotação. Cada lado guarda uma coisa: **o Sienge guarda os
números** (propostas, vencedor — é dali que sai o pedido), **o card guarda a
decisão** (o mapa em PDF da Engenharia, que equaliza escopo e diz por que aquele
fornecedor ganhou). Os dois, sempre — cotação só no PDF deixa o pedido sem
origem no Sienge.

### A ordem

1. **Item autorizado.** Só item autorizado entra na cotação. Se a SC está
   pendente: `autorizar_solicitacao` — e o sim tem de ser de **quem autoriza
   compras na obra**, dito na conversa. Nunca autorize por conta própria.
2. **Fornecedores.** O código de credor de cada um sai de `buscar_credores`
   (nome ou CNPJ; procure **pelo CNPJ**, que nome muda). Fornecedor sem cadastro
   (POP §5): `cadastrar_credor` com os dados do **cartão CNPJ** — razão social,
   endereço, cidade e UF como estão lá (`consultar_cnpj` traz o cartão; não
   complete de cabeça), telefone e e-mail do orçamento ou do contato, e o PIX só
   se o fornecedor mandou e só no CNPJ dele. Prévia, sim, confirmo. Se a tool
   disser que já existe, use o código que ela devolve (inativo se reativa na
   tela). **Cadastrar não qualifica.** Na sequência, `qualificar_fornecedor`
   com o critério do POP §5.1 que de fato vale para ele (visita técnica,
   atendimentos anteriores, PSQ, licença ambiental…). No Sienge da Base, cada
   critério é uma classe do credor. Indicação exige `indicado_por` e
   `justificativa`. Não escolha o critério por ele: se o card ou a conversa não
   dizem, pergunte. A evidência (licença, certidão, foto da visita) vai com
   `anexar_no_credor`. Prévia, sim, confirmo, nas duas.
3. **Criar a cotação**: `criar_cotacao(solicitacao_id, comprador, fornecedores)`.
   `comprador` é o código Sienge de quem compra, e tem de estar cadastrado como
   comprador no Sienge (`usuarios_do_sienge` mostra os códigos; a Suprimentos lança
   as SCs como `SUPRIMENTOS`, o Vitor como `VZP`). Na dúvida, pergunte. Prévia, sim, confirmo. Fornecedor que entrar depois:
   `incluir_fornecedor_na_cotacao`.
4. **Lançar cada proposta**: `cotacao(cotacao_id)` dá o número dos itens **da
   cotação** (não são os da SC) → `lancar_negociacao` por fornecedor, com preço
   unitário por item, frete (`frete_tipo`: nenhum, incluso ou a_pagar), desconto,
   condição de pagamento ("28", "30/60/90") e validade. A proposta vem do PDF ou
   do e-mail do fornecedor: leia os números de lá, **não arredonde nem
   complete**; o que faltar, pergunte. A tool relê e compara o total — total que
   não bate com a proposta é erro de lançamento, não diferença aceitável.
   Renegociação: `nova_rodada=True`.
5. **Mapa no card.** O mapa da Engenharia (PDF) vai anexado ao card da SC
   (`anexar_arquivo`, a partir do SharePoint da obra). O `mapa_de_cotacao` do
   Sienge devolve um **link que só abre com login no Sienge** — não dá para
   anexar direto; ponha o link num comentário do card (`comentar_tarefa`) junto
   com o número da cotação.
6. **Vencedor**: `autorizar_negociacao(cotacao_id, fornecedor_id)` — de novo, só
   com o sim de **quem autoriza compras**. Registre no card, num comentário:
   cotação nº, vencedor, total e o motivo em uma linha (o mesmo do mapa).
7. **Card na mão do próximo passo**: título passa a
   `SC <nº> · COT <nº> - <o que> - <Obra>`.

### Da cotação ao pedido

Com o vencedor autorizado, `gerar_pedido_de_compra(cotacao_id)` gera o pedido
(a API pública não cria; o conector usa a tela nova do Sienge). A prévia mostra
um pedido por fornecedor e obra, com itens, entregas, total e **condição de
pagamento** — confira com o mapa e a proposta antes do sim. Fornecedor com mais
de uma condição: pergunte qual e passe `condicoes`. Sem condição nenhuma: falta
lançá-la na negociação. Se o Sienge recusar por **endereço da obra**,
**apropriação** ou **centro de custo**, nenhum pedido foi criado: diga o que
falta (endereço e apropriação se acertam na tela, por Suprimentos) e repita
depois. O pedido nasce pendente de autorização; o número vai ao card e o título
passa a `SC <nº> · COT <nº> · PC <nº> - <o que> - <Obra>`. O primeiro pedido
gerado assim é teste: peça a Suprimentos para conferir na tela.

## Pedido de compra: análise, autorização, NF e avaliação

Gerado o pedido, o resto anda pelo conector.

1. **Análise no card.** `analise_do_pedido(pedido_id)` devolve um link do PDF
   "Análise do Pedido de Compra" que vale **2 horas**. Anexe já ao card da SC com
   `anexar_arquivo(url=<link>)` — depois de 2 h o link morre e é preciso pedir
   outro. Esse PDF é **interno**: traz os outros pedidos e preços do mesmo
   fornecedor. **Nunca vai ao fornecedor.**
2. **Autorizar ou reprovar.** `autorizar_pedido(pedido_id, observacao)` ou
   `reprovar_pedido(pedido_id, observacao)` — reprovar exige o motivo; a
   observação tem até 300 caracteres. Prévia com os itens, **sim de quem
   autoriza compras** dito na conversa, `confirmo=True`. Nunca autorize por conta
   própria. A tool relê o pedido: só diga "autorizado" com `conferido` verdadeiro.
   Registre no card, num comentário, o número do pedido e a decisão; o título
   ganha o número: `SC <nº> · COT <nº> · PC <nº> - <o que> - <Obra>`.
3. **NF de compra do recebimento** (POP §9), com o documento fiscal em mãos:
   `entregas_do_pedido(pedido_id)` mostra o que está em aberto →
   `lancar_nf_de_compra(pedido_id, numero, serie, data_emissao, entregas,
   valor_total_nf, observacao)`. Número, série e emissão saem **da NF**, como
   impressos; ponha a chave de acesso na `observacao` (`Chave NFe: ...`).
   `entregas` só quando a NF não atende o pedido inteiro: `{"1": 10}` ou
   `{"2/1": 12}`; entrega parcial final, `manter_saldo=False`. Passe sempre
   `valor_total_nf`: total que não bate com o pedido a tool recusa, e a
   diferença se resolve com o fornecedor antes, não na nota. Prévia, sim,
   `confirmo=True`. Se vier `parcial`, a NF ficou em inclusão sem itens — **não
   chame de novo** (criaria outra com o mesmo número); termine ou exclua na tela.
   Se vier `atencao` (NF não consistente), falta completar na tela antes de virar
   título. Na Base, quem lança e completa NF de compra hoje é a Isadora e o
   comprador (Willian): avise quem for. A NF vai anexada ao card (`anexar_arquivo`).
4. **Avaliar a entrega** (POP §9.1), quando o material chega:
   `criterios_de_avaliacao(pedido_id)` lista os cinco critérios (Quantidade,
   Inspeção Técnica, Qualidade, Prazo de Entrega, Dados Fiscais) →
   `avaliar_fornecimento(pedido_id, notas, observacao)`. **Todos** os critérios
   levam nota, e só **0, 5 ou 10**. Nota 0 ou 5 exige na `observacao` o motivo
   **e** a tratativa com o fornecedor. As notas vêm de quem recebeu — não
   preencha 10 por padrão; pergunte. Avaliação errada se corrige com
   `corrigir_ultima=True`. O Sienge não deixa reler a avaliação pela API: a
   resposta vem com `conferido` falso, e a conferência é na tela (Suprimentos >
   Apoio > Relatórios > Fornecedores > Avaliação de Fornecedor).

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

## Contrato novo no Sienge (POP §12.4)

Contratação fechada vira contrato com `criar_contrato`. Ele grava pela tela
"Contrato Rápido" do Sienge, com cabeçalho e itens de uma vez.

O que ele pede:
- **Fornecedor:** o código do credor.
- **Empresa:** o código que a tela mostra (4 = Mirage, 6 = Urbanit).
- **Obra:** o empreendimento (181, 125).
- **Tipo de contrato:** código ou nome, como "mão de obra".
- **Objeto** e **data de término**.
- **Itens.** Cada um leva insumo (precisa estar no orçamento da obra), quantidade, preço de mão de obra e/ou de material, unidade construtiva, item de orçamento de último nível e conta financeira.

Sem número, vai o próximo que o Sienge sugere.

A **apropriação e a conta de cada item são de quem pede**, como na SC. Ajude a achar com `itens_do_contrato` de um contrato parecido da mesma obra, mas não escolha. Cada item leva uma apropriação e uma conta, as duas 100%. Mais do que isso é pela tela.

Depois de criar:
- O contrato nasce **sem autorização**, que é sempre de uma pessoa, pela tela.
- O assinado entra com `anexar_no_contrato`, como abaixo.

Prévia, sim, confirmo.

## Anexos

O conector do Asana anexa: `anexar_arquivo` (um) e `anexar_varios`, com o arquivo
no SharePoint (`sharepoint_item_id`). Arquivo só no disco → suba antes ao
SharePoint da obra. Confira com `listar_anexos`.

**Contrato assinado e propostas também vão ao Sienge** (POP §12.4): com o
arquivo no card, `link_para_baixar` do Asana dá o link e `anexar_no_contrato`
(contrato como `CTS/550`, descrição dizendo o que é: "Contrato assinado",
"Proposta Chacon rev. 2") sobe ao contrato. Um arquivo por chamada; prévia,
sim, confirmo. `anexos_do_contrato` mostra o que já está lá. NF e boletim de
medição são `anexar_na_medicao`, não aqui. Documentos e evidências do **credor**
(qualificação §5, documentos do prestador §12.4, laudos e licenças §13) vão
para o cadastro dele com `anexar_no_credor` (credor pelo código ou CNPJ,
link do `link_para_baixar`, descrição do que é). `anexos_do_credor` lista o
que já está lá.
