---
name: skill-pr-description
description: >
  Write short, user-facing pull request descriptions as plain bullet lists. Use when drafting, rewriting, or suggesting a PR description/body, or when the user asks for a PR summary in their preferred style.
---

# PR Description Style

## Goal

Produce a PR body that a reviewer can skim in seconds: what changed for the user/product, not how the code was implemented.

## Workflow

1. Gather changes from the PR (title, commits, file list, or diff summary).
2. Group related commits into a few product-level bullets.
3. Output **only** the bullet list (unless the user asks for Test plan / Summary).
4. If asked to update the PR, use that same body as-is.

## Format rules

- Plain markdown bullets only: `- ...`
- Start each bullet with a lowercase verb when natural: `added`, `removed`, `updated`, `improved`, `can do`, `replaced`
- Prefer user-visible language (tabs, flows, labels, actions)
- Quote UI strings exactly: `"Stock Transfers"`, `"Price (with GST)"`
- Keep each bullet to one idea; 4–10 bullets typical
- For misc PRs, group polish into thematic bullets (validation, loading UI, deploy, typography) instead of listing every commit
- No file paths, class names, or commit SHAs
- No `## Summary`, `## Test plan`, or other section headers unless requested
- No "This PR…" prose paragraphs

## Do / Don't

**Do**
- `- removed "Stock orders" tab`
- `- added stock tab with "my shop" and "at housie" subTabs`
- `- can do "send to housie" and "recall from housie" from stock tab`

**Don't**
- `- Updated src/app/(tabs)/stock/index.tsx to add StockScreen`
- `- Refactor StockOrders to StockTransfers for better DX`
- Long Conventional Commit / changelog-style paragraphs

## Examples

### Feature PR (focused)

- removed "Stock orders" tab
- added "Stock Transfers" tab which host both stock order and stock return order of the selected shop
- added stock tab with "my shop" and "at housie" subTabs
- added a flow to recall from housie (stock return order)
- can do "send to housie" and "recall from housie" from stock tab and from stock transfer tab

### Misc / polish PR (grouped)

- improved catalog add-product review validation for price and quantity
- updated price labels to show "Price (with GST)" across catalog screens
- added MobileNumberModal to call or copy rider/packer numbers from pickups
- replaced ActivityIndicator with list skeletons on sales and catalog for consistent loading UI
- integrated FlashList with NativeWind styling support
- removed hardcoded font-family styles across screens for consistent typography
- added web deploy script (`hsswebdeploy.sh` / `web-deploy`)
- added `.env.example` with GST numbers and env placeholders
- added platform-aware alerts/logout confirmation for web vs native
- misc UI polish: pickup card text sizes, shop selection modal height, catalog overlay z-index, mock image URIs for web

## Checklist before returning

- [ ] Bullets only (unless user asked for more)
- [ ] User/product language, not implementation detail
- [ ] Related changes grouped
- [ ] UI labels quoted where relevant