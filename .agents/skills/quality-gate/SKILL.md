---
name: quality-gate
description: The central 6-stage pipeline every non-trivial task runs through — Pre-Audit → Spec → Approval → Implement → Post-Audit → Gate. Use this for any change beyond a trivial one-liner.
---

# Skill: Quality Gate (6-Stage Pipeline)

> This is the **central nervous system** of sdd-core. Every non-trivial change flows through
> these six stages, in order. Stage 3 (Approval) is a hard stop; deploy in Stage 6 is the only
> other hard stop.

```
┌────────────┐   ┌──────────┐   ┌────────────┐   ┌────────────┐   ┌────────────┐   ┌───────────┐
│ 1 PRE-AUDIT│ → │ 2 SPEC   │ → │ 3 APPROVAL │ → │ 4 IMPLEMENT│ → │5 POST-AUDIT│ → │ 6 GATE    │
│ Load ctx   │   │ Design   │   │ User locks │   │ Track tasks│   │ Lint/Test  │   │ Doc+Commit│
│ Check debt │   │ 6 elems  │   │ Wait OK    │   │ Follow plan│   │ Verify     │   │ Version   │
└────────────┘   └──────────┘   └────────────┘   └────────────┘   └────────────┘   └───────────┘
```

---

## Stage 1 — PRE-AUDIT (load context, check debt)

- Load `sdd_summary/00_index.md`, then only the relevant domain doc.
- Skim `sdd_summary/40_further_tasks.md` and `lessons_learned.md` for related debt/quirks.
- Confirm the current state matches expectations. If not → stop and report.
- **Output:** a clear statement of the current state and the goal.

## Stage 2 — SPEC (design)

- Produce the 6-element spec (see the `spec-first` skill): Outcomes, Scope, Constraints,
  Decisions, Tasks, Verification.
- For large/ambiguous work, run the **Clarification Phase** first
  (`sdd_summary/00_how_to_plan.md`).
- Write it to `plans/active/<feature>.md` with status `DRAFT`.
- Apply the **"Dumbest AI" test** before proceeding.

## Stage 3 — APPROVAL (hard stop 🔒)

- Present the plan. **Wait for the human to mark it `APPROVED`.**
- Do **not** write production code before approval.
- Once approved → autonomous execution is authorized (Stage 4 onward, no per-step asking).

## Stage 4 — IMPLEMENT (track tasks, follow rules)

- Execute the plan's tasks in order; check them off as you go (status → `IN_PROGRESS`).
- Follow `CODING_PHILOSOPHY.md` (4 layers) and `code-standards`.
- Apply **Refactor-or-Register** for adjacent debt (≤3 files fix now, else register).
- If reality contradicts the plan → **STOP and report.** Never improvise.

## Stage 5 — POST-AUDIT (verify)

- Run lint, typecheck, tests, and build (per `AGENTS.md` §13 Commands).
- Report **real** output. If anything fails → fix or stop; never claim green when red.

## Stage 6 — GATE (document, commit, version)

1. **Doc check** — emit `📄 sdd_summary/ outdated?` and update docs if needed.
2. **CHANGELOG** — append an entry with the correct SemVer bump.
3. **Commit** — one conventional commit per logical change.
4. Move the plan `plans/active/ → plans/done/` and set status `DONE`.
5. **Deploy** — ask for human approval. Never deploy autonomously.

---

## Scaling by token_mode

- **economy** — run the full gate but keep every stage terse; spec only for multi-layer work.
- **balanced** — full gate; spec for > 3 files.
- **full** — full gate; spec for everything non-trivial, with alternatives documented.
