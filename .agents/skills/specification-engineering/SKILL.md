---
name: specification-engineering
description: Convert agreed .NET microservice platform architecture into implementable, testable specifications, API contracts, phased milestones and acceptance criteria. Use when major design choices have been reviewed and the user asks for a full TЗ/RFC or implementation roadmap.
---

# Specification engineering

**Outcome:** a different engineer or coding agent can implement the specified component without inventing critical behavior.

1. Read accepted ADRs and approved constraints, `docs/PROJECT_STATE.md`, relevant research and architecture. Mark ambiguous or unapproved matters, and do not mask them with assumptions.
2. Divide spec by capability rather than one 100-page document: platform core, hosting/service defaults, DDD primitives, CQRS/handlers, Kafka producer, Kafka consumer, reliable messaging, Postgres, gRPC, observability and testing/tooling — only where chosen.
3. For each component follow `references/spec-template.md`: user value, exact scope, public API sketch/contracts, defaults, configuration and validation, dependency constraints, semantics, cancellation/lifecycle, failure handling, observability, security, tests, examples, compatibility and non-goals.
4. Specify *behavioral contracts*: what happens on retry, duplicate, timeout, shutdown, message malformed, database transaction rollback, outbox backlog and unsupported configuration. No hand-wavy 'handle errors'.
5. Define acceptance criteria with verifiable Given/When/Then or equivalent and a test level (unit/integration/contract/load/security). Verify API examples with type checks only once implementation is authorized.
6. Define phased milestones each yielding a usable vertical slice: lean host / minimal reference service → observability → one messaging path → reliability → persistence → API templates; adapt order to approved priorities.
7. Create a cross-cutting checklist and reference-service acceptance scenario. Ask for explicit sign-off on any still contested major design decision before declaring the spec 'implementation ready'.
8. Save in `docs/specification/`, update `docs/planning/roadmap.md` and project state.

## Exit gate
A spec may be marked `ready for implementation` only when: platform scope and non-goals are explicit; external dependency strategy is approved; semantics and failure scenarios are testable; publicly exposed API shape and compatibility policy are coherent; key ADRs are accepted; ownership/roadmap and verification are clear. Otherwise mark `draft` with blockers.
