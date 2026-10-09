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

## Project goals
1. Launch product "Formul8 Nutrition"
2. Bundle: 30% discount + 2 free gifts
3. High-converting listicle landing page
4. Sales-data analysis to inform the page
5. SEO audit + implementation

## Design
- Green colour scheme sampled from the jar: forest `#2E4A37`, mid green `#4A6649`, sage `#B5C4A8`, cream `#F5ECE5`, rose-gold `#C99A8B` (small highlights only). Defined in `theme/config/settings_schema.json`; use the CSS variables in `theme/assets/theme.css`, never hard-coded hex.
- Homepage hero = the owner's jar banner (`theme/assets/formul8-hero.jpg`, WebP + mobile crop alongside). The banner already holds the logo and tagline, so don't overlay text on the jar.
- Keep text/background contrast at WCAG AA (4.5:1).
- Footer carries the FDA disclaimer; keep it.

## Layout
- `CLAUDE.md` – this file
- `PROGRESS.md` – audit log
- `.mcp.json` – project MCP servers (Shopify Dev MCP)
- `theme/` – local DRAFT Shopify theme. Push only with `shopify theme push --unpublished`, never `--live`
