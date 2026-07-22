# 00_skill_documenting.md — Documentation Standard

> How to write and maintain the feature docs that live in `sdd_summary/`.
> Good docs are the difference between an AI that re-learns the codebase every session
> and one that loads a 200-line summary and gets to work.

---

## When to create a doc

- A new feature/module is added → create `sdd_summary/<feature>.md`.
- An existing doc's domain changed → **update it** (Post-Task Protocol forces this).
- The index has no row for the area you just touched → add one.

## When to update a doc — the forcing function

At the end of **every** task, emit:

> 📄 **`sdd_summary/` outdated?**
> This task changed logic covered by `<doc_name>.md`.
> Should I update the document now?

This single prompt is what keeps documentation from rotting within two weeks.

---

## Feature doc template

```markdown
# <feature>.md — <Human Name>

> One-line purpose.

## Overview
What this module does and why it exists. 2–4 sentences.

## Layout map
<ASCII diagram of the main flow or file relationships — optional but powerful>

## Key files
| File | Responsibility |
|------|----------------|
| `src/x/y.ts` | ... |

## Endpoints / public interface
| Method / Export | Signature | Notes |
|-----------------|-----------|-------|
| `GET /api/...` | ... | ... |

## Data / state
Key entities, shapes, invariants.

## Known issues / gotchas
- ...

## Related docs
- [[other_doc]]
```

---

## Rules

- **Terse and factual.** No marketing prose. Tables over paragraphs.
- **Reference, don't paste.** Point to `file:line`; never copy code into a doc.
- **One doc = one domain.** Split when a doc exceeds ~200 lines.
- **Keep the index in sync.** Every doc has a row in [`00_index.md`](00_index.md).
- **ASCII layout maps** for anything with a non-obvious flow.
- Documentation language follows `doc_language` in [`sdd.config.md`](../sdd.config.md).
