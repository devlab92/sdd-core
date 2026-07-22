# 31_version_history.md — Version History & Commit Rules

> The human-readable narrative of how the project evolved. Pairs with the machine-oriented
> [`CHANGELOG.md`](../CHANGELOG.md) at the repo root.

---

## Conventional Commits (required)

Format: `type(scope): subject`

| Type | Meaning | SemVer bump |
|------|---------|-------------|
| `feat` | New feature | **MINOR** |
| `fix` | Bug fix | **PATCH** |
| `refactor` | Code change, no behavior change | PATCH |
| `perf` | Performance improvement | PATCH |
| `docs` | Documentation only | — |
| `test` | Tests only | — |
| `chore` | Tooling / deps / config | PATCH |
| `ci` | CI/CD changes | — |
| `build` | Build system | — |

**Breaking change:** add `!` after type (`feat!:`) or a `BREAKING CHANGE:` footer → **MAJOR**.

Examples:
```
feat(orders): add status filter to order listing
fix(webhook): stop infinite loop on malformed payload
refactor!: rename authService.login → authService.authenticate
```

---

## Release history

> One row per released version. Newest at the top. Mirrors `CHANGELOG.md` headings.

| Version | Date | Highlights |
|---------|------|------------|
| `0.1.0` | YYYY-MM-DD | Initial sdd-core installation |
