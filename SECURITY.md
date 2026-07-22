# Security Policy

## Reporting a vulnerability

**Do not open a public issue for security vulnerabilities.**

Report privately via one of:
- GitHub **Security Advisories** → "Report a vulnerability" (preferred).
- Email the maintainer listed in `.github/CODEOWNERS`.

Please include:
- A description of the issue and its impact.
- Steps to reproduce (proof of concept if possible).
- Affected version/commit.

You can expect an acknowledgement within **72 hours** and a status update within **7 days**.
Please give us a reasonable window to fix before public disclosure.

## Scope

sdd-core is a documentation/template framework — it ships no runtime service. The most relevant
risks are in the **CI/CD workflows** (`.github/workflows/`) and in guidance that projects adopt.

## Secret-handling rules (enforced by the framework)

- Never commit `.env` or real secrets — only `.env.example` with `***` placeholders.
- Never log secrets, tokens, or PII.
- See [`.agents/skills/security-check/SKILL.md`](.agents/skills/security-check/SKILL.md).

## Supported versions

The latest `main` and the most recent tagged release receive security fixes.
