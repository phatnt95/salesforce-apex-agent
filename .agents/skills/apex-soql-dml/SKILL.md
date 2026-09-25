---
name: apex-soql-dml
description: Designs and reviews Salesforce SOQL, SOSL, DML, Database methods, selectors, dynamic SOQL, and bulk data access. Use when queries, inserts/updates/deletes/upserts, query performance, bulkification, or dynamic filtering are central to the task.
---

# SOQL / DML

## Decision tree

- Need one known object and predictable fields -> static SOQL.
- Need multiple optional filters/fields -> dynamic SOQL, but bind values and validate structural inputs.
- Need partial success -> `Database.*` methods with `allOrNone=false` where appropriate.
- Need atomic behavior -> normal DML or `allOrNone=true` deliberately.
- Need cross-object data -> prefer relationship queries where they reduce query count and preserve clarity.
- Need very large data volume -> reconsider synchronous Apex; evaluate Batch Apex, Bulk API, Async SOQL, or another platform-native option.

## Query rules

- Select only fields actually needed.
- Filter in SOQL rather than querying broad data and filtering in Apex.
- Use `Set<Id>` or other sets for `IN` filters.
- Never concatenate untrusted values into dynamic SOQL.
- Use bind variables for values.
- Whitelist dynamic field names, sort fields, operators, and object names before interpolation.
- Consider selective filters and query-plan implications for high-volume objects.
- Avoid repeated queries for the same data; load once into a map keyed by the required relationship/key.

## DML rules

- Collect records and perform DML outside loops.
- Choose atomic vs partial-success semantics intentionally.
- When using `Database.SaveResult`, map failures back to the originating records.
- For upsert, make the external-ID and duplicate behavior explicit.
- Do not rely on record ordering after DML unless the contract guarantees it.

## Review checklist

1. Query count.
2. Rows returned.
3. DML statement count.
4. DML row count.
5. Selectivity/data volume.
6. Partial-success behavior.
7. Security mode and field visibility.
8. Dynamic query injection risk.
9. Transaction consistency.
