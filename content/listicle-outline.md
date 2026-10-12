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
7. Risk reversal directly under the CTA (a guarantee line)
8. "Your free gifts" tiles, each with a "FREE $X" value tag
9. Hero image showing product and gifts, plus a sale banner with REAL dates

## What we copied (structure only) and what we did NOT copy
| Reference element | Formul8 version | Status |
|---|---|---|
| Logo-only header | Header hides the nav on the listicle template | Built |
| Social proof strip | Hidden until real rating + review count are entered | Hidden (no real data yet) |
| Two-tone headline | "5 Reasons to Try Formul8 Nutrition" / "Your gut. Your health. Your formula." | Built |
| 3 proof ticks | 30 servings in every jar · FREE shaker + frother with your jar · 30-day money-back guarantee | Built (all true) |
| Objection-killer line | Skipped: we don't know if Formul8 is a powder, so "no blender" style claims are not made | Skipped |
| CTA + badge | "30% OFF" badge + "Get 30% Off + Free Gifts" (no "today": no real end date) | Built |
| Guarantee under CTA | "Backed by our 30-day money-back guarantee" (exact owner wording; "risk-free" deliberately NOT used, terms undecided) | Built |
| Free gift tiles | Shaker and frother tiles tagged FREE (no "value" amounts: gifts have never been sold separately) | Built |
| Dated sale banner | Optional "Offer ends ..." line, hidden until a REAL date is entered | Hidden |
| Their claims (ingredients, fibre, clinical testing, 4.8 stars, 100,000 reviews, 2B sold) | NOT copied. We have no such facts. | Never |

## Page order (as built)
1. Announcement bar: green "In stock" + free-gifts line
2. Hero: headline, 3 ticks, CTA, guarantee line, "In stock", free-gift tiles, jar image (on phones: copy first, then image)
3. "Why you'll love it": 5 numbered reasons (your formula · 30 servings · 30% off · free shaker · free frother) + gifts photo + CTA
4. Reviews (renders only if the owner adds REAL reviews)
5. "What you get today": jar $49 launch price + free shaker + free frother = $49 total; note "Launch price. Regular price $70 after launch."
6. 30-Day Money-Back Guarantee block (links to the refund policy)
7. FAQ (5 questions)
8. Footer with FDA disclaimer
9. Sticky bottom bar on phones ("Launch price $49", button)

## How the button will work (important)
A Shopify discount does not add the gifts to the cart. The offer button should be a **cart link** that adds the jar and both gifts together
(`/cart/<jar variant id>:1,<shaker variant id>:1,<frother variant id>:1`); the two automatic discounts then make the gifts $0 at checkout.
Set the link in Theme settings -> Offer & stock -> "Offer button link" once the products exist.

## Placeholders the owner must fix before publishing
- FAQ "What is in Formul8 Nutrition?" and "Shipping" answers (editable in the theme editor)
- Refund policy page text must match the 30-day money-back promise
- Real reviews/ratings and a real offer end date, only if they exist
- Theme settings -> Offer & stock -> "Offer button link" (the cart link that adds jar + both gifts) is REQUIRED before launch
- Create the store refund policy (Settings -> Policies); the guarantee block links to it only once it exists
- Keep "Free gifts in stock" honest: update the gift stock number, or pause the offer when gifts run out (the page then shows "Free gifts currently out of stock")
- Supplement Facts on the product page and label

---

## Full-page structure of the reference page (fetched 2026-10-12 from the owner's Grüns link)
Structure only. None of their claims, statistics, survey results, testimonials or certifications are copied or implied for Formul8.

| Order | Reference section | What it does for conversion | Formul8 version |
|---|---|---|---|
| 1 | Top bar: "Save 61% + free gifts on your first order" and a shipping cut-off line (order by 1 PM ET for same-day shipping) | Offer and delivery promise visible immediately | Offer line: built (announcement bar). Shipping cut-off: only with REAL shipping terms (owner to supply). |
| 2 | Hero: proof strip, two-tone headline, 3 ticks, one-line objection killer, big CTA, guarantee line, gift tiles | See earlier table | Built |
| 3 | Four short customer testimonials right after the hero | Social proof early | `lp-reviews` section exists and stays hidden until the owner has REAL reviews; place it directly after the hero when filled |
| 4 | "Transform your health": four benefit categories | Shows what the product is for | NOT built: needs substantiated benefit claims and a Supplement Facts panel (none yet) |
| 5 | "Modern living leaves our bodies deficient": problem statistics | Problem framing | NOT built: statistics need real, cited sources |
| 6 | "Snackable, packable, tested": customer-survey results with a footnote describing the survey | Proof, with the survey sample disclosed | NOT built: no survey exists; never invent one |
| 7 | "Quality you can trust": testing and certifications | Trust | NOT built until real third-party tests exist |
| 8 | Offer section with a real deadline, plan cards ("Most popular"), per-option "30-day money-back guarantee" and "free gifts included" lines | Choice plus risk reversal at the decision point | Recap box with the guarantee line: built. Deadline only if real. No plan options or autoship (no subscription). |
| 9 | Accordions: why this product, ingredients and allergies, science and certifications, directions, benefits | Answers objections without leaving the page | FAQ accordion: built. Add "Ingredients and Supplement Facts" and "Directions" accordions once the label exists. |
| 10 | Guarantee section ("X% of customers use our guarantee") | Reassurance | Guarantee block built. Do NOT quote a usage percentage unless it is real. |
| 11 | "Replaces handfuls of health products at a fraction of the cost" comparison | Value framing | NOT built: needs substantiated comparison claims |

### Concrete changes this suggests for our page (need owner approval before I build them)
1. Move the (hidden-until-real) testimonials block to sit right after the hero.
2. Add "Ingredients & Supplement Facts" and "Directions" accordions to the FAQ, marked as placeholders until the label exists.
3. Add a shipping cut-off or delivery line to the top bar only when the owner has real shipping terms.
4. Keep the "Most popular" idea out: Formul8 has a single offer.
