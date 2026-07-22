<div align="center">

# 🧭 sdd-core

**A drop-in operating system for AI-assisted development.**

Spec-Driven Development · Agent Orchestration · Auto-Learning Memory · Token Economy

_Stack-agnostic · Provider-agnostic · One paste to activate_

![status](https://img.shields.io/badge/status-active-brightgreen)
![license](https://img.shields.io/badge/license-MIT-blue)
![AI](https://img.shields.io/badge/AI-Claude%20%7C%20Gemini%20%7C%20Cursor%20%7C%20Copilot-8A2BE2)
![docs](https://img.shields.io/badge/docs-first-orange)

</div>

---

## What is this?

`sdd-core` is a small set of Markdown files you drop into the root of **any** project. From that
moment, **every AI agent** that touches the repo — Claude, Gemini, Cursor, Copilot, or a local
model — reads the same rules and is forced to follow the **same order of thinking** and the **same
quality pipeline**, every time.

It's not a library and it has no runtime. It's the **culture and guardrails** that turn an AI from
an improvising code generator into a disciplined engineer.

## The problem it solves

Coding with AI fails in three predictable ways. sdd-core installs a mechanism against each:

| Chronic failure | The mechanism that stops it |
|-----------------|-----------------------------|
| 🧩 **AI improvises** decisions a human should make | **Clarification Phase** + a hard **Approval** stop before any code |
| 📉 **Documentation rots** within weeks | **Forcing function** after every task: `📄 sdd_summary/ outdated?` |
| 🕳️ **Tech debt grows invisibly** | **Refactor-or-Register** rule with a hard threshold (≤3 files fix now, else register) |

## The two engines

### 1. The 4-Layer Thinking Model — *what to think, in order*
Every agent thinks in this sequence before writing code (never skipping, never starting at 4):

```
1. THINK FIRST   →   2. STRUCTURE   →   3. SCALE   →   4. RESEARCH
   problem &            SRP, pure          IDs, components   standard first;
   edge cases           functions,         first, layered    alternatives only
   simplest sol.        early returns      separation        if justified
```
→ [`CODING_PHILOSOPHY.md`](CODING_PHILOSOPHY.md)

### 2. The 6-Stage Quality Gate — *how to execute, safely*
Every non-trivial change flows through this pipeline. **Approval** and **Deploy** are the only two
hard stops; everything between runs autonomously.

```
1 PRE-AUDIT → 2 SPEC → 3 APPROVAL 🔒 → 4 IMPLEMENT → 5 POST-AUDIT → 6 GATE
load context   design    human locks     track tasks    lint/test      doc + CHANGELOG
check debt     6 elems    the plan        follow rules   verify build   + commit + version
```
→ [`.agents/skills/quality-gate/SKILL.md`](.agents/skills/quality-gate/SKILL.md)

---

## Quickstart

```bash
# 1. Get the files into your project root (new or existing)
#    Option A — as a template: click "Use this template" on GitHub
#    Option B — copy the files in manually
#    Option C — degit (no git history):
npx degit your-github-handle/sdd-core ./my-project

# 2. Open your AI coding session (Claude Code / Cursor / Gemini / ...)

# 3. Paste the contents of BOOTSTRAP_PROMPT.md as your first message
```

The AI then:
1. Reads the framework, 2. detects your stack, 3. interviews you, 4. shows a setup plan for
**your approval**, 5. customizes everything, 6. creates initial docs and the first commit.

→ [`BOOTSTRAP_PROMPT.md`](BOOTSTRAP_PROMPT.md)

---

## How it's organized — 3 layers

```
INTELLIGENCE  (the brain)   AGENTS.md · CODING_PHILOSOPHY.md · sdd.config.md · sdd_summary/
     ↓
SKILLS        (the hands)   .agents/skills/* · plans/
     ↓
DESIGN SYSTEM (the face)    DESIGN.md.template · 44_frontend_checklist.md   (frontend only)
```
→ [`sdd_summary/00_workflow_guide.md`](sdd_summary/00_workflow_guide.md)

## File map

```
sdd-core/
├── README.md                    ← you are here
├── AGENTS.md                    ← canonical rules (single source of truth)
├── CLAUDE.md · GEMINI.md · .cursorrules   ← thin mirrors → AGENTS.md
├── CODING_PHILOSOPHY.md         ← the 4-layer thinking model
├── sdd.config.md                ← operating mode (economy | balanced | full)
├── BOOTSTRAP_PROMPT.md          ← the one-paste activation prompt
├── CHANGELOG.md                 ← AI-maintained living memory (Keep a Changelog)
├── DESIGN.md.template           ← universal design-system skeleton
│
├── sdd_summary/                 ← living knowledge base + memory
│   ├── 00_index.md              ← load this first, always
│   ├── 00_how_to_plan.md        ← planning, clarification, "dumbest AI" test, autonomy
│   ├── 00_skill_documenting.md  ← how to keep docs alive
│   ├── 00_subagent_delegation.md← delegation + context hygiene
│   ├── 00_workflow_guide.md     ← the 3-layer architecture
│   ├── lessons_learned.md       ← cross-session auto-learning
│   ├── 23_infra_troubleshooting.md · 31_version_history.md
│   ├── 40_further_tasks.md      ← tech-debt register
│   └── 44_frontend_checklist.md
│
├── plans/                       ← execution contracts
│   ├── active/ · done/          ← DRAFT → APPROVED → IN_PROGRESS → DONE
│   └── _TEMPLATE.plan.md · _TEMPLATE.clarification.md
│
├── .agents/skills/              ← the 7 skills
│   ├── quality-gate/ · spec-first/ · code-standards/ · security-check/
│   ├── subagent-orchestration/ · handoff/ · ai-spec-writing/ (optional)
│
├── .github/                     ← CI, release, issue/PR templates, CODEOWNERS, dependabot
│   └── workflows/ci.yml · release.yml
│
├── .cursor/rules/               ← file-scoped Cursor rules (token savings)
├── .editorconfig · .gitignore · .env.example
├── CONTRIBUTING.md · SECURITY.md · LICENSE
```

---

## Configuration — one file, three modes

[`sdd.config.md`](sdd.config.md) tunes how the AI behaves. A local 8K model in `economy` mode and
Claude in `full` mode both produce good results **within their constraints**.

| Behavior | Economy 🟢 | Balanced 🟡 | Full 🔴 |
|----------|-----------|------------|--------|
| Research alternatives | Skip | 1 | 3+ |
| Documentation | Minimal | Standard | Extensive |
| Sub-agents | Aggressive | Moderate | Minimal |
| Plans required | Multi-layer only | > 3 files | Everything non-trivial |
| Responses | Terse | Balanced | Detailed |

## Multi-AI interoperability

`AGENTS.md` is the **single source of truth**. `CLAUDE.md`, `GEMINI.md`, and `.cursorrules` are thin
mirrors that point to it — so switching or mixing AI tools never changes the rules.

## Versioning

Hybrid by design: the AI maintains [`CHANGELOG.md`](CHANGELOG.md) locally after every commit
(readable memory), and GitHub Actions publishes official releases. Use GitHub or don't — the
CHANGELOG is always the source of truth.

`fix:`/`chore:` → **patch** · `feat:` → **minor** · `BREAKING CHANGE`/`!` → **major**

---

## FAQ

**Do I need GitHub?** No. Everything works locally; GitHub Actions are optional bonuses.

**Does it lock me to one AI?** No. It's designed for the opposite — consistency *across* AIs.

**Isn't ~40 files overwhelming?** The bootstrap creates only what your project needs. A backend-only
service skips the design system; a provider without sub-agents disables that path.

**Can I use it on an existing project?** Yes — bootstrap scans existing code and documents it.

## Contributing

sdd-core dogfoods its own process. See [`CONTRIBUTING.md`](CONTRIBUTING.md). Security reports:
[`SECURITY.md`](SECURITY.md).

## License

[MIT](LICENSE) © 2026 Luiz Augusto Barbieri
