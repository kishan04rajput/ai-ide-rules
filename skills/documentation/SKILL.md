---
name: documentation
description: Guidelines for writing clear, useful documentation (comments, READMEs, API docs).
---

# Documentation Skill

Use this skill when writing comments, updating READMEs, or creating documentation files.

## Philosophy: "Why", not just "What"
Good documentation explains the *intent* and *context*, not just what the code is doing (the code shows that).

## Types of Documentation

### 1. Code Comments
- **Good**: `// Retry logic to handle intermittent network failures`
- **Bad**: `// Increment i by 1`
- Use JSDoc/Docstring formats for functions (params, return types).

### 2. README.md
- **Title & Description**: What is this project?
- **Getting Started**: How to install and run it.
- **Usage**: Examples of how to use it.
- **Architecture**: Brief overview of the structure.

### 3. Commit Messages
- Follow the `commit-message-generator` skill format.
- Context is key.

## Checklist for Writing Docs
- [ ] Is it up to date? (Outdated docs are worse than no docs).
- [ ] Is it concise? (Avoid walls of text).
- [ ] Is it clear to a newcomer? (Avoid jargon where possible).
- [ ] Are code examples copy-pasteable and working?
 