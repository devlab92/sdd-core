# CODING_PHILOSOPHY.md — The 4-Layer Thinking Model

> The mandatory mental model every AI agent applies **before writing code**, always in order.
> This creates a consistent engineering culture across every AI provider (cloud, local, hybrid).
> Layer N may not begin until Layer N−1 is satisfied. **Research (Layer 4) is never a starting point.**

---

## Layer 1 — THINK FIRST _(mandatory before any code)_

- Understand the problem **completely** before proposing a solution.
- Identify edge cases and error states up front.
- Choose the **simplest** solution that fully solves the problem.
- Prioritize **maintainability over cleverness**.

> If you cannot state the problem and its edge cases in plain language, you are not ready to code.

---

## Layer 2 — STRUCTURAL PATTERNS _(how to organize)_

- **Single Responsibility Principle** — one reason to change per unit.
- **Pure functions** wherever possible — same input, same output, no hidden side effects.
- **Early returns** to reduce nesting.
- **Descriptive names > comments** — the code should read as intent.
- **DRY, but no premature abstraction** — duplicate twice before you generalize.

---

## Layer 3 — SCALABILITY _(build for the future)_

- **Unique identification on everything** — stable IDs and keys.
- **Semantic HTML IDs + BEM classes** on all interactive elements (frontend).
- **Component-first frontend** — build/extend the reusable library *before* writing inline code.
  Inline one-off UI is the exception, never the default.
- **Separation by layers** — route → controller → service → repository.
- **Centralized config** — env vars in one place, never scattered literals.
- **Typed error handling at boundaries.**
- **Input validation at the frontier** — never trust data crossing a boundary.
- **Naming:** `camelCase` functions, `PascalCase` types, `snake_case` files.

> **Design note:** The most common frontend failure is inconsistent component reuse and visual
> disharmony. Layer 3 fixes this at the root: *component library first, inline code never.*

---

## Layer 4 — RESEARCH _(only after Layers 1–3)_

- If the **standard solution works, use it.** Full stop.
- Seek alternatives **only** when the standard is genuinely insufficient.
- **Document WHY** the alternative was chosen (in the plan and/or `lessons_learned.md`).
- Weigh **Efficiency vs. Token Cost** before committing to a non-standard path.

---

## Quick self-check before you write code

- [ ] I can state the problem and its edge cases plainly. _(L1)_
- [ ] Each unit I'm about to write has a single responsibility. _(L2)_
- [ ] I'm reusing/extending existing components, not duplicating them. _(L3)_
- [ ] I'm using the standard solution unless I've documented why not. _(L4)_
