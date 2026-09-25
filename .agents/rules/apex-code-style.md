---
trigger: glob
globs: "*.cls, **/*.cls, *.trigger, **/*.trigger"
description: "Apply to Apex source files for naming, readability, maintainability, and implementation style."
---
# Apex Code Style Rules

- Follow the existing repository naming and folder conventions.
- Prefer clear names over abbreviations; names should communicate business intent.
- Keep methods focused. Extract a method when it improves readability or isolates a meaningful responsibility.
- Avoid deeply nested conditionals; use guard clauses when they make control flow clearer.
- Avoid premature abstraction. Do not create frameworks or utilities for a one-off need without a demonstrated reuse case.
- Prefer immutable/read-only references where practical and avoid unnecessary state.
- Do not leave dead code, commented-out implementations, debug statements, or temporary bypasses in production code.
- Comments should explain why, business constraints, or non-obvious platform behavior—not restate the code.
- Preserve existing public APIs unless the requirement explicitly permits a breaking change.
