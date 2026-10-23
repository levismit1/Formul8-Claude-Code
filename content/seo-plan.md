# Formul8 Nutrition – pre-launch SEO setup (2026-10-23)

Brand-new store, password-protected: nothing is indexed yet. This is the setup to have ready; re-audit after launch.

## Done (in Shopify / theme)
| Item | Status |
|---|---|
| Jar product page title (50 chars) | "Formul8 Nutrition Dietary Supplement – 30 Servings" |
| Jar meta description (150 chars) | "Formul8 Nutrition: your gut, your health, your formula. 30 servings. Subscribe for 30% off your first jar plus a free shaker and hand blender/frother." (says "subscribe", so the discount claim is accurate) |
| URL handles | `formul8-nutrition`, `formul8-shaker-bottle`, `formul8-hand-blender-frother` |
| Image alt text | jar, shaker, frother photos all have descriptive alt text |
| Product structured data (JSON-LD, price + availability for Google) | Restored in the new product page (`f8-product`); Horizon had it only inside its own product section |
| Free-gift pages hidden from search | `noindex, nofollow` meta in `layout/theme.liquid` for products of type "Accessory" + Shopify `seo.hidden = 1` on both gift products (gifts are never sold separately) |
| One H1 per product page | Yes (product title) |

## For the owner at launch (Shopify admin; Claude cannot write these)
1. **Store name**: Settings -> General -> "Formul8 Nutrition" (currently the long waitlist sentence; it feeds titles, emails, footer).
2. **Homepage SEO** (Online Store -> Preferences):
   - Waitlist phase title: `Formul8 Nutrition – Join the Waitlist` (38 chars)
   - Waitlist description: `Formul8 Nutrition is a daily gut-health powder in development. Join the waitlist for early access and launch news.` (113 chars; keep the in-development wording)
   - Selling phase title: `Formul8 Nutrition – Daily Gut Health Supplement` (47 chars)
   - Selling description: `Formul8 Nutrition: your gut, your health, your formula. 30 servings per jar. Subscribe for 30% off your first jar.` (113 chars)
   - Social sharing image: the jar photo.
3. **Remove the storefront password** only at launch, then connect `formul8nutrition.com` (Settings -> Domains) and make it primary.
4. **Google Search Console + Bing Webmaster**: verify the domain, submit `https://formul8nutrition.com/sitemap.xml`.
5. **Policy pages** (refund, privacy, terms, shipping) live and linked from the footer (they are also trust signals).

## Rules
- No disease or medical claims in titles/descriptions; structure/function wording needs the qualified reviewer.
- Do not add review/rating markup (no real reviews exist).
- The listicle page (`page.listicle`) stays unpublished and noindex until launch; give it its own title/description when it goes live.

## After launch (re-audit)
Check indexing of the jar page, Core Web Vitals (the jar photo is the main image; keep it under ~300 KB), 404s, and that gift pages remain noindex.
