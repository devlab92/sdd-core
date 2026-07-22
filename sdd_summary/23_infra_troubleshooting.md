# 23_infra_troubleshooting.md — Incident Log

> A structured record of infrastructure and operational incidents, so the same fire is never
> fought twice. Every incident follows **Symptom → Cause → Fix → Prevention**.
>
> **Append only.** Newest at the top.

---

## Entry template

```markdown
### YYYY-MM-DD — <short incident title>
**Severity:** low | medium | high | critical
**Symptom:** what was observed (errors, metrics, user reports).
**Cause:** the confirmed root cause (not the guess).
**Fix:** the exact steps/commands that resolved it.
**Prevention:** the change that stops it recurring (alert, test, guardrail, doc).
```

---

## Log

<!-- New incidents go here, newest first. -->

### YYYY-MM-DD — (example) Template entry
**Severity:** low
**Symptom:** _describe what you saw._
**Cause:** _the confirmed root cause._
**Fix:** _the exact resolution._
**Prevention:** _what now prevents recurrence._
