# VZP Engenharia — plugin do escritório

Empacota o modo de trabalho do escritório VZP / Base Empreendimentos para que toda
a equipe tenha o mesmo padrão sem precisar configurar do zero.

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

## Instalação

Cada pessoa abre o arquivo `vzp-engenharia.plugin`, confirma a instalação e conecta
as ferramentas listadas em `CONNECTORS.md` com a própria conta.

## Manutenção

Para atualizar um padrão, edite o `SKILL.md` da skill correspondente e suba a versão
em `.claude-plugin/plugin.json`.
