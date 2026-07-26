# Grupo VZP — Marketplace de Skills

Skills internas separadas por empresa. Este repositório contém somente
conhecimento operacional, padrões e fluxos reutilizáveis por IAs.

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
/plugin install base-empreendimentos
```

## Instalar no Codex

Depois de clonar este repositório privado, adicione-o como marketplace de equipe
e instale somente o pacote da empresa em que a pessoa atua:

```text
codex plugin marketplace add <caminho-local-do-vzp-marketplace>
codex plugin add base-empreendimentos@vzp-engenharia-marketplace
```

O catálogo do Codex está em `.agents/plugins/marketplace.json`. Abra uma nova
tarefa depois da instalação para o Codex carregar as skills.

Em qualquer IA, a pessoa precisa primeiro ter acesso ao repositório privado com
sua própria conta GitHub. Não compartilhe tokens pessoais ou uma credencial
única entre a equipe.

## Pacotes por empresa

- `base-empreendimentos`: 5 POPs, 29 ITs técnicas, contratos e skills operacionais.
- `vla-engenharia-arquitetura`: 4 POPs vigentes.
- `vla-imobiliaria`: 4 POPs vigentes.
- `vla-patrimonial`: 1 POP vigente.

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
