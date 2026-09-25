---
name: apex-core
description: Develops and refactors Salesforce Apex using platform-aware coding conventions, governor-limit discipline, exception handling, transaction awareness, and maintainable class design. Use for general Apex classes, methods, DTOs, enums, utility code, and refactoring when a more specialized Apex skill is not the primary concern.
---

# Apex Core

## Workflow

1. Identify execution context: synchronous, Queueable, Batchable, Scheduled, trigger, invocable, REST/SOAP, or UI-facing Apex.
2. Identify transaction boundaries and expected record volume.
3. Identify data access and security requirements before writing code.
4. Prefer simple, explicit Apex over unnecessary abstraction.
5. Keep methods cohesive and side effects obvious.
6. Handle expected business failures explicitly; do not swallow exceptions.
7. Avoid hard-coded IDs, field names, URLs, credentials, or org-specific assumptions unless the requirement explicitly calls for them.
8. For behavior that varies by Salesforce/API version, verify the target API version and current official documentation.

## Coding rules

- Bulkify collection-processing code.
- Do not perform SOQL or DML inside loops unless the operation is provably bounded and intentionally designed that way.
- Prefer `List`, `Set`, and `Map` to repeatedly scanning collections.
- Keep DML close to the orchestration layer so transaction behavior is visible.
- Use meaningful names and small methods.
- Avoid static mutable state unless its lifetime and reset behavior are intentional.
- Avoid `System.debug` as application-level error handling.
- Use custom exceptions only when they add semantic value.
- Preserve existing public/global contracts unless the user explicitly requests a breaking change.

## Output expectations

When generating Apex:
- Return production-ready code, not pseudocode, when requirements are sufficient.
- Include tests when creating non-trivial production code.
- State assumptions that cannot be verified from the prompt.
- Call out governor-limit, security, transaction, and concurrency risks when material.
