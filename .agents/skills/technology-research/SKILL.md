---
name: technology-research
description: Research and compare current .NET libraries, microservice infrastructure approaches and best practices with primary-source evidence, build-vs-buy analysis and a reproducible recommendation. Use before adopting or reinventing Kafka, CQRS, gRPC, data access, observability or hosting capabilities.
---

# Technology research

**Outcome:** an evidence-backed choice or clearly documented uncertainty.

1. Clarify evaluation criteria derived from actual requirements, e.g. maintenance, license, security, support, platform version, throughput, ergonomics, lock-in, extensibility and migration.
2. Evaluate at minimum: **native framework mechanism**, **existing maintained library/ecosystem**, **our custom wrapper/implementation**, and **do nothing for MVP**, when applicable.
3. Consult official product and .NET docs, standards, source code, issue/release history, package metadata and licenses. For time-sensitive facts, verify today's version and date explicitly. Use community opinions only as secondary evidence.
4. Prefer testing a risky unknown with a small time-boxed spike *only after the user authorizes executable prototyping*. During documentation-only mode, write a proposed spike and what evidence it would gather.
5. Describe differences across semantics and operational guarantees; never assert that a feature works in production just because an abstraction exposes a method.
6. Record findings in `docs/research/<topic>.md` according to `references/research-template.md`. Link the report from `docs/research/README.md` and summarize in `docs/PROJECT_STATE.md`.
7. If the trade-off requires a lasting decision, create a **proposed** ADR with `$platform-architecture` or `$architecture-review`; ask for approval.

## Initial research candidates (not predetermined selections)
- Host bootstrap using `WebApplicationBuilder` vs `HostApplicationBuilder`, `IServiceCollection` extensions, builder composition and Aspire Service Defaults/AppHost.
- Kafka: Confluent.Kafka as a primitive vs higher-level libraries such as MassTransit/Wolverine (verify current capabilities, licenses and guarantees) vs custom hosted consumer; outbox/inbox mechanics.
- CQRS mediator: built-in dispatch vs maintained third-party mediator vs minimal proprietary interfaces; behaviors, pipeline ordering, licensing and DI boundaries.
- Database: Npgsql, EF Core, Dapper, transaction/migrations policies, repository/UoW only where beneficial.
- Telemetry: OpenTelemetry + OTLP and Serilog as optional logging adapter, no redundant competing tracing APIs.
- gRPC: ASP.NET Core gRPC/client factory/interceptors/deadlines/health/auth and compatibility story.

## Output style
Make explicit: **facts with sources**, **reasoned judgment**, **unknowns**, **comparative matrix**, **recommendation with conditions**, **cost of switching later**, and **follow-up verification**. Cite primary URLs and access dates in research files; don't cite a vague memory of the ecosystem.
