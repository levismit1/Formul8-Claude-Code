# Formul8 Listicle Landing Page – Build Notes (v0.2)

> BUILT in the local DRAFT theme as `theme/templates/page.listicle.json` (+ `sections/lp-*.liquid`). Not on Shopify yet.
> In Shopify it will be created as an UNPUBLISHED page using the `listicle` template.
> Only owner-confirmed Formul8 facts are used. Anything unknown is hidden or a visible, editable placeholder.

## What the reference page (Grüns Prime Time Sale, screenshot `images/3.jpg`) does well
1. Logo only, no navigation (nothing to click away to)
2. Social-proof strip first (stars, review count, members)
3. Two-tone problem/solution headline
4. Three check-mark proof bullets
5. One-line objection killer
6. Big CTA with a small badge on top and the offer inside the button
7. Risk reversal directly under the CTA ("Try it risk-free for 30 days")
8. "Your free gifts" tiles, each with a "FREE $X" value tag
9. Hero image showing product and gifts, plus a sale banner with REAL dates

## What we copied (structure only) and what we did NOT copy
| Reference element | Formul8 version | Status |
|---|---|---|
| Logo-only header | Header hides the nav on the listicle template | Built |
| Social proof strip | Hidden until real rating + review count are entered | Hidden (no real data yet) |
| Two-tone headline | "5 Reasons to Try Formul8 Nutrition" / "Your gut. Your health. Your formula." | Built |
| 3 proof ticks | 30 servings in every jar · FREE shaker + frother ($39.98 value) · 30-day money-back guarantee | Built (all true) |
| Objection-killer line | Skipped: we don't know if Formul8 is a powder, so "no blender" style claims are not made | Skipped |
| CTA + badge | "30% OFF TODAY" badge + "Get 30% Off + Free Gifts" | Built |
| Guarantee under CTA | "Try it risk-free for 30 days" + 30-day money-back guarantee | Built |
| Free gift tiles | FREE $14.99 shaker, FREE $24.99 frother | Built |
| Dated sale banner | Optional "Offer ends ..." line, hidden until a REAL date is entered | Hidden |
| Their claims (ingredients, fibre, clinical testing, 4.8 stars, 100,000 reviews, 2B sold) | NOT copied. We have no such facts. | Never |

## Page order (as built)
1. Announcement bar: green "In stock" + free-gifts line
2. Hero: headline, 3 ticks, CTA, guarantee line, "In stock", free-gift tiles, jar image (on phones: copy first, then image)
3. "Why you'll love it": 5 numbered reasons (your formula · 30 servings · 30% off · free shaker · free frother) + gifts photo + CTA
4. Reviews (renders only if the owner adds REAL reviews)
5. "What you get today": jar $70 + free shaker $14.99 + free frother $24.99 = $109.98 value, you pay $49
6. 30-Day Money-Back Guarantee block (links to the refund policy)
7. FAQ (5 questions)
8. Footer with FDA disclaimer
9. Sticky bottom bar on phones ($70 crossed out, $49, button)

## How the button will work (important)
A Shopify discount does not add the gifts to the cart. The offer button should be a **cart link** that adds the jar and both gifts together
(`/cart/<jar variant id>:1,<shaker variant id>:1,<frother variant id>:1`); the two automatic discounts then make the gifts $0 at checkout.
Set the link in Theme settings -> Offer & stock -> "Offer button link" once the products exist.

## Placeholders the owner must fix before publishing
- FAQ "What is in Formul8 Nutrition?" and "Shipping" answers (editable in the theme editor)
- Refund policy page text must match the 30-day money-back promise
- Real reviews/ratings and a real offer end date, only if they exist
- Supplement Facts on the product page and label
