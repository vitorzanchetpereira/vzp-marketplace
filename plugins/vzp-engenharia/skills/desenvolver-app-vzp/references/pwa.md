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

`canil-lucini`, `vzp-desenhos` e `vzp-gestao-de-imoveis` seguem com service
worker que intercepta arquivo e cache versionado à mão (`lucini-shell-v18`).
Funciona enquanto alguém lembra de subir o número a cada publicação — e o dia
que esquecer é o dia da tela destruída. Ao mexer em qualquer um deles, migrar.

Ao receber "está quebrado" ou "ficou feio" logo depois de publicar: **conferir
cache antes de mexer no layout.** Comparar o arquivo que o servidor entrega com
o que a página carregou.
