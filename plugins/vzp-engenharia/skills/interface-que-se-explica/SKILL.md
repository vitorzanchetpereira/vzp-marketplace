---
name: interface-que-se-explica
description: Passe uma interface inteira — abas, botões, cartões, gráficos e números — para um estado em que tudo se explica sozinho e cabe em qualquer tela, do celular de 320 px à TV de 80". Use ao terminar um programa, ao herdar um que já existe, ou quando alguém disser que "não entendeu o que esse número quer dizer", que a tela "está apertada", que "o texto sai do botão" ou que "sobra espaço vazio". Vale para qualquer programa nosso com interface.
---

# A interface que se explica

Esta é a passada final de um programa, e ela responde a duas perguntas que o
usuário faz o tempo todo em silêncio: **"o que é este número?"** e **"por que
esta tela está estranha no meu aparelho?"**

Não é passada de enfeite. É a diferença entre um painel que informa e um
painel que a pessoa olha, não entende, e passa a ignorar — que é o destino
normal de todo número sem explicação.

## As três leis

**1. Nada na tela fica sem explicação alcançável.** Se um número, selo,
gráfico ou botão exige conhecimento de quem construiu o sistema, ele precisa
dizer o que é. Sem exceção para "isso é óbvio": óbvio é para quem escreveu.

**2. A explicação chega por três caminhos, sempre.** Mouse, dedo e foco. Uma
interface que só explica no `hover` não explica nada no telefone — e telefone
costuma ser onde ela mais é usada.

**3. Texto nunca sai da caixa, e a página nunca rola para o lado.** Rolagem
horizontal é sempre defeito. Sempre.

---

## Parte 1 — A explicação

### O registro, separado da marcação

Prosa dentro de atributo HTML ninguém revisa, ninguém traduz e ninguém acha
depois. Um arquivo só, com todos os verbetes:

```js
export const AJUDAS = {
  aderencia: {
    titulo: 'Aderência',
    curto: 'O que você fez dividido pelo que estava previsto.',
    longo: `<p>...</p><p class="dica">Não é nota de conduta.</p>`,  // opcional
  },
};
```

Na tela, uma chave e nada mais: `data-ajuda="aderencia"`.

- **`curto`** aparece no balão. Tem de bastar sozinho — a maioria das pessoas
  nunca vai abrir o `longo`.
- **`longo`** só existe quando há algo que **muda a decisão** de quem lê: de
  onde o número vem, o que fazer com ele, e o que ele **não** quer dizer.
  Sem isso, não crie `longo` — o "?" vira ruído.

**Em dado sensível — saúde, dinheiro, nota, desempenho — o `longo` termina
dizendo o limite do próprio número.** Quem lê um número sobre si mesmo tende
a obedecê-lo, e número obedecido sem contexto faz mal.

### Os três caminhos

| entrada | gesto | espera |
| --- | --- | --- |
| mouse | passar por cima | 350 ms |
| dedo | segurar | 500 ms |
| teclado / controle remoto | receber foco | imediato |

Regras que não se negociam:

- **Segurar um botão engole o clique seguinte.** Quem estava tentando
  entender o botão não pode acioná-lo sem querer.
- **Soltar antes do tempo é toque normal.** A ajuda nunca rouba o gesto.
- **Item não acionável ganha um "?" que é botão de verdade**, alcançável por
  toque, clique e Tab. Ajuda que só encontra quem já sabe que ela existe não
  é ajuda.
- **Item acionável não ganha "?"** — dois alvos dentro de um botão criam erro
  de mira. Nele a explicação entra por segurar ou por passar o mouse.
- **O balão é `position: fixed`**, e é empurrado para dentro da tela em vez de
  centralizado à força. Balão centralizado num item do canto sai metade fora,
  e a metade que sai é sempre a que tinha a informação.
- **Rolar ou redimensionar fecha o balão**, senão ele fica apontando para o
  lugar errado.
- **Chave sem verbete grita no console.** É defeito silencioso: o elemento
  fica mudo e parece que ninguém quis explicar aquilo.

### Onde enganchar

A explicação entra nos **componentes compartilhados** — o cartão de número,
o painel, o gráfico — e não tela por tela. Uma chave no componente se espalha
por dezenas de pontos de chamada de uma vez.

A decoração roda **depois de cada desenho**, no mesmo lugar onde os ícones são
pintados. Se rodar só uma vez no arranque, a primeira tela explica e todas as
seguintes ficam mudas.

---

## Parte 2 — Caber em qualquer tela

### A regra que resolve a maioria das rolagens horizontais

```css
.grade > *, .cartao, .painel { min-width: 0; }
```

Item de grade **não encolhe além do conteúdo** a menos que se diga isso. Sem
essa linha, um nome longo estoura a coluna e empurra a página inteira para o
lado. É a origem da maioria das rolagens horizontais que existem.

Junto com ela:

```css
.valor, .rotulo, .titulo { overflow-wrap: anywhere; }
.botao { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.bloco-largo { overflow-x: auto; }   /* rola dentro de si, nunca a página */
```

### A escada de tamanhos

Teste em **320, 375, 768, 1280, 1920, 2560 e 3840**. 320 é o piso real de
celular pequeno; 3840 é a TV.

**Numa tela grande não basta alargar: a letra precisa crescer.** É a metade
que sempre falta. A três metros de distância, 13 px não se lê — e um programa
que "funciona na TV" com a tipografia do notebook não funciona na TV.

```css
@media (min-width: 2000px) { /* monitor grande: letra maior, mais respiro */ }
@media (min-width: 2600px) { /* televisão: letra bem maior, foco mais grosso */ }
```

### Espaço vazio: quando é desperdício e quando é decisão

Largura travada em 1280 px numa tela 4K deixa **dois terços da tela mortos**.
Isso é desperdício, e se conserta.

Mas **encher 100% da largura também é errado**: linha de texto muito longa não
se lê. A saída é separar as duas coisas —

- **a prosa** tem trava própria (`max-width: 62ch`) e não acompanha a tela;
- **o resto** — cartões, grades, gráficos — cresce à vontade.

Com a prosa protegida, dá para levar o container a 70–75% da largura numa TV
sem piorar a leitura. Abaixo de 50% é desperdício; 100% é ilegível.

### Foco visível não é acessibilidade opcional

```css
:focus-visible { outline: 3px solid var(--primary); outline-offset: 2px; }
```

É a **única navegação** de quem usa teclado, e a única de quem está no sofá
com um controle remoto. Numa TV, engrosse o contorno: mirar com controle é
pior que com o dedo, e muito pior que com o mouse.

---

## Parte 3 — Conferir, não achar

Olhar a tela não conta. **Medir conta.** Rode isto em cada largura da escada:

```js
window.__medir = () => {
  const conteudo = document.querySelector('.page-content');
  const vazando = [];
  for (const el of document.querySelectorAll(
    '.stat-value,.stat-rotulo,.panel-head h2,.panel-head p,.mini-button,.hero p,.hero h1')) {
    if (el.scrollWidth > el.clientWidth + 1) vazando.push(el.className + ': ' + el.textContent.slice(0, 22));
  }
  const alem = [...document.querySelectorAll('.page-content *')]
    .filter((e) => e.getBoundingClientRect().right > innerWidth + 1).map((e) => e.className);
  return {
    w: innerWidth,
    uso: Math.round(100 * conteudo.getBoundingClientRect().width / innerWidth) + '%',
    rolagemH: document.documentElement.scrollWidth > document.documentElement.clientWidth,
    vazando, alemDaJanela: alem.slice(0, 3),
    numero: getComputedStyle(document.querySelector('.stat-value')).fontSize,
  };
};
```

Aprovado quando, **em todas as larguras**: `rolagemH: false`, `vazando: []`,
`alemDaJanela: []`, `uso` entre 55% e 100%, e `numero` crescendo nas telas
grandes.

Para a explicação, confira os três caminhos e mais isto:

```
balão dentro da tela em 320 px       left >= 0 e right <= 320
segurar 220 ms                       ainda não apareceu
segurar 640 ms                       apareceu
clique logo após segurar             foi engolido
"?" só onde existe `longo`           os demais ficam sem ponto, mas alcançáveis por Tab
Esc                                  fecha a folha; de novo, fecha o balão
```

**Ambiente automatizado não dispara `focusin` com `elemento.focus()`** quando
a janela não tem foco do sistema. Não é defeito do código: emita o evento
diretamente para testar.

---

## Ordem de trabalho

1. Levante os componentes compartilhados. É neles que a explicação entra.
2. Escreva o registro inteiro de uma vez, relendo em bloco — é assim que se
   percebe que dois verbetes se contradizem.
3. Ligue as chaves nos pontos de chamada.
4. Aplique as regras de contenção de texto.
5. Monte a escada de tamanhos.
6. Meça nas sete larguras. Conserte. Meça de novo.

## O que nunca fazer

- Explicação só no `hover`.
- `title=""` como mecanismo: não aparece no dedo, não é estilizável, e demora.
- "?" dentro de botão.
- `longo` que repete o `curto` com outras palavras.
- Rolagem horizontal na página, em qualquer largura.
- Dizer que está pronto sem ter medido nas sete larguras.
