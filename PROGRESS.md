# PROGRESS.md – Audit Log

Every API call and file change is logged here. No Shopify store calls have been made yet.

| # | Date (UTC) | Type | Action | Target | Result | Rollback |
|---|------------|------|--------|--------|--------|----------|
| 1 | 2026-10-09 | Env check | Looked for Shopify plugins/MCP/CLI | local environment | None installed; Node 22 present | n/a |
| 2 | 2026-10-09 | File | Created `CLAUDE.md` | repo root | OK | delete file |
| 3 | 2026-10-09 | File | Created `PROGRESS.md` | repo root | OK | delete file |
| 4 | 2026-10-09 | File | Created `.mcp.json` (Shopify Dev MCP) and `.gitignore` | repo root | OK | delete files |
| 5 | 2026-10-09 | File | Copied owner's jar banner to `theme/assets/formul8-hero.jpg`; created `formul8-hero.webp` (55 KB) and `formul8-hero-mobile.webp` (46 KB, jar-centred crop) | theme/assets | OK | delete files |
| 6 | 2026-10-09 | File | Scaffolded local draft theme: `layout/theme.liquid`, `sections/{hero,header,footer}.liquid`, `sections/*-group.json`, `templates/index.json`, `config/settings_*.json`, `locales/en.default.json`, `assets/theme.css` | theme/ | JSON valid; local Playwright preview checked at 1440px and 390px; not pushed to Shopify | delete `theme/` |
| 7 | 2026-10-09 | File | Green palette set; mid green darkened to `#4A6649` for WCAG AA (5.48:1 on cream) | theme/config/settings_schema.json | OK | revert commit |
| 8 | 2026-10-09 | Env check | Tested connectivity: npm registry OK (200); `shopify.dev` blocked by network policy (403); `shopify-dev-mcp` timed out on connect; `SHOPIFY_STORE` / `SHOPIFY_ADMIN_TOKEN` not set | local environment | Blocked until owner updates environment settings | n/a |

## Status
- [ ] Store connection (custom app token) – waiting on owner: (a) allow `shopify.dev` + `*.myshopify.com` in network settings, (b) add `SHOPIFY_STORE` and `SHOPIFY_ADMIN_TOKEN` to the environment
- [ ] Product (draft)
- [ ] Bundle + discount + gifts (draft)
- [x] Homepage hero + green scheme (local draft theme, not yet on Shopify)
- [ ] Listicle landing page (draft theme)
- [ ] Sales analysis
- [ ] SEO audit + changes
