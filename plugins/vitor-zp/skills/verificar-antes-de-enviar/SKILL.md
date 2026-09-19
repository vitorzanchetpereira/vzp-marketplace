---
name: verificar-antes-de-enviar
description: "Antes de qualquer envio por WhatsApp, e-mail ou Asana em nome do Vitor — sempre que ele disser \"manda\", \"envia\", \"dispara\" — verificar a última comunicação feita com aquele contato e só então montar a mensagem."
---

# Verificar antes de enviar

Determinação do Vitor (17/09/2026). Vale para **todo** envio em nome dele: WhatsApp pelo número pessoal, e-mail por qualquer das quatro caixas, comentário em card do Asana.

## A regra

Quando ele disser "manda", "envia", "dispara", "pede pra fulano" — **primeiro verificar a última comunicação com aquele contato**, depois montar o envio. Nunca disparar sem olhar o fio.

A ordem é explicitamente essa: a ordem de enviar **não** dispensa a verificação. Ela dispensa só a pergunta "posso enviar?", não a conferência do histórico.

## O que verificar

1. **A pessoa já respondeu?** Se respondeu e a resposta não foi lida nesta sessão, ler antes — pode mudar o conteúdo do que vai ser enviado, ou tornar o envio desnecessário.
2. **O que já foi mandado?** Não repetir pedido já feito, não reenviar arquivo já entregue, não contradizer instrução anterior. Se o novo envio corrige ou substitui algo, dizer isso na mensagem.
3. **WhatsApp: a janela de 24h está aberta?** Sem mensagem recebida nas últimas 24h, texto livre falha com erro 131047 — tem que ser template aprovado. A verificação do fio já responde isso de graça.
4. **O contato está certo?** Conferir número/e-mail na agenda do Google antes, e não de memória. Nomes se repetem e grafias variam (Byanka/Bianca).

## Como verificar

- **WhatsApp:** `listar_mensagens(contato="55DDNNNNNNNNN")` ou `conversa(contato=...)`. Lista vazia = sem histórico registrado, trate a janela como fechada.
- **E-mail:** `buscar_email(de="...")` e `buscar_email(texto="<nome>")`, sem filtrar caixa — varre as quatro.
- **Asana:** `listar_comentarios(tarefa=...)` antes de comentar.
- **Contato:** `buscar_contato(termo="<nome>")` no Google Contatos.

## Depois de montar

Mostrar ao Vitor **destinatário e texto exato** e esperar o aval — todo envio pelo número pessoal dele exige confirmação explícita, e nunca confirmar sozinho. Em e-mail, chamar `enviar_email` sem `confirmo` devolve a prévia; é ela que se mostra.

Depois de enviar pelo WhatsApp, conferir a entrega real com `status_envio(id_mensagem)` — o retorno do envio é só o aceite da Meta, não a entrega.

## Armadilhas já encontradas

- **Arquivo pelo WhatsApp:** a API da Meta só aceita pdf, doc, docx, ppt, pptx, xls, xlsx, txt, jpeg, png, webp, mp4, 3gpp e áudio. **`.dwg` e `.zip` são recusados** (`application/octet-stream`), dentro ou fora da janela de 24h — a trava é do upload de mídia, não do tipo de mensagem. Para CAD: e-mail, ou ele mesmo manda pelo celular (o aplicativo aceita qualquer tipo).
- **Anexo grande:** enviar por `sharepoint_item_id`, nunca por base64 — base64 falhou num PDF de 17 KB e funcionou num de 14 KB, além de custar contexto. O item id sai de `sharepoint_folder_search` na pasta pai seguido de `read_resource` na URI da pasta; a busca por nome de arquivo não acha arquivo recém-gravado, o índice atrasa alguns minutos.
- **Variável de template:** cada valor em UMA linha. Quebra de linha ou 4+ espaços seguidos fazem a Meta recusar.
- **Conteúdo longo fora da janela:** nenhum template comporta texto estruturado. Gerar um PDF na identidade visual da empresa certa e mandar por `documento_para_analise` com uma linha curta.