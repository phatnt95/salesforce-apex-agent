---
name: sfdc-dev-workflow
description: >-
  Use this skill when acting as the Salesforce Developer (dev / sfdc-dev)
  subagent to scaffold, implement, format, lint, test Salesforce DX components
  (Apex, LWC, Objects, Triggers, Permission Sets) in force-app/main/default,
  and author best-practice Detailed Design Documentation after implementation.
---

# Salesforce DX Developer Workflow (`sfdc-dev-workflow`)

Follow these procedures when implementing specifications handed off by the BA main agent.

## 1. Project Conventions
- **Package Directory**: `force-app/main/default/`
- **API Version**: `68.0` (configured in [`sfdx-project.json`](../../../sfdx-project.json))
- **Code Formatting**: Prettier with `prettier-plugin-apex` and `@prettier/plugin-xml`
- **Detailed Design Docs Directory**: `docs/design/<feature-slug>-detailed-design.md`

## 2. Scaffolding & Implementation
You can scaffold components using `sf template generate` or create the files directly:
- **Apex Class**:
  `sf template generate class --name <ClassName> --output-dir force-app/main/default/classes`
- **Apex Trigger**:
  `sf template generate trigger --name <TriggerName> --output-dir force-app/main/default/triggers`
- **Lightning Web Component (LWC)**:
  `sf template generate lightning component --type lwc --name <componentName> --output-dir force-app/main/default/lwc`

### Coding Guardrails
- **Apex**:
  - Default to `public with sharing class <Name>`.
  - Enforce user-mode security on SOQL/DML (`WITH USER_MODE` or `Database.insert(..., AccessLevel.USER_MODE)`).
  - Never place SOQL or DML statements inside `for`/`while` loops.
  - Annotate LWC-callable methods with `@AuraEnabled(cacheable=true)` for reads and `@AuraEnabled` for mutations, wrapping unexpected exceptions in `AuraHandledException`.
- **LWC**:
  - Use `lwc:if`, `lwc:elseif`, `lwc:else` directives (never legacy `if:true` / `if:false`).
  - Place unit tests in `force-app/main/default/lwc/<componentName>/__tests__/<componentName>.test.js`.

## 3. Local Verification & Quality Gates
Run these commands before reporting completion to the BA agent:

1. **Format Code & Metadata XML**:
   ```bash
   npm run prettier
   ```
2. **Verify Formatting**:
   ```bash
   npm run prettier:verify
   ```
3. **Lint LWC / Aura JavaScript**:
   ```bash
   npm run lint
   ```
4. **Run LWC Jest Unit Tests**:
   ```bash
   npm run test:unit
   ```

## 4. Mandatory Detailed Design Documentation (Post-Implementation)
After completing code implementation and unit tests, you **MUST** write a comprehensive **Detailed Design Document** in `docs/design/<feature-slug>-detailed-design.md` following the best-practice template in [resources/detailed-design-template.md](./resources/detailed-design-template.md).

### Best Practices Required in Every Detailed Design Document:
1. **Document Overview & Traceability**: Link back to the BA Functional Spec (`docs/specs/<feature-slug>.md`), list API version (`68.0`), and provide an executive summary.
2. **Architecture & Sequence Diagram**: Include a Mermaid `sequenceDiagram` or `flowchart` showing the exact interaction between the User, LWC, Lightning UI API / LDS, Apex Controller, and Database.
3. **Data Model & Schema Design**: Document all standard/custom objects, fields, data types, picklist values, OWD/sharing expectations, and FLS rules.
4. **Backend Design & Governor Limits Analysis**: Document Apex classes, method signatures, exact SOQL queries, selectivity/indexing considerations, bulkification, governor limit consumption table, and exception handling (`AuraHandledException`).
5. **Frontend (LWC) Design**: Document component hierarchy, `@wire` adapters, reactive properties, data transformation logic, SLDS styling, and accessibility (`role="alert"`, `alternative-text`, loading/empty/error states).
6. **Security & Access Control**: Detail record-level security (`with sharing`), object/field-level enforcement (`WITH USER_MODE`), and Permission Set metadata.
7. **Testing & QA Strategy**: Map every Apex unit test method and LWC Jest test case to the BA Acceptance Criteria (`AC-1`, `AC-2`, etc.), covering positive, negative, empty, error, and bulk scenarios.
8. **Deployment & Post-Deployment Runbook**: Provide the complete list of deployable metadata files, `sf project deploy start` CLI commands, and post-deployment configuration steps.

## 5. Reporting Back to BA
Return a concise report containing:
1. Created/updated metadata and code file paths.
2. Path to the generated **Detailed Design Document** (`docs/design/<feature-slug>-detailed-design.md`).
3. How each Acceptance Criterion is satisfied.
4. Exact pass/fail status of `prettier:verify`, `lint`, and `test:unit`.
