---
name: "contexto-canil-lucini"
description: "Contexto operacional do Canil Lucini Ltda (criação de Spitz Alemão em Sorriso/MT) e da Animalle Pet Care. Use sempre que for gerar ou revisar documentos do Canil Lucini (dossiê de riscos, POPs, contratos) ou relatórios da Animalle Pet Care (ex.: laudo de ultrassom), para manter dados reais, aprendizados e padrões visuais já validados."
---

## Canil Lucini Ltda

Negócio de criação de Spitz Alemão (Lulu da Pomerânia), em Sorriso, Mato Grosso, Brasil.
CNPJ: 59.226.214/0001-23
Endereço: Av. Brasil, 2030, Sala 01 — Centro-Norte, Sorriso/MT
Situação: CNPJ ativo, mas com licenças ambiental e sanitária pendentes; opera em área residencial — isso gera exposição regulatória que deve ser considerada em qualquer documento relacionado.
Sócia-administradora (registro oficial): Vitória Pinheiro Lucini
Contato: lucini.v@hotmail.com, (66) 99636-6301

Vitor também produz documentos profissionais para a Animalle Pet Care, clínica veterinária em Sorriso/MT (ex.: laudos de ultrassom).

O objetivo recorrente é criar documentos profissionais e com identidade visual polida — POPs, dossiês de risco, laudos clínicos — refletindo necessidades operacionais e jurídicas reais (não modelos genéricos).

### Trabalhos já realizados

1. **Dossiê de mitigação de riscos (Canil Lucini)** — PDF de 9 páginas cobrindo riscos legais/regulatórios, acústicos/técnicos, relacionais/vizinhança e sanitários/bem-estar animal (R1–R4), tabela de referência de multas com bases legais brasileiras, e protocolo de resposta. Inclui nota técnica sobre Autorização Ambiental Simplificada (AAS/AAF) em MT para atividades de baixo impacto.
2. **POPs (Canil Lucini)** — Nove documentos DOCX (POP-OBT-001 a POP-VIG-009) cobrindo: morte de animal, vacinação, reprodução/gestação, parto/ninhada, venda/entrega, higiene, doença/isolamento, registro de pedigree ALKC, monitoramento comportamental. Referenciam as cláusulas contratuais padrão do negócio e exigências da ALKC.
3. **Laudo de ultrassom veterinário (Animalle Pet Care)** — PDF de laudo de paciente com achados estruturados de órgãos abdominais, campos de checkbox, impressões diagnósticas e blocos de assinatura dupla.

### Aprendizados e princípios-chave

- **Logo/layout em DOCX**: problema persistente de posicionamento do logo em Word nunca foi resolvido programaticamente. Vitor prefere ajustar o layout no Word manualmente. Não tentar corrigir a posição do logo em arquivos DOCX via código — piora o resultado.
- **PDF é preferido para qualidade visual** — Vitor prefere consistentemente PDF polido a formatação básica em Word quando a estética importa.
- **Disclaimer obrigatório**: todo documento que mencione exposição regulatória deve incluir aviso de que valores de multas e interpretações jurídicas precisam ser confirmados com autoridades locais e profissionais qualificados.

### Abordagem e padrões de trabalho

- Vitor trabalha de forma iterativa — revisa outputs e pede ajustes pontuais (visuais, estruturais ou de conteúdo) em múltiplas rodadas.
- Forte preferência por estética profissional e polimento visual: cor institucional teal (`#008080`), cabeçalhos/rodapés consistentes, elementos com código de cor, tipografia limpa.
- Documentos sempre fundamentados em contexto operacional real (CNPJ, endereços, nomes, bases legais reais) — nunca modelos genéricos.

### Ferramentas e recursos

- **Python + ReportLab**: ferramenta principal para geração de PDF. Padrões que funcionam bem: `BaseDocTemplate` com `PageTemplate` separados para capa vs. corpo, `Table` aninhadas para chips de cor, `KeepTogether` para manter blocos íntegros, `pdf2image` (dpi=120) para revisão visual.
- **python-docx**: usado para geração de DOCX/POPs; deixar o posicionamento do logo para o Vitor ajustar manualmente.
- Caminho de entrega de output: `/mnt/user-data/outputs/`
- Ativo de marca: logo Spitz Lucini (JPEG, fundo teal); ao usar em PDFs, amostrar pixels do canto para igualar a cor de preenchimento do canvas elimina artefatos visíveis de borda.

