---
name: discovery-interview
description: Conduct an architecture discovery interview for a reusable .NET microservice platform; elicit requirements, challenge assumptions, prioritize unknowns and maintain a decision/question backlog. Use when beginning the project or whenever consequential requirements are unclear.
---

# Discovery interview

**Outcome:** an accurate problem statement, constraints and prioritized open questions — not prematurely chosen tools.

## Workflow
1. Read `docs/00-vision.md`, `docs/PROJECT_STATE.md`, `docs/discovery/question-backlog.md`; avoid asking already answered items.
2. Create a concise **working model**: primary consumers, number/shape of services, hosting, deployment, business constraints, owner/team, expected scale, developer workflows, required reliability, security and support model.
3. Separate user facts, explicit preferences, proposals, unverified assumptions and unknowns. Do not turn a suggested library or fluent method into a hard requirement.
4. Use `references/interview-playbook.md` for categories and sequencing. Choose only the **3–5 highest-impact current questions**. Group by a single theme; explain each one's architectural consequence and offer a plausible provisional default.
5. Give the user useful preliminary design insight before asking. Treat statements such as "хочу красивый one-liner" as DX goals; investigate what operation the developer actually expects.
6. When the user answers: summarize trade-offs, update `docs/00-vision.md`, the question backlog and `docs/PROJECT_STATE.md`. Move answered items into a short resolved log. Identify contradictions explicitly.
7. If one question requires technical investigation, recommend or use `$technology-research` before requesting a decision. If the answer implies a clear candidate architecture, consult `$platform-architecture`.

## Collaboration rules
- Interview the user as an expert collaborator, not a test subject. No giant 20-question form; usually one compact batch per response.
- Ask a useful follow-up if the answer is vague or internally inconsistent; otherwise move forward.
- Not every missing detail blocks progress. Proceed with explicitly reversible assumptions for low-risk design work.
- Do not insist on perfect certainty or design every possible integration in advance.

## Output per round
- **Сейчас известно:** 2–5 facts.
- **Архитектурное следствие:** brief analysis with optional alternatives.
- **Вопросы:** 3–5 high-leverage questions, each with context and an optional suggested default.
- Repository files updated; one next action in state file.
