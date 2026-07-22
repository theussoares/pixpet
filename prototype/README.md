# PixPet — POC do webapp (4 telas navegáveis)

Abra **`index.html`** no navegador. Mantenha os 4 arquivos na MESMA pasta —
a navegação entre telas e as imagens reais dos produtos dependem disso.

## Telas
- `index.html` — Home (destaques, cashback, category circles)
- `prateleira.html` — Listagem (filtro + ordenação)
- `produto.html` — Página de produto (compra única × assinatura, frete, WhatsApp)
- `assinaturas.html` — Minhas assinaturas (envios ativos, economia, pausadas)

## Navegação
- Home: categoria/"ver tudo" → Prateleira · card → Produto
- Prateleira: card → Produto
- Bottom nav (mobile) e header ligam Início / Categorias / Assinaturas / Carrinho
- Carrinho e cashback funcionam em todas as telas

Design system: Fraunces + Inter, tokens em `../docs/design-system.md` /
`../docs/webapp-plan.md`. Fontes embutidas; imagens vêm do Supabase (carregam
ao abrir local). Demo — nenhum pedido real é processado.
