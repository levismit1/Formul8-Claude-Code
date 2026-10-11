# Refund Policy Review (v0.1)

> Review of the owner's policy (`content/refund-policy.md`) against what the website promises.
> Three independent reviewers (consistency, consumer-protection basics, practical operation) agreed on the main points.
> The owner's policy text has NOT been edited. This is not legal advice: have a qualified reviewer check the final policy.
> Placeholders `[Insert Customer Support Email]` / `[Insert Website URL]` are expected: the owner has no business email yet.

## What already works
- The policy's 30 days matches the site's exact wording "30-day money-back guarantee".
- Opened and partly used jars are eligible (a customer-friendly, clear rule).
- Damaged / defective / incorrect orders are covered; refund timing (5-10 business days) is stated.

## Decisions the owner needs to make (plain-language options)
| # | Question | Why it matters | Simple options |
|---|----------|----------------|----------------|
| 1 | **What happens to the free gifts on a refund?** (HIGH) | Gifts are $39.98 of the offer and you only have ~3 sets. The policy is silent, so support would improvise. | (a) Customer keeps the gifts, refund = what they paid for the jar. (b) Gifts must come back with the jar. (c) Gift value ($39.98) is deducted if not returned. If (b)/(c), say so near the offer on the site too. |
| 2 | **Must the jar be sent back? Who pays return shipping? Where to?** (HIGH) | Opened jars are allowed but section 5 says "if a physical return is required" without saying when. | (a) No return needed, refund on request (simplest). (b) Return required in stated cases, with who pays return shipping. |
| 3 | **Is the guarantee firm or at your discretion?** (HIGH) | "Review your request" and "once approved" read as optional. A guarantee reads as "ask within 30 days and get your money back". | Firm: "If you meet the requirements in Section 3, we will refund you." Or list the real grounds for refusing. |
| 4 | **Delete Section 7 (Subscriptions)?** | You haven't mentioned any subscription. The policy would describe a product and account feature that do not exist. | Remove it now; add back only if you launch a subscription. |
| 5 | **Pick ONE start for the 30 days.** | Section 1 says "receiving your order", Section 3 says "delivery". | Use "within 30 days of delivery" in both (needs tracking on every order). |
| 6 | **What exactly is refunded?** | Section 4 never says: item price, tax, discounts, shipping. Section 5 says original shipping is non-refundable. | Add one sentence: refund = the price you paid for the product (after discounts, plus tax charged on it); original shipping is covered in Section 5. |
| 7 | **Damaged/defective orders: deadline, photo, replacement vs refund?** | "As soon as possible" is open-ended. A replacement gift may be impossible when gift stock is 0. | Set a reporting window, ask for a photo, say what happens if a gift can't be replaced (refund the item). |
| 8 | **Are $70, $14.99 and $24.99 real reference prices?** | "Was/Normally/Value" prices must be genuine prices those items are (or will be) offered at; keep records. | Confirm, or drop the strike-throughs and the "$109.98 value" line. |
| 9 | Optional: add a neutral line on payment disputes. | The policy says nothing about card disputes. | "Contact us first so we can fix it. This does not limit your right to dispute a charge with your bank." (reviewer to confirm) |

## Website changes I can make (need the owner's approval first)
1. Put a small "See refund policy" link beside every guarantee line (homepage hero, listicle hero, recap) and add a refund-policy link to the footer. The links appear only once the policy exists in Shopify (`shop.refund_policy.url`). This adds a link, not new terms.
2. The footer currently has NO links and there is no contact page. Add a contact route once the business email exists.
3. If the shipping carve-out (original shipping not refunded) is material, consider a short qualifier next to the claim, e.g. "30-day money-back guarantee (original shipping not refunded). See refund policy." A qualified reviewer should confirm.
4. Update `content/product-copy.md` shipping/returns placeholders once decisions 1-7 are made.

## When the business email exists (4 places)
1. Policy Sections 2 and 8 (and the website URL)
2. Shopify Settings -> Notifications -> Sender email
3. Shopify Settings -> Store details -> Store contact email
4. A footer/contact link on the site
Stopgap if the email takes time: email forwarding on the domain (e.g. support@formul8nutrition.com forwarding to a personal inbox) at the domain registrar.

## How to put the policy into Shopify (owner step, after decisions + email)
1. Copy only the text from "# Refund & Return Policy" down (not the HTML comment at the top of the file).
2. Shopify admin -> Settings -> Policies -> Refund policy -> paste -> format headings/bullets with the editor toolbar -> Save.
3. Fill in the email, remove Section 7 if agreed, update "Last Updated".
Note: Shopify policies have no draft state; saving publishes the page `/policies/refund-policy`, so do this only when ready.

## Refund checklist for the owner (once orders exist)
1. Find the order by number and email; confirm it is within 30 days of delivery.
2. Orders -> Refund -> refund only the jar line.
3. Shipping box: $0.00 unless the order arrived damaged, defective or incorrect.
4. "Restock items": leave unticked for opened jars. For gifts, tick only if they physically came back. (Restocking changes the gift stock count, which feeds the "Free gifts in stock" badge.)
5. Add a note on the order, then send the refund.
