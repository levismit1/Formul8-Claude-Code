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
10. **Credential safety:** before sending ANY credential, confirm the destination host is the owner-confirmed store domain. Never send credentials to a host reached by following a redirect, and never `curl -L` with secrets. If `SHOPIFY_STORE` is the placeholder `your-store.myshopify.com` (or any redirect/non-matching host), STOP and ask the owner for the real address; never retry with a guessed host. Show the owner the exact host before the first authenticated call.

## Store
- Public domain: `formul8nutrition.com` (provided by owner). The `.myshopify.com` handle is still needed for API access; keep it in `SHOPIFY_STORE`, not in git.
- Owner is creating the app in Shopify's Dev Dashboard (form asks for App URL + redirect URLs). Use App URL `https://shopify.dev/apps/default-app-home`; redirect URL blank or `https://formul8nutrition.com/` (unused; no OAuth login). Credentials are then `SHOPIFY_CLIENT_ID` + `SHOPIFY_CLIENT_SECRET` (env/secrets, never git): exchange for a short-lived Admin API token with the client-credentials grant (`POST https://<store>.myshopify.com/admin/oauth/access_token`, `grant_type=client_credentials`); verify this works on first connection. If the owner instead has a legacy custom app, use `SHOPIFY_ADMIN_TOKEN`.
- Scopes requested: `write_products,write_inventory,write_discounts,write_themes,write_content,write_legal_policies,read_orders,read_reports`.

## Brand status (owner-confirmed 2026-10-12)
- Formul8 Nutrition is a BRAND-NEW brand: not launched, no sales history, `formul8nutrition.com` is not live/connected yet. None of the products (jar, shaker, frother) exist in Shopify yet: create all three as DRAFT products.
- Consequences: (1) goal 4 "sales analysis" cannot use sales data yet; competitor benchmarking (Grüns page) stands in until after launch. (2) The SEO "audit" is a pre-launch SEO setup of theme/pages/products, re-audited after launch. (3) Keep the store password-protected until the owner approves launch. (4) Connect the domain in Shopify (Settings -> Domains) only when ready.
- **Pricing rule (SUPERSEDED the earlier "Option A" launch-price wording on 2026-10-13):** subscription pricing = $49 first jar, then $70 per month. No struck-through "was" prices; no gift "normally"/"value" claims; never "launch price" or "regular price after launch". ("Buy once"/"one-time purchase" is now a real option, 2026-10-22; never apply it to the subscription.) Have a qualified reviewer check pricing wording before launch.

## One-time purchase option (owner decision 2026-10-22, SUPERSEDES "subscription only" / "no one-time")
- The jar can be bought **once for $70** (no subscription, no renewal, no discount) OR as a **subscription: $49 first jar, then $70 per month**. Product page shows both as radio choices with Subscribe PRE-SELECTED (owner choice); one click switches to Buy once. Selling plan "Deliver every month" has NO discount (0%); the $49 comes from the discount code `FIRST30` (30% off, subscriptions only, first payment only, once per customer, applied automatically by the buy button via `/discount/FIRST30`; scheduled 2030-01-01 = OFF until launch).
- Free gifts are for SUBSCRIBERS only (owner choice): the buy button adds gifts only for Subscribe. Shopify cannot restrict automatic Buy X Get Y gift discounts by purchase type, so a customer who manually adds a gift to a one-time jar order would get it free (known limitation; accept or revisit before launch).
- Renewal sentence shows only for Subscribe (product page) and only when the cart holds a subscription (cart). One-time shows "One-time purchase: $70. This does not start a subscription." Never call the SUBSCRIPTION "one-time"; never show renewal wording on the one-time choice. Reviewer to check both options' wording.
- The jar product must keep one-time purchase allowed (`requiresSellingPlan` false).

## Subscription (owner decision 2026-10-13)
- Owner WANTS Formul8 sold as a SUBSCRIPTION (recurring deliveries). Keep Section 7 (Subscription Orders) in `content/refund-policy.md`. This supersedes the earlier "delete Section 7" suggestion.
- **DECIDED (owner, 2026-10-13):** monthly delivery of one 30-serving jar; **$49 for the first jar, then $70 per month until cancelled**; free shaker + frother with the FIRST delivery only; **cancel any time online** (customer account) or by contacting support; 30-day money-back guarantee per policy Section 7 (each eligible delivery covered: owner to confirm this is intended).
- **Renewal disclosure (one source of truth):** `theme/snippets/subscription-terms.liquid` renders "$49 for your first jar, then $70 per month until you cancel. Cancel any time." directly under EVERY buy button, INCLUDING the phone sticky bar (there is deliberately no shortened version; the bar appears only after the hero's own sentence has scrolled away). Prices/wording come from Theme settings -> Offer & stock. Never reword per page. "Cancel any time" is a promise: only true once customer accounts and the cancel option are live and tested. Free gifts are always worded "with your first subscription delivery". Express-consent mechanism at product page / cart / Shopify checkout is an OPEN question for the qualified reviewer.
- **Shopify setup plan (after the connection works; separate approval):** product variant price **$70.00**, NO one-time purchase (requires a selling plan). The "Monthly" selling plan (every 1 month, 30% off the FIRST delivery only, 0% after) is created by the OWNER in Shopify admin with the **Shopify Subscriptions app** (product -> Purchase options), NOT through this project's API app (a plan created by a different app would not be managed by the Subscriptions app); Claude guides the steps and only READS it back. First check in the Subscriptions app UI that a first-delivery-only discount can be set; if it cannot, research alternatives with the owner before building. Gifts = separate one-time products on the first order only; two inactive gift discounts. NO subscription write scopes are requested. Verify every step against the live Shopify docs first.
- Shopify needs a subscription app (Shopify Subscriptions, free) with selling plans, a supported payment provider and customer accounts (for self-serve cancel). The product page, offer wording (price, frequency, free gifts, guarantee), FAQ, add-to-cart form (Cart API with a `selling_plan` id; cart links cannot carry selling plans) and gift discounts must all be updated once decided.
- Auto-renewal is regulated (US federal ROSCA and state auto-renewal laws): price, frequency, renewal and the way to cancel must be clearly disclosed next to the buy button, the customer must expressly consent, and cancelling must be easy. Have a qualified reviewer check before launch. Never describe the offer as "one-time" or omit the recurring nature once decided.

## Product facts (from owner)
- Formul8 Nutrition, 30 servings. **Monthly subscription: $49 for the first jar, then $70 per month** (Shopify: variant price `70.00`, NO compare-at price, selling plan gives 30% off the first delivery). Owner decisions 2026-10-13 (replaced "Option A").
- $70 → $49 is exactly 30% off (the first jar). $70 is the real recurring monthly price from the second delivery.
- **Weights (owner-confirmed):** jar 12.7 oz, shaker bottle 6 oz, hand blender/frother 5 oz.
- **Offer (owner-confirmed):** subscribe and get 30% off your first jar ($49), plus 1 FREE shaker bottle + 1 FREE hand blender/frother with the first delivery; then $70 per month.
- Planned build: gifts as separate draft products with tracked stock; two inactive automatic Buy X Get Y discounts (one per gift, qty 1, 100% off, requires Formul8 in cart) so the owner can review before activating. Verify limits against Shopify docs once connected.
- Free gifts: (1) Formul8 shaker bottle, 6 oz; (2) Formul8 hand blender/frother, 5 oz. (Owner once mentioned $14.99 / $24.99 as intended retail prices; not used on the site.) Do NOT show gift "normal price", "value" or "total value" amounts (the gifts have never been sold separately); say "free with your first delivery". Photo: `theme/assets/formul8-gifts.jpg`. Neither gift exists in Shopify yet (owner-confirmed): create as DRAFT products (names, photos, weight, stock 3).
- **Stock (owner, 2026-10-12): no stock numbers.** Owner has no actual quantities for the jar, shaker bottle or frother and wants the site to just say "In stock" (green, `--color-instock` `#2E6B34`, no count). The theme setting `gifts_in_stock` (Theme settings -> Offer & stock, a tick box) shows/hides the badge. It must be TRUE: untick it if a gift is sold out. (Owner earlier said "3 gift sets"; superseded.) In Shopify, create the three products with "Track quantity" OFF for now; before launch the owner should switch tracking ON and enter real counts so nothing is oversold. Never show fake scarcity or counts.
- **Product form + proposed formula (owner copy, `content/waitlist-copy.md`, 2026-10-12):** Formul8 is described as an easy-to-mix daily gut-health POWDER that is STILL IN DEVELOPMENT. PROPOSED ingredients (not final): prebiotic fiber, L-glutamine, green banana resistant starch, probiotics ("being considered"), ginger root extract. The copy ends with a waitlist call to action and the disclaimer "Product in development. Ingredients, quantities, flavor, and final product specifications are subject to change." Rules: use ONLY the owner's exact wording, always with the in-development disclaimer; never state amounts, strains, flavor or that the formula is final or that the product is available to buy until the owner says so; the structure/function wording ("support digestive wellness", "normal intestinal function", "may support the gut microbiome") needs qualified review and the FDA disclaimer. PLACEMENT DECIDED (owner chose "Both", 2026-10-12): homepage waitlist (Site mode = Waitlist, the default) + the proposed-formula block in the draft product copy and the listicle FAQ default. Keep the product and listicle unpublished until the formula and Supplement Facts are final.
- **Site mode (theme setting, Theme settings -> Site mode):** `waitlist` (default: coming-soon homepage = jar image + owner's waitlist copy + email form; no Shop button, no offer/free gifts, no cart/nav, no announcement bar) or `selling` (the sales homepage). Switch to Selling ONLY at launch. The Shopify PASSWORD PAGE (`templates/password.json` + `layout/password.liquid`) always shows the waitlist form + a "Store owner? Enter using password" link, so the store can stay password-protected while the public joins the waitlist (with the password on, visitors never see the homepage). The listicle template (`page.listicle`) is NOT gated by Site mode: keep any page using it unpublished until launch. Waitlist sign-ups = Shopify customers tagged `newsletter` + `waitlist`; before collecting real emails the owner needs a privacy policy, a business email and a postal address in Shopify.
- **Ingredients/Supplement Facts: not available yet (MVP launch).** Never invent or imply ingredients, amounts or benefits. Use only what is visible on the jar (name, "Dietary Supplement", 30 servings, tagline "Your gut. Your health. Your formula.") or in owner-supplied copy. Product page keeps a clearly marked placeholder for the Supplement Facts panel; product stays DRAFT until the owner supplies it (supplements need a compliant Supplement Facts label before sale).

- **Guarantee (owner-confirmed): 30-day money-back guarantee.** Use exactly that wording. Terms (from delivery? opened jars? return shipping?) are not decided; they belong on the store's refund policy page, which must match the promise. Do not add terms elsewhere.
- **Offer button (CORRECTED 2026-10-13):** Shopify cart permalinks (`/cart/<variant>:<qty>`) do NOT support selling plans, so a cart link cannot start a subscription. Until products exist, the setting `offer_link` points to the product page (subscription option selected there). Planned build (needs the products + Subscriptions plan to exist, then test): a theme add-to-cart FORM/script using Shopify's Cart API that adds the jar with its `selling_plan` id (read in Liquid from the product's selling plan groups) plus the two gift variants without a plan; discounts then make the gifts $0.

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
0. Theme merged into the Shopify default theme (product/collection/cart/404/search templates exist and tested) BEFORE Selling mode is used
0b. Waitlist phase: privacy policy + business email + postal address set in Shopify before collecting emails; then at launch change Theme settings -> Site mode to Selling and update homepage SEO title/description
1. Supplement Facts + ingredients + directions on label and product page
2. Refund policy (owner text in `content/refund-policy.md`) finalised, support email filled in once the owner has a business email, pasted into Shopify Settings -> Policies -> Refund policy, and matching the 30-day money-back guarantee
3. Offer button works end to end (on-page add-to-cart form adds the jar with its selling plan + both gifts; or product-page link while that is built) and the 2 gift discounts created and tested
3a. SUBSCRIPTION READY: Shopify Subscriptions app installed + "Monthly" plan created by the owner (30% off first delivery only, then $70) + a supported payment provider + customer accounts turned on + a real test subscription made AND cancelled by the customer + the renewal sentence/consent shown at the product page, cart and Shopify checkout + support email and footer links (Account, Contact, Refund policy, Privacy) live + qualified reviewer sign-off on auto-renewal wording and on the 30-day guarantee covering every delivery. Also decide and state when the second charge happens and any cancellation cut-off before the next charge.
4. Real stock: turn Shopify "Track quantity" ON with real counts for jar, shaker, frother; untick `gifts_in_stock` in theme settings if a gift runs out
5. Real shipping terms; FAQ answers edited (ingredients, shipping)
6. Real reviews/ratings only if they exist; real offer end date only if one exists

## Theme architecture (IMPORTANT)
- `theme/` is a minimal STARTER (homepage, listicle, password page, header/footer). It has NO product, collection, cart, search, 404, page, blog or customer-account templates, so Selling mode cannot work from this theme alone (Shopify needs a matching template for every page type it renders).
- PLAN once connected: duplicate the store's default theme (Dawn) as the draft theme (never touch the live one), pull it, and PORT our sections (`waitlist`, `password-entry`, `hero`, `gifts`, `lp-*`), snippets (`icon-*`, `subscription-terms`), the `footer` section (policy/Account/Contact links, `support_email` setting), settings (Site mode, Offer & stock, colours), CSS and templates (`index`, `password`, `page.listicle`) into it. Re-run theme-check + renders after the merge. Do not switch Site mode to Selling until product, collection and cart pages exist and are tested.
- `config/settings_data.json` holds the owner's live editor choices (e.g. Site mode). Before any `theme push`, pull first; never push a stale `settings_data.json` over the owner's changes.

## Layout
- `CLAUDE.md` – this file
- `PROGRESS.md` – audit log
- `.mcp.json` – project MCP servers (Shopify Dev MCP)
- `content/` – draft copy for owner review (`product-copy.md`, `listicle-outline.md`, `refund-policy.md`, `refund-policy-review.md`, `waitlist-copy.md`)
- `theme-build/` – OVERLAY of files added/changed on top of Shopify's Horizon theme (the real store theme "Formul8 Build", id 166384533733). As of 2026-10-22 it is the PUBLISHED (main) theme; owner approved editing it directly (keep edits small, read back every push). The old "Formul8 Draft" (166174654693) is unpublished. Uploaded via Admin assets API (no Shopify CLI here).
- `theme/` – local DRAFT Shopify theme (older starter). Push only with `shopify theme push --unpublished`, never `--live`
