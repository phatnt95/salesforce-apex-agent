---
name: apex-trigger
description: Builds and reviews Salesforce Apex triggers and trigger frameworks, including bulk processing, handler/service separation, recursion control, order-of-execution effects, and trigger-to-domain orchestration. Use when creating or modifying triggers or automation initiated by DML.
---

# Apex Trigger

## Preferred structure

Use a thin trigger that delegates to a handler/service/domain layer. Keep business rules out of the trigger body.

Typical flow:

`Trigger -> Handler -> Domain/Service -> Selector/Repository -> DML`

Do not introduce every layer automatically. Use the smallest structure that keeps responsibilities clear.

## Decision tree

- One simple invariant with no reuse -> a small handler may be enough.
- Multiple business rules or reusable operations -> service/domain layer.
- Complex read patterns -> selector/data-access layer.
- Cross-object side effects -> explicit service orchestration and transaction analysis.
- External callout required -> do not call out directly from a normal synchronous trigger; choose an async/event-based design where appropriate.

## Trigger rules

- Assume `Trigger.new` contains multiple records.
- Handle insert, update, delete, undelete contexts explicitly.
- Use `Trigger.oldMap`/`Trigger.newMap` for change detection.
- Avoid SOQL/DML inside loops.
- Avoid recursive updates and explain any intentional re-entry behavior.
- Do not assume a particular order between independent automation mechanisms unless documented and guaranteed.
- Preserve transaction atomicity unless partial success is an explicit requirement.

## Before-save vs after-save

Choose based on whether the logic needs to modify fields on the same records before persistence or needs record IDs / related-record side effects after persistence. Explain the reason when the distinction matters.

## Review checklist

- Bulk behavior with 200 records.
- Recursion/cascade behavior.
- Order-of-execution assumptions.
- Query/DML limits.
- Cross-object update volume.
- Security context of called classes.
- Async boundaries for callouts/heavy work.
- Test coverage for every trigger context and meaningful branch.
