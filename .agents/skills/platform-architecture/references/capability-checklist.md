# Capability map for architecture exploration

Do **not** blindly implement all of these. For each assign: `Must / Later / Optional / Not needed`; `build / wrap / reuse / defer`; owner; operational cost; service opt-in.

## Foundation & developer experience
- Host/runtime conventions, DI registration, options/config validation, secrets and environment profiles.
- NuGet package boundaries, dependency injection conventions, source-compatible changes, semantic versions, templates, sample services and documentation.
- Local developer environment, Docker/Compose/Aspire AppHost comparison, CI/testing workflows, migration from bare ASP.NET Core, dependency updates.

## Domain / Application
- `Entity<TId>`, `AggregateRoot<TId>`, `ValueObject`/records, strongly typed IDs, domain exceptions, domain event recording/dispatch timing.
- Commands, queries, typed results, cancellation, handler pipeline, validation, transactions, unit of work when justified, authorization boundaries.
- Domain Events vs Integration Events vs DTOs vs Kafka envelope; explicit conversion between business fact and published contract.
- Simpler service mode without aggregates or CQRS; no universal base repository by assumption.

## Kafka / integration messaging
- Producer lifetime, serializers/schema evolution, topic naming/provisioning ownership, headers, trace/context propagation, keys and partitions.
- Consumer groups/partition ownership, backpressure, concurrency, ordering, commit strategy, rebalances, controlled shutdown/restart.
- Retries with classified transient/permanent failures, exponential backoff/jitter, DLQ/quarantine, replay/poison handling, duplicate side effects, idempotency and inbox.
- Outbox consistency with PostgreSQL transaction, eventual delivery, publisher worker, backlog alerts, outbox cleanup and retention, idempotent sink.
- Contracts/versioning and compatibility tests; security (SASL/TLS, credentials), observability and quotas.

## Persistence / PostgreSQL
- Npgsql/EF Core/Dapper selection, connection pooling, migrations ownership and deployment strategy, concurrency control, transaction scope, timeouts, database per service and backups.
- Outbox/inbox schema and lifecycle only if chosen; repository/UoW shape from demonstrated needs.

## Synchronous communications
- HTTP controllers, typed clients, gRPC unary/streaming, deadlines, cancellation, retry only for safe operations, circuit-breakers, auth/interceptors and contract evolution.
- Discovery/load balancing, graceful shutdown, readiness/liveness, versioning and protobuf package ownership.

## Ops / SRE / security
- OpenTelemetry traces, metrics/log correlation, OTLP, Serilog integration, structured logging and PII redaction.
- Prometheus/Grafana/Tempo/Jaeger/Loki optional deployment examples, not platform hard requirements.
- Health probes (startup/readiness/liveness), failure isolation, rate limiting, resource usage and autoscaling.
- Authentication/authorization, service-to-service identity, secrets rotation, audit, tenancy, data protection and supply-chain security.
- Config validation, time/provider abstractions for testability, clocks/IDs, disposable integration test environments, resilience verification and performance benchmarks.

## Consider but do not presume
- Redis/distributed caching, distributed locks, schedulers, feature flags, sagas/workflows, event sourcing, service mesh, CQRS read stores, API gateway, multi-tenancy, Kubernetes operators, custom code generators and administrative UI.

## Critical quality scenarios
- DB commit succeeds, Kafka publish fails.
- Kafka message is delivered twice or replayed after an offset commit failure.
- Consumer loses partition during a long handler or an exception occurs mid-batch.
- gRPC downstream is slow, cancels or partially succeeds.
- New library version rolls out to one service while others are older.
- Startup sees invalid config or unavailable dependency; shutdown is interrupted.
- Logs accidentally contain secrets/PII, high-cardinality telemetry causes costs.
