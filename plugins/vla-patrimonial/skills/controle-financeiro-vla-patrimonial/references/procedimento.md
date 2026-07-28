# POP — Controle e Conciliação Financeira

**Aplica-se a qualquer controle financeiro** (app PayingLess, Excel ou outro).
A ferramenta muda; a metodologia é a mesma.

---

## 1. Objetivo
Manter o controle financeiro **fiel à realidade** — o razão (lançamentos) sempre
batendo com o saldo real do banco — e detectar/corrigir erros de importação,
categorização e projeção antes que virem bola de neve.

## 2. Princípios (inegociáveis)
1. **Uma verdade só:** existe UM razão (a lista de lançamentos). Dashboard, saldo,
   patrimônio, previsto×realizado são **derivados** — nunca digitados à parte.
2. **Previsão ≠ Realizado:** o que já aconteceu (realizado) e o que é projeção/
   simulação são coisas separadas. Simulação/IA **só mexe em previsão**; o
   realizado é intocável.
3. **Rastreabilidade:** todo número derivado deve levar aos lançamentos que o
   formaram (clicar e chegar no razão).

## 3. Fontes de dados (por mês)
- **Extratos** de cada conta e cada cartão (preferir **OFX/CSV**; PDF não é lido
  por máquina — pedir OFX/CSV).
  - `NU_..._DDMMM_DDMMM` = extrato da **conta corrente** (salário, Pix, boletos).
  - `Nubank_AAAA-MM-DD` = **fatura do cartão** (fechamento naquela data).
- **Saldos reais (gabarito):** um arquivo `_saldos.txt` com o saldo de cada conta
  e a fatura em aberto de cada cartão, numa data:
  ```
  data: AAAA-MM-DD
  Nubank conta: 39540.52
  Cartao Nubank: 8417.70
  Cartao Mercado Pago: 1989.90
  ```

## 4. Importação / lançamento
1. **Não duplicar, não perder:** dedup por **contagem** (multiset). Re-importar o
   mesmo arquivo não duplica; mas 2 compras iguais no mesmo dia (café, transporte)
   contam 2 — repetição legítima é preservada.
2. **Arquivo idêntico** enviado 2x é ignorado.
3. **Prefixos de pagamento** (`PAG*`, `MP*`, `Mercado Pago*`, `PIX`, `TEF`…) são
   removidos antes de identificar o estabelecimento (senão tudo cola no prefixo).
4. **Cartão sem duplicar:** a **compra** entra na data da compra (despesa). O
   **pagamento da fatura** é transferência interna (**valor 0**) — não conta de
   novo. Parcela mensal ≠ compra cheia: cuidar para não lançar as duas.
5. **Confirmação:** só grava após conferir a prévia (quantos novos, categorias).

## 5. Categorização
1. Aprende do **histórico** (estabelecimento → categoria) + **palavras-chave**.
2. **Na dúvida, deixa "a classificar"** — nunca chuta.
3. **Pix genérico** ("Transferência enviada pelo Pix — Fulano") é o maior vilão:
   o histórico tende a jogar tudo numa categoria errada. Reclassificar pelo
   **destinatário**:
   - Energisa/Enel/CPFL → **Luz** · Águas/Sanepar/Sabesp → **Água**
   - DAS/DARF/Imposto → **Impostos e Anuidades** · Unimed/Amil/Drogaria → **Saúde**
   - Contador/Planejar/Assessoria → **Contabilidade**
   - Pessoa física → identificar o motivo (senão "a classificar").

## 6. Conciliação — sempre num MOMENTO EXATO
1. Escolher a **data** (até hoje — nunca no futuro).
2. **Saldo do sistema até a data** = soma acumulada de tudo que já aconteceu
   (realizado, ativo, não-projeção) até aquele dia — **não é o último lançamento**.
3. Comparar com o **saldo real do banco na mesma data** (do `_saldos.txt`).
4. Regra do saldo a comparar: **dinheiro nas contas − faturas de cartão em aberto**
   (a compra já foi lançada como despesa; a fatura ainda não saiu do banco).
5. **Diferente? Investiga** (Seção 8) antes de forçar o número.

## 7. Âncora da auditoria
- A **última conciliação com lançamento** (valor ≠ 0) é o ponto **confiável**:
  dali para trás está certo.
- Conciliações de **valor 0** são apenas marcadores/pré-lançamento — não servem de
  âncora.
- Revisar **da âncora para frente**, lançamento por lançamento, contra o saldo de hoje.

## 8. Validações (detectores de erro)
1. **Bateu o saldo?** Se a diferença é grande → falta importar algo (ex.: a conta
   corrente inteira, ou uma fatura que veio só em PDF). Se é pequena → normal
   (timing de 1–2 dias, arredondamento).
2. **Previsto × Realizado por categoria:** se uma categoria **projetada não foi
   atingida** e **outra estourou**, o dinheiro provavelmente caiu na **categoria
   errada** → reclassificar. Diferença pequena = variação normal, tudo bem.
3. **Sinais invertidos / entradas onde deveria ter saída** = categoria ou sinal errado.

## 9. Correção e ajuste
1. Corrigir a **causa** primeiro (reclassificar, importar o que falta).
2. A diferença **residual pequena** que sobra (ex.: fatura em PDF ainda não lida,
   2 dias de defasagem) fecha com um lançamento **"Ajuste — Diferença +/-"** na
   **data** da conciliação — assim o saldo bate e fica registrado.
3. Ajuste não é para esconder erro grande: se o ajuste é grande, **investigar** (Seção 8).

## 10. Segurança
- **Mostrar antes de apagar ou alterar** dados reais — salvo autorização explícita.
- Manter os arquivos de origem (extratos) — importação é sempre refazível.

## 11. Fluxo mensal (resumo)
1. Salvar os **extratos** + `_saldos.txt` na pasta do mês.
2. **"Atualiza"** → importar (Seção 4) → categorizar (Seção 5).
3. **Conciliar** na data do gabarito (Seção 6) → **validar** (Seção 8).
4. **Corrigir** (Seção 9) → **reportar**: o que entrou, o que bateu, o que ficou
   pendente de definição.

---
*Versão 1 · 2026-07-28 · revisar quando a metodologia evoluir.*
