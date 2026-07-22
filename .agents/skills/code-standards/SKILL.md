---
name: code-standards
description: Stack-agnostic code standards plus the Refactor-or-Register rule for handling adjacent tech debt. Use during implementation (Stage 4) whenever writing or touching code.
---

# Skill: Code Standards

> Universal standards that apply to every stack. Stack-specific rules are appended by
> `BOOTSTRAP_PROMPT.md` under `AGENTS.md` §6.

## Naming
- `camelCase` — functions, variables.
- `PascalCase` — types, classes, components.
- `snake_case` — file names.
- Descriptive names over comments. Names should carry intent.

## Structure (from CODING_PHILOSOPHY Layers 2–3)
- Single Responsibility per unit. Early returns over deep nesting.
- Pure functions where possible. DRY, but no premature abstraction.
- Layered separation: route → controller → service → repository.
- Validate input at boundaries. Typed errors at boundaries.
- Centralize config; no scattered magic literals.

## Frontend (when `design_system: true`)
- **Component library first, inline code never** (Layer 3).
- Semantic `id` + BEM class on every interactive element.
- Only semantic design tokens — no hard-coded colors/spacing.

## The Refactor-or-Register Rule

When you encounter non-standard / legacy / debt-laden code adjacent to your task:

| Condition | Action |
|-----------|--------|
| Impact **≤ 3 files** AND change is straightforward | **Refactor NOW** (part of this task) |
| Impact **> 3 files** OR change is complex | **Register** in `sdd_summary/40_further_tasks.md` |

A register entry must include: **priority** (P1/P2/P3) + **affected files** + **date**.

> Never silently expand a task's scope. Either fix it cleanly now, or record it and move on.

## Hygiene
- No dead code, no commented-out blocks, no `console.log`/debug prints left behind.
- No code duplication of something that already exists — reference and reuse.
