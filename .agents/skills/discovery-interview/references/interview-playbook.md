# Interview map — choose, do not dump

## Wave A: problem and constraints (start here)
- What representative microservices are being built (API-only, background consumers, scheduled workers, gateway)? One realistic first service and one contrasting second service.
- Team and distribution: personal mono-repo, several repos, shared packages consumed by teams, public/internal NuGet? Desired change cadence and versioning.
- Where and how are services deployed (VM, Docker Compose, Kubernetes, cloud-managed), how launched locally, CI/CD context and config/secrets delivery?
- Expected traffic, number of services, uptime/SLO, state volume, Kafka throughput; are there actual bottlenecks or speculative scale goals?
- Architectural boundaries: target .NET, operating systems, existing approved dependencies, compliance/license constraints, ability to use Aspire?

## Wave B: service API and coding model
- Which integrations are opt-in? Need background-host-only apps, HTTP controllers, gRPC endpoints and out-of-process jobs independently?
- Should a service work without Platform? Are normal ASP.NET Core DI and `IOptions<T>` expected to remain accessible?
- Is command/query dispatch necessary? Where would handlers run, and what pipeline behaviors are genuinely useful?
- What DDD abstractions are recurring across *real* services? Is aggregate modeling mandatory or selective?
- Are domain and integration events always separate? What publication timing guarantees are needed?

## Wave C: reliability and semantics
- Kafka topic ownership, partitioning and ordering, consumer groups, retry vs redelivery, schema compatibility, DLQ/quarantine, rebalance/shutdown and offset commit policy.
- Required delivery and business effects: duplicates acceptable? Outbox/inbox? Sagas? Transactional coordination with Postgres?
- Retention, replay, backfills, poison messages, large messages and operational dashboards.
- Sync calls: gRPC deadlines, idempotency, retry safety, version compatibility, service discovery and auth.

## Wave D: operational experience
- AuthN/AuthZ, interservice identities, secret handling, auditing and multi-tenancy; threat model.
- Traces, structured logs, metrics, correlation IDs, PII redaction, sampling and resource costs.
- Migrations, startup validation, health readiness/liveness, graceful shutdown and degradation behavior.
- Test ergonomics (unit, integration, contracts, container tests), local Docker and example service.

## Wave E: maintainability and publishing
- Target project structure, package granularity, support policy, semantic versioning, migration and deprecation.
- Template (`dotnet new`), service defaults, analyzers/source generators? Which are optional?
- Decisions about license, distribution, keeping the public API approachable and future extension points.

## Decision priority rubric
Mark each open question `P0` (changes module boundaries or guarantees), `P1` (changes major technology choice or operability), `P2` (local/reversible detail). Ask P0 first. Note dependencies between questions to avoid premature choices.
