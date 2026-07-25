# VZP Engenharia — skills do escritório

Empacota o modo de trabalho do escritório VZP / Base Empreendimentos para que
Claude, Codex e outros agentes usem o mesmo padrão sem configuração duplicada.

## O que vem dentro

- **contexto-escritorio-vzp** — perfil de atuação (engenheiro civil pleno +
  auxiliar administrativo) e diretório de pessoas/áreas.
- **padrao-contratos** — preâmbulo, qualificação das partes, "CEP antes da cidade"
  e dados recorrentes.
- **medicao-asana** — passo a passo para lançar NF + recibo na coluna Fechamento.
- **suprimentos-asana** — automação do projeto de Suprimentos e responsável (Duana).
- **arquivamento-obras** — onde salvar NF/recibo/contrato e o padrão de nome.

## Por papel

- **Suprimentos / Compras** → medicao-asana, suprimentos-asana, arquivamento-obras
- **Contratos / Jurídico** → padrao-contratos, arquivamento-obras
- **Orçamento / Planejamento** → contexto-escritorio-vzp (base para quantitativos e orçamentos)

## Dependências

As skills podem usar ferramentas externas, mas não incorporam código nem
credenciais. Cada pessoa conecta as ferramentas listadas em `CONNECTORS.md` com a
própria conta. Os conectores MCP desenvolvidos pela VZP ficam no repositório
`vzp-conectores`.

## Manutenção

Para atualizar um padrão, edite o `SKILL.md` correspondente, valide a skill e
atualize a versão nos manifestos `.claude-plugin/plugin.json` e
`.codex-plugin/plugin.json`.
