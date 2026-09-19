---
name: "contexto-pessoal-vitor"
description: "Contexto pessoal do Vitor Zanchet Pereira: família (Vitória, bebê previsto nov/2026), saúde/fitness, financeiro pessoal, reforma residencial, viagens, processo LATAM e canil Spitz Alemão. Usar como pano de fundo em qualquer assunto pessoal do Vitor (fora do escopo de trabalho da VZP Engenharia). Não confundir com o skill contexto-vitor-vzp, que cobre apenas o profissional."
---

Vitor Zanchet Pereira é engenheiro civil especialista em planejamento, baseado em Sorriso, Mato Grosso. Dirige a VZP Engenharia (contexto profissional coberto pelo skill separado `contexto-vitor-vzp`). Este skill cobre a vida pessoal: família, saúde, financeiro pessoal, reforma da casa, viagens, processo jurídico e o canil.

Vitor tem forte base técnica e se engaja melhor com respostas estruturadas, diretas e ricas em detalhe — prefere avaliações honestas a recomendações suavizadas e valoriza quando trade-offs são nomeados explicitamente. Prefere que o Claude construa entregáveis completos usando premissas razoáveis e declaradas, em vez de fazer múltiplas perguntas de esclarecimento antes de agir. Quando precisar coletar informação estruturada dele, usar formato de uma pergunta por vez. Comunica-se em português brasileiro casual.

## Família
Companheira: Vitória Pinheiro Lucini, veterinária, dona da própria clínica (Animalle Pet Care). Primeiro filho a caminho, previsto para novembro de 2026. Vitória é stakeholder relevante em decisões pessoais (aprovação de decoração, compras de itens de bebê, planejamento de viagens). Sogros: Claudinei e Raquel Lucini. Fé católica ativa (prática e catequese).

## Bebê (projeto ativo até nov/2026)
- Travel system Infanti Romanzo com Bebê Conforto Zion e base ISOFIX: já comprado.
- Bomba de leite: Spectra S1 Plus recomendada e pesquisa concluída.
- Preparador de fórmula (Baby Brezza): adiado até confirmar necessidade pós-parto.
- Guia de cuidados domésticos para a diarista: concluído e entregue em PDF.
- Pendente: compras finais de bomba de leite e itens de bebê antes de novembro de 2026.

## Fitness / recomposição corporal
Plano finalizado em PDF (`Plano_VZP_Vitor_Final.pdf`): divisão Upper/Lower, cardio Zona 2 na bike 5x/semana (113–125 bpm), meta calórica diária com ~180g de proteína. Preferência por exercícios em máquina; trabalho de costas superiores limitado aos dias de upper body. Em aberto: possível reintrodução de movimentos com peso livre (agachamento, levantamento terra romeno) para melhorar recomposição — sinalizado mas não decidido.

## Financeiro pessoal
Planilha `Controle_Financeiro__Vitor__SIMULAÇÃO` em múltiplas revisões; o diretório do projeto pode ter versão desatualizada (REV01) — sempre preferir arquivo enviado diretamente para análise. Versão de trabalho mantida localmente em Excel. Integração via Google Apps Script com API Pluggy para sync automático de transações do Nubank foi desenhada; status de deploy desconhecido.

## Reforma residencial (quarto do casal / master bedroom)
Fluxo de trabalho: gerar conceitos visuais (ferramentas externas de IA de imagem, ex. Manus/ChatGPT — Microsoft Copilot é rejeitado para tarefas criativas/imagem) → aprovação da Vitória → só então seguir para documentação técnica e orçamento com o Claude. Aprovação visual sempre precede documentação técnica/orçamento — não pular etapa mesmo se solicitado.

## Processo jurídico — LATAM Airlines
Causa ganha na fase atual. Advogada: Poliana Perin. Honorários: 30% de êxito. LATAM ainda pode recorrer.

## Canil (Spitz Alemão, Sorriso)
Operação em zona residencial. Possui CNPJ mas não tem licenças ambiental e sanitária — dossiê de risco já produzido. Licenciamento de conformidade é item de ação em aberto.

## Viagens
Viagem em grupo para o Caribe/internacional planejada para final de março de 2027 (San Blas, Panamá, 4 pessoas/2 casais). Pesquisa comparativa de destinos e comparação de regiões de veleiro já produzidas em PDF.

## Preferências de entrega e ferramentas
- Padrão de escalonamento de saída: resposta no chat → PDF → HTML completo.
- PDF: ReportLab; validar páginas visualmente via `pdftoppm` antes da entrega; cores VZP (azul-escuro/laranja) quando o documento for da empresa; evitar emoji acima de U+2600; células de tabela com conteúdo longo usam `Paragraph()` com `colWidths` definidos.
- Google Calendar: lembretes/notificações não podem ser configurados via API (config manual); fuso `America/Cuiaba`; eventos recorrentes usam `RRULE:FREQ=YEARLY`. Calendário de aniversários da família já preenchido com eventos anuais recorrentes.
- Integrações pessoais: Gmail (`vitorzanchet@gmail.com`), Google Calendar (ID principal `vitorzanchet@gmail.com`), Google Drive. Estrutura no Drive: `Vitor Z.P → Fin → Controles Financeiros` (arquivos `.xlsx` não recuperáveis via API do Drive — requerem upload direto).
- Automação residencial: replicador de IR Intelbras (iR 1000 ou similar) para AC; ecossistema do app Mibo para câmeras de segurança.

Nota de origem: este conteúdo foi migrado de um projeto pessoal separado no Claude.ai ("Vitor Zanchet Pereira — Projeto pessoal, saúde, família, viagens e bem estar") antes de esse projeto ser apagado, para que o contexto não se perdesse.
