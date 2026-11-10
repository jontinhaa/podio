# Koraki — guia rápido da marca

Versão visual: `koraki-guia.png`.

## A ideia
Um bloco partido por um corte só, em forma de pé-de-galinha. É a pegada do corvo (koraki = corvo, em grego; "passos", em esloveno) e também o símbolo "um-para-muitos" dos diagramas de banco de dados. Quem sabe, sabe; para o resto, é uma marca firme e limpa.

## Versões (pasta `svg/`)
| arquivo | quando usar |
|---|---|
| `koraki-horizontal-fundo-escuro.svg` | **principal**. Site, apresentações, redes, fachada |
| `koraki-horizontal-fundo-claro.svg` | papel, documentos, fundos claros |
| `koraki-vertical-*.svg` | espaços quadrados ou estreitos (capa, adesivo, crachá) |
| `koraki-simbolo-*.svg` | avatar, carimbo, marca d'água, quando o nome já aparece perto |
| `*-1cor-noite / creme / preto / branco` | impressão em uma cor, gravação, bordado, nota fiscal |
| `koraki-icone-app.svg` | ícone de app (quadrado cheio; a loja arredonda os cantos) |
| `koraki-simbolo-pequeno-ambar.svg` | abaixo de 32 px: tem o corte mais grosso |

Todos os SVGs são geometria pura (sem máscara, sem fonte), então abrem iguais no Figma, Illustrator, Canva, na gráfica e no navegador.

## Cores
| nome | hex | RGB | uso |
|---|---|---|---|
| Âmbar | `#F0A23B` | 240 162 59 | símbolo sobre fundo escuro; botões e destaques no escuro |
| Âmbar queimado | `#B86E10` | 184 110 16 | símbolo sobre fundo claro |
| Noite | `#0C1715` | 12 23 21 | fundo principal; texto sobre claro |
| Igarapé | `#0F4D44` | 15 77 68 | superfícies e seções secundárias |
| Verde-água | `#7DB5A2` | 125 181 162 | gráficos, ilustração, estados |
| Creme | `#F2EFE7` | 242 239 231 | nome sobre o escuro; fundo claro (no lugar do branco) |

Regras de contraste (conferidas):
- O texto vai sempre em noite sobre creme, ou creme sobre noite (15,9:1).
- O âmbar nunca é texto sobre creme (1,8:1). No claro, use o âmbar queimado, e só para o símbolo (3,5:1).
- Sobre o igarapé, o âmbar passa (4,6:1).

## Tipografia
Familjen Grotesk 600 no nome (Google Fonts, licença OFL, uso livre). O nome no logo já está em contorno, então não redigite com a fonte. Para textos do site e materiais, use a mesma família: 600 em títulos e 400 no texto corrido.

## Respiro e tamanho mínimo
- Respiro em volta da marca: metade da altura do símbolo, livre de texto, foto ou borda.
- Horizontal: no mínimo 96 px ou 25 mm de largura.
- Símbolo: no mínimo 16 px. Abaixo de 32 px, use a versão pequena (favicon).

## Não faça
Âmbar e creme sobre fundo claro · esticar ou achatar · girar · fundo de cor média (verde-água, foto clara) sem uma tarja noite · trocar a fonte do nome · contorno, sombra, brilho ou gradiente · azul/roxo em gradiente "de tech".

## Arquivos prontos
- `png/`: horizontal em 400/800/1600 px (escuro e claro), vertical em 512/1024, símbolo em 256/512/1024, ícone de app 1024, assinatura de e-mail 300 px.
- `redes/`: avatar 1080 (seguro para corte redondo) e imagem de compartilhamento 1200×630 (Open Graph).
- `favicon/`: favicon.ico (16/32/48), favicon.svg, apple-touch-icon 180, ícones 192/512, maskable 512 e site.webmanifest.

Para o site, cole no `<head>`:
```html
<link rel="icon" href="/favicon.ico" sizes="48x48">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
<link rel="manifest" href="/site.webmanifest">
<meta name="theme-color" content="#0C1715">
<meta property="og:image" content="/koraki-og-1200x630.png">
```

## Antes de imprimir
Consultar "Koraki" no INPI (classe 42) e o domínio koraki.com.br.

Para regenerar o kit a partir das fontes: `node tools/extra/kit.mjs` e depois `node tools/extra/guia.mjs`.
