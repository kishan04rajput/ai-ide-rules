---
name: code-review
description: Reviews code changes for bugs, style issues, security, and best practices. Use when reviewing PRs or checking code quality.
---

# Code Review Skill

When reviewing code, act as a senior engineer pairing with the user. Follow these steps:

## 1. High-Level Understanding
- **Intent**: What problem is this solving?
- **Architecture**: Does this fit the existing design patterns?
- **Scope**: Is this change too big or too small?

## 2. Review Checklist

### Correctness & Logic
- [ ] Does the code actually solve the stated problem?
- [ ] Are there logical errors or race conditions?
- [ ] Are edge cases handled (e.g., null/undefined, empty lists, network failures)?
- [ ] Is input validation sufficient?

### Quality & Maintainability
- [ ] **Readability**: Is the code easy to understand? Are variable names descriptive?
- [ ] **DRY (Don't Repeat Yourself)**: Is there duplicated logic?
- [ ] **Complexity**: Can this be simplified? Is the cyclomatic complexity too high?
- [ ] **Tests**: Are there existing tests? Do they need updates? Are new tests needed?

### Performance & Scalability
- [ ] Are there O(n^2) or worse algorithms on potentially large datasets?
- [ ] Are there unnecessary database queries (N+1 problems)?
- [ ] Is memory usage optimized?

### Security (If applicable)
- [ ] Are secrets exposed?
- [ ] Is user input sanitized (SQL injection, XSS)?
- [ ] Are permission checks in place?

## 3. How to Provide Feedback
- **Be Constructive**: "Consider using X because Y" instead of "This is wrong".
- **Explain Why**: Provide context or links to documentation.
- **Distinguish Severity**:
    - **[BLOCKER]**: Must fix before merge (bugs, security).
    - **[WARN]**: Should fix (style, best practices).
    - **[NIT]**: Optional suggestions (renaming, comments).
- **Code Snippets**: improved code examples where helpful.