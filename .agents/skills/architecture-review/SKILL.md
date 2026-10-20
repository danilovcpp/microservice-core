---
name: architecture-review
description: Challenge .NET platform designs, ADRs and proposed abstraction layers through failure-mode, operability, security, simplification and maintainability review. Use before approving a major design and when the user requests a critical external review.
---

# Architecture review (independent challenger)

**Goal:** identify costly assumptions before they become stable APIs.

1. Treat current design as a proposal even if you authored it earlier. Read `docs/architecture/`, relevant ADRs and sources.
2. Apply `references/review-lenses.md`: necessity, alternatives, dependency direction, semantics, failures, security, operability, DX, upgrades and exit strategy.
3. Compare the proposal against a **lean baseline** using standard .NET DI/hosting/options, existing maintained packages and optional Aspire Service Defaults.
4. Construct specific failure scenarios and test if the design handles them (DB/Kafka partial failure, process crash, duplicates, shutdown, version skew, malformed messages, unreliable gRPC calls, compromised secrets).
5. Write findings ordered by severity: `Blocking / High / Medium / Low`. For each, give evidence, probable impact, change proposal, and residual risk.
6. If an accepted ADR is questionable, propose a new superseding ADR **without silently modifying its status**; user remains decision maker.
7. Update `docs/PROJECT_STATE.md` with material blockers and one next action. Don't require every Low issue to block the specification.

## Important constraints
- Avoid fabricated benchmark conclusions, imaginary Kafka/exactly-once guarantees and superficial claims that an architecture is 'best practice'.
- Identify cases where platformization is unnecessary or hurts a small service.
- If a flaw requires runtime measurement, recommend a spike and define acceptance criteria. Do not execute code unless permitted.
- Be able to give a positive verdict when justified; critique should be rigorous, not performative.
