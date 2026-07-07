---
name: create-plan
description:
  Create a detailed step-by-step implementation plan from a requirement.
  Use when the user asks for a plan, implementation plan, technical design,
  approach, or roadmap before coding — in Cursor, Antigravity, Claude Code,
  or any AI-enabled IDE.
---

# Create Plan

Use this skill when the user wants a **detailed implementation plan** before any code is written.

- **Persona**: Act like an experienced system designer.

Works in **Cursor, Antigravity, Claude Code**, and other AI coding tools. **Do not write or edit code** while this skill is active unless the user explicitly asks to move from planning to implementation.

---

## Phase 1 — Understand the Requirement

Before planning, build a clear picture of what is being asked.

### 1.1 Restate the goal

In 1–3 sentences, restate:

- **What** needs to be built, changed, or fixed
- **Why** it matters (user value, bug impact, business rule)
- **Done when** — how we know the work is complete

### 1.2 Gather context

Inspect the codebase and any provided materials (issues, designs, prior messages) to learn:

- Relevant files, modules, APIs, and data models
- Existing patterns, conventions, and abstractions to reuse
- Dependencies, integrations, and constraints (auth, performance, compatibility)
- Existing tests or verification paths

### 1.3 Classify the work

Label the request (one or more):

| Type | Focus |
|------|--------|
| **Feature** | New behavior or capability |
| **Bug fix** | Restore correct behavior |
| **Refactor** | Reshape code without changing outward behavior |
| **Migration** | Move data, APIs, or infrastructure |
| **Configuration / DevOps** | Build, deploy, CI, or environment changes |

### 1.4 Define scope

Explicitly list:

- **In scope** — what this plan covers
- **Out of scope** — what will not be changed
- **Assumptions** — things treated as true unless the user corrects them

---

## Phase 2 — Clarify Discrepancies

**Do not produce a final plan while important ambiguity remains.**

### 2.1 What counts as a discrepancy

Ask for clarification when you find any of these:

- Conflicting requirements in the request, docs, or codebase
- Missing acceptance criteria or success metrics
- Unclear ownership of a layer (frontend vs backend vs infra)
- Multiple valid approaches with materially different trade-offs
- Undefined edge cases, error handling, or backward-compatibility expectations
- Ambiguous terminology (same word used for different concepts)
- Scope that seems too large for one pass without user prioritization

### 2.2 How to ask

- Ask **focused, numbered questions** — only what blocks a correct plan
- Propose a **default assumption** when helpful so the user can confirm or correct quickly
- Group related questions; avoid interrogating the user on details you can infer from the repo
- If a structured question tool is available (e.g. AskQuestion), use it for decisions with clear options

### 2.3 When to proceed without asking

Proceed only when:

- The requirement is unambiguous, **or**
- Remaining unknowns are minor and you document them under **Assumptions** and **Risks**

If anything material is still unclear, **stop and ask** before Phase 3.

---

## Phase 3 — Create the Implementation Plan

Produce a **detailed, step-by-step plan** the user (or another agent) can execute without guessing.

### 3.1 Plan principles

- **Reuse first** — extend existing code and patterns; do not reinvent
- **Minimal scope** — each step should have one clear purpose
- **Ordered** — later steps may depend on earlier ones; call out dependencies
- **Verifiable** — every major step should say how to confirm it worked
- **No code** — describe what to do, not full implementations (pseudocode or signatures only when they remove ambiguity)

### 3.2 Required plan sections

Use this structure:

```markdown
# Implementation Plan: [Short title]

## Summary
[2–4 sentences: goal, approach, and expected outcome]

## Requirements understood
- [Bullet list of what was interpreted from the request]

## Assumptions
- [Bullets, or "None" if fully specified]

## Out of scope
- [Bullets]

## Affected areas
| Area | Files / modules (best guess) | Change type |
|------|------------------------------|-------------|
| ... | ... | add / modify / delete |

## Step-by-step plan

### Step 1: [Title]
- **Objective**: ...
- **Actions**: ...
- **Depends on**: none | Step N
- **Verify**: ...

### Step 2: [Title]
...

## Testing & verification
- [ ] Unit / integration tests to add or update
- [ ] Manual checks
- [ ] Regression areas to watch

## Risks & mitigations
| Risk | Mitigation |
|------|------------|
| ... | ... |

## Open questions (if any)
- [Only items deferred with user acknowledgment]
```

### 3.3 Step granularity

| Task size | Guidance |
|-----------|----------|
| Small (single file, obvious change) | 3–7 steps |
| Medium (multiple files or one layer) | 7–15 steps |
| Large (cross-cutting or new subsystem) | 15+ steps, grouped into **phases** with milestones |

Each step should be actionable in one focused work session.

### 3.4 Optional sections (use when relevant)

- **Data model / API changes** — schemas, endpoints, request/response shapes
- **Rollout / migration strategy** — feature flags, phased deploy, rollback
- **Alternatives considered** — brief note on rejected approaches and why
- **Follow-up work** — items intentionally deferred after MVP

---

## Phase 4 — Handoff

End every plan with:

1. **Recap** — one paragraph on the recommended approach
2. **Suggested execution order** — which steps to do first if splitting across PRs or sessions
3. **Explicit pause** — ask whether to proceed with implementation or adjust the plan

Do not start implementing until the user confirms or requests implementation.

---

## Anti-patterns

- ❌ Vague steps ("update the logic", "fix the bug")
- ❌ Planning without reading relevant existing code
- ❌ Skipping clarification when requirements conflict
- ❌ Mixing full code implementations into the plan
- ❌ Ignoring tests, migrations, or rollback
- ❌ Over-engineering — plan the simplest path that meets the requirement

---

## Quick checklist

Before delivering the plan:

- [ ] Requirement restated and scope defined
- [ ] Discrepancies resolved or listed as assumptions / open questions
- [ ] Steps are ordered, specific, and verifiable
- [ ] Existing patterns and files identified
- [ ] Testing and risks covered
- [ ] No code written unless user asked to implement
