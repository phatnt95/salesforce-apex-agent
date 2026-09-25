---
trigger: model_decision
description: "Apply when designing Apex classes, service layers, selectors, domain logic, transaction boundaries, or larger Salesforce application architecture."
---
# Apex Architecture Rules

- Start from the use case and transaction boundary, not from a preferred framework.
- Keep orchestration, business rules, data access, and integration concerns separable when complexity warrants it.
- Prefer existing project architecture over introducing a second competing pattern.
- Use Service/Domain/Selector-style separation only where it provides meaningful reuse, testability, or complexity control.
- Keep transaction boundaries explicit. A service should make clear what is committed together and what is delegated asynchronously.
- Avoid circular dependencies between services, selectors, domains, and utilities.
- Prefer dependency injection for meaningful external dependencies or complex collaborators; do not build an elaborate DI framework for simple code.
- Favor platform-native Flow, validation rules, approval/process capabilities, platform events, or declarative configuration when they are a better fit and the requirement does not demand Apex.
- When choosing Apex over declarative automation, document the material reason: complexity, transaction behavior, scale, integration, reuse, or platform limitation.
- Architecture decisions must account for governor limits, sharing/security, bulk behavior, deployment/version constraints, and testability.
