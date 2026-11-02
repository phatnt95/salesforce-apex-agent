# Functional Specification: <Feature Title>

## 1. User Story
- **As a** <Business Persona / Role>
- **I want to** <Business Action / Capability>
- **So that** <Business Value / CRM Outcome>

## 2. Business Rules & Domain Logic
- **Rule 1**: <Describe business criteria in plain functional language>
- **Rule 2**: <Describe filtering, sorting, or validation behavior>
- **Access & Visibility**: <Which business roles should have access and what records should they see?>

## 3. Functional UI / UX Requirements
- **Placement**: <e.g., Sales Lightning App Page / Account Record Page>
- **User Controls / Inputs**: <e.g., Industry dropdown filter with "All Industries" default>
- **Displayed Information**:
  1. <Field / Column 1 — business description & click behavior>
  2. <Field / Column 2 — business description & format>

## 4. Acceptance Criteria (Given / When / Then)
1. **AC-1 (<Primary Business Scenario>)**:
   - **Given** <Business Precondition>
   - **When** <User Action>
   - **Then** <Expected Functional Outcome>
2. **AC-2 (<Filter / Interaction Scenario>)**:
   - **Given** <Business Precondition>
   - **When** <User Action>
   - **Then** <Expected Functional Outcome>
3. **AC-3 (<Empty / Edge Case Scenario>)**:
   - **Given** <No matching records exist>
   - **When** <User views or filters the screen>
   - **Then** <Expected user-friendly message>
4. **AC-4 (<Error / Permission Scenario>)**:
   - **Given** <System or permission error occurs>
   - **When** <Data cannot be loaded>
   - **Then** <Expected clear error notification>

## 5. Open Technical Questions for `sfdc-architect`
- <List any technical feasibility, data model, or architecture questions to be answered in `docs/architecture/<feature-slug>-blueprint.md`>
