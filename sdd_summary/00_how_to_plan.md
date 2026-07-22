# 00_how_to_plan.md — The Planning Protocol

> How every plan in `plans/active/` is written, reviewed, approved, and executed.
> A plan is a contract between the human and the AI. It is the thing that makes autonomous
> execution safe.

---

## The plan lifecycle (state machine)

```
DRAFT ──▶ APPROVED ──▶ IN_PROGRESS ──▶ DONE
  │                                       │
  └──────────────▶ ABANDONED ◀────────────┘
```

- **DRAFT** — being written / under review. No production code yet.
- **APPROVED** — the human locked it. Autonomous execution may begin.
- **IN_PROGRESS** — execution underway; tasks checked off as completed.
- **DONE** — verified complete. Move file from `plans/active/` to `plans/done/`.
- **ABANDONED** — dropped. Move to `plans/done/` with a one-line reason.

The status is a field at the top of the plan file.

---

## Step 0 — The Clarification Phase (for large / ambiguous features)

**Before** writing a plan for anything complex or under-specified, write a clarification file:

```
plans/active/<feature>.clarification.md
```

- List the **open questions** — anything where a *human* should make the call
  (product behavior, trade-offs, priorities, external constraints).
- Ask, get answers, iterate. **Do not** write the plan until the questions are resolved.
- This prevents the #1 failure mode: **an AI making design decisions the human should make.**

> If a feature touches > 3 files, has UX implications, or has more than one reasonable
> approach → it needs a clarification phase first.

---

## Anatomy of a plan (the 6 elements)

Every plan (see [`_TEMPLATE.plan.md`](../plans/_TEMPLATE.plan.md)) contains:

1. **Outcomes** — what "done" looks like, in observable terms.
2. **Scope** — what is in, and explicitly what is **out**.
3. **Constraints** — tech, time, compatibility, non-negotiables.
4. **Decisions** — the design choices made (and rejected alternatives + why).
5. **Tasks** — ordered, atomic steps. Each file tagged `[CREATE]` / `[MODIFY]` / `[DELETE]`.
6. **Verification** — automated (commands + expected output) and manual checks.

---

## The Golden Rule — the "Dumbest AI" Test

> **Could an AI that has never seen this project execute this plan without asking anything?**

If not, the plan is not done. Checklist:

- ✅ Exact commands, with absolute paths.
- ✅ Exact names: secrets, files, branches, env vars.
- ✅ Expected output for every verification step.
- ✅ What to do on failure for every risky step.
- ❌ Never "adjust as needed", "check that it's fine", "handle appropriately".

---

## Autonomous Execution (Rule 7)

Once a plan is **APPROVED**:

- Execute **all** phases end-to-end, without stopping to ask for permission between steps.
- The **only** mandatory stop is **deploy**.
- If **reality contradicts the plan** — a file isn't where expected, a command fails, an
  assumption proves false — **STOP immediately and report.** Never improvise a workaround
  or silently expand scope.

This is what makes autonomy safe: the plan is the boundary, and deviations surface loudly.

---

## Token Economy in plans

- **1 plan = 1 objective.** Side-discoveries → [`40_further_tasks.md`](40_further_tasks.md).
- For `[MODIFY]` files, describe changes **surgically** — never paste the whole file.
- Only paste full content for `[CREATE]` files.
- Reference existing code as `path/to/file.ts:42`, never re-paste it.
- Tables > prose. No process narrative.
