# Referência operacional

- Empresa: VZP Engenharia
- Documento vigente: `POP-04.00-VZP-Organizacao-Arquivos-R00.docx`
- Origem: pasta mestra de POPs/ITs da VZP Engenharia
- Regra: ao existir nova revisão, reextrair e revalidar esta referência antes do uso.

> Esta referência preserva o conteúdo operacional extraído do documento fonte. Em caso de dúvida, conflito, perda de formatação ou informação incompleta, consultar o arquivo original vigente.

VZP ENGENHARIA

Sinop – Mato Grosso

Procedimento Operacional Padrão de Organização de Arquivos e Pastas

Estrutura de Pastas, Subpastas e Nomenclatura de Arquivos para SharePoint

Versão 1.0  |  Maio de 2026  |  Vitor Zanchet – Eng. Civil

## Sumário

O sumário é atualizado automaticamente pelo Word/SharePoint. Pressione Ctrl+A e depois F9 para atualizar todos os campos ao abrir o documento.

## 1. Objetivo

Este documento define a estrutura padrão de pastas, subpastas e nomeação de arquivos da VZP Engenharia, a ser replicada no ambiente SharePoint/OneDrive da empresa. O objetivo é garantir rastreabilidade, organização e fácil localização dos documentos por todos os envolvidos nos projetos e nas rotinas administrativas.

## 2. Escopo

Aplica-se a todos os arquivos e pastas armazenados no repositório digital da VZP Engenharia (SharePoint / OneDrive), abrangendo:

Obras em andamento e obras concluídas

Projetos independentes

Áreas funcionais da empresa (Financeiro, Fiscal, RH, Marketing etc.)

Compras corporativas e de obra

Cursos, treinamentos e softwares

## 3. Estrutura Raíz do Repositório

A pasta raíz do repositório da VZP Engenharia deve conter as seguintes pastas de primeiro nível:

| Pasta | Sigla | Descrição |
| --- | --- | --- |
| 00-Import | IMP | CAIXA DE ENTRADA corporativa — arquivos recebidos ainda não classificados; triados e movidos para a pasta definitiva (mesma lógica da 00-Import das obras). |
| 01-Compras | – | Compras corporativas (não vinculadas a obra) |
| 02-Correção Manual de Arquivos | — | Arquivos em triagem/correção de nomenclatura antes do arquivamento definitivo. |
| 03-Curs e Trein | CT | Cursos, treinamentos e material acadêmico |
| 04-Doc e Cad | DC | Documentos legais e cadastrais da empresa |
| 05-Est | – | Documentos de equipamentos e bens patrimoniais |
| 06-Fin | – | Financeiro corporativo (boletos, recibos, horas técnicas) |
| 07-Fisc | – | Fiscal e tributário (notas, DAS, estudos tributários) |
| 08-Inst Trab e Pop's | IT/POP | Instruções técnicas e Procedimentos Operacionais Padrão |
| 09-Mark e Prop | MP | Marketing e Propostas comerciais |
| 10-Ob Concluidas | – | Obras encerradas e entregues ao cliente |
| 11-Ob em Andam | – | Obras atualmente em execução pela VZP |
| 12-Proj | – | Projetos técnicos avulsos (sem obra associada) |
| 13-Rh e Dp | RH | Recursos Humanos e Departamento Pessoal corporativo |
| 14-Soft, Prog e Manuais | – | Softwares, programas e manuais |

## 4. Estrutura de Obras

### 4.1 Nomenclatura da Pasta de Obra

Cada obra recebe uma pasta nomeada conforme o padrão abaixo, tanto em 'Ob em Andam' quanto em 'Ob Concluidas':

Ob-[Cliente]-[TipoProjeto]-[Cidade]-[Estado]

| Nome da Pasta | Descrição |
| --- | --- |
| Ob-Animalle-VZP Eng-Hospital-SR-MT | Hospital veterinário Animalle – Sinop/MT |
| Ob-Animalle-VZP Eng-PetShop-SR-MT | PetShop Animalle – Sinop/MT |
| Ob-Cofco-Basenorte-Ap Cam-SR-MT | Apartamentos Cofco/Basenorte – Sinop/MT |
| Ob-Cofco-Basenorte-Vest-Desc-Colab-SR-MT | Vestiário/Descentralização Cofco – Sinop/MT |
| Ob-Anne-Resid-SO-SP | Residência Anne – Santo André/SP |

Usar hífen como separador entre blocos. Evitar acentos e caracteres especiais. Siglas de cidades: SR-MT = Sinop/MT, SO-SP = Santo André/SP.

### 4.2 Subpastas Padrão de Cada Obra

### Numeracao obrigatoria (Versao 1.4). As subpastas de obra sao prefixadas com numero de 2 digitos (00 a 12), que fixa a ordem de exibicao no SharePoint independentemente da ordenacao alfabetica. A sequencia reflete o fluxo de trabalho — entrada, projeto, planejamento, execucao, suprimentos, contratos, documentacao, seguranca, fiscal, medicoes e pessoas. O prefixo integra o nome da pasta e nao deve ser omitido. 05-Fin e opcional; as demais sao obrigatorias em toda obra.

| Subpasta | Sigla | Conteúdo |
| --- | --- | --- |
| 00-Import | IMP | CAIXA DE ENTRADA da obra. Destino unico de todo arquivo recebido pela equipe que ainda nao foi classificado. Ver §4.3.0. |
| 01-Compras | COMP | Processo de compras (00-Mem Calc Quant a 04-Ord Comp). Pagamentos NAO ficam aqui (ver 05-Fin) e a NF-e de entrada tambem NAO — e documento fiscal, vai para 06-Fisc. |
| 02-Contratos | CONT | Contratos com clientes, fornecedores e subempreiteiros |
| 03-Doc | DOC | Documentos gerais (atas, documentos do imóvel, registros) |
| 04-Ehs | EHS | Segurança, meio ambiente e saúde no trabalho |
| 05-Fin | FIN | Financeiro da obra — OBRIGATORIA. Ordens de pagamento, boletos e comprovantes ficam SEMPRE aqui, nunca em 01-Compras. Ver §4.3.8. |
| 06-Fisc | FISC | Notas fiscais e documentos fiscais da obra. A NF-e recebida (entrada) fica aqui, nunca em 01-Compras. |
| 07-ITs | IT | Instruções técnicas de execução da obra |
| 08-Med Serv Prop | MSP | Medições dos serviços próprios (VZP) |
| 09-Med Serv Terc | MST | Medições dos serviços terceirizados |
| 10-Plan | PLAN | Planejamento: RDO, RSO e cronograma financeiro |
| 11-Proj | PROJ | Projetos técnicos por disciplina |
| 12-Rh e Dp | RH | Documentos dos trabalhadores da obra |

Subpasta _Obsoletos (Versão 1.2). Em cada pasta Proj/<disciplina>/ e, quando aplicável, dentro da raiz de Proj/, a subpasta _Obsoletos/ armazena versões superadas (revisões antigas, arquivos duplicados, materiais de descarte). Substitui as variações anteriores OLD, Revisões antigas, _Duplicatas. O prefixo "_" garante ordenação alfabética no topo da listagem. Conteúdos jamais devem ser excluídos sem revisão do gestor — mantidos para auditoria conforme POP-01.00 §10.5.

### 4.3 Detalhamento das Subpastas

Vedacoes: 00-Import nao e area de armazenamento nem de trabalho. E vedado manter arquivo em 00-Import como local definitivo, referenciar arquivo dessa pasta em e-mail, contrato ou comunicacao formal, e imprimir prancha a partir dela — o caminho nao e estavel, pois todo arquivo ali e transitorio por definicao.

Regras para a triagem (VZP): (a) a pasta e esvaziada periodicamente — cada arquivo e renomeado conforme este POP e MOVIDO para a subpasta definitiva, nunca copiado, de modo que 00-Import vazia signifique 'nada pendente'; (b) arquivo cuja classificacao seja ambigua vai para Correcao Manual de Arquivos/Analise/, nunca permanece indefinidamente na caixa; (c) a triagem e registrada no LOG-Nomenclatura-VZP-Eng; (d) duplicata de documento ja arquivado e descartada apos conferencia por hash.

Regras para quem deposita: (a) basta soltar o arquivo em 00-Import — nome livre, formato livre; (b) se o contexto nao for obvio pelo proprio arquivo, criar uma subpasta com uma palavra de contexto (ex.: 'nf famac', 'fotos telhado') ou renomear o arquivo com essa indicacao; (c) nao apagar nem reorganizar o que ja estiver na pasta; (d) na duvida sobre a obra correta, depositar assim mesmo e avisar a VZP.

Objetivo. Eliminar a barreira de entrada. A experiencia mostra que exigir que o remetente conheca a estrutura e a nomenclatura antes de salvar um arquivo produz o pior dos resultados: o arquivo nao e salvo, ou e salvo em local aleatorio. A caixa de entrada separa o ato de ENTREGAR (livre, de qualquer pessoa) do ato de CLASSIFICAR (padronizado, de responsabilidade da VZP).

Toda obra possui uma pasta 00-Import na raiz, numerada com 00 para permanecer no topo da listagem. Ela e o ponto unico de entrada de arquivos na obra: qualquer membro da equipe que receba um documento — nota fiscal, foto de campo, orcamento de fornecedor, contrato assinado, comprovante, projeto revisado — deposita o arquivo em 00-Import, sem se preocupar com nome ou destino.

#### 4.3.0 00-Import – Caixa de Entrada da Obra

#### 4.3.1 Proj – Projetos (subpastas por disciplina)

| Subpasta | Disciplina |
| --- | --- |
| Arquitetura | Projeto arquitetônico |
| Estrutura | Projeto estrutural em concreto |
| Estruturas Metálicas | Projeto estrutural metálico |
| Elétrica | Projeto elétrico (BT, QGBT etc.) |
| SPDA | Sistema de proteção contra descargas atmosféricas |
| Hidrosanitário | Projeto hidrossanitário |
| Ar condicionado | Projeto de climatização e ventilação |
| Prevenção e combate de incêndio | PPCI / sistema de sprinklers |
| CFTV | Circuito fechado de TV e segurança eletrônica |
| Elevador | Projeto e documentação de elevador |
| Ambiental | Projeto ambiental / licenciamento |
| Canteiro | Layout e implantação do canteiro de obras |
| Luminotecnico | Projeto luminotécnico (iluminação técnica/decorativa, fotometria) |

#### 4.3.2 Plan – Planejamento

RDO – Relatório Diário de Obra

RSO – Relatório Semanal de Obra

FIN – Cronograma financeiro e fluxo de caixa da obra

Relatórios – planilhas orçamentárias, fluxos financeiros, pagamentos em aberto e demais relatórios financeiros gerados durante a obra (subpasta de FIN). Padrão de nomenclatura: ver §6.8.

#### 4.3.3 01-Compras – Processo de Aquisição

| Subpasta | Conteúdo |
| --- | --- |
| 00-Mem Calc Quant | Memória de cálculo e quantitativos |
| 01-Solicit Comp | Solicitações de compra |
| 02-Orçamentos | Orçamentos recebidos de fornecedores |
| 03-Mapa de Cotações | Planilhas de cotação e comparativo |
| 04-Ord Comp | Ordens de compra aprovadas |

O prefixo numérico (00, 01…) garante a ordem cronológica no SharePoint. A sequência abrange do levantamento de necessidade (00) à ordem de compra (04). A NF-e de entrada NÃO integra este processo — por ser documento fiscal, fica sempre em 06-Fisc, não em Compras. Ordens de pagamento e comprovantes de pagamento NÃO integram este processo: por serem atos financeiros, e não de aquisição, ficam sempre em 05-Fin (§4.3.8).

#### 4.3.4 Contratos

Subpastas por tipo de contrato (criar conforme a obra):

Cliente – Proposta

Obras Civis

Elétrica

Hidráulica

Aberturas – Portas e Janelas

Vedações – Paredes e Forro

Escavação

Gestão de Obras

Projeto Arquitetônico

Projeto Ambiental

#### 4.3.5 Doc – Documentos da Obra

Atas – Registros formais de reunião

[Nome do cliente/empreendimento] – Documentos específicos do contratante

Imóvel – Escritura, matrícula, habite-se etc.

Proj – Cópias de documentos de projeto (ARTs, aprovações)

Repres – Documentos de representantes e parceiros

#### 4.3.6 Ehs – Segurança e Meio Ambiente

APR – Análise Preliminar de Risco

DDS – Diálogo Diário de Segurança

EPIs – Fichas de entrega de EPI

Programas legais quando aplicáveis (PPRA, PCMSO, PGR)

#### 4.3.7 Rh e Dp – Recursos Humanos da Obra

Doc de Ativos – Trabalhadores em atividade

Doc de Inativos – Trabalhadores desligados

Distincao pratica: a Ordem de Compra (01-Compras/04-Ord Comp) formaliza O QUE se compra e por quanto; a Ordem de Pagamento (05-Fin/01-Ord Pag) autoriza o desembolso; o Comprovante (05-Fin/03-Comprov) atesta que o pagamento ocorreu. Os tres documentos podem referir-se a mesma compra, mas moram em pastas distintas conforme a natureza do ato.

03-Comprov – Comprovantes de pagamento (Pix, TED, recibos de quitacao). Nomenclatura: padrao OBRA-TP_OBRA-SUP-... definido em §6.5.

02-Boletos – Boletos bancarios a pagar e pagos vinculados a obra.

01-Ord Pag – Ordens de pagamento da obra (autorizacoes de pagamento a fornecedores e prestadores).

Pasta OBRIGATORIA em toda obra, destinada aos atos financeiros — distintos dos atos de aquisicao, que ficam em 01-Compras. Regra do escritorio: ordem de pagamento e comprovante de pagamento ficam SEMPRE aqui, NUNCA em Compras. Compras trata de cotar e comprar; Fin trata de pagar e comprovar.

#### 4.3.8 05-Fin – Financeiro da Obra

## 5. Áreas Funcionais da Empresa

### 5.1 Doc e Cad – Documentos e Cadastros

| Subpasta | Conteúdo |
| --- | --- |
| ARTs | Anotações de Responsabilidade Técnica emitidas |
| Certidões e Declarações | Certidões negativas, declarações diversas |
| Contratos | Contratos corporativos da empresa |
| DAS | Guias DAS – Simples Nacional |
| Laudos | Laudos técnicos emitidos pela VZP |
| Modelos | Templates e modelos de documentos |
| NRs | Normas Regulamentadoras aplicáveis |
| Programas Legais de SST | PPRA, PCMSO, PGR e outros programas obrigatórios |
| Seguros | Apólices e documentos de seguro |
| Visitas Técnicas | Relatórios e registros de visitas técnicas |

### 5.2 Fin – Financeiro

00-Ord Pag – Ordens de pagamento corporativas

01-Boletos – Boletos bancários a pagar e pagos

02-Comprov – Comprovantes de pagamento, DAS, DARF e guias (subpastas por mês, AAMM)

03-Recibos – Recibos emitidos e recebidos

04-Extratos – Extratos bancários mensais

05-Relatórios – Relatórios financeiros corporativos

06-Simulações – Simulações e estudos de cenário

07-Investimentos – Aplicações e investimentos da empresa

Horas Tecnicas – Banco de horas técnicas (transferida de Doc e Cad em 18/07/2026)

Nomenclatura dos arquivos em Fin/02-Comprov/: padrão corporativo VZP-FIN definido em §6.6. A pasta Horas Tecnicas integra o Financeiro (transferida de Doc e Cad na revisão 1.3).

### 5.3 Fisc – Fiscal

01-Nfe Entradas – NF-e de entrada

02-Nfe Saidas – NF-e de serviços emitidas

03-Estudos Tributários – Estudos e pareceres tributários

04-Informe de Rendimentos – Informes anuais de rendimentos

### 5.4 Mark e Prop – Marketing e Propostas

| Subpasta | Conteúdo |
| --- | --- |
| Camps de Mark | Campanhas de marketing e anúncios (Instagram, Meta Ads etc.) |
| Imag Prod | Imagens de produtos e materiais |
| Imag Servi | Imagens de serviços prestados |
| Imag de Ob | Fotos e vídeos de obras |
| Logo | Logotipo VZP em todas as variações (PNG, SVG, AI) |
| Placa de Obra | Artes e arquivos de placas de identificação de obra |

### 5.5 Curs e Trein – Cursos e Treinamentos

Uma subpasta por curso. Exemplos atuais:

Faculdade – organizado por semestre (Semestre 1 a 10)

Auto Cad 2D

Revit – modulo 1

SketchUp

Excel Módulo 1

Planejamento Financeiro

Pós em Estruturas Metálicas

Método VZP – Engenheiro Com IA

[Novos cursos: criar subpasta com o nome exato do curso]

### 5.6 Soft, Prog e Manuais

Uma subpasta por software. Exemplos: Revit 2026, Civil 3D 2026, TQS v25, Tekla 2025, GstarCAD 2024, FTool 6.2.

### 5.7 Rh e Dp Corporativo

Documentos de RH da empresa (não vinculados a obra). Organizar por colaborador ou por tipo de documento.

### 5.8 Inst Trab e Pop's

Instruções técnicas de execução e POPs corporativos (aplicação em todas as obras): fundação, alvenaria, revestimento, concretagem, escoramento etc.

### 5.9 Est – Equipamentos e Bens Patrimoniais

Documentos técnicos, notas fiscais e manuais de equipamentos da empresa. Organizar por equipamento (ex.: Nitro V15).

## 6. Convenção de Nomenclatura de Arquivos

### 6.1 Regras Gerais

Usar hífen (–) como separador entre blocos

Sem espaços, acentos ou caracteres especiais

Caixa mista (Title Case) para descrições compostas, com SPACE quando o nome é prosa natural (ex.: "Locação de Obra", "Execução de Concretagem"); use underscore (_) apenas quando a descrição é estruturada em blocos sintáticos do tipo Tipo_Substantivo_Local (padrão dos arquivos de projeto regidos pelo POP-01.00 §5.7).

Nome curto e direto: identificável sem abrir o arquivo

Revisão sempre ao final: R00, R01, R02…

Harmonização POP-04 × POP-01 (Versão 1.2, 17/05/2026). Em arquivos de projeto e correlatos (POP-01 §5.7 — pranchas, memoriais, listas, laudos, RVTs), a descrição usa underscore como separador interno (Tipo_Substantivo_Local). Em arquivos de gestão administrativa (POPs, ITs, comprovantes, relatórios, modelos de documentos), a descrição usa Title Case com espaços naturais (ex.: "Execução de Concretagem", "Planilha Orçamentária"). Em ambos os casos, o separador entre blocos do código (EMP-FAS-DIS-..., IT-XX.XX-..., VZP-FIN-...) é sempre o hífen sem espaços, e nunca o ponto.

### 6.2 Formato Padrão de Arquivos de Projeto

[AAMMDD]-[OBRA]-[DISC]-[TIPO]-[NUM]-[Desc]-[REV].ext

| Campo | Exemplo | Descrição |
| --- | --- | --- |
| [OBRA] | Animalle-Hosp | Sigla da obra (abreviada, sem acentos) |
| [DISC] | ARQ / ELE / HID | Sigla da disciplina (ver tabela 6.4) |
| [TIPO] | PR / GEN | PR = Prancha; GEN = Geral (memoriais, planilhas, modelos 3D, DWGs) |
| [NUM] | 01 / 02 | Número sequencial de 2 dígitos |
| [Desc] | PavTer / Agua | Descrição curta (opcional quando o número já identifica) |
| [REV] | R00 / R01 | Revisão (inicia em R00) |
| .ext | .pdf / .dwg / .rvt | Extensão original |

Observação importante. O formato acima representa o padrão mínimo do POP-04 para arquivos de projeto. Para a regra completa, autoritativa, de nomenclatura de documentos de projeto — incluindo a sequência EMP-FAS-DIS-Descricao-AAMMDD-RXX, as tabelas de empreendimentos (EMP), fases (FAS) e disciplinas (DIS), o uso do sufixo -DEV para versões em desenvolvimento e as regras de descrição (Tipo_Substantivo_Local) — consultar o POP-01.00 — Procedimento Operacional Padrão de Projetos, §5. Em caso de conflito entre os dois POPs no tratamento de pranchas, memoriais, RVTs e laudos, prevalece o POP-01.00. As regras de pastas e de nomenclatura de comprovantes/notas/recibos permanecem regidas exclusivamente por este POP-04.

### 6.3 Exemplos de Nomes de Arquivo

| Nome do Arquivo | Interpretação |
| --- | --- |
| 260512-Animalle-Hosp-ARQ-PR-01-PavTer-R00.pdf | Prancha 01 ARQ, Pav. Térreo, Rev. 00 |
| 260515-Animalle-Hosp-ARQ-PR-02-PavSup-R01.pdf | Prancha 02 ARQ, Pav. Superior, Rev. 01 |
| 260512-Animalle-Hosp-EST-PR-01-R00.pdf | Prancha 01 Estrutura, Rev. 00 |
| 260512-Animalle-Hosp-ELE-GEN-01-MemCalc-R00.xlsx | Memorial Cálculo Elétrico, Ver. 00 |
| 260512-Animalle-Hosp-ARQ-GEN-01-R00.rvt | Modelo 3D Revit Arquitetura, Ver. 00 |
| 260518-Animalle-Hosp-HID-PR-01-Agua-R02.pdf | Prancha 01 Hidro, Água Fria, Rev. 02 |

### 6.4 Abreviaturas de Disciplinas

| Sigla | Disciplina | Sigla | Disciplina |
| --- | --- | --- | --- |
| ARQ | Arquitetura | INC | Incêndio / PPCI |
| EST | Estrutura Concreto | SPDA | Prot. Descargas Atm. |
| MET | Estrutura Metálica | CFTV | CFTV / Segurança |
| ELE | Elétrica | ELV | Elevador |
| HID | Hidrossanitário | AMB | Ambiental |
| AC | Ar Condicionado | CAN | Canteiro |

### 6.5 Nomenclatura de Comprovantes de Pagamento (pasta 05-Fin/03-Comprov)

Arquivos armazenados na subpasta 05-Fin/03-Comprov (comprovantes de pagamento, extratos e recibos da obra) devem seguir o padrao abaixo. Ate a revisao 1.4 esta pasta era 01-Compras/06-Comprov; os comprovantes migraram para o Financeiro da obra na revisao 1.5.

| [AAMMDD]-[OBRA]-[TP_OBRA]-SUP-[TIPO]-[Descritor]-[ID].pdf |
| --- |

Componentes do nome:

| Componente | Descricao | Exemplo |
| --- | --- | --- |
| OBRA | Sigla da obra (4-6 letras maiusculas) | ANIMA |
| TP_OBRA | Tipo/uso da obra (HO=Hospital, RE=Residencia, CO=Comercial...) | HO |
| SUP | Fixo - indica pasta de suprimentos/compras | SUP |
| TIPO | CP = Comprovante de Pagamento \| EX = Extrato \| RC = Recibo | CP |
| AAMMDD | Data da transacao - 6 digitos sem separadores (Ano-Mes-Dia) | 260415 (15/04/2026) |
| Descritor | Fornecedor ou banco (sem espacos, sem acentos, PascalCase) | Sicredi |
| ID | Sequencial opcional para multiplos docs do mesmo dia (2, 3...); omitir se unico | 2 (segundo doc) |

Exemplos:

| Nome do Arquivo | Significado |
| --- | --- |
| 260415-ANIMA-HO-SUP-CP-Sicredi.pdf | Comprovante Sicredi - Animalle Hospital - 15/04/2026 |
| 260415-ANIMA-HO-SUP-CP-Sicredi-2.pdf | Segundo comprovante Sicredi no mesmo dia |
| 2605-ANIMA-HO-SUP-EX-Extrato.pdf | Extrato bancario de maio/2026 (mensal - sem dia) |
| 260204-ANIMA-HO-SUP-CP-Pagamento.pdf | Comprovante de pagamento generico - 04/02/2026 |

Regras complementares:

Nunca usar espacos, acentos, cedilha ou caracteres especiais no nome.

Extratos mensais usam formato AAMM no lugar de AAMMDD (ex.: 2605).

Quando houver mais de um comprovante do mesmo fornecedor na mesma data, acrescentar sufixo numerico a partir de 2 (ex.: -2, -3).

Formato preferencial de arquivo: PDF. JPG e PNG sao aceitos apenas para fotos de recibos fisicos.

O campo Descritor deve refletir o fornecedor ou banco pagador, nao o tipo de despesa.

6.6 Nomenclatura de Comprovantes Corporativos (pasta Fin/Comprovantes)

Arquivos armazenados em Fin/Comprovantes/ (separados por mês em subpastas AAMM, ex.: 26-04, 26-05) — comprovantes de transferência, boletos pagos, recibos de fornecedores corporativos e guias de tributos federais — devem seguir o padrão abaixo. Aplica-se a documentos NÃO vinculados a uma obra específica (despesas administrativas, software, contabilidade, transferências pessoais do sócio-administrador).

Estrutura do código: [AAMMDD ou AAMM]-VZP-FIN-[TIPO]-[Descritor]-[ID].(pdf|png|jpg)

Componentes: (a) VZP — sigla fixa indicando documento corporativo; (b) FIN — fixo, área financeira; (c) TIPO — BOL (Boleto Bancário), CP (Comprovante de Pagamento), EX (Extrato), RC (Recibo), DAS (Documento de Arrecadação do Simples Nacional), DARF (Documento de Arrecadação de Receitas Federais), GPS (Guia da Previdência Social), GFIP (Guia FGTS), DCTFWeb; (d) AAMMDD — data da transação para CP/RC; AAMM (sem dia) para documentos mensais como DAS, DARF, extrato; (e) Descritor — PascalCase sem espaços/acentos identificando fornecedor, banco pagador ou órgão emissor (ex.: Planejar, Sicredi, ReceitaFederal); (f) ID — sequencial opcional a partir de 2 para múltiplos documentos do mesmo Descritor no mesmo dia.

Exemplos: 260406-VZP-FIN-BOL-Planejar.png (boleto Planejar Assessoria Contábil de 06/04/2026); 260406-VZP-FIN-CP-Heitor.png (Pix para Heitor); 2602-VZP-FIN-DAS.png (DAS de fevereiro/2026, mensal); 260415-VZP-FIN-DARF-IRRF.pdf (DARF de IRRF apurado em abril/2026); 260504-VZP-FIN-CP-JoaoWeslei.png.

Regras complementares: nunca usar espaços, acentos, cedilha ou caracteres especiais; nomes auto-gerados por aplicativos bancários ("Comprovante_20260406T081257549667.png") devem ser renomeados na entrada da pasta para o padrão acima — caso o pagador não possa ser identificado pelo nome auto-gerado, abrir o arquivo, identificar o destinatário e renomear; formato preferencial PDF, mas PNG/JPG aceitos para comprovantes salvos de telas de aplicativo.

6.7 Nomenclatura de Arquivos em 02-Orçamentos (pasta Compras/02-Orçamentos)

Arquivos armazenados na subpasta 02-Orçamentos/ — propostas comerciais e cotações de fornecedores recebidas pela VZP — devem seguir o padrão abaixo. Aplica-se tanto a PDFs auto-gerados por sistemas de fornecedores quanto a planilhas de comparação interna.

Estrutura do código: [AAMMDD]-[OBRA]-[TP_OBRA]-COMP-ORC-[Fornecedor]-[NumOrcamento].(pdf|xlsx)

Componentes: (a) OBRA — sigla da obra (ANIMA, COFCO, ROSE...); (b) TP_OBRA — tipo/uso (HO, PS, RE, CO, VE...); (c) COMP — fixo, indica área Compras; (d) ORC — fixo, indica orçamento (subpasta 02); (e) Fornecedor — PascalCase sem espaços/acentos (ex.: SantaLucia, ReuterMateriais, ConstroFacil); (f) NumOrcamento — número do orçamento do fornecedor (auto-gerado pelo sistema); (g) AAMMDD — data de recebimento do orçamento.

Exemplos: 260512-ANIMA-HO-COMP-ORC-AnimallePetCare-1329.pdf (substitui "ANIMALLE PET CARE-1329.pdf"); 260315-ANIMA-PS-COMP-ORC-AnimallePisoSuperior-Aproveitamento.xlsx (planilha interna de aproveitamento).

Tolerância (Versão 1.2). Arquivos PDF puramente auto-gerados por sistemas de fornecedores podem ser mantidos com o nome original no momento da recepção, desde que sejam renomeados para o padrão acima até o fechamento do orçamento (passagem para 04-Ord Comp). Nomes contendo espaços, acentos ou caracteres especiais devem ser corrigidos em qualquer hipótese; o número do orçamento e o nome do fornecedor identificáveis no nome original devem ser preservados.

6.8 Nomenclatura de Relatórios Financeiros (pasta Plan/FIN/Relatórios)

Arquivos armazenados em Plan/FIN/Relatórios/ — planilhas orçamentárias, fluxos financeiros, planilhas de pagamentos em aberto, simuladores de custo — devem seguir o padrão abaixo. Aplica-se tanto a relatórios gerados internamente pela VZP quanto a relatórios exportados de softwares de gestão financeira de obra.

Estrutura do código: [AAMMDD]-[Descritor].(pdf|xlsx)

Componentes: (a) Descritor — PascalCase sem espaços/acentos, identificando o tipo de relatório (PlanilhaOrcamentaria, FluxoFinanceiro, PagamentosEmAberto, SimuladorCustos, RelatorioDespesas); (b) AAMMDD — data de referência do relatório.

Exemplos: 260118-PlanilhaOrcamentaria.pdf, 260123-FluxoFinanceiro.pdf, 260512-PagamentosEmAberto.pdf, 260301-SimuladorCustos-ClinicaVet.xlsx.

Observação. O contexto da obra (sigla EMP-TP_OBRA) é dado pela própria pasta (cada obra tem sua Plan/FIN/Relatórios/), portanto o prefixo OBRA-TP_OBRA não é repetido no nome do arquivo — princípio de não-redundância. Relatórios mensais sem dia específico podem usar AAMM (ex.: 2604-PagamentosEmAberto.pdf para fechamento mensal de abril/2026).

Esta seção resolve a omissão apontada no LOG-Nomenclatura-VZP-Eng e encerra a divergência entre a regra geral do §6.1 e a prática consolidada nas pastas Plan/RDO, Plan/RSO, Ehs e Rh e Dp.

Regras que permanecem obrigatórias mesmo no regime de livre nomeação: (a) a PASTA que contém as evidências segue o padrão de data deste POP; (b) é vedado o uso de arquivos compactados (.rar, .zip) como forma de arquivamento — o conteúdo deve ser extraído, sob pena de impedir a busca e a indexação no SharePoint; (c) duplicatas exatas devem ser eliminadas periodicamente; (d) documentos formais (relatórios assinados, fichas, contratos, ARTs) NÃO são evidência fotográfica e seguem integralmente o padrão deste POP.

Justificativa: o volume desses acervos (centenas de arquivos por obra) torna o renomeio manual antieconômico, e a rastreabilidade já é garantida pela pasta em que o arquivo reside — sempre datada no padrão AAMMDD (RDO) ou AA-MM-DD (RSO). O nome do arquivo não é, nesses casos, o instrumento de busca.

Fotos, vídeos e capturas de tela que servem de evidência — registros fotográficos de RDO e RSO, fotos de APR e DDS, documentos digitalizados de colaboradores — ficam DISPENSADOS do padrão de nomenclatura deste POP. Aplica-se a eles o regime de livre nomeação, mantendo-se o nome original gerado pelo dispositivo, pelo WhatsApp ou pelo aplicativo de digitalização.

6.9 Fotos e Registros de Evidência (RDO, RSO, EHS e RH)

## 7. Mapa Visual da Estrutura de Pastas

Árvore completa para replicação no SharePoint:

| Pasta / Subpasta | Observação |
| --- | --- |
| VZP-Eng (raiz) | Pasta raiz do repositório SharePoint |
| └─ Ob em Andam | Obras em execução |
| └─ Ob-[Cliente]-[Tipo]-[Cid]-[UF] | Uma subpasta por obra |
| └─ 00-Import | CAIXA DE ENTRADA — triagem periodica pela VZP (§4.3.0) |
| └─ 01-Compras | 00-Mem Calc Quant → 04-Ord Comp (sem pagamentos; NF-e em 06-Fisc) |
| └─ 02-Contratos | Por tipo de serviço contratado |
| └─ 03-Doc | Atas / Imóvel / Proj / Repres |
| └─ 04-Ehs | APR e documentos de segurança |
| └─ 05-Fin | 01-Ord Pag / 02-Boletos / 03-Comprov (obrigatoria) |
| └─ 06-Fisc | NFs e fiscal da obra |
| └─ 07-ITs | Copia do master corporativo, sincronizada |
| └─ 08-Med Serv Prop | Medições VZP |
| └─ 09-Med Serv Terc | Medições terceiros |
| └─ 10-Plan | RDO / RSO / FIN |
| └─ 11-Proj | Arquitetura / Estrutura / ELE / HID / AC / SPDA / INC / CFTV / ELV / AMB / CAN / LUM |
| └─ 12-Rh e Dp | Doc de Ativos / Inativos |
| └─ Ob Concluidas | Obras finalizadas (mesma estrutura interna) |
| └─ Proj | Projetos avulsos sem obra associada |
| └─ Compras | Compras corporativas |
| └─ 00-Mem Calc Quant / 01-Solicit Comp / 02-Orçamentos |  |
| └─ 03-Mapa de Cotações / 04-Ord Comp / 05-Ord Pag / 06-Comprov / 07-Nfe |  |
| └─ Curs e Trein | Cursos e treinamentos |
| └─ Faculdade | Semestres 1 a 10 |
| └─ Auto Cad 2D / Revit / SketchUp / Excel / [outros] |  |
| └─ Doc e Cad | Documentos legais e cadastrais |
| └─ ARTs / Certidões e Declarações / Contratos / DAS |  |
| └─ Laudos / Modelos / NRs / Prog. Legais SST / Seguros / Visitas Técnicas |  |
| └─ Est | Equipamentos e bens patrimoniais |
| └─ Fin | Financeiro corporativo |
| └─ Boletos / Comprovantes / Horas Tecnicas / Recibos |  |
| └─ Fisc | Fiscal e tributário |
| └─ Estudos Tributários / Notas Emitidas |  |
| └─ Inst Trab e Pop's | ITs e POPs corporativos |
| └─ Mark e Prop | Marketing e propostas comerciais |
| └─ Camps de Mark / Imag Prod / Imag Servi / Imag de Ob / Logo / Placa de Obra |  |
| └─ Rh e Dp | RH corporativo |
| └─ Soft, Prog e Manuais | Softwares e licenças |
| └─ Revit 2026 / Civil 3D 2026 / TQS v25 / Tekla 2025 / GstarCAD 2024 / FTool 6.2 |  |

## 8. Instruções para Configuração no SharePoint

### 8.1 Estrutura Recomendada

Criar um Site de Equipe no SharePoint: VZP Engenharia

Criar uma Biblioteca de Documentos principal chamada VZP-Eng

Replicar toda a árvore de pastas deste POP dentro dessa biblioteca

Obras em andamento e concluídas devem estar em subpastas separadas

### 8.2 Permissões Sugeridas

Acesso total: Vitor Zanchet (gestor) e colaboradores diretos

Acesso restrito por pasta de obra: parceiros e terceiros

Pastas Doc e Cad, Fin e Fisc: acesso restrito ao gestor

### 8.3 Sincronização OneDrive

Sincronizar a biblioteca completa no computador do gestor

Demais colaboradores: sincronizar somente as pastas das obras em que atuam

Dúvidas sobre nomenclatura ou criação de novas pastas: consultar o gestor antes de criar qualquer item fora do padrão deste POP.

## 9. Controle do Documento

| Versão | Data | Responsável | Descrição |
| --- | --- | --- | --- |
| 1.0 | Maio/2026 | Vitor Zanchet | Versão inicial |
| 1.1 | 15/05/2026 | Vitor Zanchet | Inserção em §6.2 de referência ao POP-01.00 (Procedimento Operacional Padrão de Projetos) como POP autoritativo para nomenclatura de documentos de projeto. Padronização editorial do título do POP-04 para a forma completa 'Procedimento Operacional Padrão de Organização de Arquivos e Pastas' (capa e cabeçalho). |
| 1.2 | 17/05/2026 | Vitor Zanchet | Adicionada disciplina Luminotecnico em §4.3.1. Adicionada subpasta Relatórios em §4.3.2 (Plan/FIN). Adicionada regra geral de subpasta _Obsoletos/ em pastas Proj/<disciplina>/. Harmonizada ambiguidade entre POP-04 §6.1 e POP-01 §5.7 sobre separadores internos (underscore para arquivos de projeto, espaços naturais com Title Case para arquivos de gestão administrativa). Criadas três novas seções de nomenclatura: §6.6 (Fin/Comprovantes corporativo — padrão VZP-FIN), §6.7 (02-Orçamentos — padrão OBRA-TP-COMP-ORC), §6.8 (Plan/FIN/Relatórios — padrão Descritor-AAMMDD). Referência à nova IT-06.01 (Traços de Obra) consolidada em Inst Trab e Pop's. |
| 1.3 | 18/07/2026 | Vitor Zanchet | Harmonizacao POP x repositorio apos revisao automatica de nomenclatura. §5.1/§4.2: nomes de pasta corrigidos para ITs, Med Serv Prop, ARTs e NRs, eliminando apostrofo e acento vedados pelo §6.1. §5.2: estrutura de Fin atualizada para as subpastas numeradas 00-Ord Pag a 07-Investimentos; Horas Tecnicas transferida de Doc e Cad para Fin. §5.3: estrutura de Fisc atualizada para 01-Nfe Entradas a 04-Informe de Rendimentos. Criada a §6.9, que institui o regime de livre nomeacao para fotos e registros de evidencia (RDO, RSO, EHS, RH) e veda o arquivamento em .rar/.zip. |
| 1.4 | 18/07/2026 | Vitor Zanchet | Instituida a caixa de entrada por obra: criada a §4.3.0 (00-Import), com regras de deposito, triagem e vedacoes. §4.2: numeracao obrigatoria das subpastas de obra (00-Import, 11-Proj, 10-Plan, 07-ITs, 01-Compras, 05-Fin opcional, 02-Contratos, 03-Doc, 04-Ehs, 06-Fisc, 08-Med Serv Prop, 09-Med Serv Terc, 12-Rh e Dp), fixando a ordem de exibicao no SharePoint. Mapa visual do §7 atualizado. Aplicado a 11 obras em 18/07/2026. |
| 1.5 | 18/07/2026 | Vitor Zanchet | Separacao entre aquisicao e financeiro na obra. Ordens de pagamento e comprovantes deixam de integrar 01-Compras e passam a residir sempre em 05-Fin (regra do gestor). §4.3.3: Compras reduzida a 6 subpastas (00-Mem Calc Quant a 05-Nfe), removidas 05-Ord Pag e 06-Comprov; 07-Nfe renumerada para 05-Nfe. Criada a §4.3.8 (05-Fin da obra: 01-Ord Pag, 02-Boletos, 03-Comprov), tornando a pasta obrigatoria em toda obra. §6.5 atualizada: comprovantes de obra agora em 05-Fin/03-Comprov. Conteudo migrado nas 11 obras em 18/07/2026. |
| 1.6 | 18/07/2026 | Vitor Zanchet | Padronizacao data-first do escritorio: AAMMDD passa a ser o PRIMEIRO bloco do nome em todos os padroes de nomenclatura (§6.2 arquivos de projeto, §6.5 comprovantes da obra, §6.6 Fin corporativo VZP-FIN, §6.7 orcamentos, §6.8 relatorios financeiros), alinhando a VZP as convencoes ja adotadas pela BASE e pela VLA. Exemplos e formatos-modelo atualizados. Numeracao de subpastas de obra (00-Import a 12) mantida da v1.5. |
| 1.7 | 19/07/2026 | Vitor Zanchet | Correcao: NF-e de entrada e documento FISCAL — removida a subpasta 05-Nfe de 01-Compras (Compras encerra em 04-Ord Comp); a NF-e recebida passa a residir em 06-Fisc. §4.3.3, tabela de subpastas, tabela de Compras e mapa visual (§7) atualizados. |
| 1.8 | 19/07/2026 | Vitor Zanchet | Reordenacao da numeracao das subpastas de obra para ordem ALFABETICA (00-Import mantida no topo), a pedido do gestor: 00-Import, 01-Compras, 02-Contratos, 03-Doc, 04-Ehs, 05-Fin, 06-Fisc, 07-ITs, 08-Med Serv Prop, 09-Med Serv Terc, 10-Plan, 11-Proj, 12-Rh e Dp. Tabela de subpastas, mapa visual (§7) e referencias no texto atualizados; aplicado nas pastas das obras/servicos. |
| 1.9 | 19/07/2026 | Vitor Zanchet | Atualizada a Estrutura Raiz (§3): as pastas de 1o nivel passam a ser numeradas com 00-Import no topo, refletindo a numeracao aplicada no repositorio. Inclui a 00-Import corporativa e a Correcao Manual de Arquivos. |

Elaborado por: Vitor Zanchet – Engenheiro Civil | VZP Engenharia

E-mail: vitor@vzpengenharia.com.br  |  Instagram: @vzp.engenharia

ADENDO 01 – Novos Prefixos e Convenções de Nomenclatura

Data: 25/05/2026  |  Responsável: VZP-Eng

1. Prefixo LCM – Lista de Controle de Materiais / Suprimentos

Documentos de controle de suprimentos e materiais internos VZP-Eng utilizam o prefixo LCM, seguindo o mesmo padrão de numeração IT/POP:

| Prefixo | Formato | Exemplo |
| --- | --- | --- |
| LCM | LCM-XX.XX-VZP-Descricao-RXX.ext | LCM-01.00-VZP-Suprimentos-R01.docx |

Localização: Inst Trab e Pop's/

2. Convenção COFCO-EHS – Documentos EHS de Terceiros (COFCO)

Documentos de EHS emitidos pela COFCO e aplicáveis às obras do parque COFCO-Basenorte recebem o prefixo COFCO-EHS para identificação padronizada:

| Documento original | Nome padronizado |
| --- | --- |
| Proc. EHS 009 – Gestão de Contratadas | COFCO-EHS-009-Gestao_Contratadas.pdf |
| Padronização EPIs – Fase 1 (Capacete, Luvas, Botinas) | COFCO-EHS-EPIs-Contratados-Fase1-Capacete_Luvas_Botinas.pdf |

Localização: [Obra]/Ehs/ (raiz da pasta EHS de cada obra COFCO)
