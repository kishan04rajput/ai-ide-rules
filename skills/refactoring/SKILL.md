---
name: refactoring
description: Improving code structure without changing its external behavior. Focuses on clean code, DRY, and SOLID principles.
---

# Refactoring Skill

Use this skill when cleaning up code, reducing technical debt, or improving readability.

## Core Principles
1.  **Behavior Preservation**: The code must do exactly the same thing before and after refactoring (verified by tests).
2.  **Small Steps**: Make small, incremental changes.
3.  **Green State**: Ensure tests pass after every small change.

## Common Refactoring Targets
- **Duplicated Code**: Apply DRY (Don't Repeat Yourself). Extract functions/components.
- **Long Functions**: Break them down into smaller, single-responsibility helpers.
- **Magic Numbers/Strings**: Replace with named constants.
- **Complex Conditionals**: Simplify logic, use guard clauses, or extract booleans.
- **Naming**: Rename variables/functions to reveal intent.

## Step-by-Step Process
1.  **Identify Smell**: What is wrong? (Hard to read? Duplicated? Tightly coupled?)
2.  **Plan**: Decide on the refactoring pattern (e.g., Extract Method, Rename Variable).
3.  **Verify Tests**: Ensure current tests pass. If no tests exist, **write them first**.
4.  **Execute**: Apply the refactoring.
5.  **Verify**: Run tests again.
6.  **Cleanup**: Remove unused code/imports.

> [!TIP]
> If a refactor breaks something and you can't fix it quickly, **revert** and try a smaller step.
