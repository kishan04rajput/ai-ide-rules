---
name: loop-until-objective-achieved
description: >-
  Run a multi-pass implement-verify-refine feedback loop until new or changed
  code is irreducible and acceptance criteria pass. Use when the user wants
  iterative feature work, bug fixes, or code that keeps getting tested and
  simplified across passes until nothing meaningful can be removed.
---

# Loop Until Objective Achieved

Use this skill for **standalone agents, Claude Code, Cursor IDE, Antigravity IDE**, or any AI coding workflow where the agent should **not stop after the first draft**.

The agent runs **passes** until the objective is met **and** the new/edited code has **converged** (no further meaningful simplification without losing clarity or behavior).

---

## Phase 0 — Intake (before any code)

Do not write code until intake is complete.

### 0.1 Classify the work

Ask the user (or infer from context):

- **Feature** — new behavior to add
- **Bug fix** — broken behavior to restore
- **Refactor-with-behavior-lock** — reshape code without changing outward behavior

### 0.2 Capture the objective

Get a short, testable statement:

- **What** to implement or fix
- **Expected behavior** — inputs, outputs, edge cases, error cases
- **Acceptance criteria** — how we know it is done (user-visible or testable)
- **Out of scope** — what must not change

### 0.3 Clarifying questions (use common sense)

Ask only what is needed to avoid wrong assumptions. Examples:

- Where should this live (file, module, layer)?
- Any existing pattern in the repo to mirror?
- Performance, security, or backward-compatibility constraints?
- For bugs: exact repro steps, expected vs actual, when it started?
- How should this be tested (existing suite, manual steps, both)?

### 0.4 Lock the contract

Before Pass 1, restate in 3–5 bullets:

1. Objective
2. Expected behavior
3. Acceptance checks (tests + manual if needed)
4. Files/areas likely touched
5. Stop condition for the loop

Wait for user confirmation if anything is ambiguous.

---

## The pass loop

Each pass follows the same skeleton:

```
INTAKE (once) → PASS N → PLAN → WORK → VERIFY → CONVERGE CHECK → PASS N+1 or STOP
```

### Pass types

| Pass | Focus | Rules |
|------|--------|--------|
| **1 — Implement** | Make it work | Match existing project structure, naming, patterns, and layering. Minimal scope. No premature optimization. |
| **2 — Optimize** | Simplify new/edited code | Remove duplication, dead code, unnecessary indirection. Prefer idiomatic constructs already used in the repo. |
| **3+ — Refine** | Same as Pass 2 | Only touch code introduced or modified for this objective. Each pass must be a **strict improvement** or **no-op**. |

**Important:** Pass 2 and later are **not** feature passes. Do not add behavior unless a test or acceptance criterion exposes a gap.

---

## Per-pass workflow

### Step 1 — State the pass

At the start of each pass, say:

- Pass number and type (Implement / Optimize / Refine)
- What you will change in this pass
- What you will **not** change

### Step 2 — Plan (before any code, every pass)

**Do not write or edit code until this plan is written.**

Create a **detailed, step-by-step implementation plan** for the current pass. The plan must be specific enough that another engineer could follow it without guessing.

Include:

1. **Goal of this pass** — one sentence tied to pass type (Implement / Optimize / Refine)
2. **Files to read first** — which existing files/modules to inspect for patterns and context
3. **Files to create or edit** — exact paths and what changes each file needs
4. **Ordered steps** — numbered actions in execution order (e.g. add type → add service method → wire controller → add test)
5. **Patterns to follow** — existing project conventions, helpers, or examples to mirror
6. **Verification plan** — what tests or checks will run after this pass
7. **Out of scope for this pass** — what you will deliberately not touch

**Pass-specific planning:**

- **Pass 1 (Implement):** Plan the full feature or fix end-to-end — data flow, layers, error handling, and tests.
- **Pass 2+ (Optimize / Refine):** Plan only targeted simplifications — what to remove, inline, or consolidate, and why each change is safe.

Only after the plan is complete, proceed to Step 3.

### Step 3 — Work

- **Pass 1:** Implement the feature or fix using existing conventions. Read surrounding code first.
- **Pass 2+:** Edit only new/changed code. Candidate simplifications:
  - Remove unused variables, branches, helpers
  - Inline one-use wrappers
  - Collapse redundant conditionals
  - Replace custom logic with existing project utilities
  - Tighten names only when it improves clarity

**Do not** "optimize" by:

- Changing unrelated files
- Trading clarity for cleverness
- Removing error handling or validation
- Breaking public APIs without explicit approval

### Step 4 — Verify (every pass, no exceptions)

Run checks appropriate to the project:

1. **Acceptance criteria** from Phase 0
2. **Automated tests** — project test command, focused tests on touched areas
3. **Bug repro** — original steps must pass for fixes
4. **Regression smoke** — related flows still work

If verification fails:

- Fix within the **same pass** if the failure is from this pass
- Do **not** advance to the next pass until verification passes
- If stuck after 2 fix attempts in one pass, report blocker and ask the user

### Step 5 — Pass report

End each pass with:

```markdown
## Pass N report

**Changes:** (brief)
**Verification:** (what ran, pass/fail)
**Diff summary:** lines added/removed in scope
**Simplifications this pass:** (list or "none")
**Ready for next pass:** yes/no
```

---

## Convergence — when to stop

Stop the loop when **all** are true:

1. **Objective met** — acceptance criteria pass
2. **Verification green** — tests and manual checks pass
3. **Irreducible code** — Pass N made **no meaningful simplification** compared to Pass N−1

### "Irreducible" means

Any of:

- Zero net reduction in complexity (no removable lines, helpers, or branches)
- Only cosmetic renames left, rejected as non-improvements
- Further edits would harm readability or violate project conventions

### Convergence check (Pass 2+)

Before starting another refine pass, ask:

> Can I remove or simplify anything in the new/edited code **without** changing behavior or hurting clarity?

- **No** → **STOP**, deliver final summary
- **Yes** → one more **Refine** pass with a concrete list of targets

### Safety limits

- **Max passes:** 8 total (1 implement + up to 7 refine). If not converged, stop and explain what remains non-irreducible and why.
- **No infinite loops:** If two consecutive passes produce identical or equivalent diffs, **STOP**.
- **User override:** If the user says stop, stop immediately after the current pass completes.

---

## Final delivery

When the loop stops, provide:

1. **Objective** — restated
2. **What shipped** — behavior in plain language
3. **Pass history** — one line per pass
4. **Verification evidence** — commands run and results
5. **Files changed** — list
6. **Residual risks** — or "No potential issues and bugs found."

---

## Examples

### Feature

**User:** "Add export to CSV on the reports page."

**Intake:** Expected columns, file name, empty state, large dataset behavior, existing export patterns.

**Pass 1:** Add export using same service/hook pattern as PDF export.
**Pass 2:** Remove duplicate mapping; reuse shared formatter.
**Pass 3:** Inline single-use helper; tests still green.
**Pass 4:** No meaningful simplifications → **STOP**.

### Bug fix

**User:** "Login fails when email has a plus sign."

**Intake:** Repro steps, expected login success, regex/validation location.

**Pass 1:** Fix validation to allow `+` in local part; match existing validator style.
**Pass 2:** Simplify conditional chain; add/adjust test.
**Pass 3:** No further removable code → **STOP**.

---

## Anti-patterns

- Stopping after Pass 1 when the user invoked this skill
- Refactoring unrelated legacy code during Optimize passes
- Advancing to the next pass while tests are failing
- Endless rename churn — not convergence
- Adding scope without user approval
- Skipping verification "because the change is small"
- Writing or editing code before completing the per-pass step-by-step plan

---

## Invocation

User may say:

- "Use loop until objective achieved"
- "Keep iterating until the code can't be simplified further"
- "Implement, test, then refine in passes"

Treat that as explicit activation of this full workflow.
