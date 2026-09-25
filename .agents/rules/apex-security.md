---
trigger: model_decision
description: "Apply when Apex reads, writes, exposes, or dynamically queries Salesforce data, especially controller, API, service, and integration code."
---
# Apex Security Rules

- Security is part of correctness. Identify the execution mode and sharing behavior before implementation.
- Use `with sharing` or an explicitly justified alternative for classes that operate on user-facing data.
- Enforce CRUD/FLS where required by the execution context and API surface; do not assume object access implies field access.
- Prefer user-mode data operations when they are appropriate to the requirement and supported by the project's API version.
- Do not use system mode as a shortcut to bypass authorization requirements.
- Treat every external/user-provided value as untrusted.
- Dynamic SOQL must bind values and whitelist structural elements such as field names and sort directions.
- Do not expose fields or records merely because the running user can execute the Apex class.
- Avoid logging secrets, tokens, credentials, sensitive payloads, or unnecessary personal data.
- When security behavior depends on Salesforce release/API version, inspect the project's API version before making a definitive claim.
