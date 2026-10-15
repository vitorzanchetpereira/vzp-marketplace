---
name: whatsapp-grupos-para-asana
description: >-
  Ler grupos do WhatsApp e levar as definições — decisão tomada, prazo,
  responsável, valor, especificação — ao Asana. Duas entradas: a ROTINA das 18h,
  que coleta pelo WhatsApp Web e cria os cards na seção "Entrada WhatsApp", e o
  pedido avulso ("lê o grupo", "o que ficou definido no grupo da obra", ou um
  arquivo "Conversa do WhatsApp com…"), que mostra a prévia antes de criar. Só
  funciona no computador onde o leitor está instalado (scripts locais).
---

# Grupo do WhatsApp → definições no Asana

## Por que não é pelo conector

O conector do WhatsApp **não alcança grupo**: o número está em Coexistência, e a
Meta bloqueia grupo nesse modo, sem exceção. Sobram dois caminhos, e os dois
terminam no mesmo leitor (`C:\claude\scripts\whatsapp-grupo-ler.py`):

| Entrada | Quem dispara | Prévia |
| --- | --- | --- |
| **Rotina**: `C:\claude\scripts\whatsapp-grupos\coletar.py` lê os grupos da config pelo WhatsApp Web | Agendador do Windows, 18h | **Não**: cria na seção "Entrada WhatsApp" e a equipe revisa lá (decisão do Vitor, 15/10/2026) |
| **Avulso**: exportação da conversa, ou `coletar.py um "<grupo>"` | Alguém nesta conversa | **Sim**, sempre (passo 5) |

O WhatsApp Web roda com o aparelho conectado em `C:\claude\config\whatsapp-web\<conta>`
— hoje o número **11 94337-1041**, que está nos grupos da Base. Só lê: nada se
envia pelo WhatsApp a partir daqui.

## Modo rotina (18h, sem ninguém olhando)

Quem chama é `C:\claude\scripts\whatsapp-grupos\rodar-diario.cmd`, depois de
`coletar.py todos`. Grupos e destinos ficam em `C:\claude\config\whatsapp-grupos.json`.
Para cada grupo da config:

1. `python C:\claude\scripts\whatsapp-grupo-ler.py ler "<arquivo da coleta>"`.
   `novas: 0` → pula.
2. Separe os baldes como no passo 3 e procure duplicata como no passo 4.
3. `criar_secao` "Entrada WhatsApp" no `projeto_id` do grupo (devolve a
   existente se já houver), `criar_tarefa` com o `projeto_id`, e
   `mover_para_secao` para ela. Notas como no passo 6, com a linha extra
   **"Criado automaticamente pela rotina das 18h — revisar e mover para a coluna
   certa, ou apagar."**
4. Os *em aberto* do dia viram **um** card só por grupo, "Em aberto — <grupo> —
   DD/MM", com a lista e os números das mensagens. Sem em aberto, sem card.
5. Rode o `para_marcar`.

Na rotina **não se pergunta nada**, porque não há ninguém para responder. Grupo
fora da config não se lê; grupo sem `projeto_id` se pula e entra no resumo.
Responsável só com e-mail certo. Termine com um resumo curto (grupos, cards,
pulados, erros), que vai para `C:\claude\trabalho\whatsapp-grupos\rotina.log`.

Se a coleta trouxer `historico_sincronizando: true` com `chegou_no_corte: false`,
o aparelho ainda não puxou tudo do celular: crie o que veio, marque, e diga no
resumo que pode faltar mensagem anterior.

## 1. Avulso: exportar (ou coletar)

Grupo que está na config nem precisa de exportação:
`C:\claude\scripts\whatsapp-grupos\.venv\Scripts\python C:\claude\scripts\whatsapp-grupos\coletar.py um "<grupo>"`
e siga do passo 2 com o `arquivo` que ele devolve. Fora disso:

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

O destino de cada grupo está em `C:\claude\config\whatsapp-grupos.json`
(`workspace`, `projeto_id`, `projeto`). Grupo que ainda não está lá: pergunte
**uma vez** o workspace (`VZP`, `VLA`, `Base`) e o projeto, e acrescente o grupo
à config. Assim ele também entra na rotina das 18h.

Antes de propor, **procure duplicata**: `buscar_tarefas` com 2–3 palavras do
assunto no workspace. Achou card do mesmo assunto aberto → propor **comentário**
nele em vez de card novo.

## 5. Prévia — obrigatória no avulso

`criar_tarefa` **não tem prévia própria**: grava na hora, e sai assinado pela
conta de quem conectou o Asana. Por isso, no avulso, a prévia é daqui, sempre,
e nada é criado sem o "sim" **nesta conversa**. (A rotina é a única exceção, e
só porque escreve numa seção de triagem.)

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
- No avulso, não criar card de *Em aberto* por conta própria (na rotina, é o
  card único do passo 4 do modo rotina).
- A rotina só **cria** na seção "Entrada WhatsApp". Não mexe, não comenta, não
  conclui nem apaga card existente: duplicata, na rotina, se pula e entra no
  resumo.
- Não abrir o WhatsApp Web **sem janela** (headless): em 15/10/2026 isso
  desconectou o aparelho. O `coletar.py` já abre com janela fora da tela.
