---
name: desenvolver-app-vzp
description: >-
  Construir um app da casa do zero, acrescentar tela a um que já existe ou
  consertar tela — sempre PWA instalável, navegável, que se explica e cabe em
  qualquer tamanho de tela. Use ao começar programa novo, ao criar ou mexer em
  qualquer tela, painel, aba, formulário ou botão, e ao herdar um programa para
  saber o que conferir. Vale para todo programa nosso com interface: canil,
  saúde, ConstruBASE, mapa, imóveis, VERO, planejamento.
---

# Desenvolver um app da casa

Isto não é passada de acabamento. Tudo aqui é mais barato de fazer na primeira
tela do que de acrescentar na décima — e é justamente o que hoje precisa ser
pedido toda vez. Pedido deixa de ser pedido quando vira regra: **estas decisões
já estão tomadas, não se pergunta por elas.**

O que sobra para decidir é o que só o Vitor decide: o que o programa faz, que
número importa, como o trabalho realmente acontece.

## O molde da casa

A pilha não é escolha nova a cada projeto — ela já existe em 20+ repositórios:

- **Node + Express + `pg`**, módulos ES (`servidor.mjs`, `src/*.js`)
- **Front em HTML, CSS e JavaScript puro**, servido de `public/`, com um
  `comum.js` para o que se repete entre telas
- **Postgres** (Supabase ou Neon)
- **Publicação** em Cloud Run (`Dockerfile` + `cloudbuild.yaml`) ou Render

React/Next existe só em `vzp-planejamento`. **App novo não
nasce em React sem motivo dito em voz alta** — carregar build, tipos e
ecossistema para uma tela de cadastro é custo sem retorno, e quebra a regra de
que qualquer um dos programas se abre e se conserta do mesmo jeito.

## Todo app nasce PWA

Não é etapa posterior. No primeiro commit que serve uma página já entram:

- `manifest.webmanifest` com nome, ícones (192 e 512), `start_url`,
  `theme_color` e `display`
- `sw.js` registrado
- **botão de instalar** por `beforeinstallprompt` — hoje só 4 dos nossos apps
  têm, e sem ele o app é um site que por acaso tem manifesto

**A regra que já custou uma tela destruída:** o endereço do JS e do CSS carrega
a versão (`/app.js?v=117w-mtxn`), e o service worker **não intercepta
requisição de arquivo do app**. Sem isso o navegador serve JavaScript de uma
versão com o CSS de outra, com defeito diferente em cada aparelho — e a pessoa
conclui que a correção não funcionou.

Detalhe e código de referência em `references/pwa.md`.

## As nove leis da tela

**1. Toda tela em que se entra tem como sair.** Botão de voltar, sempre. Em PWA
com `display: standalone` isso é obrigação dobrada: ali não existe o botão do
navegador, e sem o seu a pessoa fica presa.

**2. Nada é beco sem saída.** Botão que não navega, número que não abre o que o
compõe, cartão que não leva ao registro — cada um é defeito, não "ainda não
implementado".

**3. A tela diz o que é e o que fazer ali**, por escrito, nela mesma. Não em
treinamento, não em mensagem de chat, não deduzido do nome do menu.

**4. Vazio ensina.** Lista vazia mostra por onde se começa. Branco faz a pessoa
procurar defeito onde não há.

**5. Todo tamanho de tela, e sobra de espaço conta como erro.** Coluna órfã,
cartão sozinho na fileira, metade da largura em branco. Escolher um número de
colunas que o conteúdo preencha é parte de fazer, não polimento depois. De 320 px
a monitor grande.

**6. Mesma aba.** Zero `target="_blank"`, zero `window.open()` — inclusive para
domínio de terceiro. Quem decide abrir em aba nova é quem usa, pelo botão
direito.

**7. Edição tem começo e fim.** Um botão "Editar" liga o modo, um "Concluir"
desliga. Fora do modo, os controles não existem; dentro dele, ficam sempre
visíveis — esconder no `hover` é esconder a porta de uma função que a pessoa
acabou de pedir.

**8. A explicação chega por mouse, dedo e foco.** Interface que só explica no
`hover` não explica nada no telefone — e telefone costuma ser onde ela mais é
usada.

**9. Toda aba abre com o painel dela.** Logo abaixo do título, antes de
qualquer lista ou formulário, vem a fileira de cartões com os números que
importam naquela aba — o que está atrasado, o que vence, quanto está em dia,
quanto entrou. Quem abre a aba lê a situação num relance, sem rolar. Cada
cartão obedece à lei 2: toca e leva ao que compõe o número (filtra a lista
abaixo, rola até o painel certo ou abre a aba de onde ele vem). Número de
enfeite não entra: aba sem dado ainda diz isso (lei 4) em vez de mostrar zeros.
A quantidade de cartões casa com as colunas da grade (lei 5) — seis cabem em
3 × 2 no tablet e 2 × 3 no celular, cinco deixam um órfão. Referência: a aba
Saúde e o Plantel do `canil-lucini`.

O detalhe de como escrever a explicação, o registro de verbetes em arquivo
separado e a conferência tela a tela estão na skill **`interface-que-se-explica`**,
que é a irmã desta. Esta diz o que nasce junto com o app; aquela, como levar uma
interface inteira ao estado final.

## O rodapé

**Botão de melhorias**, como já existe em ConstruBASE, Gestão de Imóveis/VERO,
Planejamento e Saúde Pessoal. Não é aba: é botão no rodapé da navegação,
alcançável de qualquer tela, com rotas liberadas para toda conta — inclusive a
que perdeu acesso a tudo, que é justamente quem precisa reclamar. Ao copiar,
manter as cinco decisões do padrão (fonte: `projetos/saude-pessoal/src/melhorias.js`).

**Melhoria entregue fecha o card.** O botão de melhorias não é caixa de entrada
só de ida: quem pediu precisa ver que foi feito. Ao terminar uma melhoria pedida
ali, **volte no card e marque a sugestão como feita** — com uma linha do que
entrou — antes de dizer que acabou. "Feita" quer dizer "a testar", não
"arquivada". Card que fica em aberto depois de pronto ensina a pessoa a parar de
pedir, e some o rastro de quem entregou o quê.

## Dado e publicação

Três armadilhas que já derrubaram app nosso em produção, cada uma calada:

- **`pool.on('error')` em todo `new pg.Pool`** — sem ouvinte, conexão ociosa
  reciclada mata o processo inteiro.
- **`timestamptz` alimentado por `datetime-local`** erra pelo fuso do servidor.
  No Cloud Run isso é UTC, e a hora sai 4 h fora em Cuiabá.
- **Rota que espera trabalho longo** leva 502 no proxy enquanto o trabalho
  termina certo — a tela diz "não deu" sobre algo que deu.

Detalhe em `references/dados.md` e `references/publicar.md`.

## Olhar a tela pronta, não só o código

**Toda melhoria termina abrindo a tela no navegador e olhando** — de verdade,
nas três larguras (celular, tablet, monitor). Não é opcional, e não se
substitui por ler o código: `grep` e `node --check` provam que o script roda,
não que a tela ficou boa. "Compila" não é "ficou bom", e "está no ar" não é
"está apresentável".

O que só o olho pega — e que já foi entregue torto porque ninguém abriu:

- **escrita estourando o card** — texto vazando a borda porque o container não
  tem padding, ou porque a altura é fixa;
- **coisas espalhadas** — campo, botão, selo ou cartão desalinhado, fora da
  grade, ou solto no meio do branco;
- **sobreposição** — um elemento por cima do outro; alça, etiqueta ou botão
  saindo do lugar;
- **sobra de espaço** — coluna órfã, metade da largura em branco.

Renderizar (preview ou navegador), **olhar** e, quando fizer sentido, tirar o
print é parte de fazer — não passada de acabamento. Ficou ruim, conserta antes
de dizer que acabou. Não dá para abrir a tela (sem dado, sem login)? Então
reproduz o pedaço numa página isolada e olha nela — nunca se declara pronto no
escuro.

## Antes de dizer que acabou

Primeiro a tela renderizada na frente (a seção acima). Só então varrer, nesta
ordem, na largura de celular, de tablet e de monitor:

1. Cada botão da tela leva a algum lugar?
2. Dá para voltar de toda tela?
3. O endereço do JS/CSS mudou desde a versão anterior?
4. Instala pelo botão, no celular?
5. Algum número sem verbete? Alguma explicação só no `hover`?
6. Lista vazia ensina?
7. Sobrou espaço grande em branco em alguma largura?
8. `grep` por `_blank` e `window.open` dá zero?
9. Toda aba abre com o painel de indicadores no topo, e cada cartão leva a algum lugar?
