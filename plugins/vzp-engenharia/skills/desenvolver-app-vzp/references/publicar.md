# Publicar

## Onde

**Cloud Run** (`Dockerfile` + `cloudbuild.yaml`, projeto `central-vzp`, região
`us-central1`) ou **Render**. A publicação é push na branch do gatilho — não há
passo manual, e por isso o que está na branch **é** o que está no ar.

No PowerShell é `gcloud.cmd`, não `gcloud`: com `gcloud` o erro parece falta de
permissão e é política de execução local.

**Segredo novo nasce sem acesso.** Criar o segredo não dá permissão à conta de
serviço; a política IAM sai vazia e o deploy falha falando de contêiner que não
sobe, nunca de permissão. Conceder o acesso é parte de criar o segredo.

## Trabalho longo não espera

Rota que **espera** o trabalho terminar antes de responder leva **502**: o proxy
desiste, e o Node continua e termina o trabalho direito. É a pior forma de
falha — a tela diz "não deu" sobre algo que deu, e quem clicou vai mexer na
credencial, no painel, em tudo menos no lugar certo.

O molde é dispara-e-acompanha: a rota dispara e volta na hora, e o andamento se
lê de estado **persistido** (no ConstruBase é a tabela `fin_sync`, um registro
por escopo, com o erro de cada um). Três detalhes que não são opcionais:

- **Trava contra disparo repetido, no servidor.** Sem ela o segundo clique
  dobra a carga na API de terceiro e traz o 429.
- **`catch` na tarefa solta.** Rejeição não tratada derruba o processo, e o
  trabalho de fundo leva o app no ar junto.
- **O botão mostra em que passo está.** "Sincronizando…" por três minutos é
  indistinguível de travado — e é aí que a pessoa clica de novo.

## Depois de publicar

1. O endereço do JS e do CSS mudou? (senão, ver `pwa.md`)
2. Abrir no celular e instalar pelo botão.
3. Aparelho que já tinha o app aberto se curou sozinho no `controllerchange`?
