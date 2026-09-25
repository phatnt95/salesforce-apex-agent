---
trigger: model_decision
description: "Apply when writing or reviewing SOQL, SOSL, DML, selectors, repositories, dynamic queries, or data-access logic in Apex."
---
# Apex SOQL/DML Rules

- Bulkify every data-access operation.
- Query records once per logical dataset; collect IDs/keys first, then query using sets/maps.
- Never put SOQL, SOSL, or DML inside a loop in normal application code.
- Select only fields required by the operation. Avoid broad field selection patterns.
- Prefer static SOQL when query structure is known at compile time.
- For dynamic SOQL, bind values rather than concatenating user-controlled values. Whitelist object names, field names, sort fields, and operators when they must be dynamic.
- Use collections and maps to avoid repeated lookups and N+1 queries.
- Choose Database methods with explicit `allOrNone` behavior when partial success is required.
- Handle `SaveResult`/query results intentionally; do not silently swallow failures.
- Consider row locking only when concurrent updates can cause a real consistency problem; document why `FOR UPDATE` is needed.
- Keep selector/data-access classes focused on retrieval. Do not hide unrelated business behavior inside selectors.
- Preserve sharing/security expectations of the calling layer.
