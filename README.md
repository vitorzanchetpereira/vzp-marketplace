# VZP Engenharia — Marketplace

Repositorio de plugins do escritorio VZP / Base Empreendimentos.

## Como a equipe instala

No Cowork/Claude: Customize > Plugins > Add marketplace, e informe:

    vitorzanchetpereira/vzp-marketplace

Depois: Browse plugins > VZP Engenharia > Install.

Ou pela linha de comando do Claude Code:

    /plugin marketplace add vitorzanchetpereira/vzp-marketplace
    /plugin install vzp-engenharia

## Como atualizar um padrao

1. Edite o SKILL.md correspondente em plugins/vzp-engenharia/skills/.
2. Suba a versao em plugins/vzp-engenharia/.claude-plugin/plugin.json e aqui no marketplace.json.
3. Faca commit/push. A equipe roda "Update" no marketplace para receber a nova versao.
