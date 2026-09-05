# Referência operacional

- Empresa: VZP Engenharia
- Documento vigente: `POP-04.00-VZP-Organizacao-Arquivos-R01.docx` — **Versão 2.1 | 27/08/2026**
- Origem: `Documentos Compartilhados/VZP-Eng/08-Inst Trab e Pop's/` (SharePoint)
- Reextraída em 05/09/2026. A revisão anterior desta referência vinha do **R00 (Versão 1.0, Maio/2026)**, treze revisões atrás, e por isso descrevia uma estrutura que não existe mais.
- Regra: ao existir nova revisão, reextrair e revalidar esta referência antes do uso. **Não confie na linha "Documento vigente" sem conferir a revisão no SharePoint** — ela registra o que era verdade na extração, não hoje.

> Esta referência preserva o conteúdo operacional extraído do documento fonte. Em caso de dúvida, conflito, perda de formatação ou informação incompleta, consultar o arquivo original vigente.

VZP ENGENHARIA

Sinop – Mato Grosso

Procedimento Operacional Padrão de Organização de Arquivos e Pastas

Estrutura de Pastas, Subpastas e Nomenclatura de Arquivos para SharePoint

Versão 2.1  |  Agosto de 2026  |  Vitor Zanchet – Eng. Civil

## 1. Objetivo

Define a estrutura padrão de pastas, subpastas e nomeação de arquivos da VZP Engenharia, a ser replicada no ambiente SharePoint/OneDrive da empresa, garantindo rastreabilidade, organização e fácil localização dos documentos.

## 2. Escopo

Aplica-se a todos os arquivos e pastas do repositório digital da VZP Engenharia (SharePoint / OneDrive), abrangendo obras em andamento e concluídas, projetos independentes, áreas funcionais da empresa, compras corporativas e de obra, cursos, treinamentos e softwares.

## 3. Estrutura Raiz do Repositório

| Pasta | Sigla | Descrição |
| --- | --- | --- |
| 00-Import | IMP | CAIXA DE ENTRADA corporativa — arquivos recebidos ainda não classificados; triados e movidos para a pasta definitiva (mesma lógica da 00-Import das obras). |
| 01-Compras | – | Compras corporativas (não vinculadas a obra) |
| 02-Correção Manual de Arquivos | — | Arquivos em triagem/correção de nomenclatura antes do arquivamento definitivo |
| 03-Curs e Trein | CT | Cursos, treinamentos e material acadêmico |
| 04-Doc e Cad | DC | Documentos legais e cadastrais da empresa |
| 05-Est | – | Documentos de equipamentos e bens patrimoniais |
| 06-Fin | – | Financeiro corporativo (boletos, recibos, horas técnicas) |
| 07-Fisc | – | Fiscal e tributário (notas, DAS, estudos tributários) |
| 08-Inst Trab e Pop's | IT/POP | Instruções técnicas e Procedimentos Operacionais Padrão |
| 09-Mark e Prop | MP | Marketing e **PROPAGANDA**: campanhas, imagens, logo e placa de obra. "Prop" é PROPAGANDA, **não proposta** — a proposta comercial fica em 15-Vendas. |
| 10-Ob Concluidas | – | Obras encerradas e entregues ao cliente |
| 11-Ob em Andam | – | Obras atualmente em execução pela VZP |
| 12-Proj | – | Projetos técnicos avulsos (sem obra associada) |
| 13-Rh e Dp | RH | Recursos Humanos e Departamento Pessoal corporativo |
| 14-Soft, Prog e Manuais | – | Softwares, programas e manuais |
| 15-Vendas | VEN | Comercial da empresa — lado da RECEITA: 00-Propostas e 01-Contratos. Contrato de COMPRA corporativo fica em 01-Compras/05-Contratos. Ver §5.10. |

## 4. Estrutura de Obras

### 4.1 Nomenclatura da Pasta de Obra

`Ob-[Cliente]-[TipoProjeto]-[Cidade]-[Estado]`

Exemplos: `Ob-Animalle-VZP Eng-Hospital-SR-MT`, `Ob-Cofco-Basenorte-ApCam-SR-MT`, `Ob-Anne-Resid-SO-SP`.

Hífen como separador entre blocos; evitar acentos e caracteres especiais. Siglas de cidade: `SR-MT` = Sinop/MT, `SO-SP` = Santo André/SP.

### 4.2 Subpastas Padrão de Cada Obra

Numeração obrigatória (v1.4, reordenada para ordem alfabética na v1.8). O prefixo de 2 dígitos integra o nome e não deve ser omitido. `05-Fin` é obrigatória; as demais também, salvo indicação.

| Subpasta | Sigla | Conteúdo |
| --- | --- | --- |
| 00-Import | IMP | CAIXA DE ENTRADA da obra. Destino único de todo arquivo recebido ainda não classificado. Ver §4.3.0. |
| 01-Compras | COMP | Processo de compras (00-Mem Calc Quant a 05-Contratos). **Pagamentos NÃO ficam aqui** (ver 05-Fin) e a **NF-e de entrada também NÃO** — é documento fiscal, vai para 06-Fisc. |
| 02-Vendas | VEN | Lado da RECEITA na obra: 00-Propostas e 01-Contratos (contrato de venda). Contrato de compra NÃO fica aqui. Ver §4.3.4. |
| 03-Doc | DOC | Documentos gerais (atas, documentos do imóvel, registros) |
| 04-Ehs | EHS | Segurança, meio ambiente e saúde no trabalho |
| 05-Fin | FIN | Financeiro da obra — OBRIGATÓRIA. Ordens de pagamento, boletos e comprovantes ficam SEMPRE aqui. Ver §4.3.8. |
| 06-Fisc | FISC | Notas fiscais e documentos fiscais da obra. A NF-e recebida fica aqui, nunca em 01-Compras. |
| 07-ITs | IT | Instruções técnicas de execução da obra |
| 08-Med Serv Prop | MSP | Medições dos serviços próprios (VZP) |
| 09-Med Serv Terc | MST | Medições dos serviços terceirizados |
| 10-Plan | PLAN | Planejamento: RDO, RSO e cronograma financeiro |
| 11-Proj | PROJ | Projetos técnicos por disciplina |
| 12-Rh e Dp | RH | Documentos dos trabalhadores da obra |

**Subpasta `_Obsoletos` (v1.2).** Em cada `Proj/<disciplina>/` e, quando aplicável, na raiz de `Proj/`, guarda versões superadas. Substitui OLD, "Revisões antigas" e `_Duplicatas`. O prefixo `_` mantém no topo da listagem. Conteúdo jamais excluído sem revisão do gestor.

### 4.3 Detalhamento das Subpastas

#### 4.3.0 00-Import — Caixa de Entrada da Obra

**Vedações:** não é área de armazenamento nem de trabalho. É vedado manter arquivo ali como local definitivo, referenciar arquivo dessa pasta em e-mail/contrato/comunicação formal, e imprimir prancha a partir dela — o caminho não é estável.

**Triagem (VZP):** (a) a pasta é esvaziada periodicamente — cada arquivo é renomeado e **movido**, nunca copiado, de modo que `00-Import` vazia signifique "nada pendente"; (b) caso ambíguo vai para `02-Correção Manual de Arquivos/Analise`, nunca permanece na caixa; (c) a triagem é registrada no LOG-Nomenclatura-VZP-Eng; (d) duplicata exata é descartada após conferência por hash.

**Quem deposita:** basta soltar o arquivo — nome livre, formato livre. Se o contexto não for óbvio, criar subpasta com uma palavra de contexto ou renomear o arquivo com essa indicação. Não apagar nem reorganizar o que já estiver na pasta.

**Objetivo:** eliminar a barreira de entrada. Exigir que o remetente conheça a estrutura antes de salvar produz o pior resultado: o arquivo não é salvo, ou é salvo em local aleatório. A caixa separa o ato de ENTREGAR (livre) do ato de CLASSIFICAR (padronizado, da VZP).

#### 4.3.1 11-Proj — Projetos (subpastas por disciplina)

Arquitetura · Estrutura · Estruturas Metálicas · Elétrica · SPDA · Hidrosanitário · Ar condicionado · Prevenção e combate de incêndio · CFTV · Elevador · Ambiental · Canteiro · Luminotecnico

#### 4.3.2 10-Plan — Planejamento

- RDO — Relatório Diário de Obra
- RSO — Relatório Semanal de Obra
- FIN — Cronograma financeiro e fluxo de caixa da obra
- Relatórios — planilhas orçamentárias, fluxos, pagamentos em aberto (subpasta de FIN). Nomenclatura: §6.8.

#### 4.3.3 01-Compras — Processo de Aquisição

| Subpasta | Conteúdo |
| --- | --- |
| 00-Mem Calc Quant | Memória de cálculo e quantitativos |
| 01-Solicit Comp | Solicitações de compra |
| 02-Orçamentos | Orçamentos recebidos de fornecedores |
| 03-Mapa de Cotações | Planilhas de cotação e comparativo |
| 04-Ord Comp | Ordens de compra aprovadas |
| 05-Contratos | Contratos de COMPRA assinados e aditivos, em subpastas por tipo de serviço ou fornecedor |

**A NF-e de entrada NÃO integra este processo** — por ser documento fiscal, fica sempre em `06-Fisc`. **Ordens de pagamento e comprovantes também NÃO** — por serem atos financeiros, ficam sempre em `05-Fin` (§4.3.8).

#### 4.3.4 02-Vendas e 01-Compras/05-Contratos — os dois lados do contrato

A pasta segue o **LADO da relação**, não o tipo de documento: se a empresa **PAGA** (fornecedor, subempreiteiro, projetista, locador, prestador), o contrato mora em `01-Compras/05-Contratos`; se a empresa **RECEBE** (cliente, unidade, alienação), mora em `02-Vendas/01-Contratos`.

`02-Vendas` tem duas subpastas obrigatórias: `00-Propostas` (proposta comercial, orçamento de venda e QQP até o fechamento) e `01-Contratos` (contrato de venda assinado e aditivos).

**Regra da pasta de obra:** a pasta da obra pertence ao cliente / ao empreendimento e vai com ele no encerramento. Por isso, dentro da obra, todo contrato de execução — inclusive o de gestão de obras que a própria VZP presta — figura do lado de `01-Compras/05-Contratos`. O contrato de VENDA desse serviço vive na pasta mãe da empresa, em `15-Vendas/01-Contratos`, e reaparece na obra pelo lado de compras. Não duplicar.

**Fronteira:** enquanto o documento serve para vender, fica em `00-Propostas`; assinado, ele e os aditivos passam a residir em Contratos, do lado correspondente. Documento societário ou cadastral (contrato social, alteração contratual) NÃO é comercial — vai para `04-Doc e Cad`.

Subpastas por tipo de contrato em `01-Compras/05-Contratos` (criar conforme a obra): Cliente · Obras Civis · Elétrica · Hidráulica · Aberturas – Portas e Janelas · Vedações – Paredes e Forro · Escavação · Gestão de Obras · Projeto Arquitetônico · Projeto Ambiental

#### 4.3.5 03-Doc — Documentos da Obra

Atas · [Nome do cliente/empreendimento] · Imóvel (escritura, matrícula, habite-se) · Proj (cópias de ARTs, aprovações) · Repres

#### 4.3.6 04-Ehs — Segurança e Meio Ambiente

APR · DDS · EPIs · Programas legais quando aplicáveis (PPRA, PCMSO, PGR)

#### 4.3.7 12-Rh e Dp — Recursos Humanos da Obra

Doc de Ativos · Doc de Inativos

#### 4.3.8 05-Fin — Financeiro da Obra

Pasta **OBRIGATÓRIA** em toda obra, destinada aos atos financeiros — distintos dos atos de aquisição, que ficam em `01-Compras`. Regra do escritório: ordem de pagamento e comprovante ficam SEMPRE aqui, NUNCA em Compras. Compras trata de cotar e comprar; Fin trata de pagar e comprovar.

- `01-Ord Pag` — Ordens de pagamento da obra
- `02-Boletos` — Boletos bancários a pagar e pagos
- `03-Comprov` — Comprovantes de pagamento (Pix, TED, recibos de quitação). Nomenclatura: §6.5.

**Distinção prática:** a Ordem de Compra (`01-Compras/04-Ord Comp`) formaliza O QUE se compra e por quanto; a Ordem de Pagamento (`05-Fin/01-Ord Pag`) autoriza o desembolso; o Comprovante (`05-Fin/03-Comprov`) atesta que o pagamento ocorreu. Os três podem referir-se à mesma compra, mas moram em pastas distintas conforme a natureza do ato.

## 5. Áreas Funcionais da Empresa

### 5.1 04-Doc e Cad

| Subpasta | Conteúdo |
| --- | --- |
| ARTs | Anotações de Responsabilidade Técnica emitidas |
| Certidões e Declarações | Certidões negativas, declarações diversas |
| DAS | Guias DAS – Simples Nacional |
| Laudos | Laudos técnicos emitidos pela VZP |
| Modelos | Templates e modelos de documentos |
| NRs | Normas Regulamentadoras aplicáveis |
| Programas Legais de SST | PPRA, PCMSO, PGR e outros |
| Seguros | Apólices e documentos de seguro |
| Visitas Técnicas | Relatórios e registros de visitas técnicas |

### 5.2 06-Fin — Financeiro

`00-Ord Pag` · `01-Boletos` · `02-Comprov` (comprovantes, DAS, DARF e guias, em subpastas por mês AAMM) · `03-Recibos` · `04-Extratos` · `05-Relatórios` · `06-Simulações` · `07-Investimentos` · `Horas Tecnicas`

Nomenclatura em `06-Fin/02-Comprov`: padrão corporativo VZP-FIN do §6.6. `Horas Tecnicas` integra o Financeiro (transferida de Doc e Cad na v1.3).

**Atenção:** a numeração corporativa **não é a mesma da obra**. No corporativo, boletos são `01-Boletos`; na obra, `02-Boletos`.

### 5.3 07-Fisc — Fiscal

`01-Nfe Entradas` · `02-Nfe Saidas` · `03-Estudos Tributários` · `04-Informe de Rendimentos`

### 5.4 09-Mark e Prop — Marketing e Propaganda

**Correção de legenda:** a sigla MP significa "Marketing e **PROPAGANDA**". As revisões anteriores registravam "Marketing e Propostas comerciais", e foi essa leitura errada que levou proposta comercial a ser arquivada na pasta de marketing. A pasta guarda somente propaganda, campanha e identidade visual; a proposta comercial fica em `15-Vendas/00-Propostas` (§5.10).

Camps de Mark · Imag Prod · Imag Servi · Imag de Ob · Logo · Placa de Obra

### 5.5 03-Curs e Trein

Uma subpasta por curso. Ex.: Faculdade (por semestre) · Auto Cad 2D · Revit – modulo 1 · SketchUp · Excel Módulo 1 · Planejamento Financeiro · Pós em Estruturas Metálicas · Método VZP – Engenheiro Com IA.

### 5.6 14-Soft, Prog e Manuais

Uma subpasta por software. Ex.: Revit 2026, Civil 3D 2026, TQS v25, Tekla 2025, GstarCAD 2024, FTool 6.2.

### 5.7 13-Rh e Dp Corporativo

Documentos de RH da empresa (não vinculados a obra). Organizar por colaborador ou por tipo de documento.

### 5.8 08-Inst Trab e Pop's

Instruções técnicas de execução e POPs corporativos, aplicáveis a todas as obras.

### 5.9 05-Est — Equipamentos e Bens Patrimoniais

Documentos técnicos, notas fiscais e manuais de equipamentos da empresa. Organizar por equipamento (ex.: Nitro V15).

### 5.10 15-Vendas — Comercial

Área comercial no nível corporativo, com a mesma lógica de funil da obra (§4.3.4). `00-Propostas` (propostas emitidas pela VZP a clientes e ao grupo, nomenclatura `AAMMDD-VZP-PRO-Descricao_RXX`) e `01-Contratos` (contratos de VENDA assinados e aditivos, vindos da antiga Doc e Cad/Contratos).

É aqui que vive o contrato de gestão de obras que a VZP vende e que reaparece dentro da obra pelo lado de compras. **Não pertence a esta pasta:** contrato de obra específica (`01-Compras/05-Contratos` da própria obra), contrato de COMPRA corporativo (`01-Compras/05-Contratos` corporativo), contrato social e alterações (`04-Doc e Cad`) e material de propaganda (`09-Mark e Prop`).

## 6. Convenção de Nomenclatura de Arquivos

### 6.1 Regras Gerais

- Hífen como separador entre blocos
- Sem espaços, acentos ou caracteres especiais
- Title Case para descrições compostas, com espaço quando o nome é prosa natural ("Locação de Obra"); underscore apenas quando a descrição é estruturada em blocos `Tipo_Substantivo_Local` (padrão POP-01.00 §5.7)
- Nome curto e direto: identificável sem abrir o arquivo
- Revisão sempre ao final: R00, R01, R02…

**Harmonização POP-04 × POP-01 (v1.2).** Arquivos de projeto usam underscore interno; arquivos de gestão administrativa usam Title Case com espaços naturais. Em ambos, o separador entre blocos do código é sempre o hífen sem espaços, nunca o ponto.

### 6.2 Formato Padrão de Arquivos de Projeto

`[AAMMDD]-[OBRA]-[DISC]-[TIPO]-[NUM]-[Desc]-[REV].ext`

| Campo | Exemplo | Descrição |
| --- | --- | --- |
| OBRA | Animalle-Hosp | Sigla da obra, sem acentos |
| DISC | ARQ / ELE / HID | Disciplina (tabela §6.4) |
| TIPO | PR / GEN | PR = Prancha; GEN = Geral |
| NUM | 01 / 02 | Sequencial de 2 dígitos |
| Desc | PavTer / Agua | Descrição curta (opcional) |
| REV | R00 / R01 | Revisão (inicia em R00) |

**Este é o padrão mínimo.** Para a regra completa e autoritativa de documentos de projeto — sequência EMP-FAS-DIS-Descricao-AAMMDD-RXX, tabelas de empreendimentos, fases e disciplinas, sufixo `-DEV` — consultar o **POP-01.00 §5**. Em conflito no tratamento de pranchas, memoriais, RVTs e laudos, **prevalece o POP-01.00**. Pastas e nomenclatura de comprovantes/notas/recibos permanecem regidas por este POP-04.

### 6.3 Exemplos

`260512-Animalle-Hosp-ARQ-PR-01-PavTer-R00.pdf` · `260512-Animalle-Hosp-EST-PR-01-R00.pdf` · `260512-Animalle-Hosp-ELE-GEN-01-MemCalc-R00.xlsx` · `260518-Animalle-Hosp-HID-PR-01-Agua-R02.pdf`

### 6.4 Abreviaturas de Disciplinas

ARQ Arquitetura · EST Estrutura Concreto · MET Estrutura Metálica · ELE Elétrica · HID Hidrossanitário · AC Ar Condicionado · INC Incêndio/PPCI · SPDA Prot. Descargas Atm. · CFTV CFTV/Segurança · ELV Elevador · AMB Ambiental · CAN Canteiro

### 6.5 Comprovantes de Pagamento da Obra (05-Fin/03-Comprov)

`[AAMMDD]-[OBRA]-[TP_OBRA]-SUP-[TIPO]-[Descritor]-[ID].pdf`

Até a v1.4 esta pasta era `01-Compras/06-Comprov`; os comprovantes migraram para o Financeiro da obra na v1.5.

| Componente | Descrição | Exemplo |
| --- | --- | --- |
| OBRA | Sigla da obra (4-6 letras maiúsculas) | ANIMA |
| TP_OBRA | Tipo/uso (HO=Hospital, RE=Residência, CO=Comercial…) | HO |
| SUP | Fixo — pasta de suprimentos/compras | SUP |
| TIPO | CP = Comprovante · EX = Extrato · RC = Recibo | CP |
| AAMMDD | Data da transação, 6 dígitos | 260415 |
| Descritor | Fornecedor ou banco, PascalCase | Sicredi |
| ID | Sequencial opcional (2, 3…) | 2 |

Exemplos: `260415-ANIMA-HO-SUP-CP-Sicredi.pdf` · `2605-ANIMA-HO-SUP-EX-Extrato.pdf` (extrato mensal usa AAMM, sem dia).

Regras: nunca espaços, acentos, cedilha ou caracteres especiais; sufixo numérico a partir de 2 para o mesmo fornecedor na mesma data; PDF preferencial (JPG/PNG só para fotos de recibo físico); o Descritor reflete o **fornecedor ou banco pagador**, não o tipo de despesa.

### 6.6 Comprovantes Corporativos (06-Fin/02-Comprov)

`[AAMMDD ou AAMM]-VZP-FIN-[TIPO]-[Descritor]-[ID].(pdf|png|jpg)`, em subpastas por mês AAMM.

TIPO: BOL · CP · EX · RC · DAS · DARF · GPS · GFIP · DCTFWeb. AAMMDD para CP/RC; AAMM para mensais (DAS, DARF, extrato).

Exemplos: `260406-VZP-FIN-BOL-Planejar.png` · `2602-VZP-FIN-DAS.png` · `260415-VZP-FIN-DARF-IRRF.pdf`

Nomes auto-gerados por aplicativos bancários devem ser renomeados na entrada da pasta; se o pagador não for identificável pelo nome, abrir o arquivo e identificar.

### 6.7 Arquivos em 02-Orçamentos

`[AAMMDD]-[OBRA]-[TP_OBRA]-COMP-ORC-[Fornecedor]-[NumOrcamento].(pdf|xlsx)`

Exemplo: `260512-ANIMA-HO-COMP-ORC-AnimallePetCare-1329.pdf`

**Tolerância (v1.2):** PDFs auto-gerados por sistemas de fornecedores podem manter o nome original na recepção, desde que renomeados até o fechamento do orçamento (passagem para `04-Ord Comp`). Nomes com espaços, acentos ou caracteres especiais devem ser corrigidos em qualquer hipótese.

### 6.8 Relatórios Financeiros (10-Plan/FIN/Relatórios)

`[AAMMDD]-[Descritor].(pdf|xlsx)` — ex.: `260118-PlanilhaOrcamentaria.pdf`, `260123-FluxoFinanceiro.pdf`.

O contexto da obra é dado pela própria pasta, portanto o prefixo OBRA-TP_OBRA **não é repetido** no nome — princípio de não-redundância. Relatórios mensais podem usar AAMM.

### 6.9 Fotos e Registros de Evidência (RDO, RSO, EHS e RH)

Fotos, vídeos e capturas que servem de evidência ficam **dispensados** do padrão de nomenclatura, mantendo o nome original do dispositivo/aplicativo. O volume torna o renomeio manual antieconômico, e a rastreabilidade já é garantida pela pasta, sempre datada.

**Permanecem obrigatórios mesmo nesse regime:** (a) a PASTA segue o padrão de data deste POP; (b) é **vedado** arquivar em `.rar`/`.zip` — o conteúdo deve ser extraído, sob pena de impedir busca e indexação no SharePoint; (c) duplicatas exatas eliminadas periodicamente; (d) documentos formais (relatórios assinados, fichas, contratos, ARTs) **não** são evidência fotográfica e seguem integralmente o padrão.

## 7. Mapa Visual da Estrutura

> **Divergência conhecida no documento fonte (apontada em 05/09/2026).** No `.docx` R01, o §7 não foi atualizado junto com o corpo: ele ainda lista Compras corporativa terminando em `05-Ord Pag / 06-Comprov / 07-Nfe`, Fin como `Boletos / Comprovantes / Horas Tecnicas / Recibos` e Fisc como `Estudos Tributários / Notas Emitidas`. Essas três listas contrariam o §4.3.3, o §5.2 e o §5.3 do próprio documento. **Vale o corpo, não o mapa.** O mapa abaixo já está corrigido.

```
VZP-Eng (raiz)
├─ 00-Import
├─ 01-Compras          00-Mem Calc Quant · 01-Solicit Comp · 02-Orçamentos
│                      03-Mapa de Cotações · 04-Ord Comp · 05-Contratos
├─ 02-Correção Manual de Arquivos    Analise · Exclusão
├─ 03-Curs e Trein     uma subpasta por curso
├─ 04-Doc e Cad        ARTs · Certidões e Declarações · DAS · Laudos · Modelos
│                      NRs · Programas Legais de SST · Seguros · Visitas Técnicas
├─ 05-Est              por equipamento
├─ 06-Fin              00-Ord Pag · 01-Boletos · 02-Comprov · 03-Recibos
│                      04-Extratos · 05-Relatórios · 06-Simulações
│                      07-Investimentos · Horas Tecnicas
├─ 07-Fisc             01-Nfe Entradas · 02-Nfe Saidas · 03-Estudos Tributários
│                      04-Informe de Rendimentos
├─ 08-Inst Trab e Pop's
├─ 09-Mark e Prop      Camps de Mark · Imag Prod · Imag Servi · Imag de Ob
│                      Logo · Placa de Obra
├─ 10-Ob Concluidas    Ob-[Cliente]-[Tipo]-[Cid]-[UF]  (mesma estrutura interna)
├─ 11-Ob em Andam      Ob-[Cliente]-[Tipo]-[Cid]-[UF]
│   └─ 00-Import · 01-Compras · 02-Vendas · 03-Doc · 04-Ehs · 05-Fin
│      06-Fisc · 07-ITs · 08-Med Serv Prop · 09-Med Serv Terc
│      10-Plan · 11-Proj · 12-Rh e Dp
├─ 12-Proj
├─ 13-Rh e Dp
├─ 14-Soft, Prog e Manuais   uma subpasta por software
└─ 15-Vendas           00-Propostas · 01-Contratos
```

## 8. Configuração no SharePoint

- Site de Equipe: VZP Engenharia. Biblioteca principal: `VZP-Eng`. Replicar toda a árvore dentro dela.
- Obras em andamento e concluídas em subpastas separadas.
- **Permissões:** acesso total ao gestor e colaboradores diretos; acesso restrito por pasta de obra a parceiros e terceiros; `04-Doc e Cad`, `06-Fin` e `07-Fisc` restritas ao gestor.
- **Sincronização:** biblioteca completa no computador do gestor; demais colaboradores sincronizam somente as obras em que atuam.

Dúvidas sobre nomenclatura ou criação de novas pastas: consultar o gestor antes de criar qualquer item fora do padrão.

## 9. Controle do Documento

| Versão | Data | Descrição |
| --- | --- | --- |
| 1.0 | Maio/2026 | Versão inicial |
| 1.1 | 15/05/2026 | §6.2 remete ao POP-01.00 para nomenclatura de projeto |
| 1.2 | 17/05/2026 | Disciplina Luminotecnico; subpasta Relatórios em Plan/FIN; `_Obsoletos` em Proj/<disciplina>; harmonização de separadores; criadas §6.6, §6.7 e §6.8 |
| 1.3 | 18/07/2026 | Nomes corrigidos (ITs, Med Serv Prop, ARTs, NRs — sem apóstrofo nem acento); Fin numerada 00-Ord Pag a 07-Investimentos; Horas Tecnicas movida de Doc e Cad para Fin; Fisc atualizada; criada §6.9 |
| 1.4 | 18/07/2026 | Caixa de entrada por obra (§4.3.0); numeração obrigatória das subpastas de obra |
| 1.5 | 18/07/2026 | **Separação entre aquisição e financeiro:** ordens de pagamento e comprovantes saem de 01-Compras e passam a residir sempre em 05-Fin; removidas `05-Ord Pag` e `06-Comprov`; criada §4.3.8 |
| 1.6 | 18/07/2026 | Padronização data-first: AAMMDD como PRIMEIRO bloco em todos os padrões |
| 1.7 | 19/07/2026 | **NF-e de entrada é documento FISCAL** — removida `05-Nfe` de 01-Compras (encerra em 04-Ord Comp); NF-e recebida passa a 06-Fisc |
| 1.8 | 19/07/2026 | Subpastas de obra reordenadas para ordem alfabética (00-Import no topo) |
| 1.9 | 19/07/2026 | Estrutura raiz (§3) numerada, com 00-Import no topo |
| 2.0 | 27/08/2026 | **Área comercial.** Na obra, `02-Contratos` passa a `02-Vendas` (00-Propostas / 01-Contratos). No corporativo, criada `15-Vendas` (§5.10) |
| 2.1 | 27/08/2026 | **Contrato existe nos DOIS lados.** Criada `01-Compras/05-Contratos` (obra e corporativo) para todo contrato de compra; `02-Vendas/01-Contratos` passa a conter só contrato de VENDA. Corrigida a legenda MP: Marketing e PROPAGANDA (§5.4) — causa raiz do arquivamento errado de propostas. Migradas 69 pastas de contrato nas 12 obras |

## ADENDO 01 — Novos Prefixos (25/05/2026)

**LCM — Lista de Controle de Materiais / Suprimentos.** `LCM-XX.XX-VZP-Descricao-RXX.ext` (ex.: `LCM-01.00-VZP-Suprimentos-R01.docx`). Localização: `08-Inst Trab e Pop's/`.

**COFCO-EHS — Documentos EHS de terceiros.** Documentos emitidos pela COFCO e aplicáveis às obras do parque COFCO-Basenorte recebem o prefixo `COFCO-EHS`. Ex.: `COFCO-EHS-009-Gestao_Contratadas.pdf`. Localização: `[Obra]/04-Ehs/`.

---

Elaborado por: Vitor Zanchet – Engenheiro Civil | VZP Engenharia
