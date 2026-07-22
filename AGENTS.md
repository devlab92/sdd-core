# AGENTS.md — Canonical Agent Rules

> **This is the single source of truth for how any AI agent must operate in this project.**
> `CLAUDE.md`, `GEMINI.md`, and `.cursorrules` are thin mirrors that point here.
> Read this file **fully** at the start of every session before touching code.

---

## 0. Configuration

Read [`sdd.config.md`](sdd.config.md) at session start. It defines the operating mode
(`token_mode`, `ai_provider`, feature toggles) that changes how aggressively you apply
the rules below. If the file is missing, assume `token_mode: balanced` and everything enabled.

---

## 1. Behavior Matrix

Your behavior scales with `token_mode` from `sdd.config.md`:

| Behavior | Economy 🟢 | Balanced 🟡 | Full 🔴 |
|----------|-----------|------------|--------|
| Research alternatives | Skip | 1 alternative | 3+ alternatives |
| Documentation generated | Minimal (bullets) | Standard (full template) | Extensive + examples |
| Sub-agents | Aggressive | Moderate (research + audit) | Minimal (heavy research only) |
| Responses | Terse, no filler | Balanced | Detailed with explanations |
| Plans required | Multi-layer changes only | For > 3 files | Everything non-trivial |
| CHANGELOG entries | feat/fix only | feat/fix/refactor | All commit types |
| Context loading | Index only, on-demand | Index + relevant doc | Full domain scan |
| Code comments | Only non-obvious | Key decisions + edge cases | Comprehensive |

---

## 2. Stack

> _Filled by `BOOTSTRAP_PROMPT.md` when this framework is installed into a project._

- **Language(s):** `<detected>`
- **Framework(s):** `<detected>`
- **Package manager:** `<detected>`
- **Deploy target:** `<detected>`

---

## 3. Coding Philosophy

Before writing **any** code, follow the 4-layer thinking model in
[`CODING_PHILOSOPHY.md`](CODING_PHILOSOPHY.md), **in order**:

1. **Think First** — understand the problem, edge cases, simplest solution.
2. **Structural Patterns** — SRP, pure functions, early returns, descriptive names.
3. **Scalability** — unique IDs, component-first, layered separation, typed errors.
4. **Research** — only if the standard solution is insufficient; document *why*.

You may not skip a layer. Layer 4 is never a starting point.

---

## 4. Mandatory: Before ANY Change — The 6-Stage Quality Gate

Every non-trivial task runs through the pipeline in
[`.agents/skills/quality-gate/SKILL.md`](.agents/skills/quality-gate/SKILL.md):

```
1. PRE-AUDIT  →  2. SPEC  →  3. APPROVAL  →  4. IMPLEMENT  →  5. POST-AUDIT  →  6. GATE
Load context     Design       User locks      Track tasks      Lint/Test/Build   Doc + Commit
Check debt       6 elements   the plan        Follow rules     Verify            Version bump
```

- **Stage 3 (APPROVAL) is a hard stop.** Never write production code before the plan is
  marked `APPROVED` by the human.
- For large/ambiguous features, run the **Clarification Phase** first
  (see [`sdd_summary/00_how_to_plan.md`](sdd_summary/00_how_to_plan.md)).

---

## 5. Mandatory: After ANY Change — Post-Task Protocol

Run every item, in order, at the end of every task:

1. **Post-audit** — lint, typecheck, test, and (if applicable) build. Report real output.
2. **Documentation check** — emit the forcing-function prompt:
   > 📄 **`sdd_summary/` outdated?**
   > This task changed logic covered by `<doc_name>.md`.
   > Should I update the document now?
3. **CHANGELOG** — append an entry to [`CHANGELOG.md`](CHANGELOG.md) with the correct
   SemVer bump (see §11).
4. **Commit** — one conventional commit per logical change.
5. **Deploy nudge** — deploy is the **only** mandatory human-approval stop after approval.
   Never deploy autonomously; ask.

---

## 6. Code Standards

See [`.agents/skills/code-standards/SKILL.md`](.agents/skills/code-standards/SKILL.md).
Universal defaults (stack-specific rules filled by bootstrap):

- `camelCase` functions, `PascalCase` types/components, `snake_case` files.
- Descriptive names over comments. No dead code, no commented-out blocks.
- Validate input at boundaries; type errors at boundaries.
- Centralize config (env vars in one place).

---

## 7. Boundaries — NEVER Do This

- ❌ Never commit `.env` or any real secret. Use `.env.example` with `***` placeholders.
- ❌ Never log raw secrets, tokens, or PII.
- ❌ Never write production code before a plan is `APPROVED`.
- ❌ Never deploy without explicit human approval.
- ❌ Never improvise when reality contradicts the plan — **STOP and report** (see §9).
- ❌ Never use vague instructions in plans ("adjust as needed", "check it's fine").
- ❌ Never paste code that already exists in the repo — reference `file:line`.
- _Stack-specific prohibitions appended by bootstrap._

---

## 8. Token Economy

Context is a budget. Waste degrades quality ("Lost in the Middle").

1. Never paste code that already exists — reference `path/to/file.ts:42`.
2. For `[MODIFY]` files in plans, describe changes **surgically**; don't paste whole files.
3. Only paste full content for `[CREATE]` files.
4. Tables > prose for enumerations.
5. **1 plan = 1 objective.** Side-discoveries go to `sdd_summary/40_further_tasks.md`.
6. No process narrative ("first I considered X but…").
7. Don't repeat rules already in this file — reference them.
8. Load [`sdd_summary/00_index.md`](sdd_summary/00_index.md) first, then only the relevant
   domain doc. Compact context after long tasks.

---

## 9. Autonomous Execution Protocol

Once a plan is `APPROVED`:

- Execute **all** phases end-to-end without stopping to ask.
- The **only** mandatory stop is **deploy**.
- If **reality contradicts the plan** (a file isn't where expected, a command fails, an
  assumption is false) → **STOP immediately and report**. Never improvise a workaround.

---

## 10. Sub-Agent Strategy

See [`sdd_summary/00_subagent_delegation.md`](sdd_summary/00_subagent_delegation.md).
Delegate read-only research, multi-file scans, and audits to lightweight sub-agents to keep
main context clean. Keep implementation (write access + full context) in the main agent.

---

## 11. Refactor-or-Register Rule

When you find non-standard / legacy / debt-laden code adjacent to your task:

- **Impact ≤ 3 files AND straightforward** → **refactor NOW** (part of this task).
- **Impact > 3 files OR complex** → **register** in
  [`sdd_summary/40_further_tasks.md`](sdd_summary/40_further_tasks.md) with:
  priority + affected files + date. Do **not** silently expand scope.

---

## 12. Versioning (Hybrid)

- Maintain [`CHANGELOG.md`](CHANGELOG.md) locally (Keep a Changelog format).
- Bump rule: `fix:`/`chore:` → **PATCH**, `feat:` → **MINOR**, `BREAKING CHANGE` / `!` → **MAJOR**.
- GitHub Actions (`.github/workflows/release.yml`) produces official releases.
- **Never delete CHANGELOG entries — only append.** It is the project's living memory.

---

## 13. Commands

> _Exact dev/build/test/deploy commands filled by `BOOTSTRAP_PROMPT.md`._

| Action | Command |
|--------|---------|
| Install | `<filled>` |
| Dev | `<filled>` |
| Build | `<filled>` |
| Test | `<filled>` |
| Lint | `<filled>` |
| Deploy | `<filled>` |

---

## 14. Documentation Protocol

See [`sdd_summary/00_skill_documenting.md`](sdd_summary/00_skill_documenting.md).
Every feature doc lives in `sdd_summary/`. The index is the map. Keep docs alive via the
Post-Task Protocol (§5).
