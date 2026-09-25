---
trigger: glob
globs: "*Test.cls, **/*Test.cls, **/test/**, **/tests/**"
description: "Apply to Apex unit tests, test factories, mocks, and test data setup."
---
# Apex Testing Rules

- Test observable behavior and business outcomes, not implementation details.
- Use isolated test data; do not depend on existing org records unless a platform feature explicitly requires it.
- Prefer `@TestSetup` for reusable baseline data.
- Every bulk-capable unit should have a bulk test that exercises realistic collection sizes and relationship patterns.
- Cover success, validation/error paths, boundary cases, and important authorization/security behavior.
- Test asynchronous code with `Test.startTest()` / `Test.stopTest()` so queued work executes within the test transaction.
- Use mocks/stubs for external callouts; tests must not make real external HTTP requests.
- Assert meaningful field values, record counts, state transitions, and errors. Avoid assertions that only prove code executed.
- Avoid `SeeAllData=true` unless there is a documented platform-specific reason.
- Keep test factories deterministic and reusable; do not hide critical setup inside opaque helpers.
