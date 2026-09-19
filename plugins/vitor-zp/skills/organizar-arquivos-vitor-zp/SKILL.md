---
name: organizar-arquivos-vitor-zp
description: "Organizar arquivos e pastas pessoais do Vitor Zanchet Pereira (pasta Consultórias/Vitor Z.P). Use ao triar a caixa de entrada 00-Import, classificar, nomear, mover ou localizar documentos pessoais do Vitor. Não usar para VZP, Base ou VLA."
---

# Organizar arquivos — Vitor Z.P (pessoa física)

## Regra de entidade

- Aplicar SOMENTE à pasta pessoal do Vitor: `Consultórias/Vitor Z.P` (Modelo 01 — PF do POP-00.00-Organizacao-Arquivos, rev. vigente R06).
- Não usar a estrutura da VZP Engenharia, da Base Empreendimentos nem das empresas VLA aqui, e não usar esta skill nelas.
- Documento de obra, de cliente PJ ou corporativo não pertence a esta pasta — encaminhar para a empresa correspondente.

## Fontes de verdade (ler antes de classificar)

1. `09-Inst Trab e Pop's/POP-00.00-Organizacao-Arquivos-R06.docx` — estrutura e nomenclatura.
2. `09-Inst Trab e Pop's/Logs/DECISOES-Nomenclatura-Vitor-ZP.md` — decisões já consolidadas do Vitor. **Prevalecem sobre o POP** quando houver conflito, e as "Dúvidas em aberto" não devem ser decididas sozinho.
3. `09-Inst Trab e Pop's/POP-05.00-Vitor-Controle-Financeiro-R03` — para dúvidas de classificação financeira.

## 00-Import é a caixa de entrada do assistente

O Vitor joga arquivo em `00-Import` com **nome livre e formato livre** — sem se preocupar com destino. Classificar é tarefa do assistente, não dele.

1. Triar sem pedir autorização arquivo por arquivo: identificar o conteúdo (abrir/ler o PDF quando o nome não bastar), renomear pelo padrão e **MOVER** para a pasta definitiva. Nunca copiar.
2. `00-Import` vazia significa "nada pendente" — é o único estado correto ao fim da triagem.
3. Caso ambíguo vai para `03-Correção Manual de Arquivos/Analise`, com o motivo registrado. Nunca deixar arquivo parado na caixa.
4. Duplicata exata de documento já arquivado: conferir por hash e descartar. Demais exclusões dependem de autorização do Vitor.
5. Registrar toda triagem em `09-Inst Trab e Pop's/Logs/DECISOES-Nomenclatura-Vitor-ZP.md`, na seção "Triagem de 00-Import": origem, destino, nome aplicado e contexto do documento.
6. Vedado usar `00-Import` como local definitivo ou referenciar caminho de arquivo que esteja nela.

## Estrutura de 1º nível (Modelo 01 — PF)

```
00-Import                    caixa de entrada (transitória)
01-Clientes/<Cliente>        Contratos | Controles | Recibos | Relatorios
02-Compras                   00-Mem Calc Quant | 01-Solicit Comp | 02-Orçamentos |
                             03-Mapa de Cotações | 04-Ord Comp
03-Correção Manual de Arquivos   Analise | Exclusão
04-Curs e Trein              uma subpasta por curso
05-Doc e Cad                 Cadastros | Contratos | Doc Jurid | Doc Pess |
                             Imóveis | Veiculos | Embarcações
06-Est e Patri               balanço patrimonial pessoal, ativos e dívidas
07-Fin                       00-Ord Pagamento | 01-Boletos | 02-Comprov |
                             04-Extratos | 05-Relatorios |
                             06-Investimentos | 07-Simulações | 08-Previsões
08-Fisc                      01-Nfe Entradas | 02-Nfe Saidas |
                             03-Imposto de Renda | 04-Certificados
09-Inst Trab e Pop's         POPs, ITs, Logs, _Obsoletos
10-Mark e Prop               Curriculos | Fotos de Perfil | Videos
11-Saude
12-Viagens
```

A numeração integra o nome da pasta e não pode ser omitida nem reordenada. **O `03` de `07-Fin` não existe mais** (ver regra abaixo) e as irmãs não são renumeradas: `02-Comprov` continua `02` e `04-Extratos` continua `04`.

## Recibo mora com o comprovante (15/09/2026) — revoga `07-Fin/03-Recibos`

Determinação do Vitor, unificando o critério em todo o grupo:

- **Não existe mais `07-Fin/03-Recibos`.** Recibo, comprovante de pagamento e extrato de
  pagamento ficam todos em **`07-Fin/02-Comprov/AA-MM`**. Se a pasta reaparecer, migrar o
  conteúdo e eliminá-la.
- **A distinção é só o código `TIPO` no nome**, nunca a pasta. A pasta não classifica; o
  nome classifica.
- `01-Boletos` e `04-Extratos` **não** são afetados: boleto e extrato bancário continuam em
  pasta própria, cada um com sua regra.
- Não confundir com as outras pastas chamadas `Recibos`, que **permanecem**:
  `01-Clientes/<Cliente>/Recibos` e as de imóvel em `05-Doc e Cad/Imóveis/...`. Aquilo é
  documentação do cliente e do imóvel, não arquivo financeiro do mês.
- Executado em 15/09/2026: 2 recibos movidos para `07-Fin/02-Comprov/26-09`, renomeados de
  `REC` para `RC`, pasta eliminada.

### Fronteiras que costumam gerar erro

- Compras encerra em `04-Ord Comp`. **Ordem de pagamento e comprovante vão para 07-Fin; NF-e vai para 08-Fisc.**
- `07-Fin/07-Simulações` = cenário de algo que **ainda não existe** ("e se..."). `07-Fin/08-Previsões` = projeção de operação que **já existe** (forecast sobre dados reais). `07-Fin/05-Relatorios` = retrato do passado consolidado.
- `10-Mark e Prop` = Marketing e **Propriedade/Propaganda** — nunca proposta comercial.
- Contrato assinado (locação, serviços, compra e venda) vai para `05-Doc e Cad/Contratos`. O recibo das parcelas desse contrato vai para `07-Fin/02-Comprov` — não duplicar.
- Cadastro mestre (contatos, fornecedores, clientes) tem cópia única em `05-Doc e Cad/Cadastros`; os outros setores referenciam, não duplicam.

## Nomenclatura

### Regras gerais

- Sem espaços, acentos, cedilha, vírgula, ponto ou caracteres especiais. Separador entre blocos: hífen simples.
- Data de competência sempre `(AAAA-MM)`; proibido "Abril 2026", "04/2026", "abr-26".
- Versão sempre `REVxx`; proibido "- v2", "- copia", "- 4".
- Nome curto e identificável sem abrir o arquivo.
- Subpastas de mês em `07-Fin`: padrão **`AA-MM`** (ex.: `26-09`), como já praticado em `01-Boletos` e `02-Comprov`. Desde 15/09/2026 este é o padrão de **todo o grupo** — foi daqui e da VZP que ele saiu, e a Base foi alinhada a ele (181 pastas renomeadas de `2604` para `26-04`).
- Não confundir a pasta `AA-MM` (com hífen) com o prefixo `AAMMDD` do nome do arquivo (sem hífen). Hífen na pasta, corrido no arquivo.
- Quatro dígitos que parecem mês podem ser **ano**: `2025` e `2022` são anos. Só é `AA-MM` quando os dois últimos dígitos vão de `01` a `12` — e ainda assim conferir o contexto, porque `08-Fisc/03-Imposto de Renda/2012` é o ano 2012, não dezembro de 2020.

### Padrão codificado (documentos pessoais e cadastrais)

`NATUREZA-NOME-TIPO-QUALIFICADOR-REVxx-(AAAA-MM).ext`

- **NATUREZA** (3 letras): DOC=Doc e Cad · FIN=Financeiro · FIS=Fiscal · PAT=Est e Patri · CMP=Compras · MKT=Mark e Prop · CLI=Clientes · SAU=Saúde · VIA=Viagens · CUR=Curs e Trein
- **NOME**: titular em blocos de 3 letras, um por nome — Vitor Zanchet Pereira → `VIT-ZAN-PER`.
- **TIPO**: sigla do conteúdo (CNH, RGCPF, TITELEIT, CTRVEIC, ESCRIT, PATLIQ, DOSFIN, CTRFIN, DOSFUT).
- Obrigatórios: NATUREZA, NOME, TIPO. Opcionais: QUALIFICADOR, REVxx, (AAAA-MM).
- Exemplos: `DOC-VIT-ZAN-PER-CNH-AB.pdf` · `PAT-VIT-ZAN-PER-PATLIQ-REV04-(2026-08).xlsx`
- POPs mantêm o padrão próprio `POP-NN.NN-...-RXX`.

### Padrão de documentos financeiros (decisão 2026-07-18, TIPO revisado em 15/09/2026)

`AAMMDD-VZP-FIN-<TIPO>-<Beneficiário>-R<valor>.ext`

| TIPO | Conteúdo | Onde mora |
| --- | --- | --- |
| `RC` | Recibo | `07-Fin/02-Comprov/AA-MM` |
| `CP` | Comprovante de pagamento | `07-Fin/02-Comprov/AA-MM` |
| `EX` | Extrato | `07-Fin/04-Extratos/AA-MM` |
| `BOL` | Boleto | `07-Fin/01-Boletos/AA-MM` |

- **`RC` substitui o antigo `REC`** (15/09/2026), para falar a mesma língua da Base e da VZP.
  Não gerar mais `REC`; ao encontrar um, renomear.
- Valor: centavos com hífen no lugar da vírgula e milhar sem ponto — R$1.470,59 → `R1470-59`.
- Recibo emitido pelos vendedores contra o comprador: o **comprador** é o Beneficiário, e o bem + a parcela vão no qualificador. Ex.: `260903-VZP-FIN-RC-Geovanna-Caminhao-P20de68-R1470-59.pdf`.

### Padrão de documentos fiscais

`AAMMDD-VZP-FISCAL-NFe<nº>-<Prestador>.ext`, em subpasta `AAMM`.

> Atenção: as subpastas de `08-Fisc/01-Nfe Entradas` ainda estão em `AAMM` sem hífen
> (`2605`, `2607`). A padronização `AA-MM` decidida em 15/09/2026 foi aplicada às pastas
> **Fin**; estender ao Fisc é decisão em aberto — não renomear por conta própria.

### Exceções de nomenclatura já decididas

- **Extratos bancários** (`07-Fin/04-Extratos/AA-MM`): organizados por lote de download, **mantendo o nome original**. Não renomear; duplicatas entre lotes são esperadas.
- Fotos e capturas de tela usadas só como evidência: nome livre.
- Arquivos legados `DOC-VIT-ZAN-PER-*` em 07-Fin: **não renomear em massa** — a migração para o padrão `AAMMDD-VZP-FIN-*` é dúvida aberta no log de decisões.

## Execução

1. Preservar histórico, revisão e rastreabilidade; nunca sobrescrever arquivo oficial.
2. Vedado arquivar em `.zip`/`.rar` — extrair o conteúdo.
3. Versão superada vai para `_Obsoletos/` na própria pasta, nunca excluída sem autorização.
4. Ao encontrar situação nova que exija decisão de nomenclatura, aplicar o critério mais próximo do POP, registrar em `DECISOES-Nomenclatura-Vitor-ZP.md` e avisar o Vitor no fechamento — não travar a triagem.

## Entrega

Informar: arquivos triados com origem → destino e nome aplicado; pastas criadas; itens enviados para Analise e por quê; decisões de nomenclatura novas registradas no log; e confirmar se `00-Import` ficou vazia.