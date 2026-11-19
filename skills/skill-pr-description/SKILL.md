---
name: skill-pr-description
description: "Write short, user-facing pull request descriptions as two bullet-list sections: \"What's New?\" and \"Fixes\". Use when drafting, rewriting, or suggesting a PR description/body, or when the user asks for a PR summary in their preferred style."
---

# PR Description Style

## Goal

Produce a PR body that a reviewer can skim in seconds: what changed for the user/product, not how the code was implemented.

## Output template

Always use exactly this structure:

```
What's New?
- Bullet point 1
- Bullet point 2

Fixes
- Bullet point 1
- Bullet point 2
```

## Workflow

1. Gather changes from the PR (title, commits, file list, or diff summary).
2. Split changes into new features/behavior (`What's New?`) and bug fixes (`Fixes`).
3. Group related commits into a few product-level bullets within each section.
4. Output **only** the `What's New?` and `Fixes` sections (unless the user asks for Test plan / Summary).
5. If asked to update the PR, use that same body as-is.

## Format rules

- Exactly two sections, in this order, each heading on its own plain-text line (no `#`, no bold):
  - `What's New?`
  - `Fixes`
- No blank line between a heading and its first bullet; bullets start on the very next line
- One blank line between the two sections
- Bullets use `- ...` only (never `*`)
- Start each bullet with a capital letter
- Omit a section entirely if it has no items
- `What's New?`: new features, new screens/flows, changed behavior, UI polish, docs/tooling
- `Fixes`: bug fixes, typos, regressions, broken flows; start each bullet with `Fixed`
- In `What's New?`, start each bullet with a verb when natural: `Added`, `Removed`, `Updated`, `Improved`, `Can do`, `Replaced`
- Prefer user-visible language (tabs, flows, labels, actions)
- Quote UI strings exactly: `"Stock Transfers"`, `"Price (with GST)"`
- Keep each bullet to one idea; 4–10 bullets typical per section
- For misc PRs, group polish into thematic bullets (validation, loading UI, deploy, typography) instead of listing every commit
- Only list a fix if it is fully fixed in the PR; partial fixes are left out or described accurately
- No file paths, class names, or commit SHAs
- No other headings (`## Summary`, `## Test plan`, etc.) unless requested
- No "This PR…" prose paragraphs

## Do / Don't

**Do**
- `- Removed "Stock orders" tab`
- `- Added stock tab with "my shop" and "at housie" subTabs`
- `- Can do "send to housie" and "recall from housie" from stock tab`
- `- Fixed back navigation from company setup creating a duplicate company`

**Don't**
- `- Updated src/app/(tabs)/stock/index.tsx to add StockScreen`
- `- Refactor StockOrders to StockTransfers for better DX`
- `## What's New?`, `**What's New?**` or `What's new?` (use the exact plain-text heading `What's New?`)
- A blank line between a heading and its bullets
- `* ...` bullets (use `- ...`)
- Putting bug fixes under `What's New?`
- Long Conventional Commit / changelog-style paragraphs

## Examples

### Feature PR (focused)

```
What's New?
- Removed "Stock orders" tab
- Added "Stock Transfers" tab which host both stock order and stock return order of the selected shop
- Added stock tab with "my shop" and "at housie" subTabs
- Added a flow to recall from housie (stock return order)
- Can do "send to housie" and "recall from housie" from stock tab and from stock transfer tab

Fixes
- Fixed stock order list not refreshing after creating a new order
```

### Misc / polish PR (grouped)

```
What's New?
- Updated price labels to show "Price (with GST)" across catalog screens
- Added MobileNumberModal to call or copy rider/packer numbers from pickups
- Replaced ActivityIndicator with list skeletons on sales and catalog for consistent loading UI
- Integrated FlashList with NativeWind styling support
- Added web deploy script (`hsswebdeploy.sh` / `web-deploy`)
- Added `.env.example` with GST numbers and env placeholders
- Added platform-aware alerts/logout confirmation for web vs native

Fixes
- Fixed catalog add-product review validation for price and quantity
- Fixed inconsistent typography caused by hardcoded font-family styles
- Fixed pickup card text sizes, shop selection modal height, catalog overlay z-index and mock image URIs on web
```

### Fixes-only PR

```
Fixes
- Fixed OTP autofill on the OTP screen
- Fixed "categoryies" typo in category preferences selected count
```

## Checklist before returning

- [ ] Only `What's New?` and `Fixes` sections (unless user asked for more), empty section omitted
- [ ] Plain-text headings exactly `What's New?` and `Fixes`, bullets directly below with no blank line
- [ ] One blank line between the two sections
- [ ] `-` bullets, each starting with a capital letter
- [ ] Features under `What's New?`, bug fixes under `Fixes` starting with `Fixed`
- [ ] User/product language, not implementation detail
- [ ] Related changes grouped
- [ ] UI labels quoted where relevant