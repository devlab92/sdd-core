# 00_workflow_guide.md — The 3-Layer Architecture

> A map of how sdd-core is organized, so a new agent understands the system in one read.
> Everything in the framework belongs to one of three layers.

---

```
┌──────────────────────────────────────────────────────────────┐
│  LAYER 1 — INTELLIGENCE  (the brain: what to think, in order)  │
│                                                                │
│   AGENTS.md ............. canonical rules (single source)      │
│   CODING_PHILOSOPHY.md .. the 4-layer thinking model           │
│   sdd.config.md ......... operating mode (economy/balanced/full)│
│   CLAUDE.md / GEMINI.md / .cursorrules .. thin mirrors → AGENTS │
│   sdd_summary/ .......... living knowledge base + memory        │
└──────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────┐
│  LAYER 2 — SKILLS  (the hands: how to execute reliably)        │
│                                                                │
│   .agents/skills/quality-gate ...... the 6-stage pipeline      │
│   .agents/skills/spec-first ........ the 6-element spec         │
│   .agents/skills/code-standards .... refactor-or-register       │
│   .agents/skills/security-check .... secrets & data audit       │
│   .agents/skills/subagent-orchestration .. delegation          │
│   .agents/skills/handoff ........... multi-agent state machine  │
│   plans/ ........................... the execution contracts    │
└──────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────┐
│  LAYER 3 — DESIGN SYSTEM  (the face: how it looks & feels)     │
│                                                                │
│   DESIGN.md.template .... semantic tokens, themes, WCAG, a11y   │
│   44_frontend_checklist.md .. pre-delivery UI gate             │
└──────────────────────────────────────────────────────────────┘
```

---

## How a task flows through the layers

1. **Intelligence** decides *what* and *in what order* (philosophy + config + rules).
2. **Skills** enforce *how* it gets done safely (quality gate → spec → approval → build).
3. **Design System** governs *how the result looks* (only for projects with a frontend).

## Reading order for a brand-new agent

1. `AGENTS.md`
2. `sdd.config.md`
3. `CODING_PHILOSOPHY.md`
4. `sdd_summary/00_index.md` → the relevant domain doc
5. The active plan in `plans/active/` (if any)
