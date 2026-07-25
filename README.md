# VZP Engenharia — Marketplace de Skills

Skills compartilhadas do escritório VZP / Base Empreendimentos. Este repositório
contém somente conhecimento operacional, padrões e fluxos reutilizáveis por IAs.

O código dos conectores MCP fica no repositório privado
[`vzp-conectores`](https://github.com/vitorzanchetpereira/vzp-conectores).

## Limite deste repositório

Aqui entram apenas instruções e recursos de skills. Não entram clientes de API,
webhooks, bancos, tokens, infraestrutura ou motores de aplicações.

O marketplace é atualmente público. Skills com nomes, e-mails, IDs internos ou
procedimentos confidenciais devem ser revisadas antes da distribuição externa;
se necessário, o catálogo deve ser separado em uma edição interna privada e uma
edição pública do produto.

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

Adicione este repositório como marketplace local ou de equipe e instale o plugin
`vzp-engenharia`. O catálogo do Codex está em
`.agents/plugins/marketplace.json`.

## Atualizar um padrão

1. Edite o `SKILL.md` correspondente em `plugins/vzp-engenharia/skills/`.
2. Valide a skill.
3. Atualize a versão nos manifestos do Claude e do Codex e nos dois catálogos.
4. Faça commit e push para disponibilizar a atualização.
