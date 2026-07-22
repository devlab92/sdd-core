---
name: security-check
description: Secrets and sensitive-data audit checklist. Use before every commit and whenever touching auth, config, env vars, logging, or external inputs.
---

# Skill: Security Check

> A fast, checklist-driven audit. Ideal to delegate to a sub-agent (see `subagent-orchestration`).
> Run before every commit and whenever touching auth, config, I/O boundaries, or logging.

## Secrets & config
- [ ] No `.env` or real secret is staged/committed. Only `.env.example` with `***` placeholders.
- [ ] No hard-coded API keys, tokens, passwords, or connection strings.
- [ ] Secrets come from env/secret manager, referenced in **one** centralized config module.

## Logging & output
- [ ] No secrets, tokens, or PII in logs, error messages, or telemetry.
- [ ] Sensitive values masked as `***` in docs and sample output.

## Input & boundaries
- [ ] All external input (user, network, files) is validated at the boundary.
- [ ] Queries are parameterized — no string-built SQL / command injection surface.
- [ ] Output is encoded/escaped for its sink (HTML, shell, SQL) to prevent injection/XSS.

## AuthN / AuthZ
- [ ] Every protected route/action checks authentication **and** authorization.
- [ ] No security decision relies on client-side checks alone.

## Dependencies
- [ ] No known-vulnerable dependencies introduced (`npm audit` / `pip-audit` / equivalent).
- [ ] New dependencies are reputable and actually needed.

## On finding an issue
- **In scope of the task** → fix now.
- **Out of scope** → register in `sdd_summary/40_further_tasks.md` as **🔴 P1** and flag to the human.
