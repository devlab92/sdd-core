# plans/ — Execution Contracts

This directory holds the specs (plans) that make autonomous execution safe.

```
plans/
├── active/     # DRAFT | APPROVED | IN_PROGRESS — the current work
├── done/       # DONE | ABANDONED — safe to archive/delete
├── _TEMPLATE.plan.md            # copy this to start a plan
└── _TEMPLATE.clarification.md   # copy this first for large/ambiguous features
```

## Lifecycle
```
DRAFT ──▶ APPROVED ──▶ IN_PROGRESS ──▶ DONE
  └────────────▶ ABANDONED
```

## Rules
- One plan = one objective.
- No production code until Status is **APPROVED** (a hard stop).
- For large/ambiguous features, resolve a `.clarification.md` **first**.
- On completion, move the file from `active/` to `done/`.

See [`sdd_summary/00_how_to_plan.md`](../sdd_summary/00_how_to_plan.md) for the full protocol.
