---
name: pr-review
description:
  Review pull requests for typos, logical gaps, broken flows, caching
  opportunities, and other errors. Use when the user asks to review a PR,
  pull request, or branch changes before merge.
---

# PR Review

Use this skill when reviewing a **pull request** or branch diff before merge.

Act as a senior engineer. Focus on correctness, flow, and practical improvements — not style nits unless they cause confusion.

---

## Phase 1 — Understand the PR

Before reviewing line by line:

- **Intent**: What problem does this PR solve?
- **Scope**: What files and behaviors changed?
- **Context**: Read the PR description, linked issues, and surrounding code — not just the diff in isolation.

Gather the full change set (diff, commits, or branch comparison) before giving feedback.

---

## Phase 2 — Review Checklist

Work through every item below. For each finding, note **file**, **location**, **what is wrong**, and **suggested fix**.

### Typos

- [ ] Check for any typo in code, comments, strings, variable names, log messages, docs, and UI copy introduced or touched by this PR.

### Logical gaps

- [ ] Check for any logical gap — missing conditions, unhandled edge cases, incomplete validation, wrong assumptions, or behavior that does not match the stated intent.

### Broken flow

- [ ] Check for any broken flow — dead ends, unreachable code, incorrect state transitions, missing error paths, async/race issues, or user/system journeys that stop or fail unexpectedly.

### Caching opportunities

- [ ] Check if cache can be implemented — repeated expensive reads, identical computations, or stable data fetched multiple times where caching (in-memory, HTTP, DB query, or application-level) would meaningfully reduce cost or latency without stale-data risk.

### Other errors

- [ ] Check for any other error — bugs, regressions, security issues, performance problems, missing tests, API contract breaks, type/syntax issues, or integration failures not covered above.

---

## Phase 3 — Report Findings

Structure the review clearly:

1. **Summary** — one short paragraph on whether the PR is ready to merge and the main risks.
2. **Findings** — grouped by checklist category (Typos, Logical gaps, Broken flow, Caching, Other errors).
3. **Severity** on each item:
   - **[BLOCKER]** — must fix before merge
   - **[WARN]** — should fix; acceptable only with a clear reason
   - **[NIT]** — optional improvement
4. **Verdict** — Approve, Request changes, or Comment only.

Be specific and constructive. Include code references or snippets when they make the issue clear.
