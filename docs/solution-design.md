# solution-design.md — PixPet

> Autor: **Arquiteto de Software** (papel Opus 4.8). Validado pelo **CTO**.
> Insumo: `spec.md`. Cobre a arquitetura da POC e o mapa da Fase 2 (Nuxt 3).

## 1. Fase 1 — Arquitetura da POC

Protótipo autocontido, sem build, sem dependências externas em runtime.

- **Um arquivo**: `prototype/index.html` (HTML + CSS + JS inline). Motivo: coesão
  visual e portabilidade (abre local com fotos reais **e** publica como Artifact com
  fallback SVG). Fatiar entre agentes paralelos prejudicaria a coesão — decisão do
  Arquiteto de **não** paralelizar a POC.
- **Estado**: objeto `cart` em memória + `render()` idempotente. Sem framework.
- **Design tokens**: CSS custom properties em `:root`, redefinidas para dark via
  `@media (prefers-color-scheme)` e `:root[data-theme=...]`. Componentes consomem só
  tokens — nunca cor crua dentro de media query.
- **Imagens**: `<img src="{supabase}">` com `onerror` → placeholder SVG por categoria.
  CSP do Artifact bloqueia host externo ⇒ fallback assume; local ⇒ foto real carrega.
- **Acessibilidade**: viewport sem `user-scalable=no`; `:focus-visible`;
  `prefers-reduced-motion`; contraste AA nos dois temas.

### Contrato de dados (produto) — espelha o payload real
```ts
interface Produto {
  id: string
  nome: string
  marca: string
  preco: number
  preco_promocional: number | null
  imagem_url: string
  estoque?: number
  categoria: 'racao' | 'higiene' | 'brinquedo' | 'acessorio'
}
```

## 2. Fase 2 — Mapa Nuxt 3 (produção)

Mapeamento por camada, no padrão do `agents.md`. Cada camada é fronteira de trabalho
paralelo dos Devs (Sonnet).

| Camada | Responsabilidade | Dev |
|--------|------------------|-----|
| `camadas/core` | Tipos, schemas Zod, utils de preço/moeda, formatação BRL | Dev Tipos |
| `camadas/ui` | Design system (tokens, botões, cards, drawer) a partir da POC | Dev Vue/Nuxt |
| `camadas/escolha-produto` | Catálogo, categorias, busca, PDP (SSR/SEO) | Dev Vue/Nuxt |
| `camadas/checkout` | Carrinho, frete, Pix + cartão | Dev Vue/Nuxt + Dev Stores |
| `camadas/my-purchases` | Pedidos, assinatura recorrente, saldo de cashback | Dev Stores |
| `camadas/admin` (novo) | Painel do dono: CRUD produto, estoque, pedidos | Dev Vue/Nuxt |

### Decisões técnicas (CTO)
- **SSR obrigatório** nas rotas de catálogo e PDP → resolve o SEO fraco do site atual.
  `useAsyncData` para fetch server-side; nada de fetch client-only em conteúdo indexável.
- **Persistência**: Supabase (auth + saldo de cashback + produtos/estoque). Já é o host
  das imagens; reaproveita infra.
- **Stores Pinia** no padrão `useStoreDeX` / `defineStore`: `useCartStore`,
  `useCashbackStore`, `useCatalogStore`. Consumo com `storeToRefs()`.
- **Pagamento**: Pix como primário (peso no Brasil) + cartão. Store de pagamento é
  **crítica** → revisão obrigatória do Code Reviewer Sênior (Opus).
- **i18n**: `pt` primário; `es` paridade se houver expansão. Toda string via `$t()`.
- **Tracking**: GTM + Pixel + Sentry nos eventos de funil (view_item, add_to_cart,
  begin_checkout, purchase) sem duplicação.

## 3. Riscos e mitigações (CTO)
| Risco | Mitigação |
|-------|-----------|
| SEO continuar fraco | SSR + teste de view-source no CI (A-Fase2) |
| Cashback vazar saldo entre clientes | Store isolada + revisão Opus + RLS no Supabase |
| Botão sem handler (erro do site atual) | Teste Vitest cobrindo add_to_cart em toda PDP |
| Zoom bloqueado de novo | Lint de viewport proibindo `user-scalable=no` |

## 4. Handoff para execução paralela (Engenheiro de Software)
Ordem: `core` → `ui` (deriva da POC) → `escolha-produto` → `checkout` →
`my-purchases`/`admin`. Cada Dev recebe caminhos absolutos, contrato de interface e
chaves i18n. Integração via worktrees; revisão do Code Reviewer em todo merge, aprofundada
em `checkout` e cashback.
