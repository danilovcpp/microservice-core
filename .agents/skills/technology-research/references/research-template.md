# Research memo template

> Copy into `docs/research/<topic>.md`, fill only applicable sections.

```
# <Topic>
Status: draft | ready-for-decision | accepted-as-evidence | stale
Last checked: YYYY-MM-DD
Owner: Architect + user

## Decision question
## Context and mandatory constraints
## Comparison criteria (ranked)
## Options
| Option | What it buys | Limits / runtime semantics | Maintainer/license/compatibility | Operations and migration |
| ... |
## Sources
- [Official link](https://...) — verified YYYY-MM-DD; concrete fact supported
## Gaps and assumptions
## Recommendation and why (including a minimal alternative)
## Verification/prototype plan (if needed)
## Decisions affected / ADR links
```

Rules: distinguish package's documented feature from independently verified behavior. Note versions and dates for mutable facts. Document potential dependency leaks into domain and public contracts. Use cost/complexity estimates as ranges with assumptions, not fabricated precision.
