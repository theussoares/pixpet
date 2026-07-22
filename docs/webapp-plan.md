# Webapp PixPet — plano de telas (fonte: zip Stitch "pet_commerce_com_cashback")

Referência aprovada para o **webapp**. Tipografia travada: **Fraunces (títulos) + Inter (corpo)**.
Design system em `design-system.md` atualizado com os tokens do Stitch.

## Telas (IA do app)
- [x] **PDP** (`prototype/produto.html`) — compra única × assinatura (frequência 30/45/60
      + cashback extra), galeria, avaliações, frete por CEP, WhatsApp, benefícios,
      relacionados, carrinho funcional, bottom nav.
- [x] **Home** (formato app): banner "Exclusivo App", category circles, destaques com
      badge de cashback, bottom nav.
- [x] **Prateleira / PLP**: Filter + Sort, chips de categoria, cards com cashback,
      "Load more".
- [x] **Minhas Assinaturas**: Active Shipments (Editar/Adiar/Enviar agora), resumo de
      economia + rewards, planos pausados/cancelados.

## Tokens Stitch (Material 3) — para a camada ui do Nuxt
- primary `#FF721C`, on-primary `#fff`, primary dark `#a04100`
- secondary/success-cashback `#00A2B4`
- surface-warm (bg) `#FFF8F1`, card `#fff`, text-rich `#2A2C33`, on-surface-variant `#594237`
- tertiary/amber `#c99300` / `#FFBB00`, error `#ba1a1a`, border-muted `#E2E4E9`
- raio: card `.5rem`, botões pill/`full`, badge `.25rem`
- toque mínimo **48px**, ritmo 8px, sombra ambiente única `0 4px 20px rgba(42,44,51,.05)`

## Modelo de produto (decisão do PO)
Subscription-first: toda ração oferece **Compra Única × Assinatura PixPet** com
**cashback base 5% + 5% extra na assinatura (10% total)** e desconto de 10% no preço.
