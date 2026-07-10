---
name: suprimentos-asana
description: >-
  Regras do projeto Asana de Suprimentos (Base Empreendimentos / URBANIT / MIRAGE):
  automação que reposiciona tarefas novas, como corrigir seção e descrição, e quem
  é o responsável. Use ao criar ou atualizar tarefas de contratos, notas fiscais,
  recibos, medições, listas de materiais ou solicitações de compra no Asana.
---

# Suprimentos no Asana — Base Empreendimentos

## Responsável

Toda tarefa de **contrato, NF, recibo, medição, lista de materiais ou solicitação de
compra** tem como responsável a **Duana Fernanda Hanauer Machado** (Suprimentos).

- `assignee` = Asana user GID `1207878814282741`
- E-mail: `suprimentos.baseemp@gmail.com`
- Vale para URBANIT e MIRAGE.

## Automação do projeto (importante)

No projeto **URBANIT - Suprimentos** (GID `1213779123366734`, workspace BASE
Empreendimentos, Time OBRAS) há uma automação: toda tarefa recém-criada é movida
para a seção **Solicitações de Compras** e tem a descrição sobrescrita por um
template de compra.

**Como contornar ao criar via API/conector:**

1. Ao criar o card, `section_id` e `html_notes` são **ignorados** na criação.
2. Logo depois, corrija com `update_tasks`:
   - `add_projects` com `project_id` + `section_id` da seção desejada
     (ex.: **Fechamento**, GID `1213779709755721`).
   - Reenvie o `html_notes`.
3. A automação **não re-dispara** na edição, então a correção fica.

## Anexos

A API do conector Asana **não sobe arquivos**. Anexe pelo navegador (Chrome): abra a
task, localize o file input oculto da task e faça o upload dos PDFs. Confirme com
`get_attachments`.
