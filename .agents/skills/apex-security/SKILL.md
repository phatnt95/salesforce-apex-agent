---
name: apex-security
description: Designs and reviews Salesforce Apex data access security, including sharing, user/system mode, CRUD/FLS, secure SOQL/DML, dynamic queries, callout credentials, and prevention of unauthorized data exposure. Use when Apex accesses user data, performs privileged operations, exposes APIs, or handles security-sensitive records.
---

# Apex Security

## Security-first workflow

1. Identify who invokes the code.
2. Identify which records the caller should be able to see/change.
3. Identify object and field permissions.
4. Identify whether the operation intentionally requires elevated privileges.
5. Choose sharing and data-access mode explicitly.
6. Test both authorized and unauthorized cases.

## Rules

- Do not assume Apex execution context automatically matches the user's intended permissions.
- Prefer least privilege.
- Use sharing keywords and data-access modes deliberately; do not add `without sharing` as a convenience.
- For user-facing data access, enforce object/field permissions and sharing according to the requirement.
- For privileged service operations, document why elevated access is necessary and keep the privileged boundary narrow.
- Dynamic SOQL must bind values and validate any structural tokens.
- Never expose secrets, access tokens, passwords, or credentials in logs, exceptions, test data, or source control.
- Prefer Named Credentials / External Credentials for callout authentication rather than hard-coded secrets.

## Version awareness

Salesforce security behavior evolves by API version. For new code, check the target API version before making claims about defaults or supported security clauses. Do not blindly apply legacy patterns to a newer API version.

## Security review checklist

- Sharing model.
- Object CRUD.
- Field-level security.
- User vs system mode.
- Dynamic SOQL injection.
- Sensitive-field exposure.
- Guest/portal/community access.
- Callout credential handling.
- Error-message leakage.
- Tests proving both allowed and denied access.
