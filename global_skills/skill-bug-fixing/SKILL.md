---
name: bug-fixing
description: Systematic process for implementing minimal, intelligent bug fixes in any language (Implementation Only).
---

# Bug-Fixing Skill

Use this skill when a bug has already been **identified and analyzed** using the `identify-bugs` skill. This skill focuses on the **implementation and verification** of the fix across any programming language.

- **Persona**: Act like you are a master of the language being fixed and you know every core concept of this language.

## 1. Fix Strategy
- **Alternative Solutions**: Consider at least two ways to solve the problem before implementing.
- **Paradigm Alignment**: Ensure the fix aligns with the language's native paradigms (e.g., idiomatic Rust, functional approaches in Haskell, or event-driven patterns in Node.js).
- **Strategic Impact**: Evaluate how the chosen solution integrates with the existing architecture and its long-term maintainability.
- **Refinement**: Ensure the solution directly addresses the **root cause** identified during analysis, rather than just masking symptoms.

## 2. Implementation Rules
- **Least Code Rule**: Implement the fix with the **minimum amount of code change** required to maintain simplicity and reduce risk.
- **Future-Proof**: Fix it in a way that prevents similar patterns of bugs from recurring.
- **Naming**: Use highly descriptive and meaningful names for any new variables, functions, or helpers, following language-specific conventions.
- **Performance & Scalability**: Ensure the fix does not introduce performance regressions or scalability bottlenecks.
- **Integrity**: Ensure no existing functionalities are broken. Use the "Do Not Repeat Yourself" (DRY) principle to avoid duplication.

## 3. Verification & Validation
- **Verify Fix**: Confirm the original reproduction steps now pass consistently.
- **Regression Check**: Run existing test suites or manually validate related modules to ensure zero regression.
- **Edge Case Validation**: Explicitly test the boundary conditions (memory limits, concurrency, null-safety) identified during the analysis phase.
- **Final Result**: State "No potential issues and bugs found" if verification is clean, or provide a detailed list of potential risks/side effects.

> [!IMPORTANT]
> This skill is for **implementing** fixes in any language. For finding and analyzing bugs, use the **identify-bugs** skill. Always ensure you understand the root cause before writing any code.
