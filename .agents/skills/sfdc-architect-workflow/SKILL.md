---
name: sfdc-architect-workflow
description: >-
  Use this skill when acting as the Salesforce Technical Architect
  (sfdc-architect) subagent to analyze existing Salesforce metadata, answer
  technical feasibility questions for the BA, and author a Technical Solution
  Blueprint in docs/architecture/<feature-slug>-blueprint.md.
---

# Salesforce Technical Architect Workflow (`sfdc-architect-workflow`)

Follow this workflow when invoked by the Business Analyst (`BA`) main agent to provide technical guidance or design a Salesforce solution.

## Step 1: Current-State Metadata Discovery
1. Inspect `force-app/main/default/` (`objects/`, `classes/`, `triggers/`, `lwc/`, `aura/`, `flexipages/`, `permissionsets/`, `layouts/`) to identify reusable components, existing schema fields, and naming conventions.
2. Read the BA's functional specification in `docs/specs/<feature-slug>.md` (if already created).

## Step 2: Technical Feasibility & Well-Architected Assessment
Evaluate the business requirements across three pillars:
- **Trusted (Security & Access)**: Which OWD sharing model, `with sharing` enforcement, `WITH USER_MODE` SOQL/DML, and Permission Sets are required?
- **Easy (Declarative vs. Code)**: Can standard Lightning components, Dynamic Forms, or Flows satisfy the requirement, or is custom LWC + Apex required?
- **Adaptable (Performance & Limits)**: How will queries remain selective? Are custom indexes, pagination, or `@AuraEnabled(cacheable=true)` needed?

## Step 3: Author the Technical Solution Blueprint
Write the blueprint to `docs/architecture/<feature-slug>-blueprint.md` following the template in [resources/solution-blueprint-template.md](./resources/solution-blueprint-template.md).

## Step 4: Return Handoff Package to BA
Provide the BA with:
1. Direct answers to any technical questions asked by the BA.
2. Link to `docs/architecture/<feature-slug>-blueprint.md`.
3. A ready-to-use technical scope summary that the BA can forward to `sfdc-dev` for implementation.

