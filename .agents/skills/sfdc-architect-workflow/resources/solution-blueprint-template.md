# Technical Solution Blueprint: <Feature Title>

## 1. Architectural Overview
- **Functional Spec Reference**: [`docs/specs/<feature-slug>.md`](../specs/<feature-slug>.md)
- **Architect**: Salesforce Technical Architect Subagent (`sfdc-architect`)
- **Target API Version**: `68.0`
- **Recommended Pattern**: <e.g., Custom LWC + Reactive Wire Service + Cacheable Apex Controller>

### 1.1 Declarative vs. Programmatic Justification
| Requirement Area | Chosen Approach (Declarative / Code) | Architectural Rationale |
| :--- | :--- | :--- |
| Data Storage | Standard/Custom Object & Fields | ... |
| Business Logic / Query | Apex (`with sharing`, `WITH USER_MODE`) | ... |
| User Interface | Lightning Web Component (`lwc`) | ... |
| Access Control | Permission Set | ... |

---

## 2. Proposed Metadata & Component Manifest (`force-app/main/default/`)
| Component Type | API Name | Target Path | Action (Create / Modify) | Technical Specification |
| :--- | :--- | :--- | :--- | :--- |
| Custom Object / Field | `<Object.Field__c>` | `objects/<Object>/fields/<Field__c>.field-meta.xml` | Create | Data type, length/picklist values, FLS |
| Apex Class | `<ControllerName>` | `classes/<ControllerName>.cls` | Create | Method signatures, annotations, sharing, SOQL structure |
| Apex Test Class | `<ControllerNameTest>` | `classes/<ControllerNameTest>.cls` | Create | Required test scenarios & bulk coverage |
| LWC | `<componentName>` | `lwc/<componentName>/` | Create | Targets (`lightning__AppPage`, etc.), wire adapters, columns/events |
| Permission Set | `<PermSet_Name>` | `permissionsets/<PermSet_Name>.permissionset-meta.xml` | Create | Object, field, and class access grants |

---

## 3. Data Model, Security & Sharing Design
- **OWD & Record Visibility**: ...
- **CRUD & FLS Enforcement**: ...
- **SOQL Selectivity & Governor Limits Guardrails**: ...

---

## 4. Implementation Guidelines for `sfdc-dev`
1. Follow `.agents/skills/sfdc-dev-workflow/SKILL.md`.
2. Implement the exact metadata manifest in Section 2.
3. Author unit tests (Apex + LWC Jest) covering all BA Acceptance Criteria (`AC-1..AC-n`).
4. Author the post-implementation Detailed Design Document at `docs/design/<feature-slug>-detailed-design.md`.

