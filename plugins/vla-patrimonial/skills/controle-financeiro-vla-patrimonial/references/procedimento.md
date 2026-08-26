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
- **Extratos** de cada conta e cada cartão (preferir **OFX/CSV** para lançar; PDF
  não é lido linha a linha por máquina — pedir OFX/CSV para a importação).
  - `NU_..._DDMMM_DDMMM` = extrato da **conta corrente** (salário, Pix, boletos).
  - `Nubank_AAAA-MM-DD` = **fatura do cartão** (fechamento naquela data).
  - Alguns bancos exportam o extrato em **`.zip`** direto do app — **extrair antes
    de importar** (o motor/planilha não lê zip).
  - **Olhar TODOS os arquivos da pasta do mês por data de modificação**, não só
    os que vieram dentro de um `.zip` — uma fatura de cartão solta (ex.: fatura
    aberta, ainda não fechou) pode ter sido salva na mesma leva e passar
    despercebida se o olho for só atrás dos zips.
- **Saldos reais (gabarito):** um arquivo `_saldos.txt` com o saldo de cada conta
  e a fatura em aberto de cada cartão, numa data:
  ```
  data: AAAA-MM-DD
  Nubank conta: 39540.52
  Cartao Nubank: 8417.70
  Cartao Mercado Pago: 1989.90
  ```
- **Sem gabarito?** Mesmo não lendo linha a linha, o **PDF traz o resumo do
  período** ("Saldo inicial", "Saldo final do período") — dá para abrir com
  qualquer leitor de PDF (ex.: `pdfplumber`) e usar esses dois números como
  checksum daquela conta, no lugar do `_saldos.txt`.

## 4. Importação / lançamento
1. **Não duplicar, não perder:** dedup por **contagem** (multiset). Re-importar o
   mesmo arquivo não duplica; mas 2 compras iguais no mesmo dia (café, transporte)
   contam 2 — repetição legítima é preservada.
2. **Arquivo idêntico** enviado 2x é ignorado.
3. **Um formato por vez:** o dedup por contagem compara contra o que **já está
   gravado** — ele não enxerga duplicata **dentro do mesmo lote**. Importar o
   CSV e o OFX do **mesmo período juntos numa só leva** faz cada lançamento
   contar 2x (nenhum dos dois "já estava gravado" ainda, então nenhum é
   descartado como repetição). Escolher **um formato só** por extrato (CSV ou
   OFX, tanto faz) e conferir a prévia antes de gravar.
4. **Prefixos de pagamento** (`PAG*`, `MP*`, `Mercado Pago*`, `PIX`, `TEF`…) são
   removidos antes de identificar o estabelecimento (senão tudo cola no prefixo).
5. **Cartão sem duplicar:** a **compra** entra na data da compra (despesa). O
   **pagamento da fatura** é transferência interna (**valor 0**) — não conta de
   novo. Parcela mensal ≠ compra cheia: cuidar para não lançar as duas.
6. **Transferência entre contas da mesma pessoa/empresa** (ex.: conta da
   empresa → conta pessoal do sócio, "é tudo eu mesmo"): tratar **igual a
   pagamento de fatura/RDB** — **zerar o valor nas duas pontas** e marcar como
   transferência interna, sem categoria. Decisão do Vitor (2026-08-01): relatório
   limpo vale mais do que o saldo instantâneo de uma conta batendo sozinho —
   manter valor real (mesmo só na ponta de destino) sempre poluiu o previsto×
   realizado com receita/despesa fantasma. O saldo TOTAL da pessoa (todas as
   contas somadas) não muda de qualquer jeito — só o saldo *daquela conta
   isolada* deixa de bater com o extrato dela sozinha enquanto a outra ponta não
   é conferida junto (mesma limitação que RDB já tinha).
7. **Nunca editar um lançamento por filtro ambíguo** (ex.: `data + conta +
   eh_transferencia_interna=True`): pode casar mais de um lançamento (ex.: um
   RDB do mesmo dia) e corrigir o errado sem avisar. **Sempre localizar e editar
   pelo `id` único** do lançamento antes de gravar.
8. **Confirmação:** só grava após conferir a prévia (quantos novos, categorias).
9. **Parcela duplicada por data diferente (ARMADILHA RECORRENTE — reincidiu em
   ago/2026):** a fatura do cartão data a parcela pela ABERTURA da fatura; um
   lançamento antigo (planilha ou fatura anterior) pode ter datado a MESMA
   parcela pelo aniversário da compra. Datas diferentes → o dedup exato não
   pega, e a prévia mostra como "novo" algo que já está lançado.
   **A janela de conferência é o MÊS, não o dia** (decisão do Vitor,
   2026-08-26): a regra antiga só olhava mesmo valor **no mesmo dia** e por isso
   deixou passar de novo em ago/2026 — os pares caíram em 02/08 contra
   20–30/08. Antes de gravar, para cada linha nova, procurar no razão um
   lançamento **do mesmo mês** com:
   - **mesmo remetente/estabelecimento** — descrição normalizada, já sem os
     prefixos de pagamento (`PAG*`, `MP*`, `PIX`…, item 4.4); e
   - **mesmo valor, com tolerância de ±R$ 0,05** — fatura e planilha arredondam
     a parcela de formas diferentes e o centavo separa o par (visto em ago/2026:
     1.327,35 × 1.327,34 e 318,41 × 318,40; valor exato não pegaria).
   Bateu → **atenção a duplicidade**: não gravar sem conferir. Vale para
   **qualquer** lançamento, não só os marcados "Parcela N/M" (esses são só os
   mais prováveis). É **aviso, não exclusão automática**: repetição legítima
   no mesmo mês existe (dois abastecimentos iguais, duas compras iguais) — a
   linha entra destacada na prévia e quem confirma decide. Repete a cada fatura
   nova até o motor de importação aprender a janela mensal.

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
5. **Fórmula completa (com dinheiro guardado/investido):** o sistema NÃO
   rastreia RDB/investimento como conta própria (é zerado na importação — item
   4.5). Por isso o cheque certo é:
   **dinheiro guardado (RDB etc.) + dinheiro disponível (contas correntes) −
   fatura do cartão em aberto = saldo do sistema.** "Fatura em aberto" = soma
   das compras do cartão **desde o último fechamento até hoje** (não a conta
   inteira do cartão, que acumula todo o histórico).
6. **Diferente? Investiga** (Seção 8) antes de forçar o número.

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
*Versão 4 (R03) · 2026-08-26 · revisar quando a metodologia evoluir.*

### Histórico de revisões
- **R03 (2026-08-26):** a conferência de duplicidade passa de **mesmo dia** para
  **mesmo mês** — mesmo remetente + mesmo valor (±R$ 0,05) dentro do mês pede
  atenção a duplicidade, para qualquer lançamento (não só "Parcela N/M").
  Motivo: as parcelas do cartão duplicaram de novo em ago/2026, com o par
  separado por até 28 dias e, em dois casos, por 1 centavo.
- **R02 (2026-08-01):** correção da R01 — transferência entre contas da mesma
  pessoa/empresa passa a **zerar** (como fatura/RDB), não manter valor real
  (decisão explícita do Vitor: relatório limpo > saldo instantâneo por conta);
  +nunca editar lançamento por filtro ambíguo, sempre por `id`; +armadilha
  recorrente da parcela duplicada por data diferente (fatura vs. planilha) e
  como detectar (mesma descrição+valor, ignorando data); +olhar todos os
  arquivos da pasta por data de modificação, não só os de dentro de `.zip`;
  +fórmula completa de conciliação (guardado + disponível − fatura em aberto =
  saldo do sistema).
- **R01 (2026-08-01):** +zip precisa extrair; +checksum por PDF (saldo
  inicial/final) quando falta `_saldos.txt`; +dedup não cobre duplicata dentro
  do mesmo lote (importar um formato por vez); +transferência entre contas da
  mesma pessoa/empresa (valor real nas duas pontas, categoria só na origem) —
  **substituído na R02**.
- **R00 (2026-07-28):** versão inicial.
