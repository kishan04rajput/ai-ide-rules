---
name: debugging
description: Systematic approach to finding and fixing bugs. Includes Root Cause Analysis (RCA).
---

# Debugging & Root Cause Analysis (RCA) Skill

Use this skill when the user reports a bug or when you encounter an error. Do not guess; follow this process.

## 1. Reproduce & Isolate
- **Constraint**: Can you reproduce it consistently?
- **Environment**: Does it happen locally? In production? specific browsers?
- **Isolate**: Remove independent variables. Create a minimal reproduction case if possible.

## 2. Root Cause Analysis (RCA) Process
1.  **Observe**: What is the error message? What is the stack trace?
2.  **Hypothesize**: valid hypotheses based on the code flow.
3.  **Test Hypothesis**: verifying assumptions (logs, breakpoints, inspecting state).
4.  **Pinpoint**: Identify the exact line of code or logic gap causing the issue.

> [!IMPORTANT]
> Fix the *cause*, not the *symptom*.

## 3. Implement Fix
- Apply the fix with minimal code changes.
- Ensure the fix addresses the root cause.

## 4. Verification & Side Effects
- **Verify Fix**: Run the reproduction case again to confirm it passes.
- **Regression Check**: Run related tests to ensure no new bugs were introduced.
- **Edge Cases**: Test limits (nulls, empty states, limits).

## 5. Report
- Explain **what** went wrong (the bug).
- Explain **why** it went wrong (the root cause).
- Explain **how** you fixed it (the solution).
