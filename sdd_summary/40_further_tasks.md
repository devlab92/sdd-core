# 40_further_tasks.md — Tech-Debt & Deferred-Task Register

> The destination for everything the **Refactor-or-Register** rule defers, plus any
> side-discovery that would violate "1 plan = 1 objective". Registering debt here is what
> keeps it from growing **invisibly**.

See the rule in [`AGENTS.md`](../AGENTS.md#11-refactor-or-register-rule).

---

## Priority legend

| Priority | Meaning |
|----------|---------|
| 🔴 P1 | Blocks/risks correctness or security. Do next. |
| 🟠 P2 | Meaningful debt; schedule soon. |
| 🟡 P3 | Nice to have; opportunistic. |

---

## Open

| Priority | Task | Affected files | Registered | Notes |
|----------|------|----------------|------------|-------|
| 🟡 P3 | _(example) Extract duplicated date formatting into a helper_ | `src/a.ts`, `src/b.ts`, `src/c.ts`, `src/d.ts` | YYYY-MM-DD | > 3 files → registered, not refactored inline |

---

## Resolved

| Task | Resolved | Commit / Plan |
|------|----------|---------------|
| _…_ | _…_ | _…_ |
