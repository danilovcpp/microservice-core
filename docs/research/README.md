# Каталог исследований

Статус: **темы запланированы, результатов ещё нет**. Не представлять перечисленные варианты как изученные или одобренные без проверки.

## Направления исследования
1. **Build-vs-buy и hosting** — стандартные ASP.NET Core / Generic Host / DI+Options против собственного Platform bootstrap; Aspire Service Defaults, AppHost; шаблоны отдельно от runtime.
2. **Kafka и надёжная интеграция** — низкоуровневый Confluent.Kafka, поддерживаемые high-level библиотеки и собственная оркестрация; rebalance, retries, DLQ/replay, идемпотентность, outbox/inbox.
3. **Application/CQRS** — обычный DI, mediator-библиотеки, поддержка и лицензии; необходимость CQRS в простых сервисах.
4. **PostgreSQL** — Npgsql, EF Core, Dapper, транзакции, migrations, outbox и цена репозиторных абстракций.
5. **gRPC** — штатный ASP.NET Core gRPC, client factory, interceptors, deadline, auth, совместимость контрактов, retry semantics.
6. **Observability** — OpenTelemetry/OTLP, Serilog, correlation, метрики, cardinality и health checks.
7. **DDD primitives** — минимальные базовые модели против крупных DDD-framework; запись и dispatch domain events.
8. **DX и доставка** — внутренний NuGet, `dotnet new`, semantic versioning, integration/contract testing.

Использовать `$technology-research` и его шаблон. Каждый исследовательский документ: **дата проверки, версии, ссылки на надёжные источники, критерии сравнения, неизвестные и вывод**.

## Официальные отправные точки (не рекомендации к выбору)
- [ASP.NET Core / Generic Host](https://learn.microsoft.com/aspnet/core/fundamentals/host/generic-host)
- [Aspire Service Defaults](https://learn.microsoft.com/dotnet/aspire/fundamentals/service-defaults)
- [Aspire architecture overview](https://learn.microsoft.com/dotnet/aspire/architecture/overview)
- [.NET DDD microservice design](https://learn.microsoft.com/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/ddd-oriented-microservice)
- [.NET Domain and Integration Events](https://learn.microsoft.com/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/domain-events-design-implementation)
- [.NET integration events](https://learn.microsoft.com/dotnet/architecture/microservices/multi-container-microservice-net-applications/integration-event-based-microservice-communications)
- [OpenTelemetry .NET](https://opentelemetry.io/docs/languages/dotnet/)
- [Apache Kafka](https://kafka.apache.org/documentation/)
- [PostgreSQL](https://www.postgresql.org/docs/)

Ссылки — точки входа в будущее исследование, а не свидетельство, что автор стартового набора выполнил полноценный аудит актуальных версий и лицензий.
