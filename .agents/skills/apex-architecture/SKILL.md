---
name: apex-architecture
description: Designs Salesforce Apex application architecture, including service/domain/selector patterns, transaction boundaries, integration boundaries, dependency management, testability, bulk processing, and trade-offs between declarative and programmatic automation. Use for solution design or when a feature spans multiple Apex classes, objects, triggers, or integrations.
---

# Apex Architecture

## Design workflow

1. Clarify the business invariant and entry points.
2. Identify data ownership and object relationships.
3. Map synchronous vs asynchronous work.
4. Define security boundary.
5. Define transaction and rollback requirements.
6. Choose the smallest architecture that supports reuse and testing.
7. Identify governor-limit and data-volume risks.
8. Define tests and observability before implementation.

## Layering guidance

Use layers only when they provide a concrete benefit.

- Trigger: entry point and context delegation.
- Handler: trigger-context orchestration.
- Domain/service: business rules and use cases.
- Selector/repository: reusable data access.
- Integration client: external communication.
- DTO/wrapper: stable boundary representation.

Avoid a ceremony-heavy framework for simple requirements.

## Transaction design

Ask:
- Must all changes succeed or fail together?
- Can the work be deferred?
- Could another transaction update the same records concurrently?
- Is the operation idempotent?
- What happens when an external system is unavailable?

## Declarative vs Apex

Prefer standard Salesforce configuration when it fully satisfies the requirement and remains maintainable. Use Apex when the requirement needs programmatic complexity, reusable logic, unsupported orchestration, advanced integration, or scale characteristics that configuration cannot safely provide.

## Architecture output

For design requests, provide:
- component diagram in text;
- responsibility of each class;
- data flow;
- transaction boundary;
- security boundary;
- async/integration boundary;
- key trade-offs;
- test strategy.
