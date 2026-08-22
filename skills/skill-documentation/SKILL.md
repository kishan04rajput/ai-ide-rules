---
name: documentation
description: Guidelines for writing high-quality, intent-focused documentation and comments.
---

# Documentation Skill

Use this skill when writing in-code comments, READMEs, or technical guides. Focus on the **content and intent** of the documentation.

## Philosophy: Intent Over Implementation
Do not document *what* the code is doing (the code itself is the documentation for that). Document **why** it is doing it and any **context** a reader might lack.

## Documentation Targets

### 1. In-Code Comments
- **Contextual**: Explain non-obvious logic, business rules, or "hacks" required by external systems.
- **Standardized**: Use appropriate docstring/comment formats for the language (e.g., JSDoc for JS).
- **Maintenance**: Delete stale comments; they are more dangerous than no comments.

### 2. Project Documentation (README)
- **High-Level**: Provide the "Big Picture" of the module or project.
- **Actionable**: Installation, usage examples, and troubleshooting steps must be clear and tested.

### 3. Separation of Concerns
- This skill is for **writing content**. For **commit message formatting**, refer to the `commit-message-generator` skill.

## Checklist
- [ ] Does this explain the **why**?
- [ ] Is it concise and free of jargon?
- [ ] Is it located where a developer would naturally look for it?