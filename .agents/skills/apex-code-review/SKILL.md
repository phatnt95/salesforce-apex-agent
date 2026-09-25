---
name: apex-code-review
description: Reviews Salesforce Apex for correctness, governor limits, security, bulkification, performance, maintainability, test quality, and architectural risks. Use for code reviews, pull requests, generated Apex validation, refactoring assessments, and pre-deployment checks.
---

# Apex Code Review

Review in this order:

## 1. Correctness

- Does the code satisfy the stated requirement?
- Are null, empty, duplicate, and boundary cases handled?
- Are trigger contexts and transaction behavior correct?

## 2. Governor limits / scale

- SOQL in loops?
- DML in loops?
- Unbounded queries?
- Excessive heap/CPU/string processing?
- Async work created per record unnecessarily?
- Will it work for a bulk transaction?

## 3. Security

- Sharing mode appropriate?
- CRUD/FLS/data-access mode appropriate?
- Dynamic query safe?
- Sensitive fields exposed?
- Credentials/secrets protected?

## 4. Architecture

- Is responsibility in the right layer?
- Is trigger logic thin?
- Are transaction boundaries explicit?
- Is an async boundary needed?
- Is the abstraction justified?

## 5. Tests

- Happy path?
- Negative path?
- Bulk path?
- Security path?
- Async/callout path?
- Assertions meaningful?

## Severity

Classify findings as:

- **Blocker** — correctness, security, data loss, or guaranteed runtime failure.
- **High** — likely production failure, limit risk, or major maintainability issue.
- **Medium** — meaningful design/performance/test gap.
- **Low** — readability or minor consistency improvement.

Do not invent issues. If behavior depends on org metadata or API version, state that dependency.
