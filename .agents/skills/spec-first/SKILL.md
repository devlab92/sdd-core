---
name: spec-first
description: Enforces writing a 6-element specification before implementation — Outcomes, Scope, Constraints, Decisions, Tasks, Verification. Use in Stage 2 of the quality gate, for any change that needs a plan.
---

# Skill: Spec-First

> No production code without a spec. A spec is the contract that makes autonomous execution safe.
> This is Stage 2 of the `quality-gate`.

## The 6 elements

Every spec (plan) contains exactly these, in order:

1. **Outcomes** — what "done" looks like, in observable/testable terms.
2. **Scope** — what's **in**, and explicitly what's **out**.
3. **Constraints** — tech, compatibility, time, non-negotiables.
4. **Decisions** — choices made + rejected alternatives + *why* (per `CODING_PHILOSOPHY.md` L4).
5. **Tasks** — ordered, atomic steps. Tag each file `[CREATE]` / `[MODIFY]` / `[DELETE]`.
6. **Verification** — automated (exact commands + expected output) and manual checks.

Use the template at `plans/_TEMPLATE.plan.md`.

## The "Dumbest AI" test (must pass before Approval)

> Could an AI that has never seen this project execute this spec without asking anything?

- ✅ Exact commands with absolute paths.
- ✅ Exact names: files, branches, env vars, secrets.
- ✅ Expected output for every verification step.
- ✅ Failure handling for every risky step.
- ❌ No "adjust as needed" / "check it's fine".

## Token discipline in specs

- `[MODIFY]` → describe changes surgically; never paste whole files.
- `[CREATE]` → full content is fine.
- Reference existing code as `file:line`. Tables over prose. 1 spec = 1 objective.

## Clarification first (large/ambiguous features)

If more than one reasonable approach exists, or a human should decide a trade-off, write
`plans/active/<feature>.clarification.md` and resolve the questions **before** the spec.
