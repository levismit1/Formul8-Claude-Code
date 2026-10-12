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
- Owner is creating the app in Shopify's Dev Dashboard (form asks for App URL + redirect URLs). Use App URL `https://shopify.dev/apps/default-app-home`; redirect URL blank or `https://formul8nutrition.com/` (unused; no OAuth login). Credentials are then `SHOPIFY_CLIENT_ID` + `SHOPIFY_CLIENT_SECRET` (env/secrets, never git): exchange for a short-lived Admin API token with the client-credentials grant (`POST https://<store>.myshopify.com/admin/oauth/access_token`, `grant_type=client_credentials`); verify this works on first connection. If the owner instead has a legacy custom app, use `SHOPIFY_ADMIN_TOKEN`.
- Scopes requested: `write_products,write_inventory,write_discounts,write_themes,write_content,write_legal_policies,read_orders,read_reports`.

## Product facts (from owner)
- Formul8 Nutrition, 30 servings. Regular price **$70**, sale price **$49** (Shopify: price `49.00`, compare-at `70.00`).
- $70 → $49 is exactly 30% off.
- **Offer (owner-confirmed):** 30% off + 1 jar of Formul8 Nutrition + 1 FREE shaker bottle + 1 FREE hand blender/frother. Working assumption: the 30% is the $70 → $49 sale (customer pays $49 for the jar, gifts $0). Owner to correct if the 30% should stack on top of $49 (= $34.30).
- Planned build: gifts as separate draft products with tracked stock; two inactive automatic Buy X Get Y discounts (one per gift, qty 1, 100% off, requires Formul8 in cart) so the owner can review before activating. Verify limits against Shopify docs once connected.
- Free gifts: (1) Formul8 shaker bottle, normal price **$14.99**; (2) Formul8 hand blender/frother, normal price **$24.99** (= $39.98 of free gifts; $109.98 total value with the $70 jar). Photo: `theme/assets/formul8-gifts.jpg`. Still to confirm: do they already exist as products in Shopify?
- **Stock:** owner has 3 gift sets in stock. Per owner (changed from the earlier red "Only 3 left"), the site shows a GREEN "In stock" badge (`--color-instock` `#2E6B34`) with no count. It must be TRUE: set gift inventory to 3 in Shopify; the theme setting `gifts_left` (Theme settings → Offer & stock) controls the badge and hides it at 0. If the owner later wants scarcity wording (e.g. "Only 3 left"), it must match real inventory; never show fake or stale scarcity or fake countdowns.
- **Ingredients/Supplement Facts: not available yet (MVP launch).** Never invent or imply ingredients, amounts or benefits. Use only what is visible on the jar (name, "Dietary Supplement", 30 servings, tagline "Your gut. Your health. Your formula."). Product page keeps a clearly marked placeholder for the Supplement Facts panel; product stays DRAFT until the owner supplies it (supplements need a compliant Supplement Facts label before sale).

- **Guarantee (owner-confirmed): 30-day money-back guarantee.** Use exactly that wording. Terms (from delivery? opened jars? return shipping?) are not decided; they belong on the store's refund policy page, which must match the promise. Do not add terms elsewhere.
- **Offer button:** a cart link that adds the jar + both gifts together (a discount alone does not add items). Set it in Theme settings -> Offer & stock -> "Offer button link" once products exist.

## Inspiration (owner-provided)
- Competitor landing page the owner likes: `https://gruns.co/pages/gruns-prime-time-sale` (Grüns, supplement gummies; strip the ad-tracking query string). Owner supplied a screenshot (`images/3.jpg`; analysed in `content/listicle-outline.md`). Copy the STRUCTURE only, never their claims, reviews, stats or imagery.

## Project goals
1. Launch product "Formul8 Nutrition"
2. Bundle: 30% discount + 2 free gifts
3. High-converting listicle landing page
4. Sales-data analysis to inform the page
5. SEO audit + implementation

## Design
- Green colour scheme sampled from the jar: forest `#2E4A37`, mid green `#4A6649`, sage `#B5C4A8`, cream `#F5ECE5`, rose-gold `#C99A8B` (small highlights only). Defined in `theme/config/settings_schema.json`; use the CSS variables in `theme/assets/theme.css`, never hard-coded hex.
- Homepage hero = the owner's jar banner (`theme/assets/formul8-hero.jpg`, WebP + mobile crop alongside). The banner already holds the logo and tagline, so don't overlay text on the jar.
- Green `#2E6B34` is the "In stock" badge colour (white text on a green pill, or green text on cream/white; 6.42:1 and 5.51:1). No red is used on the site.
- Keep text/background contrast at WCAG AA (4.5:1).
- Footer carries the FDA disclaimer; keep it.

## Landing-page rules
- Never invent or copy reviews, ratings, review counts, "clinically tested", ingredient or nutrient claims, or "as seen in" logos. Reviews/ratings sections stay hidden until the owner supplies real ones.
- Countdowns/"offer ends" only with a real end date.
- Verify the theme with (1) Shopify's real checker: `@shopify/theme-check-node` (`themeCheckRun(themeDir)`; must report NO OFFENSES), (2) rendering the Liquid with `liquidjs` and screenshotting with Playwright at 1440px and 390px.
- Settings `number` type allows only ONE decimal: dollar-and-cents values (e.g. 14.99) must be `text` settings.
- Guarantee wording: use only "30-day money-back guarantee". Never "risk-free", "no questions asked", etc. until the refund policy says so.
- Do not describe the offer as time-limited ("today", "ends soon") without a real end date.

## Before publishing checklist (owner)
1. Supplement Facts + ingredients + directions on label and product page
2. Refund policy (owner text in `content/refund-policy.md`) finalised, support email filled in once the owner has a business email, pasted into Shopify Settings -> Policies -> Refund policy, and matching the 30-day money-back guarantee
3. Offer button link set (cart link adding jar + both gifts) and the 2 gift discounts created and tested
4. Gift stock in Shopify = number in theme settings; pause offer at 0
5. Real shipping terms; FAQ answers edited (ingredients, shipping)
6. Real reviews/ratings only if they exist; real offer end date only if one exists

## Layout
- `CLAUDE.md` – this file
- `PROGRESS.md` – audit log
- `.mcp.json` – project MCP servers (Shopify Dev MCP)
- `content/` – draft copy for owner review (`product-copy.md`, `listicle-outline.md`, `refund-policy.md`, `refund-policy-review.md`)
- `theme/` – local DRAFT Shopify theme. Push only with `shopify theme push --unpublished`, never `--live`
