# Contributing to sdd-core

Thanks for helping improve sdd-core. This project **practices what it preaches** — contributions
follow the same protocol the framework enforces.

## Workflow

1. **Open an issue first** for anything beyond a typo (use the templates in `.github/ISSUE_TEMPLATE/`).
2. **Branch** from `main`: `feat/<slug>`, `fix/<slug>`, or `docs/<slug>`.
3. **Write a plan** for non-trivial changes (`plans/_TEMPLATE.plan.md`) and get it approved
   before implementing — yes, we dogfood the Quality Gate.
4. **Commit** using [Conventional Commits](#commit-format).
5. **Update docs + CHANGELOG** as part of the change (Post-Task Protocol).
6. **Open a PR** using the checklist in `.github/PULL_REQUEST_TEMPLATE.md`.

## Commit format

```
type(scope): subject
```
`feat` → minor · `fix`/`chore`/`refactor`/`perf` → patch · `feat!` or `BREAKING CHANGE:` → major.
Full table: [`sdd_summary/31_version_history.md`](sdd_summary/31_version_history.md).

## Branching strategy

- `main` — always releasable.
- Short-lived feature/fix branches → PR → squash merge.

## Requirements before requesting review

- [ ] Change follows `CODING_PHILOSOPHY.md` (4 layers).
- [ ] `AGENTS.md` remains the single source of truth (mirrors not duplicated).
- [ ] Markdown links are valid (relative paths resolve).
- [ ] Docs and `CHANGELOG.md` updated.
- [ ] Conventional commit messages.

## Local hooks (optional but recommended)

For projects that install sdd-core, we recommend **Husky + commitlint + lint-staged**:
```bash
npm i -D husky @commitlint/{cli,config-conventional} lint-staged
npx husky init
echo 'npx --no -- commitlint --edit "$1"' > .husky/commit-msg
```
See `BOOTSTRAP_PROMPT.md` for setup guidance tailored to the detected stack.

## Code of conduct

Be kind, be precise, assume good faith. Use `they/them` when a contributor's pronouns are unknown.
