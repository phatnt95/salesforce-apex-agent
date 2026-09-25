---
trigger: manual
description: "Use as an explicit pre-merge Apex review checklist. Mention @apex-review to activate it."
---
# Apex Pre-Merge Review Checklist

Review the change in this order:

1. **Correctness** — Does it satisfy the requirement and handle edge cases?
2. **Bulk safety** — Any SOQL/SOSL/DML/callout in loops? Any unbounded collections or limit risks?
3. **Security** — Sharing, CRUD/FLS, user/system mode, input validation, dynamic SOQL, and data exposure.
4. **Transaction design** — Is work synchronous when it should be, or asynchronous when necessary? Are partial failures handled intentionally?
5. **Automation interaction** — Could Flow, Trigger, Process, Platform Event, or other automation cause recursion or duplicate work?
6. **Performance** — Query selectivity, unnecessary fields, repeated work, large loops, and avoidable serialization.
7. **Maintainability** — Clear responsibilities, existing patterns reused, no unnecessary abstraction.
8. **Testing** — Success, failure, bulk, boundary, security, and async paths are covered with meaningful assertions.
9. **Deployment safety** — No hard-coded IDs, environment-specific secrets, or assumptions that only work in one org.
10. **Salesforce version behavior** — If behavior is release/API-version dependent, verify the project's API version and documentation before concluding.

Report findings by severity: **Blocker**, **High**, **Medium**, **Low**. Do not invent issues without evidence from the code or project context.
