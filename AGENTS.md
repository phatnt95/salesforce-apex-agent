# Salesforce Apex Engineering Rules

These rules apply to this Salesforce Apex workspace.

## Core invariants
- Write bulk-safe Apex. Never place SOQL, SOSL, or DML inside loops unless there is a documented and unavoidable reason.
- Treat governor limits as design constraints, not cleanup items.
- Keep triggers thin: orchestration only; business logic belongs in appropriate classes.
- Respect Salesforce security: sharing, CRUD/FLS, user/system mode, and data exposure must be deliberate.
- Do not invent Salesforce object, field, API, or platform behavior. Inspect metadata or official Salesforce documentation when uncertain.
- Prefer platform-native capabilities over custom abstractions when they satisfy the requirement.
- Tests must verify behavior, bulk cases, negative cases, and important security/async paths—not only coverage.
- Avoid hard-coded record IDs, credentials, environment-specific URLs, and other org-specific values.
- Before changing an existing pattern, inspect nearby code and follow established project conventions unless there is a clear reason to improve them.

## Implementation discipline
1. Understand the transaction context and data volume before coding.
2. Identify security context and integration/callout requirements.
3. Reuse existing services/selectors/utilities when appropriate.
4. Make the smallest change that satisfies the requirement.
5. Validate with focused tests and static checks where available.
