# Design System — PixPet (fonte: zip "Pet Shop Ecommerce Revamp" aprovado pelo cliente)

Sistema visual escolhido pelo cliente. É a fonte de verdade para a POC e para o
build Nuxt (`camadas/ui`).

## Tipografia
- Display: **Bricolage Grotesque** (400/700/800) — títulos, preços, nomes.
- Corpo: **DM Sans** (400/500/600) — texto, labels, botões.
- Embutidas como @font-face data-URI (CSP/proxy bloqueiam CDN de fonte).

## Cores (tokens)
| Token | Valor | Uso |
|-------|-------|-----|
| `--bg` | `#FFF8F0` | fundo (creme quente) |
| `--fg` | `#1C1208` | texto |
| `--card` | `#FFFFFF` | cards |
| `--primary` | `#FF5722` | ação/CTAs/preço-destaque/desconto |
| `--secondary` | `#FFF3E0` | superfícies suaves/peach |
| `--secondary-fg` | `#7C3A1E` | labels sobre creme |
| `--muted` / `--muted-fg` | `#F5EDE0` / `#8B7355` | fundos/textos secundários |
| `--accent` / `--accent-deep` | `#00BFA5` / `#00897B` | teal (destaques, band, assinatura) |
| `--amber` | `#FFB300` | moeda/cashback |
| `--destructive` | `#D4183D` | erros/remover |
| `--radius` | `1rem` (16px), pills `999px` | cantos |

## Regras de estilo
- Tudo arredondado: cards `rounded-2xl`, botões/pills `rounded-full`.
- Sombras suaves (nada de offset duro), sem textura/grão, sem borda pesada.
- Foto de produto em área branca (fundo branco das fotos funde sem emenda).
- Botão primário: laranja + texto branco (padrão do sistema do cliente).
- Light mode apenas (por enquanto).
