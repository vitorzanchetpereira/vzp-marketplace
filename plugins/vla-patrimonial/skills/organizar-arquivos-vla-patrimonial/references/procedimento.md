# Referência operacional

- Empresa: VLA Patrimonial
- Documento vigente: `POP-01.00-VLA-Organizacao-Arquivos-R01.docx`
- Origem: pasta mestra de POPs/ITs da empresa
- Regra: ao existir nova revisão, reextrair e revalidar esta referência antes do uso.

> Esta referência preserva o conteúdo operacional extraído do documento fonte. Em caso de dúvida, conflito, perda de formatação ou informação incompleta, consultar o arquivo original vigente.

VLA PATRIMONIAL

Gestão e Planejamento Patrimonial Familiar

PROCEDIMENTO DE ORGANIZAÇÃO DE ARQUIVOS E PASTAS

POP-01.00 — Organização de Arquivos — Rev. 01

Estrutura de Pastas, Subpastas e Nomenclatura por Ativo Patrimonial

| Campo | Conteúdo |
| --- | --- |
| Código | POP-01.00 — VLA Patrimonial |
| Revisão | R01 (substitui R00 de 08/05/2026) |
| Data de emissão | 21/07/2026 |
| Elaborado por | Vitor Zanchet — Gestão Patrimonial |
| Alinhamento | Padrão-mestre do Grupo: Base R06 / VZP; espelha o POP-04 R01 da Imobiliária |
| Aplicação | Microsoft SharePoint / OneDrive — VLA Patrimonial |

Nota de revisão. A R01 mantém o mapa de pastas do R00 e acrescenta o que faltava: a estrutura interna padrão de cada ativo (fazenda, imóvel urbano e veículo), a governança (00-Import, _Obsoletos, Correção Manual, Logs) e a nomenclatura alinhada ao padrão-mestre do Grupo (hífen, Title Case, sem acento). Validada no exemplo FAZ JOARES.

## Sumário

## 1. Objetivo

Definir a estrutura padronizada de pastas, subpastas e a nomenclatura de arquivos do repositório da VLA Patrimonial, garantindo rastreabilidade por ativo, integridade documental e aderência ao padrão único do Grupo (Base/VZP). Aplica-se a fazendas, imóveis urbanos, veículos, documentos da família e estudos de sucessão.

## 2. Estrutura raiz do repositório

| # | Módulo | Conteúdo |
| --- | --- | --- |
| 00 | Import | Caixa de entrada geral (arquivos a triar) |
| 01 | Bens e Imóveis Vendidos | Histórico de ativos alienados (rastreabilidade) |
| 02 | Bens e Imóveis em Posse | Fazendas, imóveis urbanos e veículos ativos |
| 03 | Correção Manual de Arquivos | Triagem humana: Análise e Exclusão |
| 04-08 | Curs / Doc e Cad / Est / Fin / Fisc | Áreas de apoio (cursos, documentos da família, estratégia, financeiro, fiscal) |
| 09 | Inst Trab e POPs | POPs, instruções, normas e Logs |
| 10-12 | Mark / RH / Soft | Marketing, RH e softwares |

## 3. Estrutura interna por ativo (a novidade da R01)

Cada ativo em posse recebe as subpastas-padrão abaixo, com prefixo numérico. A subpasta 00-Import é a caixa de entrada do ativo e _Obsoletos guarda versões superadas.

### 3.1 Fazenda / imóvel rural

| # | Subpasta | Conteúdo |
| --- | --- | --- |
| 01 | Matricula e Escritura | Matrícula, escritura, registro |
| 02 | CAR e SICAR | CAR, SICAR, SIMCAR, retificações |
| 03 | CCIR e ITR | CCIR, ITR, CND rural |
| 04 | Georreferenciamento | Mapas, faixas, memoriais, DWG |
| 05 | Contratos | Compra, arrendamento, parceria, comodato, cessão |
| 06 | Creditos e Controles | Controle de crédito, tabelas, planilhas |
| 07 | Licenciamento Ambiental | IBAMA, INDEA, SEMA, autorização de queima, APF |
| 08 | Documentos e Cadastros | Dados bancários, requerimentos, procurações |
| 09 | Rendimentos e Arrendamento | Comprovantes e relatórios de arrendamento |
| 10 | Fotos | Imagens da propriedade |

### 3.2 Imóvel urbano

| # | Subpasta | Conteúdo |
| --- | --- | --- |
| 01 | Matricula e Escritura | Matrícula, escritura, registro |
| 02 | IPTU | Carnês e comprovantes por ano |
| 03 | Contratos | Compra, venda, locação, comodato |
| 04 | Notificacoes e Processos | Notificações, protocolos, ações |
| 05 | Documentos | Certidões, cadastros, correspondências |
| 06 | Projetos e Plantas | Projetos, plantas, croquis |
| 07 | Fotos | Imagens do imóvel |

### 3.3 Veículo

| # | Subpasta | Conteúdo |
| --- | --- | --- |
| 01 | Documento | CRLV, CRV, DUT |
| 02 | Compra e Venda | Nota fiscal, recibo, contrato |
| 03 | Licenciamento e IPVA | Licenciamento anual, IPVA, taxas |
| 04 | Multas e Infracoes | Autuações, recursos |
| 05 | Manutencao | Ordens de serviço, revisões, notas |
| 06 | Seguro | Apólice, sinistros |
| 07 | Fotos | Imagens do veículo |

## 4. Convenção de nomenclatura de arquivos

- Separador hífen (-); sem espaços/acentos/cedilha nos blocos de código; descritor em Title Case (espaços permitidos).

- Datas: AAMMDD (dia), AAMM (mês), AAAA (ano). Revisão ao final: R00, R01…

Estrutura: [Sigla]-[TIPO]-[Descricao]-[data]-RXX.ext

| Sigla | Tipo | Sigla | Tipo |
| --- | --- | --- | --- |
| CTR | Contrato | MAT | Matrícula |
| DEC | Declaração / ITR | MAP | Mapa / georreferenciamento |
| REL | Relatório / planilha | DOC | Documento / certidão / cadastro |
| REC | Recibo / comprovante | PRO | Proposta / orçamento |
| ATA | Ata / ação judicial | FOT | Fotografia |

Exemplo aplicado (FAZ JOARES): Joares-CTR-Compra Talhao 07 v1.doc · Joares-MAP-Eliana Faixas 01 a 18.dwg · Joares-REL-Controle Credito Talhao 07.xls.

## 5. Governança

- 00-Import: entrada livre; a VLA renomeia e MOVE (nunca copia) para a subpasta definitiva; ambíguos vão para Correção Manual/Análise; triagem registrada no LOG.

- _Obsoletos: guarda revisões antigas e duplicatas; conteúdo não é excluído sem revisão do gestor.

- Correção Manual de Arquivos: Análise (ambíguos) e Exclusão (duplicatas/obsoletos). Logs de nomenclatura em Inst Trab e POPs/Logs.

## 6. Controle de revisões

| Rev. | Data | Responsável | Descrição |
| --- | --- | --- | --- |
| R00 | 08/05/2026 | Vitor Zanchet | Mapa inicial de pastas + nomenclatura (underscore). |
| R01 | 21/07/2026 | Vitor Zanchet | Estrutura interna padrão por ativo (fazenda/urbano/veículo); governança 00-Import/_Obsoletos/Correção Manual/Logs; nomenclatura alinhada ao padrão-mestre (hífen, Title Case); marca VLA. |

VLA Patrimonial — Sorriso/MT — confidencial, uso interno. Padrão-mestre do Grupo: Base Empreendimentos POP-04 R06.
