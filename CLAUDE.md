# Formul8 Nutrition – Shopify Project Conventions

Owner is an e-commerce owner and a **beginner**: explain steps plainly, define jargon, one step at a time.

## Always-do rules
1. **Plan first.** Outline logic and get approval before any mutation or file change.
2. **Never edit the Live theme.** Work only in a draft/duplicate theme. Check the theme `role` is not `MAIN` before every push.
3. **Draft first.** Create products as `DRAFT`, discounts inactive/scheduled, pages unpublished. The owner reviews, then publishes.
4. **Audit log.** Append every API call and file change to `PROGRESS.md` (timestamp, action, target, result, rollback).
5. **Read back** every mutation to verify it.
6. **No secrets in git.** Tokens live in env vars (`SHOPIFY_STORE`, `SHOPIFY_ADMIN_TOKEN`) or a git-ignored `.env`.
7. **Never publish, delete, or send anything customer-facing without explicit approval.**
8. Save new learnings about the store schema (metafields, collections, theme layout) to Auto Memory.
9. Supplement marketing: avoid disease/medical claims; flag anything needing compliance review.

## Store
- Public domain: `formul8nutrition.com` (provided by owner). The `.myshopify.com` handle is still needed for API access; keep it in `SHOPIFY_STORE`, not in git.

## Product facts (from owner)
- Formul8 Nutrition, 30 servings. Regular price **$70**, sale price **$49** (Shopify: price `49.00`, compare-at `70.00`).
- $70 → $49 is exactly 30% off.
- **Offer (owner-confirmed):** 30% off + 1 jar of Formul8 Nutrition + 1 FREE shaker bottle + 1 FREE hand blender/frother. Working assumption: the 30% is the $70 → $49 sale (customer pays $49 for the jar, gifts $0). Owner to correct if the 30% should stack on top of $49 (= $34.30).
- Planned build: gifts as separate draft products with tracked stock; two inactive automatic Buy X Get Y discounts (one per gift, qty 1, 100% off, requires Formul8 in cart) so the owner can review before activating. Verify limits against Shopify docs once connected.
- Free gifts: (1) Formul8 shaker bottle, normal price **$14.99**; (2) Formul8 hand blender/frother, normal price **$24.99** (= $39.98 of free gifts; $109.98 total value with the $70 jar). Photo: `theme/assets/formul8-gifts.jpg`. Still to confirm: do they already exist as products in Shopify?
- **Stock:** owner says only **3** gift sets are left. Show "Only 3 left" in RED (`--color-urgent` `#B71C1C`). Scarcity must be TRUE: set the gift inventory to 3 in Shopify, update the theme setting `gifts_left` (Theme settings → Offer & stock) to match, and hide the message at 0. Never show fake or stale scarcity or fake countdowns. Assumption: "3" = 3 free-gift sets (owner to confirm).
- **Ingredients/Supplement Facts: not available yet (MVP launch).** Never invent or imply ingredients, amounts or benefits. Use only what is visible on the jar (name, "Dietary Supplement", 30 servings, tagline "Your gut. Your health. Your formula."). Product page keeps a clearly marked placeholder for the Supplement Facts panel; product stays DRAFT until the owner supplies it (supplements need a compliant Supplement Facts label before sale).

## Inspiration (owner-provided)
- Competitor landing page the owner likes: `https://gruns.co/pages/gruns-prime-time-sale` (Grüns, supplement gummies; strip the ad-tracking query string). Not yet reviewed in detail: page was not reachable from the session.

## Project goals
1. Launch product "Formul8 Nutrition"
2. Bundle: 30% discount + 2 free gifts
3. High-converting listicle landing page
4. Sales-data analysis to inform the page
5. SEO audit + implementation

## Design
- Green colour scheme sampled from the jar: forest `#2E4A37`, mid green `#4A6649`, sage `#B5C4A8`, cream `#F5ECE5`, rose-gold `#C99A8B` (small highlights only). Defined in `theme/config/settings_schema.json`; use the CSS variables in `theme/assets/theme.css`, never hard-coded hex.
- Homepage hero = the owner's jar banner (`theme/assets/formul8-hero.jpg`, WebP + mobile crop alongside). The banner already holds the logo and tagline, so don't overlay text on the jar.
- Red `#B71C1C` is reserved for stock/urgency messaging only (red text on cream/white, or white text on a red pill). Never red text on the sage footer (fails contrast).
- Keep text/background contrast at WCAG AA (4.5:1).
- Footer carries the FDA disclaimer; keep it.

## Layout
- `CLAUDE.md` – this file
- `PROGRESS.md` – audit log
- `.mcp.json` – project MCP servers (Shopify Dev MCP)
- `content/` – draft copy for owner review (`product-copy.md`, `listicle-outline.md`)
- `theme/` – local DRAFT Shopify theme. Push only with `shopify theme push --unpublished`, never `--live`
