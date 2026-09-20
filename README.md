# Grupo VZP — Marketplace de Skills

Skills internas separadas por empresa. Este repositório contém somente
conhecimento operacional, padrões e fluxos reutilizáveis por IAs.

O código dos conectores MCP fica no repositório privado
[`vzp-conectores`](https://github.com/vitorzanchetpereira/vzp-conectores).

## Limite deste repositório

Aqui entram instruções e recursos de skills, e a **declaração** dos conectores
MCP de cada pacote (`.mcp.json`: nome e URL do serviço). Não entram clientes de
API, webhooks, bancos, tokens, infraestrutura ou motores de aplicações.

Um conector só pode ser declarado aqui se autenticar por OAuth, que é o que
o serviço negocia com cada pessoa na hora de vincular. Conector que dependa de
token estático no cabeçalho fica fora — a chave viraria conteúdo do repositório.
É o caso da Central de Comunicação (Zara), que segue como conector
personalizado no claude.ai.

O marketplace é privado e destinado somente à equipe autorizada da VZP. Como as
skills podem conter nomes, e-mails, IDs internos e procedimentos confidenciais,
cada integrante deve receber acesso individual ao repositório e não deve
redistribuir o conteúdo fora das empresas.

## Compatibilidade

- Claude: catálogo `.claude-plugin/marketplace.json`
- Codex: catálogo `.agents/plugins/marketplace.json`
- Outros agentes: skills no formato aberto `SKILL.md`

## Instalar no Claude

No Cowork/Claude, abra **Customize > Plugins > Add marketplace** e informe:

```text
vitorzanchetpereira/vzp-marketplace
```

Pelo Claude Code:

```text
/plugin marketplace add vitorzanchetpereira/vzp-marketplace
/plugin install vzp-engenharia
```

## Instalar no Codex

Depois de clonar este repositório privado, adicione-o como marketplace de equipe
e instale somente o pacote da empresa em que a pessoa atua:

```text
codex plugin marketplace add <caminho-local-do-vzp-marketplace>
codex plugin add vzp-engenharia@vzp-engenharia-marketplace
```

O catálogo do Codex está em `.agents/plugins/marketplace.json`. Abra uma nova
tarefa depois da instalação para o Codex carregar as skills.

Em qualquer IA, a pessoa precisa primeiro ter acesso ao repositório privado com
sua própria conta GitHub. Não compartilhe tokens pessoais ou uma credencial
única entre a equipe.

## Pacotes por empresa

- `vzp-engenharia`: 4 POPs e 30 ITs técnicas vigentes, gestão de contatos e o
  padrão de interface.
- `base-empreendimentos`: 5 POPs, 29 ITs técnicas, contratos, skills operacionais
  e o fechamento trimestral do contrato de gestão.
- `vla-engenharia-arquitetura`: 4 POPs vigentes.
- `vla-imobiliaria`: 4 POPs vigentes.
- `vla-patrimonial`: 1 POP vigente.
- `canil-lucini`: contexto operacional do Canil Lucini e da Animalle Pet Care.

Carteiras pessoais (mesmo POP de Controle e Conciliação Financeira, base de
dados separada por pessoa):

- `vitor-zp`: finanças pessoais de Vitor Zanchet Pereira, mais o contexto
  pessoal e profissional dele, a organização dos arquivos pessoais, a
  verificação antes de enviar e o registro do log do dia.
- `vitoria-lucini`: finanças pessoais de Vitória Lucini.
- `luciana-zanchet`: finanças pessoais de Luciana Zanchet.

Instale apenas os pacotes das empresas em que a pessoa atua. Quando duas
empresas tiverem procedimentos diferentes para o mesmo trabalho, mantenha
skills distintas e nunca aplique silenciosamente a regra de uma empresa à
outra. Se a empresa não estiver explícita no pedido, a IA deve confirmar antes
de executar.

## Atualizar um padrão

1. Identifique a empresa responsável pelo padrão.
2. Edite o `SKILL.md` correspondente dentro do pacote dessa empresa.
3. Mantenha uma única fonte de conteúdo; os manifestos apenas adaptam a instalação para cada IA.
4. Valide a skill e todas as referências.
5. Atualize a versão nos manifestos e catálogos aplicáveis.
6. Faça commit e push para disponibilizar a atualização.

## Conectores

Cada pacote declara em `.mcp.json` os conectores que a empresa usa. Quando o
mesmo serviço serve mais de uma empresa (Asana, Google Contatos, PayingLess),
ele é declarado em cada pacote com **o mesmo nome** — é pelo nome que o cliente
reconhece que é um conector só: abre uma conexão, pede uma autorização, e
autorizar por um pacote vale para todos.

**A tela não mostra assim, e isso assusta.** Em *Personalizar → Conectores* o
`Asana` aparece cinco vezes, uma por pacote que o declara ("Fornecido pelo
plugin Vla imobiliaria", "...Vzp engenharia", e assim por diante). São cinco
linhas para um servidor só. Quem contar linha vai achar que duplicou; não
duplicou.

**Conector de plugin não tem painel de permissão por ferramenta.** Aquela tela
de Aprovar / Requer aprovação / Bloquear existe só para conector da conta
(personalizado e de terceiro), porque nesses a Anthropic guarda o token e
consegue listar as ferramentas do servidor. O de plugin **não existe na conta** —
a API de conectores da conta não o devolve; ele vive na instalação do plugin, e
quem controla o que ele faz é a permissão da sessão. É o preço de migrar para o
marketplace, pago em troca de atualizar num lugar só. Se algum conector precisar
mesmo desse controle fino, o caminho é mantê-lo personalizado de propósito.

**Como se escreve o nome:** primeira letra de cada palavra em maiúscula e `-`
entre elas — `Google-Contatos`, `Construir-Reformar`, `Asana`. Essa chave não é
rótulo: ela vira o endereço da ferramenta (`plugin:vzp-engenharia:Asana`), e por
isso **não aceita espaço** nem acento — só letra, número, `-` e `_`. É também por
ela que passa a autorização, então renomear um conector existente obriga a
autorizar de novo — mudar o nome não é ajuste cosmético, é troca de identidade.

O hífen é escolha de 19/09/2026, depois de o sublinhado ter sido julgado feio na
lista de conectores do claude.ai. Espaço era o pedido e **não existe** aqui;
hífen é o mais perto que a chave chega. Nome de uma palavra só foi descartado
por explicar menos — `Google-Contatos` diz de onde vem o contato, `Contatos`
não.

Um serviço não deve existir ao mesmo tempo aqui e como conector personalizado
no claude.ai. Dois conectores iguais na lista não é cosmético: cada um tem seu
próprio consentimento e seu próprio estado, e a IA escolhe um sem dizer qual.
Numa ferramenta que grava, é a diferença entre gravar com a identidade certa e
com a errada. Declarado aqui, o personalizado sai.
