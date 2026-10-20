---
name: platform-architecture
description: Design modular .NET microservice building blocks, public composition APIs, package boundaries and hosting/runtime conventions; produce alternatives, diagrams and ADR proposals. Use after core constraints are understood or when new capabilities affect the architecture.
---

# Platform architecture

Design for **new service created quickly, transparently and safely**; avoid hiding operational or dependency cost behind a one-line API.

## Procedure
1. Read accepted ADRs, latest discovery constraints and relevant research. Identify the actual developer persona, first reference service and 2–3 top user journeys.
2. Draw **boundaries before namespaces**: Domain primitives, Application/CQRS, Messaging abstractions, Kafka adapter, Persistence/Postgres, gRPC, Observability, Security, Hosting/ServiceDefaults, Template/Tooling, Testing.
3. Build a dependency direction graph; domain should not depend on Kafka, EF, gRPC, Serilog or Platform bootstrap. Keep public abstractions small and optional. Distinguish contracts shared *between* services from platform runtime dependencies.
4. Compare at least two viable macro-architectures, including a lean combination of stock .NET + curated packages. Analyze when ordinary DI extension methods work better than a custom `Platform` builder.
5. Present **DX sketches** for HTTP, Kafka worker, gRPC and hybrid services. Use **illustrative** C# with correct intent; label signatures as proposals unless verified. Show service opt-in/opt-out and explicit options/configuration.
6. Trace critical flows: request → handler → domain event → DB commit → outbox → Kafka publish → consumer → inbox/idempotent side effect. Trace separate gRPC path. Highlight failed steps, retries and transactions.
7. Propose package matrix (purpose, API, dependency direction, mandatory/optional, runtime ownership), and distinguish code package vs template vs Aspire/local AppHost/deployment recipe.
8. Apply `references/capability-checklist.md`, run `$architecture-review` on nontrivial decisions and log **proposed** ADRs. Update `docs/architecture/platform-map.md` and state file.

## Principles
- Prefer hosting integration via existing .NET contracts; avoid global statics/service locator and magic scan behavior unless justified.
- Packages should not require the whole platform. Don't couple database to Kafka by default or enforce CQRS/DDD for small read-only services.
- Configuration should be discoverable, validated, secure by default and overrideable, with reasonable ordering/duplicate-registration behavior.
- Public API, semantic versioning and migration/deprecation are product features; stable conventions matter more than terse syntax.
- Keep guarantees honest: Kafka ordering within partition only, delivery semantics depend on system design, consumer commits and business effect are distinct.
