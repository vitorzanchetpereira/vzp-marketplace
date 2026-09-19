---
name: gestao-contatos-vzp
description: "Padronizar contatos do Vitor/VZP no Google Contatos: nomenclatura TIPO-Solução-Função-Empresa-Pessoa, códigos, regra de telefone e fluxo de salvar/atualizar. Usar ao criar, corrigir ou reclassificar qualquer contato (inclusive a partir de print do WhatsApp)."
---

# Gestão de Contatos — Padrão VZP

O **Google Contatos** é a fonte-mestra dos contatos do Vitor. A planilha `260629-VZP-CONTATOS-Padronizacao_Mestre_vXX.xlsx` (VZP-Eng/14-Soft, Prog e Manuais/Contatos 2026), aba **Padrão**, é a legenda dos códigos. Sempre grave no Google Contatos; a planilha só é editada quando o Vitor pedir para registrar um código novo.

## Padrão de nome

`[TIPO] - [Solução] - [Função] - [Empresa] - [Pessoa]`, separado por " - ", **omitindo os segmentos vazios**. Preencher também os campos **empresa** e **cargo** do contato quando fizer sentido. Nomes em MAIÚSCULAS; sem títulos (Eng/Arq/Dr).

## Telefone (obrigatório)

Sempre `+55 + DDD + 9 + 8 dígitos`. Se o número vier com 8 dígitos após o DDD (celular sem o 9), **prefixe o 9**. Ex.: `66 9974-3285` → `+5566999743285`. Fixo fica sem o 9.

## Códigos de TIPO

- **MAT** só material · **SERV** só serviço · **MAT+SERV** fornece e instala
- **CLI** cliente · **INC** incorporadora (Base Empreendimentos) · **ORG** órgão/concessionária (ex.: Águas de Sorriso/Aegea)
- **COMBUST** posto de combustível
- **FAM** família · **AMG** amigo · **EDU** educação · **PES/OUT** pessoal/outros

## Solução (o que é/faz)

Material: ELE, HID, GES, VID, TIN, MET (estrut. metálica), CON (concreto/cimento/brita), REV, ESQ, FER, COB, GER.
Serviço: PINT, ALV, TERR, SERR (serralheria/solda), TRANS, TOPO, PROJ, PLAN, CLIMA, IMP, IMOB, MKT, MEC (mecânica/auto elétrica/manutenção), FIT, FINAN, COMER (comércio/varejo — restaurante, loja, mercado), SST, CONST (construção/obra), **LOC** (locação), **MAQ** (máquinas/ferramentas), **FUND** (fundações), **POSTO** (posto de combustível).

## Função

OP (operacional), COM, TEC, ADM, FIN, JUR, DIR, ARQ, ENG, ENG OB, QUA, COMP.

## Regras já fixadas pelo Vitor

- **Posto de combustível** → `COMBUST - POSTO - [nome] - [local]`.
- **Locadora de máquinas/ferramentas** (Casa do Construtor, Mestre da Obra, Loca Sorriso, Vitrine, empilhadeira, mini escavadeira) → `SERV - LOC - MAQ - [empresa/pessoa]`.
- **Empreiteiro** (mão de obra de construção) → `SERV - CONST - [pessoa]`, cargo EMPREITEIRO. **Não** classificar empreiteiro como PROJ.
- **Operário** (pedreiro/servente/operador de máquinas) → `SERV - [solução] - OP - [empresa] - [pessoa]`, cargo descritivo.
- **Fundações** (projeto e/ou execução) → `SERV - FUND - [empresa] - [pessoa]`.
- **Mecânica/auto elétrica** → `SERV - MEC - ...`. **Concreteira** → `MAT - CON - ...`. **Estruturas metálicas** → `MAT - MET - ...`. **Restaurante/food** → `SERV - COMER - ...`.
- **Interno da Base Empreendimentos** → `INC - CONST - [função] - BASE EMPREENDIMENTOS - [pessoa]`.
- **Família** → `FAM - [relação] - [nome]`, cargo = relação. Relações: PRIMO, PRIMA, IRMÃO, IRMÃ, PAI, MÃE, TIO, TIA, SOGRO, SOGRA, CUN (cunhado), AVÓ, AVÔ, ESP (esposa). Marido/esposa de parente entra como PRIMO/PRIMA por afinidade se o Vitor tratar assim.
- **Amigo** → `AMG - [nome]`.

## Fluxo

1. Antes de criar, **buscar duplicidade** (`buscar_contato`) pelo telefone e pelo nome. Se já existir salvo fora do padrão, atualizar em vez de duplicar.
2. Montar o nome no padrão; preencher empresa e cargo.
3. Criar/atualizar no Google Contatos.
4. **Confirmar antes de chutar a RELAÇÃO** (cliente x fornecedor x família x amigo) quando não dá pra deduzir do perfil comercial — o Vitor prefere responder "primo", "empreiteiro", etc. do que ter classificação errada. Um perfil pessoal sem contexto vira, no máximo, provisório em OUT, sinalizado.
5. Nunca apagar contato sem mostrar e pedir confirmação literal.

## Automação

Existe uma tarefa diária (7h, Sorriso) que varre o WhatsApp pessoal, salva sozinha os contatos de conta comercial com ramo óbvio e lista os duvidosos para o Vitor confirmar.