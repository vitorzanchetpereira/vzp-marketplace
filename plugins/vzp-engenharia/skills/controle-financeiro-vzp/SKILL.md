---
name: controle-financeiro-vzp
description: >-
  Aplicar o POP de Controle e Conciliação Financeira nas finanças da VZP Engenharia. Use em importação de extratos (OFX/CSV), categorização, conciliação de saldo num momento exato (bater saldo numa data), validação previsto × realizado e correção de lançamentos — funciona no app, em Excel ou em qualquer ferramenta. Confirmar a empresa antes de executar e não misturar as finanças com as de outra empresa do grupo.
---

# Controle e Conciliação Financeira — VZP Engenharia

## Regra de empresa

- Aplicar às finanças da **VZP Engenharia**.
- A **metodologia é a mesma** em todo o grupo (este POP); o que muda é a base de dados (contas e cartões desta empresa).
- Confirmar a empresa antes de agir quando não estiver explícita. Nunca misturar lançamentos/saldos de empresas diferentes.

## Fonte obrigatória

Ler integralmente [references/procedimento.md](references/procedimento.md) antes de executar. É o POP de Controle e Conciliação Financeira (mesmo conteúdo do documento oficial `POP-*-Controle-Financeiro-R01.docx`).

## Preparação

1. Reunir os extratos do mês (conta e cartões, em **OFX/CSV**; PDF não é lido — pedir OFX/CSV) e o **saldo real** de cada conta/cartão numa data (gabarito).
2. Confirmar a empresa e o período.

## Execução (resumo — detalhe no procedimento)

1. **Importar** sem duplicar e sem perder repetição legítima; tirar prefixos de pagamento (PAG*/MP*).
2. **Categorizar**; na dúvida, "a classificar". Reclassificar Pix genérico pelo destinatário.
3. **Conciliar num momento exato**: saldo do sistema até a data × saldo real do banco na mesma data (dinheiro − faturas em aberto).
4. **Validar**: bateu o saldo? previsto × realizado por categoria (categoria projetada não atingida + outra estourada = categorização errada).
5. **Corrigir** a causa; resíduo pequeno fecha com lançamento "Ajuste — Diferença" na data.

## Registros

Manter os extratos de origem (importação é refazível) e registrar as conciliações/ajustes no razão.
