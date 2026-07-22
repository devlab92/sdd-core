# 00_subagent_delegation.md — Sub-Agent Delegation & Context Hygiene

> Delegation keeps the main agent's context clean. Research, scanning, and auditing are
> token-heavy and low-creativity — perfect for lightweight sub-agents. Implementation stays
> in the main agent, which holds write access and full context.

Applies only when `subagent_enabled: true` in [`sdd.config.md`](../sdd.config.md).

---

## Delegation matrix

| Task type | Suggested model tier | Rationale |
|-----------|----------------------|-----------|
| Quick file lookup | lightest / `flash_lite` | Minimal tokens, fast |
| Codebase research (multi-file) | light / `flash` | Moderate context, isolated |
| Security audit | light / `flash` | Checklist-driven, isolated |
| Complex architecture planning | strong / `pro` / inherit | Needs full reasoning |
| Code implementation | **main agent** | Needs write tools + full context |
| Post-task doc updates | light / `flash` | Formulaic, low creativity |

> Map the tiers to whatever your provider offers (Claude sub-agents, Gemini flash/pro,
> local small/large models).

---

## Delegation intensity by `token_mode`

- **economy** — delegate aggressively; keep the main agent almost purely for writes.
- **balanced** — delegate research + audit; plan and implement in main.
- **full** — delegate only heavy research; the strong model does most of the thinking.

---

## Context Hygiene — the "Smart Zone"

LLM quality degrades past ~60–80% of context capacity ("Lost in the Middle"). Defend the zone:

1. **On-demand loading** — load [`00_index.md`](00_index.md) first, then only the relevant doc.
2. **Terse output** — no filler, no re-pasting code, no process narrative.
3. **Compact after long tasks** — summarize what matters, drop the rest.
4. **Delegate heavy reads** — a sub-agent returns a conclusion, not 2,000 lines of files.

---

## What a good delegation looks like

- **Give the sub-agent a narrow, closed question** ("Which files import `authService`?
  Return a file:line list.") — not an open-ended task.
- **Ask for the conclusion, not the raw material.** The sub-agent reads; the main agent decides.
- **Never delegate writes** that need full project context.
