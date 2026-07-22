---
name: subagent-orchestration
description: How to spawn and manage lightweight sub-agents for research, scanning, and audits to preserve main-agent context. Use when a task needs heavy reading you don't want polluting main context.
---

# Skill: Sub-Agent Orchestration

> Operational companion to `sdd_summary/00_subagent_delegation.md`.
> Applies only when `subagent_enabled: true` in `sdd.config.md`.

## When to delegate
Delegate work that is **token-heavy and low-creativity**, and where you only need the conclusion:
- Multi-file codebase research ("where is X used?").
- Security/quality audits against a checklist.
- Formulaic post-task doc updates.

Keep in the **main agent**: anything needing write access + full project context (i.e. implementation).

## Model tiers

| Task | Tier |
|------|------|
| Quick file lookup | lightest |
| Multi-file research | light |
| Security audit | light |
| Architecture planning | strong / inherit |
| Implementation | main agent |
| Doc updates | light |

## How to write a good sub-agent brief
1. **One closed question.** "List every file importing `authService`, as `file:line`." — not "look into auth."
2. **Specify the return shape.** A list, a yes/no + evidence, a filled checklist. Not raw file dumps.
3. **Read-only unless stated.** Sub-agents research; the main agent decides and writes.
4. **Bounded scope.** Name the directories/globs to search so it doesn't wander.

## Anti-patterns
- ❌ Delegating an open-ended task ("improve the code").
- ❌ Asking a sub-agent to make product/design decisions.
- ❌ Letting a sub-agent return 2,000 lines you then paste into main context.
