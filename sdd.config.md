---
# ─────────────────────────────────────────────────────────────
# SDD-Core Configuration
# The AI reads this file at session start. No dependencies — edit by hand.
# ─────────────────────────────────────────────────────────────
token_mode: balanced          # economy | balanced | full
ai_provider: cloud            # cloud | local | hybrid
local_model_context: 8000     # context window size in tokens (if local/hybrid)
auto_changelog: true          # AI appends to CHANGELOG.md after commits
auto_doc_update: true         # AI runs the "sdd_summary/ outdated?" forcing function
design_system: true           # false for backend-only projects (skips DESIGN.md)
subagent_enabled: true        # false if the AI provider has no sub-agent support
language: pt-BR               # language for conversation / UI
doc_language: en              # language for documentation files
---

# How this file works

The values above tune the **Behavior Matrix** in [`AGENTS.md`](AGENTS.md#1-behavior-matrix).
Change them to fit the project and the AI running it.

## `token_mode`
- **`economy`** 🟢 — Local/cheap models or tight budgets. Terse output, aggressive sub-agent
  delegation, minimal docs, plans only for multi-layer changes.
- **`balanced`** 🟡 — The sane default. Full templates, moderate delegation, plans for > 3 files.
- **`full`** 🔴 — Frontier models, quality over cost. Extensive docs, multiple research
  alternatives, plans for everything non-trivial.

## `ai_provider`
- **`cloud`** — Claude / Gemini / GPT with large context.
- **`local`** — Ollama / LM Studio / etc. Pair with a realistic `local_model_context`.
- **`hybrid`** — Cloud for planning, local for bulk edits (or vice versa).

## Feature toggles
Set to `false` to disable a subsystem the project doesn't need (e.g. `design_system: false`
for a pure API service, `subagent_enabled: false` for an AI without sub-agent support).

> **Why this matters:** a local 8K model in `economy` mode behaves fundamentally differently
> from a frontier model in `full` mode — and both produce good results *within their constraints*.
