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

Os dois arquivos originais de vídeo ficam fora do deploy (ver `.vercelignore`):
são as fontes, e o site usa as versões otimizadas geradas a partir delas.

| Arquivo                             | Papel                                        |
| ----------------------------------- | -------------------------------------------- |
| `public/hero-loop.mp4`              | Loop do topo, 531 KB, sem áudio, ida e volta |
| `public/tour-nova-sede.mp4`         | Tour de 1 min, 720p, 7,9 MB                  |
| `CPPEM_Interiores_Realistas*.mp4`   | Fontes, não publicadas                       |

## Antes de publicar

O domínio ainda não existe. Trocar `https://novasede.cppem.com.br` pelo endereço
real em três lugares do `index.html`: `canonical`, `og:url` e `og:image` (esta
precisa ser absoluta para o preview do WhatsApp funcionar).

O redirect `/nova-sede` e `/novasede` no site oficial aponta para o mesmo
endereço, via `NEXT_PUBLIC_NOVA_SEDE_URL` (ver `next.config.ts` do
`SiteColegioCPPEM`).

## De onde vêm os materiais

- **Fotos dos ambientes** (`public/img/*.webp`): quadros extraídos do vídeo de
  interiores, recortados para tirar as tarjas gravadas.
- **Renders das quadras, mapa e brasão**: extraídos da apresentação
  `apresentacaoescola/apresentacao-operacao-nova-sede-cppem.html`.
- **`public/campus-3d.html`**: o planejador 3D que estava embutido naquela
  apresentação, com a paleta trocada para o azul-marinho e o dourado do colégio.
  Carrega three.js por CDN e roda em modo apresentação (gira sozinho, com
  botões de aproximação).

Todo render, vídeo e planta é material ilustrativo — a página sinaliza isso em
cada bloco de mídia e no rodapé. Manter esse aviso ao trocar qualquer imagem.
