# Referência operacional

- Empresa: VLA Imobiliária
- Documento vigente: `POP-04.00-VLA-Organizacao-Arquivos-R01.docx`
- Origem: pasta mestra de POPs/ITs da empresa
- Regra: ao existir nova revisão, reextrair e revalidar esta referência antes do uso.

> Esta referência preserva o conteúdo operacional extraído do documento fonte. Em caso de dúvida, conflito, perda de formatação ou informação incompleta, consultar o arquivo original vigente.

VLA IMOBILIÁRIA

Gestão Patrimonial e Administração de Imóveis — Sorriso/MT

PROCEDIMENTO DE ORGANIZAÇÃO DE ARQUIVOS E PASTAS

POP-04.00 — Organização de Arquivos — Rev. 01

Estrutura de Pastas, Subpastas e Nomenclatura de Arquivos para SharePoint

| Campo | Conteúdo |
| --- | --- |
| Código | POP-04.00 — VLA Imobiliária |
| Revisão | R01 (substitui R00 de Maio/2026) |
| Data de emissão | 21/07/2026 |
| Elaborado por | Vitor Zanchet — Eng. Civil / Gestão Patrimonial |
| Alinhamento | Padrão-mestre do Grupo: POP-04 R06 (Base Empreendimentos), espelhado pela VZP-Eng |
| Aplicação | Microsoft SharePoint / OneDrive for Business |

Nota de revisão. A R01 alinha a nomenclatura da VLA Imobiliária ao padrão-mestre do Grupo (Base R06 / VZP): separador hífen, caixa mista (Title Case), descritores em PascalCase, sem acentos nem cedilha, revisão ao final e as convenções de governança 00-Import, _Obsoletos, Correção Manual de Arquivos e Logs. A estrutura temática por imóvel é mantida; muda a forma de nomear arquivos e a governança das pastas.

## Sumário

## 1. Objetivo

Estabelecer a estrutura padronizada de pastas e a convenção de nomenclatura de arquivos do repositório digital da VLA Imobiliária, garantindo rastreabilidade por imóvel, período e tipo de documento, integridade documental, busca eficiente e aderência ao padrão único de nomenclatura do Grupo (Base / VZP).

Este POP rege como os documentos administrativos, contratuais, fiscais e financeiros dos imóveis administrados são armazenados e nomeados. As regras de documentos de projeto (pranchas, memoriais, laudos) seguem o POP-01.00; em conflito no tratamento dessas peças, prevalece o POP-01.00.

## 2. Campo de aplicação

Aplica-se a todos os colaboradores, parceiros e prestadores que produzam, armazenem ou consultem arquivos no repositório da VLA Imobiliária: imóveis em carteira e fora dela, documentos e cadastros, financeiro, fiscal, marketing, RH, cursos e softwares.

## 3. Estrutura raiz do repositório

A raiz é dividida em módulos de primeiro nível, cada um com prefixo numérico de 2 dígitos que fixa a ordem de exibição no SharePoint. O prefixo integra o nome e não deve ser omitido.

| # | Módulo | Sigla | Conteúdo |
| --- | --- | --- | --- |
| 00 | Import | IMP | Caixa de entrada geral (arquivos a triar) — §4.3 |
| 01 | Bens e Imóveis em Carteira | BIC | Documentos por imóvel: contratos, boletos, vistorias, IPTU, comissões |
| 02 | Bens e Imóveis fora da Carteira | BFC | Imóveis não administrados ativamente |
| 03 | Correção Manual de Arquivos | CMA | Triagem humana: Análise e Exclusão — §7 |
| 04 | Curs e Trein | CT | Cursos e treinamentos |
| 05 | Doc e Cad | DC | Cadastros, modelos de contrato, fichas de inquilinos, família Zanchet |
| 06 | Est | EST | Documentos estratégicos e organização interna |
| 07 | Fin | FIN | Financeiro: extratos, boletos, cobrança — por titular |
| 08 | Fisc | FISC | Fiscal: IPTU por ano e proprietário, ITR, tabela IR |
| 09 | Inst Trab e Pop's | ITP | ITs, POPs, Normas, Checklists e Logs — §8 |
| 10 | Mark e Prop | MKT | Marketing: anúncios, logomarca, catálogos, papelaria |
| 11 | Rh e Dp | RH | Recursos Humanos e Departamento Pessoal |
| 12 | Soft, Prog e Manuais | SPM | Softwares, programas, manuais e licenças |

## 4. Estrutura de imóveis (módulo BIC)

### 4.1 Nomenclatura da pasta de imóvel

Cada imóvel recebe pasta com prefixo numérico e nome em caixa mista, sem acentos, com hífen entre blocos:

NN-[Imovel]-[Localizacao]

Exemplos: 01-Apartamento Bela Vitta · 03-Casa Condominio Ilha Bela-Sorriso · 05-Colinas.

### 4.2 Subpastas padrão de cada imóvel de locação

Numeração obrigatória. Todas devem existir em cada imóvel de locação, na ordem do ciclo do contrato. As variações da R00 (TERMO VISTORIA/VISTORIA; COMPROVANTE/COMPROVANTES; CONTA/CONTAS DE CONSUMO) ficam padronizadas conforme abaixo.

| # | Subpasta | Conteúdo esperado |
| --- | --- | --- |
| 00 | Import | Entrada a triar (transitório) — §4.3 |
| 01 | Boletos | Boletos de cobrança ao inquilino, por ano |
| 02 | Comissao | Comprovantes e planilhas de comissão |
| 03 | Comprovantes | Comprovantes de pagamentos recebidos, por ano |
| 04 | Contas Consumo | Água, luz, gás, internet — imóvel e inquilino |
| 05 | Contrato | Contrato de locação vigente e aditivos |
| 06 | Distrato | Distrato(s) de locações encerradas |
| 07 | Documentos | Inquilino / Fiador / Imovel / Proprietario |
| 08 | Informe Pagamentos | Informes anuais ao proprietário |
| 09 | Iptu | Carnês e comprovantes de IPTU, por ano |
| 10 | Notas Fiscais | Notas fiscais do imóvel |
| 11 | Reajuste Aluguel | Cartas, planilhas e notificações de reajuste |
| 12 | Vistoria | Termos de entrada/saída (subpastas Fotos e Rascunhos) |
| — | _Obsoletos | Versões superadas e duplicatas — §4.4 |

### 4.3 00-Import — caixa de entrada

Ponto único de entrada, no topo por ser 00. Separa o ato de ENTREGAR (livre) do ato de CLASSIFICAR (padronizado, responsabilidade da VLA).

- Quem deposita: solta o arquivo (nome/formato livres); se o contexto não for óbvio, cria subpasta com uma palavra de contexto (ex.: nf condominio); não apaga nem reorganiza o que já estiver lá.

- Triagem (VLA): a pasta é esvaziada periodicamente — cada arquivo é renomeado por este POP e MOVIDO (nunca copiado) para a subpasta definitiva; ambíguos vão para Correção Manual de Arquivos/Análise; a triagem é registrada no LOG-Nomenclatura.

- Vedações: não é área de armazenamento; é vedado manter arquivo ali como definitivo ou referenciá-lo em e-mail/contrato — o caminho é transitório.

### 4.4 _Obsoletos

Em cada pasta que acumule versões, a subpasta _Obsoletos guarda versões superadas, revisões antigas e duplicatas. O prefixo "_" a mantém no topo. Conteúdos nunca são excluídos sem revisão do gestor — preservados para auditoria. Substitui variações antigas como OLD, "revisões antigas" e "_Duplicatas".

## 5. Áreas funcionais

Módulos corporativos (não vinculados a um imóvel específico). Cada um mantém prefixo numérico e, quando acumular versões, subpasta _Obsoletos.

| Módulo | Organização interna |
| --- | --- |
| 05-Doc e Cad | Certidões e Procurações; Fichas de Inquilinos (por imóvel); Modelos de Contratos; Zanchet (família/sucessão) |
| 07-Fin | Extratos-Boletos-Cobranca por titular de conta (ex.: 01-Amanda, 02-Diogo…); subpastas Cobranca, Emissao de Boletos, Extratos |
| 08-Fisc | IPTU por ano → por proprietário; Tabela IR por ano |
| 10-Mark e Prop | Anúncio de Imóveis (por imóvel); Logo VLA; Cartões; Catálogo; Papelaria; Placa |

## 6. Convenção de nomenclatura de arquivos

### 6.1 Regras gerais

- Usar hífen (-) como separador entre blocos do código.

- Sem espaços, acentos, cedilha ou caracteres especiais nos blocos de código.

- Caixa mista (Title Case) para descrições em prosa natural (ex.: Locacao Andre Silva); descritores de fornecedor/pessoa/banco em PascalCase (ex.: Sicredi, Colinas491A).

- Datas: AAMMDD para documento com dia; AAMM para mensais; AAAA para anuais (IPTU, IR).

- Revisão sempre ao final: R00, R01, R02… Versões em desenvolvimento usam sufixo -DEV.

- Nome curto e identificável sem abrir o arquivo.

### 6.2 Documentos de imóvel (contratos, distratos, vistorias)

[Imovel]-[TIPO]-[Descricao]-[AAMMDD]-RXX.ext

Exemplos: BelaVitta-CTR-Locacao Andre Silva-260115-R00.pdf · IlhaBela-VIST-Entrada-260201-R00.pdf · Colinas491A-DIST-Encerramento-260430-R00.pdf.

### 6.3 Comprovantes, boletos e comissões (por imóvel)

[AAMMDD]-[Imovel]-FIN-[TIPO]-[Descritor]-[ID].pdf

Exemplos: 260510-BelaVitta-FIN-BOL-Condominio.pdf · 260510-BelaVitta-FIN-CP-Elo.pdf · 260430-Colinas491B-FIN-COM-Imobiliaria.pdf. Extratos mensais usam AAMM.

### 6.4 IPTU e documentos fiscais

[AAAA]-[Proprietario]-IPTU-[Imovel].pdf

Exemplos: 2026-Luciana-IPTU-Colinas491A.pdf · 2026-SPZ-IPTU-Lote12Qd28.pdf.

### 6.5 Extratos e documentos financeiros corporativos

[AAMM]-[Titular]-EX-[Conta].ext | [AAMMDD]-VLA-FIN-[TIPO]-[Descritor]-[ID].ext

Exemplos: 2601-Luciana-EX-41000-4.ofx · 260406-VLA-FIN-CP-Planejar.pdf.

### 6.6 Tabela de tipos (TIPO)

| Sigla | Tipo | Sigla | Tipo |
| --- | --- | --- | --- |
| CTR | Contrato de locação | BOL | Boleto |
| DIST | Distrato | CP | Comprovante de pagamento |
| VIST | Termo de vistoria | EX | Extrato bancário |
| REAJ | Reajuste de aluguel | COM | Comissão |
| IPTU | IPTU | NF | Nota fiscal |
| INF | Informe (pagamentos/rendimentos) | CONS | Contas de consumo |
| DOC | Documento/certidão | FICHA | Ficha cadastral |

Siglas de imóvel (Imovel) em PascalCase, ex.: BelaVitta, Riviera, IlhaBela, Colinas491A..E, EscSorriso, Suica329, SitioSaoRoque, SPZ, Coavil. Novos imóveis recebem sigla no cadastro da pasta.

## 7. Correção Manual de Arquivos e Logs

O módulo 03-Correção Manual de Arquivos recebe o que exige intervenção humana, em duas subpastas: Análise (arquivos ambíguos, de projeto/imóvel incerto, nomenclatura duvidosa) e Exclusão (duplicatas, revisões antigas, pastas vazias e obsoletos candidatos a descarte). Itens claramente obsoletos podem ser removidos direto, sempre registrando no log.

Toda triagem e renomeação em massa é registrada no LOG fixo LOG-Nomenclatura-VLA-Imobiliaria.pdf, em 09-Inst Trab e Pop's/Logs/. As decisões do gestor sobre dúvidas recorrentes ficam em DECISOES-Nomenclatura-VLA-Imobiliaria.md e passam a ser aplicadas automaticamente.

## 8. Inst Trab e Pop's — subpastas codificadas

A pasta 09-Inst Trab e Pop's organiza-se por subpastas com prefixo de código, no padrão do Grupo:

| Prefixo | Subpasta | Conteúdo |
| --- | --- | --- |
| POP | Procedimentos | Procedimentos Operacionais Padrão de gestão |
| IT | Instruções de Trabalho | Instruções técnicas de execução |
| CHK | Checklists | Listas de verificação (ex.: limpeza, vistoria) |
| LCM | Listas e Controles | Planilhas de controle de materiais/serviços |
| NRM | Normas | Normas técnicas e legislação (locação, condomínio) |
| LOG | Logs | Registros de auditoria de nomenclatura e organização |

Arquivos substituídos vão para _Obsoletos. O nome segue o padrão geral (§6.1): sem acentos, hífen entre blocos, revisão ao final. Ex.: POP-04.00-VLA-Organizacao-Arquivos-R01.pdf.

## 9. Configuração no SharePoint

- Biblioteca principal replicando os 13 módulos da §3; versionamento automático (mínimo 10 versões).

- Metadados gerenciados: Imóvel, Tipo de Documento, Ano, Proprietário, Status do Imóvel.

- Alerta automático na pasta Contrato de cada imóvel a cada novo upload; exibição do IPTU agrupada por Ano + Proprietário.

## 10. Controle de revisões

| Revisão | Data | Responsável | Descrição |
| --- | --- | --- | --- |
| R00 | Mai/2026 | Vitor Zanchet | Versão inicial — mapeamento da estrutura + padrão underscore/MAIÚSCULAS. |
| R01 | 21/07/2026 | Vitor Zanchet | Alinhamento ao padrão-mestre do Grupo (Base R06 / VZP): hífen, Title Case, PascalCase, sem acentos; governança 00-Import, _Obsoletos, Correção Manual e Logs; Inst Trab codificada; tabelas de TIPO e siglas de imóvel. |

VLA Imobiliária — Sorriso/MT — documento de uso interno. Padrão-mestre de nomenclatura do Grupo: Base Empreendimentos POP-04 R06.
