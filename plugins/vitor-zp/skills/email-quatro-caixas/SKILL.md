---
name: email-quatro-caixas
description: >-
  Ler, buscar, responder, enviar, organizar em pastas e triar e-mail nas quatro
  caixas do Vitor (VZP Engenharia, Gmail pessoal, Base e Planejamento) usando as
  ferramentas locais em C:\claude\scripts, sem passar pelo conector do Outlook.
  Use sempre que o pedido envolver e-mail dele — inclusive "manda um e-mail",
  "responde essa mensagem", "o que chegou hoje", "arruma minha caixa". Só
  funciona no Claude Code do notebook dele; não funciona no aplicativo nem no
  celular.
---

# E-mail nas quatro caixas — ferramentas locais

## Onde isto funciona, e onde não funciona

Estas ferramentas rodam **no notebook do Vitor**, pelo Claude Code. Elas
dependem de Python local e de credenciais cifradas com **DPAPI**, que só o
usuário do Windows dele abre, e só naquela máquina.

**Não funcionam no aplicativo (Cowork) nem no celular.** Se o pedido chegar por
ali, diga isso em vez de tentar — não existe caminho por conector para as três
caixas não-Microsoft.

## Por que não usar o conector do Outlook

O conector **remove `<img>` do corpo que devolve — na leitura, não só no envio**.
Conferir e-mail por ele leva a diagnóstico falso: o corpo parece quebrado quando
está inteiro. Para leitura fiel, use as ferramentas abaixo, ou busque o MIME cru
com `graph-token.ps1`.

O conector continua útil para uma busca rápida **só na caixa da VZP**.

## As quatro caixas

| Caixa | Transporte | Observação |
| --- | --- | --- |
| `vitor@vzpengenharia.com.br` | Graph | a padrão; é onde quase todo o trabalho acontece |
| `vitorzanchet@gmail.com` | SMTP/IMAP | pessoal |
| `vitor.baseemp@gmail.com` | SMTP/IMAP | Base Empreendimentos |
| `planejamento@baseempreendimentos.com` | IMAP | **não envia** — a Hostinger bloqueia a saída; use `-Rascunho` |

Registro em `C:\claude\config\contas-email.json`.

## O que rodar

```powershell
# ler e buscar (todas as caixas de uma vez)
C:\claude\scripts\ler-email.ps1
C:\claude\scripts\ler-email.ps1 -Buscar 'medicao'
C:\claude\scripts\ler-email.ps1 -De 'daniela' -Desde '2026-08-01'
C:\claude\scripts\ler-email.ps1 -Caixa 'VZP' -NaoLidas
C:\claude\scripts\ler-email.ps1 -Numero 3          # abre a mensagem inteira

# enviar  (SEM -Enviar é só ensaio)
C:\claude\scripts\enviar-email.ps1 -De 'vitor@vzpengenharia.com.br' `
    -Para 'alguem@exemplo.com' -Assunto 'Assunto' -Html '<p>Corpo</p>'
C:\claude\scripts\enviar-email.ps1 ... -Enviar
C:\claude\scripts\enviar-email.ps1 ... -Rascunho

# responder mantendo o fio
C:\claude\scripts\enviar-email.ps1 -Responder 3 -Html '<p>Texto novo</p>'
C:\claude\scripts\enviar-email.ps1 -Responder 3 -ResponderTodos -Html '...'

# pastas
C:\claude\scripts\pastas-email.ps1 -Caixa 'VZP'
C:\claude\scripts\pastas-email.ps1 -Caixa 'Pessoal' -Criar 'Obras'
C:\claude\scripts\pastas-email.ps1 -Numero 3 -Para 'Obras'

# triagem por regras (SEM -Aplicar é só ensaio)
C:\claude\scripts\aplicar-regras-email.ps1
C:\claude\scripts\aplicar-regras-email.ps1 -Aplicar
```

## Regras de conduta

1. **Nunca enviar sem mostrar antes.** Rode o ensaio, mostre remetente,
   destinatários, assunto e corpo, e espere ele dizer que pode. `-Enviar` é
   irreversível. O padrão dos scripts já é ensaio — mantenha assim.
2. **Nunca aplicar triagem sem mostrar antes.** Idem para `-Aplicar`: espalhar
   mensagem por pasta e sumir com o não-lido é chato de desfazer.
3. **A assinatura é automática.** Cada caixa tem a sua em
   `C:\claude\config\assinaturas\`. Não escreva assinatura no corpo — sairia
   duplicada. Se o script avisar que a assinatura falta, avise ele em vez de
   improvisar uma.
4. **Responder é `-Responder N`, não mensagem nova.** O encadeamento vive em
   `In-Reply-To`/`References`; "RE:" no assunto sozinho não encadeia, e a
   resposta chega solta ao lado da conversa.
5. **Ao conferir se um e-mail saiu certo, não confie no conector** (item acima).

## Antes de dizer que algo falhou

Confira a credencial do Graph:

```powershell
C:\claude\scripts\graph-token.ps1 -Diagnostico
C:\claude\scripts\verificar-contas-email.ps1
```

Se a credencial do Graph tiver expirado, o conserto é ele clicar duas vezes em
`C:\claude\scripts\AUTORIZAR-EMAIL-VZP.cmd` — uma janela normal do Windows,
porque o login precisa de navegador. Não tente autorizar de dentro da sessão.
