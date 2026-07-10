---
name: medicao-asana
description: >-
  Passo a passo aprovado para lançar uma medição (NF + recibo) na coluna Fechamento
  do projeto Asana de Suprimentos. Use ao lançar/registrar medição, pagamento de
  fornecedor, ou NF e recibo no Asana da Base Empreendimentos / URBANIT.
---

# Lançar medição no Fechamento (Asana)

Fluxo validado para lançar uma medição (NF + recibo) na coluna **Fechamento** do
projeto URBANIT - Suprimentos. Replicar em medições futuras.

1. **Conferir valores.** Ler os PDFs (NF-e e recibo) e conferir valores/parcelas —
   não confiar só na memória do usuário. Se houver divergência (ex.: recibo declara
   pagamento já quitado, valores não batem com o total dito), **perguntar antes de
   lançar**.
2. **Salvar arquivos** nas pastas locais da obra no padrão
   `AAMMDD-UG-CATEGORIA-Descricao.pdf` — ver skill **arquivamento-obras**
   (NF → `Fisc/01-Nfe-Recebidas`; recibo → `Fin/Recibos`).
3. **Criar a task** (`create_tasks`). Nome no padrão do quadro: `UG - <descrição>`.
   Definir `due_on` = data do pagamento. Responsável = Duana (ver **suprimentos-asana**).
4. **Corrigir seção/descrição.** A automação joga a task em Solicitações de Compras e
   troca a descrição. Corrigir com `update_tasks` (`add_projects` com project_id +
   section_id de **Fechamento**; reenviar `html_notes`). Ver **suprimentos-asana**.
5. **Anexar os 2 PDFs** pelo navegador (Chrome): abrir a task, `find` o file input
   oculto, `file_upload` com os caminhos locais. Confirmar com `get_attachments`.
6. **Descrição do card** deve deixar claro: total, parcelas, o que já está pago e o
   que vence (com dados PIX quando houver).
