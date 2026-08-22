---
name: identify-bugs
description: Systematic process for identifying and analyzing bugs (Identification Only).
---

# Identify-Bugs Skill

Use this skill when tasked with **identifying or analyzing** a bug. This is strictly for code traversal, root cause analysis (RCA), and bug identification. **Do not use this skill for implementing fixes or writing fix code.**

- **Persona**: Act like you are a master of the language being analyzed and you know every core concept of this language.

## 1. Reproduce & Isolate
- **Consistent Repro**: Can the bug be reproduced consistently? Document the steps.
- **Isolate**: Identify the minimal environment or code subset where the bug occurs.
- **Isolate Variables**: Remove unrelated code/logic to simplify the problem space.

## 2. Code Traversal & Method Analysis
- **Entry Point**: Start traversing code from a clear starting point (e.g., API endpoint, event trigger, or specific function call).
- **Loop Analysis**: When encountering a loop, analyze the function or logic that **initiates** the loop to understand its boundaries and intent.
- **Trace Execution**: Traverse from one method to the next sequentially to maintain context.
- **Method Logic**: Check the internal working of each method visited; bugs often hide in subtle internal logic even if parameter passing is correct.

## 3. State & Data Flow Analysis
- **State Tracking**: Trace how the **internal state** of an object or system changes at each step. Identify where the state diverges from the expected value.
- **Data Integrity**: Verify that all arguments and parameters passed between methods are correct and maintain integrity.
- **Side Effects**: In functional or hybrid languages, check for unexpected side effects in "pure" functions.
- **Type Safety**: In statically typed languages, look for unsafe casts or logic that bypasses type checks. In dynamic languages, check for unexpected type mutations.

## 4. Concurrency & Resource Analysis
- **Race Conditions**: If the language supports concurrency (async/await, threads, actors), check if multiple processes are accessing shared state without proper synchronization.
- **Resource Leaks**: Look for unclosed streams, database connections, or memory that isn't being freed (even in GC languages, check for global references/closures).
- **Deadlocks/Starvation**: Analyze if execution is hanging due to circular dependencies on resources or locks.

## 5. Paradigm-Specific Quiddities
- **Language Master Lens**: Apply your mastery of the specific language's "quirks" (e.g., Python's mutable default arguments, JavaScript's `this` context/event loop, Rust's ownership, or C's pointer arithmetic).
- **Control Flow Logic**: Analyze logic hierarchies. In OO, check for inheritance/polymorphism abuse. In Functional, check for deep recursion or complex closure captured variables.

## 6. Understand & Explain (RCA)
- **Root Cause**: Identify the **root cause** of the issue, not just the symptoms, and explain why it occurs.
- **Bug Type**: Categorize as a **logical bug**, **race condition**, **memory/resource issue**, or **syntax/runtime bug**.
- **Scope check**: If a bug is found, investigate **why** it's happening and determine what **other locations** in the codebase might be affected by the same pattern.
- **Explain**: Clearly describe the bug and its origin in plain language before acting.

## 7. Scenario Evaluation
- **Universal Edge Cases**: Consider extremes: maximum/minimum integers, empty strings/collections, null/undefined, character encoding (UTF-8), timezones, and network latency.
- **Impact Analysis**: Assess how this bug (and potential fixes) might affect the broader system.

## 8. Verification (Identification Only)
- **Confirmation**: Ensure the identified bug's source has been pinpointed and its reproduction steps are fully understood.
- **Reporting**: List any potential risks or related issues found during the traversal.

> [!IMPORTANT]
> This skill is for **identifying** bugs in any language (current or future). For implementing fixes, use the **bug-fixing** skill. Always find the root cause before proceeding.
