# Salesforce Apex Antigravity Rules

A focused Rules pack for Salesforce Apex projects using Google Antigravity.

Antigravity Rules are persistent constraints and architectural invariants, while Skills are reusable multi-step workflows/knowledge packages. Keep broad invariants here and keep procedural guidance in `.agents/skills`. See the official Rules documentation for activation and precedence.

## Included rules

- `AGENTS.md` — compact workspace-wide Apex invariants; always active.
- `apex-soql-dml.md` — SOQL/SOSL/DML and data-access constraints; model decision.
- `apex-trigger.md` — trigger-specific constraints; glob activated.
- `apex-security.md` — Apex security constraints; model decision.
- `apex-testing.md` — test-file constraints; glob activated.
- `apex-async.md` — async Apex and integration constraints; model decision.
- `apex-code-style.md` — source formatting/readability constraints; glob activated.
- `apex-architecture.md` — architecture constraints; model decision.
- `apex-review.md` — explicit pre-merge review checklist; manual activation.

## Installation

Copy `.agents/rules/` and `AGENTS.md` to the Salesforce project root.

Recommended combined structure:

```text
.salesforce-project/
├── AGENTS.md
└── .agents/
    ├── rules/
    │   ├── apex-soql-dml.md
    │   ├── apex-trigger.md
    │   ├── apex-security.md
    │   ├── apex-testing.md
    │   ├── apex-async.md
    │   ├── apex-code-style.md
    │   ├── apex-architecture.md
    │   └── apex-review.md
    └── skills/
        └── ... existing Salesforce Apex skills ...
```

## Design choice

Use `always_on` only for short invariants in `AGENTS.md`. Use `model_decision` for detailed domain constraints, `glob` for file-specific rules, and `manual` for deliberate audit/checklist activation. This keeps the persistent prompt small while preserving progressive disclosure.

The rules are intentionally complementary to the Apex Skills pack rather than duplicating its workflows.
