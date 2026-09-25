---
name: apex-async-integration
description: Designs Salesforce Apex asynchronous processing and integrations using Queueable, Batchable, Schedulable, future methods, platform events, HTTP callouts, Named Credentials, retries, and failure handling. Use when Apex must perform callouts, heavy processing, scheduled work, or operations beyond one synchronous transaction.
---

# Apex Async & Integration

## Decision tree

- Small deferred unit of work -> Queueable.
- Very large data set -> Batch Apex or an external bulk-processing mechanism.
- Time-based execution -> Schedulable, usually delegating to Queueable/Batch.
- Legacy/simple async requirement -> `@future` only when its constraints fit; do not introduce it by default.
- Event-driven decoupling -> Platform Events / Change Data Capture when appropriate.
- External HTTP callout -> Named Credential / External Credential plus an async boundary if the invocation context cannot perform a callout.

## Queueable

- Pass only serializable, bounded state.
- Avoid chaining indefinitely.
- Design idempotency when retries or duplicate execution are possible.
- Make failure handling observable.

## Batch

- Choose batch size deliberately based on query shape and per-record work.
- Keep each execute scope independently safe.
- Avoid stateful mode unless accumulated state is necessary.
- Make finish behavior explicit.

## Callouts

- Use Named Credentials/External Credentials for authentication.
- Set timeouts deliberately.
- Validate response status and payload.
- Avoid logging secrets or sensitive payloads.
- Define retry policy only for transient failures; do not blindly retry permanent validation/authentication failures.
- Design idempotency for operations that can be retried.

## Failure model

Document:
- transient vs permanent errors;
- retry count/backoff;
- dead-letter/manual recovery path;
- transaction rollback behavior;
- user-visible status;
- monitoring/logging.
