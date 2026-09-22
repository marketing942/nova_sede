# Nova Sede · Colégio CPPEM

Apresentação pública da nova sede, em HTML estático. Sem build: `index.html` na
raiz e todos os arquivos servidos a partir de `public/`.

## Rodar localmente

```bash
python -m http.server 8099
# abre http://localhost:8099
```

## Deploy (Vercel)

`vercel.json` fixa `outputDirectory: "."` — sem isso a Vercel trataria a pasta
`public/` como a raiz publicada e o `index.html` não seria encontrado.

A página não usa vídeo. Os dois vídeos originais e o `sacada nova.png` ficam
na pasta como fonte, mas fora do deploy (ver `.vercelignore`).

| Arquivo                        | Papel                                            |
| ------------------------------ | ------------------------------------------------ |
| `public/img/hero-aerea.webp`   | Foto do topo (render aéreo do conjunto)          |
| `public/img/carrossel/*.webp`  | Imagens do carrossel "Um passeio pela escola"    |
| `public/img/fachada.webp`      | Montagem da fachada sobre o prédio real          |

`public/` não usa cache longo no navegador (`max-age=0, must-revalidate`): as
imagens são trocadas mantendo o nome, e um cache de um ano fazia visitantes
continuarem vendo a versão antiga. Ao trocar um arquivo que já foi publicado,
aumente também o `?v=` onde ele é referenciado no `index.html`.

## Antes de publicar

O domínio ainda não existe. Trocar `https://novasede.cppem.com.br` pelo endereço
real em três lugares do `index.html`: `canonical`, `og:url` e `og:image` (esta
precisa ser absoluta para o preview do WhatsApp funcionar).

O redirect `/nova-sede` e `/novasede` no site oficial aponta para o mesmo
endereço, via `NEXT_PUBLIC_NOVA_SEDE_URL` (ver `next.config.ts` do
`SiteColegioCPPEM`).

## De onde vêm os materiais

- **Topo**: render aéreo do conjunto, enviado pela direção.
- **Carrossel**: recortes dos renders aprovados "sacada nova" (visão geral e
  quadras) e "sala interna", sem as tarjas gravadas.
- **Fachada, pilares e brasão**: extraídos da apresentação
  `apresentacaoescola/apresentacao-operacao-nova-sede-cppem.html`. A fachada
  é uma montagem sobre a foto do prédio real do terreno.
- **`public/campus-3d.html`**: o planejador 3D que estava embutido naquela
  apresentação, com a paleta trocada para o azul-marinho e o dourado do colégio.
  Carrega three.js por CDN e roda em modo apresentação (gira sozinho, com
  botões de aproximação).

Todo render e a planta são material ilustrativo, e a página sinaliza isso em
cada bloco de mídia e no rodapé. Manter esse aviso ao trocar qualquer imagem.
