---
name: whatsapp-grupos-para-asana
description: >-
  Ler a conversa exportada de um grupo do WhatsApp ("Exportar conversa", .txt ou
  .zip), tirar dela as definições — decisão tomada, prazo, responsável, valor,
  especificação — e criar os cards no Asana depois de mostrar a prévia ao Vitor.
  Use quando ele disser "lê o grupo", "passa o grupo pro Asana", "o que ficou
  definido no grupo da obra", ou mandar um arquivo "Conversa do WhatsApp com…".
  Só funciona no Claude Code do notebook dele (o leitor é script local).
---

# Grupo do WhatsApp → definições no Asana

## Por que é por exportação

O conector do WhatsApp **não alcança grupo**: o número está em Coexistência, e a
Meta bloqueia grupo nesse modo, sem exceção. Ferramenta não oficial que lê grupo
(Baileys, Evolution, "WhatsApp Web automatizado") arrisca banir o número da VZP —
não é caminho. Fica a exportação, que é do próprio WhatsApp e não arrisca nada.

## 1. O Vitor exporta

No celular: grupo → ⋮ (ou nome do grupo, no iPhone) → **Exportar conversa** →
**Sem mídia** → mandar para si (e-mail ou OneDrive). Sem mídia porque o leitor
não vê foto, e o arquivo com mídia passa fácil de 100 MB.

Para achar o arquivo no notebook, procure o mais novo em `Downloads` e no
OneDrive com nome `Conversa do WhatsApp com *` ou `WhatsApp Chat*` (`.txt` ou
`.zip`). Achou mais de um grupo? Pergunte qual. Não achou? Peça o caminho — não
adivinhe.

## 2. Ler só o que é novo

```powershell
python C:\claude\scripts\whatsapp-grupo-ler.py ler "<arquivo>"
```

Devolve JSON com `novas`, o `arquivo` .md da leitura e o comando `para_marcar`.
Leia o `.md` inteiro. Cada mensagem tem número (`#12`) — é por ele que a prévia
cita a origem.

- `novas: 0` → nada novo desde a última vez; diga isso e pare.
- Veio `aviso` → o export começa depois da última marcação: pode haver um buraco
  de mensagens nunca lidas. Diga ao Vitor antes de seguir.
- Primeira vez com um grupo grande: pergunte se quer tudo ou desde uma data
  (`--desde 2026-10-01`). Grupo de obra de um ano inteiro vira centenas de cards
  inúteis.
- iPhone exporta `_chat.txt`: o nome sai do `.zip`. Se o `.txt` vier solto, passe
  `--grupo "Nome do grupo"` — senão o estado fica gravado sob `_chat`.

## 3. Separar o que é definição

Três baldes. Só os dois primeiros viram card.

| Balde | O que é | Exemplo |
| --- | --- | --- |
| **Definição** | decisão tomada, que alguém vai cobrar depois | "Piso do térreo: porcelanato 90×90 cinza, Portobello" |
| **Pendência** | ação com dono (dito ou óbvio) e, se houver, prazo | "João cota esquadria até sexta" |
| **Em aberto** | perguntado e não respondido, ou discussão sem fecho | "Vamos de alumínio ou PVC?" sem resposta |

Regras de leitura:

- **Definição precisa de quem fechou.** "Acho que é melhor X" não é definição;
  "fechado, X" ou o Vitor/dono do assunto concordando é. Na dúvida, vai para
  *Em aberto* — card falso de decisão é pior que card faltando.
- **A última palavra vale.** Se mudou de ideia no meio do fio, o card leva a
  versão final e cita as duas mensagens.
- **Junte o que é um assunto só.** Cinco mensagens sobre o mesmo piso = um card.
- Bom-dia, figurinha, "ok", "👍" sozinho e mídia sem legenda não são nada.
- **Data relativa** ("sexta", "semana que vem") se converte pela data da
  mensagem, não pela de hoje — e o dia da semana se confere no calendário, não
  de cabeça. Fuso de Sorriso, UTC−4.

## 4. Destino no Asana

Pergunte **uma vez por grupo** o workspace (`VZP`, `VLA`, `Base`) e o projeto, e
grave em `C:\claude\trabalho\whatsapp-grupos\destinos.json`:

```json
{ "obra-mirage": { "workspace": "Base", "projeto_id": "120…", "projeto": "Mirage — Obra" } }
```

A chave é o `chave` que o leitor devolve. Nas próximas vezes, leia daí e só
confirme na prévia.

Antes de propor, **procure duplicata**: `buscar_tarefas` com 2–3 palavras do
assunto no workspace. Achou card do mesmo assunto aberto → propor **comentário**
nele em vez de card novo.

## 5. Prévia — obrigatória

`criar_tarefa` **não tem prévia própria**: grava na hora, e sai assinado pela
conta do Vitor. Por isso a prévia é daqui, sempre, e nada é criado sem o "sim"
dele **nesta conversa**.

Mostre uma tabela numerada:

| # | Tipo | Card | Responsável | Prazo | Origem |
| --- | --- | --- | --- | --- | --- |
| 1 | Definição | Piso térreo: porcelanato 90×90 cinza (Portobello) | — | — | #3, 15/10 08:10, João |
| 2 | Pendência | Cotar esquadria em alumínio preto | João | 23/10 | #9, 15/10 08:20, Vitor |
| 3 | Comentar | em "Esquadrias Mirage" (card existente) | | | #11 |

E embaixo, a lista *Em aberto* (não vira card — o Vitor decide).

Ele aprova tudo, por número ("1 e 3"), ou corrige. Corrigiu → mostre de novo só
o que mudou.

## 6. Criar

Para cada item aprovado, `criar_tarefa` com:

- `nome`: curto, começando pelo assunto ("Piso térreo: …"), sem "Definição:".
- `notas`, nesta forma, na voz do assistente (nunca primeira pessoa do Vitor):

  ```
  Definido no grupo de WhatsApp "<grupo>".
  <o que ficou decidido, em 1–3 linhas>

  Origem: #3 15/10/2026 08:10 João Suprimentos — "<trecho curto da mensagem>"
  Registrado pelo assistente do Vitor a partir da exportação da conversa.
  ```

- `responsavel`: só se a pessoa tem conta no Asana e o e-mail é certo
  (`pessoas_do_workspace`). Nome de WhatsApp não é e-mail — sem certeza, deixa
  vazio e o nome vai nas notas.
- `vencimento`: `AAAA-MM-DD`, só se o prazo foi dito.

Mostre os links criados ao final.

## 7. Marcar como lido

Só depois de criar (ou de o Vitor dizer que não precisava de nada), rode o
`para_marcar` que o `ler` devolveu. Se a sessão cair antes, nada se perde: a
próxima leitura devolve as mesmas mensagens, e a busca de duplicata do passo 4
segura card repetido.

```powershell
python C:\claude\scripts\whatsapp-grupo-ler.py estado   # o que já foi lido, por grupo
```

## O que não fazer

- **Não responder no grupo** nem mandar nada a ninguém do grupo por causa da
  leitura. Ler é ler.
- **Não subir o export** para lugar nenhum além de `C:\claude\trabalho\whatsapp-grupos\`:
  são mensagens de terceiros.
- Não criar card de *Em aberto* por conta própria.
- Não confirmar nada dentro de rotina automática — esta skill é sempre com o
  Vitor presente.
