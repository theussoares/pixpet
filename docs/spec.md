# spec.md — PixPet · Redesign da Loja de Ração

> Autor: **Product Owner** (papel Opus 4.8 — decisão de alto impacto).
> Status: aprovado para POC. Fase 1 = protótipo de apresentação. Fase 2 = build Nuxt 3.

## 1. Problema

O site atual (`pixpet.shop/petshop`) é um andaime gerado por IA (Lovable). Sintomas
observados e confirmados pelo cliente:

- **Botões sem handler** — "adicionar ao carrinho" / "comprar" não executam. Uma loja
  cujos botões não funcionam não vende.
- **SPA sem SSR** — produtos renderizados via JS indexam mal. Quem busca "ração X" no
  Google não encontra a loja.
- **`user-scalable=no`** — bloqueia zoom. O público de pet shop tem muita gente mais
  velha; não poder ampliar preço/produto derruba acessibilidade e conversão.
- **Sem checkout real, estoque ou painel do dono** — o dono não consegue tocar a loja
  sozinho.

Pontos que **funcionam e devem ser preservados**: proposta clara (ração, brinquedos,
higiene, acessórios), **cashback** (diferencial real no segmento), OG/social tags,
intenção mobile-first, e o fato de já estar no ar (o cliente já entende o valor).

## 2. Objetivo do produto

E-commerce de ração **de verdade** (não plataforma de rifa/roleta): catálogo + carrinho
+ checkout ponta a ponta, com **cashback** e **assinatura recorrente** como motores de
retenção. Núcleo indexável (SSR) e operável pelo dono.

## 3. Escopo por fase

### Fase 1 — POC de apresentação (este entregável)
Protótipo HTML de alta fidelidade, apresentável a stakeholders, provando visual +
interação. **Diferencial-tese: os botões funcionam de verdade.**

### Fase 2 — Produção (Nuxt 3 SSR)
Ver `solution-design.md`.

## 4. Critérios de aceite — Fase 1 (mensuráveis)

| # | Critério | Como medir |
|---|----------|------------|
| A1 | Adicionar ao carrinho **funciona** | Clicar em "Adicionar" incrementa o badge do carrinho e insere o item no drawer, sem reload |
| A2 | Carrinho recalcula em tempo real | Alterar quantidade atualiza subtotal, cashback estimado e frete instantaneamente |
| A3 | Produtos reais | Os 5 produtos fornecidos aparecem com nome, marca, preço, preço promocional e desconto % corretos |
| A4 | Cashback visível por produto e no total | Cada card mostra "PixCoins" a ganhar; o carrinho soma o cashback |
| A5 | Zoom liberado | Sem `user-scalable=no`; `pinch-to-zoom` funciona |
| A6 | Contraste AA | Texto principal ≥ 4.5:1 em ambos os temas (claro/escuro) |
| A7 | Responsivo | Sem scroll horizontal do body de 320px a 1440px |
| A8 | Sem "cara de IA" | Direção de arte "casa de ração de bairro": tipografia de sinalização (Anton, embutida), papel kraft com grão, etiquetas furadas, cupom de fidelidade — fora dos defaults genéricos |
| A9 | Fallback de imagem | Se a imagem do produto falhar, exibe placeholder SVG coerente (não quebra o layout) |
| A10 | Foco de teclado visível | Todo controle interativo tem estado `:focus-visible` |

## 5. Critérios de aceite — Fase 2 (para referência do Arquiteto)

- SSR: página de produto retorna HTML renderizado (view-source contém nome/preço).
- Checkout Pix + cartão ponta a ponta.
- Cashback com saldo persistido por cliente (auth + saldo).
- Painel do dono: CRUD de produto, estoque, pedidos.
- Assinatura recorrente de ração.
- WhatsApp integrado.
- Busca + categorias no padrão do mercado (ração seca/úmida/prescrita, farmácia/
  antipulgas, higiene, brinquedos).

## 6. Fora de escopo (Fase 1)
Pagamento real, backend, autenticação, persistência. A POC simula estado no cliente.

## 7. Dados de referência (produtos reais fornecidos)

1. Golden — Ração Úmida Sachê Adulto Peixe Raças Médias — R$ 6,25 → **R$ 5,47**
2. Hercosul — Tapete Higiênico 30un Raças Pequenas — R$ 41,06 → **R$ 35,16** — estoque 47
3. Magnus — Tapete Higiênico 50un Raças Médias — R$ 64,81
4. Pawise — Brinquedo Bola Raças Pequenas — R$ 35,91
5. ORIGINAL — R$ 100,00
