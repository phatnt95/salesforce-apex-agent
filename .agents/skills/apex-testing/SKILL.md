---
name: apex-testing
description: Creates and reviews Salesforce Apex tests, test data factories, bulk tests, negative tests, security tests, asynchronous tests, callout mocks, and behavior-focused test suites. Use when adding or modifying Apex tests or validating production Apex quality.
---

# Apex Testing

## Testing strategy

Test behavior and business outcomes, not just coverage percentage.

Every non-trivial feature should consider:

1. Happy path.
2. Boundary/edge cases.
3. Invalid input.
4. Bulk input.
5. No-data behavior.
6. Permission/security behavior when applicable.
7. Exception/error behavior.
8. Async behavior when applicable.
9. Callout success/failure when applicable.

## Test data

- Prefer isolated test data created by the test or a reusable factory.
- Avoid depending on existing org data unless the platform requires it and the dependency is explicit.
- Make test records minimal but realistic.
- Do not hard-code production IDs.

## Assertions

- Assert meaningful field values, record counts, status transitions, errors, and side effects.
- Avoid tests that only assert no exception was thrown.
- Use `Test.startTest()` / `Test.stopTest()` to isolate governor limits and flush supported async work.
- For bulk logic, test a meaningful multi-record collection rather than only a single record.

## Callouts

Use `HttpCalloutMock` or the appropriate test abstraction. Assert both request/response behavior and resulting Salesforce state.

## Async

For Queueable, Batchable, Scheduled, and future work, verify the observable outcome after `Test.stopTest()` and cover failure paths where practical.

## Quality gate

Before declaring a test complete, ask:
- Would this fail if the business rule broke?
- Does it protect against regression?
- Does it exercise bulk behavior?
- Does it verify important negative/security cases?
- Is it independent of org-specific production data?
