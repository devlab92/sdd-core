---
name: ai-spec-writing
description: Optional skill for projects that build AI/LLM features. Guides prompt architecture, tool/function design, evals, and guardrails. Use only when the project ships AI-powered functionality.
---

# Skill: AI Spec Writing (optional)

> Load this **only** for projects that build AI/LLM-powered features. It adds prompt- and
> agent-architecture discipline on top of the normal spec.

## When it applies
The project ships: a chatbot/assistant, RAG, an agent/tool-runner, an LLM-as-judge, content
generation, classification/extraction over natural language, or similar.

## Extra spec sections (add to the 6-element spec)

1. **Task definition** — the exact job the model does, with 2–3 input→output examples.
2. **Prompt architecture** — system vs. user roles; where instructions, context, and data go.
   Keep instructions stable and cacheable; put volatile data last.
3. **Tools / functions** — for each: name, purpose, typed input schema, output shape, failure mode.
4. **Context strategy** — what's retrieved/loaded, ordering, and the token budget.
5. **Guardrails** — refusal conditions, input/output validation, PII handling, injection defense.
6. **Evaluation** — a small eval set with expected outputs; how regressions are caught.

## Principles
- **Deterministic scaffolding, probabilistic core.** Validate/parse model output; never trust it raw.
- **Fail closed.** On low confidence or invalid output, degrade safely — don't guess.
- **Version prompts** like code; record changes in `lessons_learned.md`.
- **Measure before tuning.** No prompt change without an eval to prove it helped.

## Provider notes
Model IDs, pricing, context limits, and caching differ per provider — confirm against current
provider docs rather than from memory before committing to a model or budget.
