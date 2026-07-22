# lessons_learned.md — Auto-Learning Memory

> The project's cross-session memory. The AI **appends** here whenever it learns something
> that a future session would waste tokens rediscovering: a library quirk, an anti-pattern
> that bit us, a project-specific convention, a decision and its reasoning.
>
> **Append only. Never delete.** Newest at the top.

---

## How to write an entry

```markdown
### YYYY-MM-DD — <short title>
**Category:** pattern | anti-pattern | quirk | decision
**Context:** what we were doing.
**Lesson:** the takeaway, stated as a rule for next time.
**Evidence:** `file:line` or command output that proves it.
```

Keep entries short. One lesson per entry. Link related docs with `[[doc_name]]`.

---

## Log

<!-- New entries go here, newest first. -->

### YYYY-MM-DD — (example) Seed entry
**Category:** decision
**Context:** Bootstrapped sdd-core into this project.
**Lesson:** The knowledge base is loaded index-first; keep feature docs under ~200 lines.
**Evidence:** [[00_index.md]]
