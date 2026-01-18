---
name: bug-fixing
description: Systematic process for reproducing, identifying root causes, and implementing minimal, intelligent bug fixes.
---

# Bug-Fixing Skill

Use this skill when tasked with fixing a bug. This is the **single source of truth** for reproduction, analysis, and implementation of fixes.

## 1. Reproduce & Isolate
- **Consistent Repro**: Can the bug be reproduced consistently? Document the steps.
- **Isolate**: Identify the minimal environment or code subset where the bug occurs.
- **Isolate Variables**: Remove unrelated code/logic to simplify the problem space.

## 2. Understand & Explain (RCA)
- **Analyze**: Thoroughly understand the existing code flow.
- **Determine Cause**: Find the **root cause**, not just the symptoms.
- **Categorize**: Is it a **logical bug** (incorrect result) or a **syntax/runtime error** (crash/exception)?
- **Explain**: Describe the bug and its cause in plain language before acting.

## 3. Scenario Evaluation
- **Edge Cases**: Consider boundary conditions (nulls, empty lists, extreme values).
- **Impact Analysis**: What else might this fix affect?
- **Alternative Solutions**: Consider at least two ways to solve the problem.

## 4. Implementation Rules
- **Least Code Rule**: Implement the fix with the **minimum amount of code change** required.
- **Future-Proof**: Fix it in a way that prevents similar bugs from recurring.
- **Naming**: Use meaningful names for any new variables or helpers.
- **Integrity**: Ensure no existing functionalities are broken.

## 5. Verification
- **Verify Fix**: Confirm the original reproduction steps now pass.
- **Regression Check**: Ensure no new issues were introduced.
- **Final Result**: State "No potential issues and bugs found" if verification is clean, or list potential risks.

> [!IMPORTANT]
> Always reproduce and explain before you implement. Fix the cause, not the behavior.
