# Red-team checklist

## Necessary abstraction?
- What repeatable pain does this package eliminate? Is it used by at least two genuinely different services?
- Is the custom type a meaningful domain contract or only a rename of a vendor API?
- Can it be removed in one sprint? What breaks when underlying library changes?

## Dependency/lifecycle correctness
- Does Domain reference a framework or infrastructure concept?
- Are host startup, background service lifetimes, scope creation, options validation and cancellation explicit?
- Is the public API stable, composable, testable, discoverable and usable without package X?

## Consistency / messaging
- Are publication-after-commit, transactional outbox, consumer deduplication and retries consistent with the DB/broker boundary?
- Is 'exactly once' limited to a real provable scope? Could a handler send email or make HTTP calls twice?
- What happens on poison data, partition rebalance, offset rewind, DLQ reinjection, Kafka outage or schema migration?

## Network and security
- Are gRPC deadlines propagated? Are retries safe given method semantics?
- Are secrets/PII excluded from logs and telemetry? Are internal endpoints authenticated as appropriate?
- Is configuration validated before traffic, and is least privilege applied?

## Operability and economics
- Can a new service owner diagnose a stuck outbox, lagging consumer, unhealthy gRPC dependency or leaked DB connection?
- Are metrics cardinality, tracing sampling and telemetry cost bounded?
- Who upgrades NuGet packages, resolves CVEs, publishes releases and maintains compatibility?

## Counterfactual
- Would `builder.Services.Add...`, Aspire Service Defaults, ASP.NET Core gRPC and standard libraries solve 80% of the problem?
- What does a service that needs only one capability have to reference or run?
- What is the worst upgrade/migration scenario in 2 years?
