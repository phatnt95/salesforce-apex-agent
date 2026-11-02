# Salesforce Apex & Multi-Agent Antigravity Pack

A comprehensive **Rules, Skills, and Multi-Agent Orchestration pack** for Salesforce DX (Apex & LWC) projects built on the **Google Antigravity Customization System**.

Antigravity **Rules** define persistent constraints, role boundaries, and architectural invariants, while **Skills** provide reusable multi-step workflows, domain expertise, and documentation templates.

---

## Multi-Agent Team Architecture

Configured in [`AGENTS.md`](AGENTS.md), this pack establishes a 3-role multi-agent workflow:

1. **Main Agent — Pure Business Analyst (`BA`)**:
   - Focuses strictly on CRM business processes, user personas, business rules, User Stories, and functional Acceptance Criteria (`Given / When / Then`).
   - Authors functional specifications in `docs/specs/<feature-slug>.md` using [`ba-spec-workflow`](.agents/skills/ba-spec-workflow/SKILL.md).
2. **Subagent — Salesforce Technical Architect (`sfdc-architect`)**:
   - Defined in [`.agents/agents/sfdc-architect.md`](.agents/agents/sfdc-architect.md).
   - Inspects existing Salesforce metadata, evaluates technical feasibility across Salesforce Well-Architected pillars (Trusted, Easy, Adaptable), and authors Technical Solution Blueprints in `docs/architecture/<feature-slug>-blueprint.md` using [`sfdc-architect-workflow`](.agents/skills/sfdc-architect-workflow/SKILL.md).
3. **Subagent — Salesforce Developer (`sfdc-dev`)**:
   - Defined in [`.agents/agents/sfdc-dev.md`](.agents/agents/sfdc-dev.md).
   - Implements Apex, LWC, Triggers, Objects, and Permission Sets in `force-app/main/default/`, runs local verification (`prettier`, `lint`, `test:unit`), and authors post-implementation Detailed Design Documentation in `docs/design/<feature-slug>-detailed-design.md` using [`sfdc-dev-workflow`](.agents/skills/sfdc-dev-workflow/SKILL.md).

---

## Project Structure

```text
salesforce-apex-agent/
├── AGENTS.md                                              # Multi-agent team orchestration (BA, Architect, Dev)
├── LICENSE
├── README.md
└── .agents/
    ├── agents/                                            # Workspace subagent definitions
    │   ├── sfdc-architect.md                              # Salesforce Technical Architect subagent
    │   └── sfdc-dev.md                                    # Salesforce LWC & Apex Developer subagent
    ├── rules/                                             # Persistent & conditional Apex guardrails
    │   ├── apex-architecture.md                           # Architecture constraints (model decision)
    │   ├── apex-async.md                                  # Async Apex & integration constraints (model decision)
    │   ├── apex-code-style.md                             # Source formatting & readability constraints (glob)
    │   ├── apex-review.md                                 # Explicit pre-merge review checklist (manual)
    │   ├── apex-security.md                               # Sharing, CRUD/FLS & user-mode security (model decision)
    │   ├── apex-soql-dml.md                               # SOQL/SOSL/DML & data-access constraints (model decision)
    │   ├── apex-testing.md                                # Test-file constraints (glob)
    │   └── apex-trigger.md                                # Trigger-specific constraints (glob)
    └── skills/                                            # Reusable workflows, domain knowledge & templates
        ├── apex-architecture/
        │   └── SKILL.md                                   # Service/domain/selector patterns & transaction design
        ├── apex-async-integration/
        │   └── SKILL.md                                   # Queueable, Batchable, Schedulable, Events & Callouts
        ├── apex-code-review/
        │   └── SKILL.md                                   # Governor limits, security, bulkification & quality review
        ├── apex-core/
        │   └── SKILL.md                                   # Core Apex conventions, DTOs, exceptions & refactoring
        ├── apex-security/
        │   └── SKILL.md                                   # User/system mode, sharing, CRUD/FLS & secure SOQL/DML
        ├── apex-soql-dml/
        │   └── SKILL.md                                   # Selective SOQL, SOSL, bulk DML & dynamic queries
        ├── apex-testing/
        │   └── SKILL.md                                   # Bulk tests, test factories, mocks & assertions
        ├── apex-trigger/
        │   └── SKILL.md                                   # Trigger frameworks, recursion control & handler separation
        ├── ba-spec-workflow/
        │   ├── SKILL.md                                   # BA requirement elicitation & orchestration workflow
        │   └── resources/
        │       └── user-story-template.md                 # Functional specification template (docs/specs/)
        ├── sfdc-architect-workflow/
        │   ├── SKILL.md                                   # Technical discovery & blueprint design workflow
        │   └── resources/
        │       └── solution-blueprint-template.md         # Technical blueprint template (docs/architecture/)
        └── sfdc-dev-workflow/
            ├── SKILL.md                                   # SFDX implementation, verification & documentation workflow
            └── resources/
                └── detailed-design-template.md            # Post-implementation design template (docs/design/)
```

---

## Included Rules (`.agents/rules/`)

| Rule File | Activation | Scope |
| :--- | :--- | :--- |
| [`AGENTS.md`](AGENTS.md) | Always active | 3-role multi-agent boundaries (`BA`, `sfdc-architect`, `sfdc-dev`) & delegation protocol |
| [`apex-architecture.md`](.agents/rules/apex-architecture.md) | Model decision | Service layers, selectors, domain logic, and transaction boundaries |
| [`apex-async.md`](.agents/rules/apex-async.md) | Model decision | Queueable, Batchable, Schedulable, future methods, platform events, and callouts |
| [`apex-code-style.md`](.agents/rules/apex-code-style.md) | Glob (`**/*.cls`, `**/*.trigger`) | Naming conventions, formatting, and readability constraints |
| [`apex-review.md`](.agents/rules/apex-review.md) | Manual | Explicit pre-merge Apex code review checklist |
| [`apex-security.md`](.agents/rules/apex-security.md) | Model decision | Sharing (`with sharing`), `WITH USER_MODE`, `AccessLevel.USER_MODE`, and CRUD/FLS |
| [`apex-soql-dml.md`](.agents/rules/apex-soql-dml.md) | Model decision | Bulkified SOQL/SOSL/DML, selectivity, and dynamic query safety |
| [`apex-testing.md`](.agents/rules/apex-testing.md) | Glob (`**/*Test*.cls`) | Test isolation, assertions, bulk testing, and test data practices |
| [`apex-trigger.md`](.agents/rules/apex-trigger.md) | Glob (`**/*.trigger`) | One trigger per object, logicless triggers, and bulk handler routing |

---

## Included Skills (`.agents/skills/`)

### Role & Delivery Workflow Skills
- **[`ba-spec-workflow`](.agents/skills/ba-spec-workflow/SKILL.md)** — Elicits business requirements, writes functional User Stories (`docs/specs/<feature-slug>.md`) from [`user-story-template.md`](.agents/skills/ba-spec-workflow/resources/user-story-template.md), coordinates with `sfdc-architect` and `sfdc-dev`, and conducts acceptance sign-off.
- **[`sfdc-architect-workflow`](.agents/skills/sfdc-architect-workflow/SKILL.md)** — Inspects `force-app/main/default/`, evaluates Well-Architected trade-offs, and produces Technical Solution Blueprints (`docs/architecture/<feature-slug>-blueprint.md`) from [`solution-blueprint-template.md`](.agents/skills/sfdc-architect-workflow/resources/solution-blueprint-template.md).
- **[`sfdc-dev-workflow`](.agents/skills/sfdc-dev-workflow/SKILL.md)** — Scaffolds and implements SFDX metadata, runs Prettier/ESLint/Jest quality gates, and authors Detailed Design Documents (`docs/design/<feature-slug>-detailed-design.md`) from [`detailed-design-template.md`](.agents/skills/sfdc-dev-workflow/resources/detailed-design-template.md).

### Apex Technical Domain Skills
- **[`apex-architecture`](.agents/skills/apex-architecture/SKILL.md)** — Service/domain/selector layering, transaction boundaries, and declarative vs. programmatic trade-offs.
- **[`apex-async-integration`](.agents/skills/apex-async-integration/SKILL.md)** — Async Apex patterns (`Queueable`, `Batchable`, `Schedulable`), Platform Events, Named Credentials, and callout resilience.
- **[`apex-code-review`](.agents/skills/apex-code-review/SKILL.md)** — Comprehensive code review procedure for governor limits, security, bulkification, and maintainability.
- **[`apex-core`](.agents/skills/apex-core/SKILL.md)** — Platform-aware Apex coding conventions, DTOs, enums, exception handling, and refactoring.
- **[`apex-security`](.agents/skills/apex-security/SKILL.md)** — Data access security, sharing modes, CRUD/FLS enforcement, and injection prevention.
- **[`apex-soql-dml`](.agents/skills/apex-soql-dml/SKILL.md)** — Query selectivity, bulk DML, `Database` methods, and safe dynamic SOQL.
- **[`apex-testing`](.agents/skills/apex-testing/SKILL.md)** — Behavior-focused unit tests, test data factories, bulk/negative/permissions testing, and callout mocks.
- **[`apex-trigger`](.agents/skills/apex-trigger/SKILL.md)** — Trigger handler orchestration, recursion guards, and order-of-execution safety.

---

## Installation in a Target Salesforce Project

Copy [`AGENTS.md`](AGENTS.md) and the `.agents/` directory into the root of your Salesforce DX project:

```text
<your-salesforce-project>/
├── AGENTS.md
├── sfdx-project.json
├── package.json
├── .agents/
│   ├── agents/
│   │   ├── sfdc-architect.md          # Salesforce Technical Architect subagent
│   │   └── sfdc-dev.md                # Salesforce LWC & Apex Developer subagent
│   ├── rules/
│   │   └── ... (8 Apex rule files)
│   └── skills/
│       └── ... (3 role workflow skills + 8 Apex domain skills)
├── docs/
│   ├── specs/                         # Functional Specs authored by BA
│   ├── architecture/                  # Solution Blueprints authored by sfdc-architect
│   └── design/                        # Detailed Design Docs authored by sfdc-dev
└── force-app/
    └── main/
        └── default/                   # Salesforce DX metadata (classes, lwc, triggers, objects, etc.)
```

## Design Principles

- **Progressive Disclosure**: Keep `always_on` instructions in [`AGENTS.md`](AGENTS.md) focused on role orchestration, use `model_decision` and `glob` for contextual rules, and load detailed procedural steps and templates on demand via `.agents/skills/`.
- **Separation of Concerns**: Strict separation between business specification (`BA`), technical architecture (`sfdc-architect`), and code implementation (`sfdc-dev`) ensures traceable documentation across `docs/specs/`, `docs/architecture/`, and `docs/design/`.

