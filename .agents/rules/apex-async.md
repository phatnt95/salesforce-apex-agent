---
trigger: model_decision
description: "Apply when implementing Queueable, Batchable, Schedulable, future methods, platform-event processing, callouts, retries, or other asynchronous Apex."
---
# Apex Async and Integration Rules

- Choose the smallest async mechanism that satisfies the requirement.
- Use Queueable for discrete asynchronous jobs and job chaining; use Batch for genuinely large datasets; use Scheduled only for time-based execution.
- Do not use asynchronous Apex merely to hide poor bulkification or governor-limit design.
- Callouts must use an appropriate callout-capable execution context and secure credential configuration.
- Prefer Named Credentials/External Credentials over hard-coded endpoints, usernames, passwords, or tokens.
- Make retry behavior explicit. Do not create uncontrolled retry loops or duplicate side effects.
- Design integration operations for idempotency where retries or duplicate delivery are possible.
- Persist enough diagnostic context to troubleshoot failures without logging secrets or sensitive payloads.
- Consider transaction boundaries carefully: database changes before an async enqueue are not automatically part of the later transaction.
- Test both successful and failed async/integration paths.
