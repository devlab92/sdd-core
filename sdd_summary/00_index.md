# 00_index.md — Master Documentation Index

> **Load this file first, always.** It is the map of the project's knowledge base.
> Then load **only** the specific domain doc you need. Never scan all docs blindly —
> that is the fastest way to burn context (see Token Economy in `AGENTS.md`).

---

## How to use this index

1. Identify the domain your task touches (from the tables below).
2. Load **only** that doc.
3. If no doc exists for the domain, that's a signal: create one after the task
   (see [`00_skill_documenting.md`](00_skill_documenting.md)).

---

## Protocol & meta docs (always relevant)

| Doc | Purpose |
|-----|---------|
| [`00_how_to_plan.md`](00_how_to_plan.md) | How to write plans, the clarification phase, the "dumbest AI" test, autonomous execution |
| [`00_skill_documenting.md`](00_skill_documenting.md) | How to write and maintain feature docs |
| [`00_subagent_delegation.md`](00_subagent_delegation.md) | When and how to delegate to sub-agents; context hygiene |
| [`00_workflow_guide.md`](00_workflow_guide.md) | The 3-layer architecture: Intelligence → Skills → Design System |

---

## Living memory

| Doc | Purpose |
|-----|---------|
| [`lessons_learned.md`](lessons_learned.md) | Patterns, anti-patterns, project quirks learned across sessions |
| [`31_version_history.md`](31_version_history.md) | SemVer history + conventional commit rules |
| [`40_further_tasks.md`](40_further_tasks.md) | Tech-debt register (Refactor-or-Register outputs) |
| [`23_infra_troubleshooting.md`](23_infra_troubleshooting.md) | Incident log (Symptom → Cause → Fix → Prevention) |
| [`44_frontend_checklist.md`](44_frontend_checklist.md) | Pre-delivery UI checklist |

---

## Feature / domain docs

> _Populated by `BOOTSTRAP_PROMPT.md` and grown as the project evolves._
> One row per feature or module. Keep alphabetical.

| Doc | Module / Feature | Key files |
|-----|------------------|-----------|
| `<example>_auth.md` | Authentication | `src/auth/*` |
| _…_ | _…_ | _…_ |

---

## Naming convention

- `00_*` — protocol / meta (loaded often).
- `2x_*` — operations / infra.
- `3x_*` — history / versioning.
- `4x_*` — tasks / checklists.
- `<name>.md` — a specific feature or module.
