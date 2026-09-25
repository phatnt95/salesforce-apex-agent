---
trigger: glob
globs: "*.trigger, **/*.trigger, *Trigger*.cls, **/*Trigger*.cls"
description: "Apply to Salesforce trigger and trigger-handler changes."
---
# Trigger Rules

- One trigger per object per project unless the existing architecture explicitly requires otherwise.
- Keep the trigger thin. It should delegate to a handler/service layer.
- Do not put business rules, SOQL, or DML directly in the trigger.
- Handle all trigger contexts explicitly: before/after and insert/update/delete/undelete as applicable.
- Always design for 1..200 records and bulk execution.
- Never assume trigger order across automation mechanisms.
- Avoid static Boolean recursion guards that incorrectly skip records in bulk or multi-transaction scenarios. Prefer a context-aware recursion strategy.
- Do not perform callouts directly from a trigger. Enqueue appropriate asynchronous work when a callout is required.
- Be conscious of Salesforce order of execution and downstream automation.
- Keep handler methods small and intention-revealing.
