# PWA: instalável, e sem servir versão misturada

## O manifesto

`public/manifest.webmanifest`, ligado no `<head>` com
`<link rel="manifest" href="/manifest.webmanifest">`:

```json
{
  "name": "Nome por extenso",
  "short_name": "Nome curto",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#008080",
  "icons": [
    { "src": "/icons/192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icons/512.png", "sizes": "512x512", "type": "image/png" },
    { "src": "/icons/512.png", "sizes": "512x512", "type": "image/png", "purpose": "maskable" }
  ]
}
```

`display: standalone` tira o botão Voltar do navegador. É por isso que a lei 1
da tela existe: sem botão de voltar seu, o app instalado vira armadilha.

## O botão de instalar

O navegador só oferece instalação uma vez e no momento dele. Guardar o evento é
o que permite oferecer quando fizer sentido:

```js
let convite = null;
addEventListener('beforeinstallprompt', (ev) => {
  ev.preventDefault();          // sem isso o navegador decide a hora
  convite = ev;
  botaoInstalar.hidden = false;
});
botaoInstalar.onclick = async () => {
  if (!convite) return;
  convite.prompt();
  await convite.userChoice;
  convite = null;
  botaoInstalar.hidden = true;  // o evento é de uso único
};
addEventListener('appinstalled', () => { botaoInstalar.hidden = true; });
```

O Chrome só oferece instalar se o app responde **alguma coisa** sem internet.
Por isso o service worker guarda um arquivo só: a página de "sem conexão".

## O service worker que NÃO intercepta

Em 12/09/2026 o `saude-pessoal` serviu **JavaScript de uma versão com o CSS de
outra**: tela destruída, defeito diferente em cada navegador, porque cada um
guardou uma mistura própria. O service worker antigo guardava a casca inteira e
entregava a cópia dele.

Funcionar offline é bom; mostrar a versão errada é inaceitável. O molde atual,
em `projetos/saude-pessoal/public/sw.js`:

- guarda **um** arquivo, `/offline.html`
- entra na frente **só de navegação**, nunca de arquivo do app
- `skipWaiting()` no `install`, e no `activate` apaga todo cache que não seja o
  da versão atual, depois `clients.claim()`

E na página, o conserto do aparelho preso em versão velha — recarrega **uma
vez**, sozinho:

```js
let jaRecarregou = false;
navigator.serviceWorker.addEventListener('controllerchange', () => {
  if (jaRecarregou) return;
  jaRecarregou = true;
  location.reload();
});
```

## A versão no endereço

`/app.js` com endereço fixo não atualiza: o navegador segura pelo `max-age`. A
chave sai do tamanho + `mtime` do arquivo, então muda sozinha quando o arquivo
muda. Referência: `projetos/saude-pessoal/src/http.js`.

```js
const chave = (info) => info.size.toString(36) + '-' + Math.round(info.mtimeMs).toString(36);
// no HTML servido: '/app.js'  ->  `/app.js?v=${chave(infoDoAppJs)}`
```

Cabeçalhos, e cada um tem motivo:

| O quê | Cabeçalho | Por quê |
| --- | --- | --- |
| `index.html` | `cache-control: no-store` | é quem carrega a chave nova; guardado, nunca chega |
| `.js`, `.css` | `cache-control: no-cache` + `ETag` | "pode guardar, mas pergunte antes": revalida em 304, não re-baixa |

`no-cache` não é desperdício — 304 é resposta vazia.

## Os que ainda têm a armadilha

**`canil-lucini` é o caso inteiro.** Service worker que intercepta arquivo com
cache de casca versionado à mão (`lucini-shell-v18`). Funciona enquanto alguém
lembra de subir o número a cada publicação — e o dia que esquecer é o dia da
tela destruída. Ao mexer nele, migrar.

**`vzp-gestao-de-imoveis` é meio caminho.** HTML e manifesto já vêm da rede
primeiro, e `/api/` e `/ical/` nunca entram em cache — isso está certo. O que
sobra é o estático: JS e CSS são cache-primeiro sem carimbo de versão no
endereço, então a primeira carga depois de publicar ainda mistura. Falta só o
carimbo, não o service worker inteiro.

**`vzp-desenhos` já resolveu, por outro caminho, e vale ler.** Lá o código vem
da rede primeiro e só o WebAssembly (10 MB, nunca muda) vem do cache. O próprio
arquivo conta que na v1 tudo era cache-primeiro e uma correção no `app.mjs`
simplesmente não chegava — uma hora de medição para descobrir que a página
rodava o script de antes. Duas saídas legítimas para o mesmo problema: carimbar
a versão no endereço, ou não interceptar o que muda.

Ao receber "está quebrado" ou "ficou feio" logo depois de publicar: **conferir
cache antes de mexer no layout.** Comparar o arquivo que o servidor entrega com
o que a página carregou.
