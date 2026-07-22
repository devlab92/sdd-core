---
name: handoff
description: Multi-agent handoff state machine (DEV → READY_FOR_DEPLOY → DEPLOYED) for workflows where one AI develops and another deploys. Use when coordinating work across agents or sessions.
---

# Skill: Multi-Agent Handoff

> Coordinates work across agents/sessions so nothing is deployed by surprise and state is never
> ambiguous. Use for dual-AI workflows (e.g. a dev agent + a deploy agent) or long-running work
> handed between sessions.

## State machine

```
DEV ──▶ READY_FOR_DEPLOY ──▶ DEPLOYED
 │              │                 │
 └── blocked ◀──┘        rollback ┘
```

| State | Meaning | Who acts next |
|-------|---------|---------------|
| `DEV` | Implementation in progress | Dev agent |
| `READY_FOR_DEPLOY` | Post-audit green, committed, docs + CHANGELOG updated | Human approves → deploy agent |
| `DEPLOYED` | Live and smoke-tested | — |
| `blocked` | Reality contradicted the plan / failing check | Human |

## Handoff record

Track state at the top of the active plan (or a `plans/active/<feature>.handoff.md`):

```markdown
Status: READY_FOR_DEPLOY
Handoff-from: dev-agent (session 2026-07-22)
Commit: <sha>
Verified: lint ✅  types ✅  tests ✅  build ✅
Notes: <anything the next agent must know>
Deploy command: <exact command, filled from AGENTS.md §13>
```

## Rules
- Only move to `READY_FOR_DEPLOY` after Stage 5 (Post-Audit) is fully green.
- **Deploy is always a human-approved step** — the deploy agent waits for explicit go.
- On `blocked`, write the reason and stop. Never work around a contradiction.
- A handoff must be self-contained: the receiving agent should need nothing outside the record + repo.
