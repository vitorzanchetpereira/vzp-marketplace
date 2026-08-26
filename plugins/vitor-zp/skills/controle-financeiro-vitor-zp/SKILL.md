---
name: controle-financeiro-vitor-zp
description: >-
  Aplicar o POP de Controle e Conciliação Financeira nas finanças pessoais de Vitor Zanchet Pereira. Use em importação de extratos (OFX/CSV), categorização, conciliação de saldo num momento exato (bater saldo numa data), validação previsto × realizado e correção de lançamentos — funciona no app PayingLess, em Excel ou em qualquer ferramenta. Confirmar de quem é a carteira antes de executar e não misturar com as finanças de outra pessoa ou empresa do grupo.
---

# Controle e Conciliação Financeira — Vitor Zanchet Pereira

## Regra de carteira

- Aplicar às **finanças pessoais de Vitor Zanchet Pereira**.
- A **metodologia é a mesma** em todo o grupo (este POP); o que muda é a base de
  dados — as contas, os cartões e o razão desta pessoa.
- Nunca misturar com as finanças da **VZP Engenharia** (a PJ dele) nem com as da Vitória ou da Luciana. Na dúvida sobre de quem é o
  extrato ou o saldo, perguntar antes de lançar.
- No **PayingLess** cada pessoa é um razão separado; o seletor de pessoa é o que
  decide onde o lançamento cai. Conferir quem está ativo antes de importar.

## Fonte obrigatória

Ler integralmente [references/procedimento.md](references/procedimento.md) antes de
executar. É o POP de Controle e Conciliação Financeira (mesmo conteúdo do documento
oficial `POP-05.00-Vitor-Controle-Financeiro-R03.docx`, em
`Consultórias\Vitor Z.P\09-Inst Trab e Pop's`).

## Preparação

1. Reunir os extratos do mês (conta e cartões, em **OFX/CSV**; PDF não é lido — pedir OFX/CSV) e o **saldo real** de cada conta/cartão numa data (gabarito).
2. Confirmar de quem é a carteira e qual o período.

## Execução (resumo — detalhe no procedimento)

1. **Importar** sem duplicar e sem perder repetição legítima; tirar prefixos de pagamento (PAG*/MP*).
2. **Conferir duplicidade na janela do mês**: mesmo remetente + mesmo valor (±R$ 0,05) dentro do mesmo mês pede atenção — é aviso, não exclusão automática (item 4.9).
3. **Categorizar**; na dúvida, "a classificar". Reclassificar Pix genérico pelo destinatário.
4. **Conciliar num momento exato**: saldo do sistema até a data × saldo real do banco na mesma data (dinheiro − faturas em aberto).
5. **Validar**: bateu o saldo? previsto × realizado por categoria (categoria projetada não atingida + outra estourada = categorização errada).
6. **Corrigir** a causa; resíduo pequeno fecha com lançamento "Ajuste — Diferença" na data.

## Registros

Manter os extratos de origem (importação é refazível) e registrar as conciliações/ajustes no razão.
