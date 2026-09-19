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
reconhece que é o mesmo conector e mostra um só na lista.

Um serviço não deve existir ao mesmo tempo aqui e como conector personalizado
no claude.ai. Dois conectores iguais na lista não é cosmético: cada um tem seu
próprio consentimento e seu próprio estado, e a IA escolhe um sem dizer qual.
Numa ferramenta que grava, é a diferença entre gravar com a identidade certa e
com a errada. Declarado aqui, o personalizado sai.
