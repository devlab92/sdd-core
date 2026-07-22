# 🚀 BOOTSTRAP_PROMPT.md — Zero-to-Hero Initialization

> **What this is:** the single prompt you paste into any AI session to activate sdd-core in a
> project. The AI reads it, scans the codebase, interviews you, and customizes the framework to
> your stack — turning generic templates into a project-specific operating manual.

---

## How to use (human)

1. Copy the sdd-core files into the **root** of your project (new or existing).
2. Open an AI coding session (Claude Code, Cursor, Gemini, etc.).
3. Paste **everything below the line** as your first message.
4. Answer the AI's questions. Approve the setup plan when asked.

---

<!-- ─────────────  PASTE FROM HERE  ───────────── -->

You are initializing the **sdd-core** framework in this project. Follow these steps **in order**.
Do not write application code during bootstrap — you are configuring the framework itself.

### Step 1 — Read the framework
Read, in this order: `AGENTS.md`, `sdd.config.md`, `CODING_PHILOSOPHY.md`,
`sdd_summary/00_index.md`, `sdd_summary/00_how_to_plan.md`. Confirm you understand:
- the 4-layer thinking model,
- the 6-stage Quality Gate,
- the Behavior Matrix (economy/balanced/full),
- the Autonomous Execution + "Dumbest AI" rules.

### Step 2 — Detect the stack
Scan the repository (do not paste file contents back — summarize). Determine:
- Language(s), framework(s), package manager, runtime.
- How the app is run, built, tested, linted, deployed (read `package.json` scripts, `Makefile`,
  `pyproject.toml`, CI files, etc.).
- Whether there's a frontend (→ `design_system` on/off).

Report a concise stack summary as a table.

### Step 3 — Interview the human
Ask only what you could not infer. Typically:
1. **Domain** — what does this project do, in one sentence?
2. **Deploy target** — where does it run in production?
3. **Token mode** — economy / balanced / full? (default: balanced)
4. **AI provider** — cloud / local / hybrid? Context window if local.
5. **Team size** — solo / small / larger? (affects CODEOWNERS, PR strictness)
6. **Anything the AI must never touch** (protected dirs, generated code)?

Wait for answers before continuing.

### Step 4 — Present a setup plan (get approval)
Write `plans/active/bootstrap.md` (status DRAFT) listing exactly what you'll customize:
- `sdd.config.md` values,
- `AGENTS.md` §2 Stack, §6 Code Standards (stack-specific), §7 Boundaries, §13 Commands,
- `.github/workflows/ci.yml` steps for the detected stack,
- `.github/CODEOWNERS` handle,
- `LICENSE` copyright holder,
- initial `sdd_summary/` feature docs for existing modules,
- `DESIGN.md` from the template (only if there's a frontend).

**Stop and wait for the human to APPROVE** before editing.

### Step 5 — Execute (after approval)
Autonomously, without asking between steps:
1. Fill `sdd.config.md` with the agreed values.
2. Customize `AGENTS.md` (Stack, Commands, Code Standards, Boundaries).
3. Fill CI workflow steps; set the CODEOWNERS handle and LICENSE holder.
4. Populate `sdd_summary/00_index.md` with a row per existing module, and create an initial
   feature doc for each significant module (use the template in `00_skill_documenting.md`).
5. If frontend: copy `DESIGN.md.template` → `DESIGN.md` and fill tokens/scales you can infer.
6. Seed `sdd_summary/lessons_learned.md` with any project quirks discovered while scanning.
7. Add the first `CHANGELOG.md` entry: `feat: initialize sdd-core`.

### Step 6 — Verify & hand off
- Run lint/typecheck/test/build if they exist; report real output.
- Emit the doc-check forcing function.
- Propose the initial commit(s) as conventional commits (do **not** deploy).
- Move `plans/active/bootstrap.md` → `plans/done/`.
- Print a short "You're set up" summary: mode, stack, what to do next.

### Optional — local commit hooks
If the human wants stricter local quality (and the stack supports Node tooling), offer to set up
**Husky + commitlint + lint-staged** so conventional commits and staged-file checks run pre-commit.

<!-- ─────────────  END PASTE  ───────────── -->

---

## Notes
- Bootstrap **only creates what the project needs** — it won't force a design system on a
  backend-only service, or sub-agents on a provider that lacks them.
- Re-running bootstrap on an already-initialized project should update, not duplicate.
