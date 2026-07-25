# VZP Engenharia — conteúdo em classificação

Este pacote mantém temporariamente skills que ainda não foram atribuídas com
segurança a uma única empresa.

## O que vem dentro

- **padrao-contratos** — conteúdo atual menciona VZP e Base Empreendimentos e
  precisa ser separado após validação dos POPs de cada empresa.

## Por papel

- **Contratos / Jurídico** → padrao-contratos

Não aplicar este conteúdo sem confirmar primeiro qual empresa rege o trabalho.

## Dependências

As skills podem usar ferramentas externas, mas não incorporam código nem
credenciais. Cada pessoa conecta as ferramentas listadas em `CONNECTORS.md` com a
própria conta. Os conectores MCP desenvolvidos pela VZP ficam no repositório
`vzp-conectores`.

## Manutenção

Para atualizar um padrão, edite o `SKILL.md` correspondente, valide a skill e
atualize a versão nos manifestos `.claude-plugin/plugin.json` e
`.codex-plugin/plugin.json`.
