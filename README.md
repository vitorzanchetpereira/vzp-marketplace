# VZP Engenharia — Marketplace de Skills

Skills compartilhadas do escritório VZP / Base Empreendimentos. Este repositório
contém somente conhecimento operacional, padrões e fluxos reutilizáveis por IAs.

O código dos conectores MCP fica no repositório privado
[`vzp-conectores`](https://github.com/vitorzanchetpereira/vzp-conectores).

## Limite deste repositório

Aqui entram apenas instruções e recursos de skills. Não entram clientes de API,
webhooks, bancos, tokens, infraestrutura ou motores de aplicações.

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

Adicione este repositório como marketplace local ou de equipe e instale o plugin
`vzp-engenharia`. O catálogo do Codex está em
`.agents/plugins/marketplace.json`.

Em qualquer IA, a pessoa precisa primeiro ter acesso ao repositório privado com
sua própria conta GitHub. Não compartilhe tokens pessoais ou uma credencial
única entre a equipe.

## Pacotes por empresa

- `vzp-engenharia`: conteúdo legado de contratos, ainda em classificação.
- `base-empreendimentos`: 5 POPs, 29 ITs técnicas e skills operacionais já existentes.
- `vla-engenharia-arquitetura`: 4 POPs vigentes.
- `vla-imobiliaria`: 4 POPs vigentes.
- `vla-patrimonial`: 1 POP vigente.

Instale apenas os pacotes das empresas em que a pessoa atua. Quando duas
empresas tiverem procedimentos diferentes para o mesmo trabalho, mantenha
skills distintas e nunca aplique silenciosamente a regra de uma empresa à
outra. Se a empresa não estiver explícita no pedido, a IA deve confirmar antes
de executar.

## Atualizar um padrão

1. Edite o `SKILL.md` correspondente em `plugins/vzp-engenharia/skills/`.
2. Valide a skill.
3. Atualize a versão nos manifestos do Claude e do Codex e nos dois catálogos.
4. Faça commit e push para disponibilizar a atualização.
