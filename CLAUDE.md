# vzp-marketplace

O marketplace do grupo: skills, conectores e plugins, separados por empresa.

**Este repositorio e a fonte unica.** Nada de skill como upload na conta do
claude.ai e nada de conector avulso: o que vale esta versionado aqui. Upload
local convive com o do marketplace e fica **congelado** no dia do envio — foi
isso que manteve conector aposentado voltando a aparecer.

Dois catalogos, e os dois precisam da entrada: `.claude-plugin/marketplace.json`
(Claude) e `.agents/plugins/marketplace.json` (Codex). Cada plugin tem
`.claude-plugin/plugin.json`, `.codex-plugin/plugin.json` e, quando declara
conector, `.mcp.json`.

**Nao tem tela**, entao a skill `desenvolver-app-vzp` nao se aplica aqui — mas e
aqui que ela mora (`plugins/vzp-engenharia/skills/desenvolver-app-vzp/`). Mudou
uma regra de tela? Muda neste repositorio, nao na cabeca de quem pede.

**Armadilhas deste repositorio:**

- **Acentuacao por arquivo:** `marketplace.json` usa acentos; `plugin.json` usa
  ASCII. Nao uniformize — respeite o que cada arquivo ja faz.
- **O mesmo servico se declara com o mesmo nome** em todo pacote que o usa (o
  cliente deduplica por nome), e **nao pode existir ao mesmo tempo** aqui e como
  conector avulso no claude.ai.
- **Conector de bearer estatico fica de fora** — e o caso da Zara / Central de
  Comunicacao, que continua como conector avulso de proposito.
- **Apagar o conector avulso e o ULTIMO passo**, depois de o do plugin estar
  autorizado e respondendo. Nunca o primeiro.
