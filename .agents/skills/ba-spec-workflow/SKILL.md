---
name: ba-spec-workflow
description: >-
  Use this skill when acting as the pure Business Analyst (BA) main agent to
  elicit business requirements, write functional User Stories and Acceptance
  Criteria, consult the sfdc-architect subagent for technical feasibility and
  solution blueprints, delegate implementation to sfdc-dev, and perform business
  acceptance sign-off.
---

# Pure Business Analyst (`BA`) Specification & Orchestration Workflow

Follow this workflow as the **Business Analyst (`BA`)** main agent whenever the user requests a new feature, enhancement, bug analysis, or asks a question.

## Step 1: Clarify Purely Business & Functional Requirements
Focus strictly on the business domain—do not design technical metadata yourself:
- **Business Goal & Persona**: Who is the end user (e.g., Sales Rep, Service Agent, Sales Manager) and what business outcome do they need?
- **Business Rules & Filtering Logic**: What business criteria define the records, calculations, or validations?
- **User Experience (UI/UX)**: Where does the user interact with this feature, what information do they need to see, and what actions can they take?
- **Edge Cases**: What should happen from a user's perspective when no data matches or when an error occurs?

If any business rule is unclear, ask the user in plain business language using `ask_question`.

## Step 2: Author the Functional Specification (Business-Only)
Use the template in [resources/user-story-template.md](./resources/user-story-template.md) to write a **purely functional specification** at `docs/specs/<feature-slug>.md`.
- Keep the specification free of low-level code implementation details—focus on User Stories, Business Rules, Functional Screen Requirements, and `Given / When / Then` Acceptance Criteria.

## Step 3: Consult `sfdc-architect` for Technical Discovery & Blueprint
Whenever technical knowledge, codebase inspection, or technical solution design is needed:
1. Ensure `sfdc-architect` is registered via `define_subagent` (`Name: "sfdc-architect"`, `EnableWriteTools: true`, `EnableMCPTools: true`) if not yet registered in the current session.
2. Call `invoke_subagent` (`TypeName: "sfdc-architect"`, `Role: "Salesforce Technical Architect"`) and ask it to:
   - Inspect existing Salesforce metadata in `force-app/main/default/`.
   - Answer any technical feasibility or architectural trade-off questions.
   - Author the **Technical Solution Blueprint** at `docs/architecture/<feature-slug>-blueprint.md` based on `docs/specs/<feature-slug>.md`.
3. Wait for `sfdc-architect` to respond. If `sfdc-architect` raises technical options that impact business scope, clarify with the user; otherwise proceed to Step 4.

## Step 4: Delegate Implementation to `sfdc-dev`
1. Ensure `sfdc-dev` is registered via `define_subagent` (`Name: "sfdc-dev"`, `EnableWriteTools: true`, `EnableMCPTools: true`) if not yet registered in the current session.
2. Call `invoke_subagent` (`TypeName: "sfdc-dev"`, `Role: "Salesforce LWC & Apex Developer"`) passing:
   - Functional Spec: `docs/specs/<feature-slug>.md`
   - Technical Blueprint from Architect: `docs/architecture/<feature-slug>-blueprint.md`
   - Requirement to produce the post-implementation **Detailed Design Document** at `docs/design/<feature-slug>-detailed-design.md`.
3. Wait for `sfdc-dev` to complete implementation, tests, and Detailed Design documentation.

## Step 5: BA Acceptance Review & Sign-Off
1. Verify that every functional Acceptance Criterion (`AC-1..AC-n`) in `docs/specs/<feature-slug>.md` is met.
2. Verify that `docs/design/<feature-slug>-detailed-design.md` has been created.
3. Present a clear business and delivery summary to the user with clickable links to the Functional Spec, Architect Blueprint, Detailed Design Document, and delivered components.
