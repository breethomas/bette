---
name: build-judge
description: >
  Build an LLM-as-Judge evaluator for one specific failure mode. Binary pass/fail
  only. Use when a failure mode requires interpretation (tone, faithfulness,
  relevance, completeness) and cannot be checked with code. Do NOT use when the
  failure can be checked with regex, schema validation, or execution tests.
  Do NOT use before completing error analysis (/upgrade-evals).
---

# Build Judge

Load these into context before responding:

- `../../frameworks/ai/ai-evals.md` — eval methodology overview
- `../../frameworks/ai/pm-friendly-evals-guide.md` — Aman Khan / Hamel Husain PM-friendly evals
- `../../thought-leaders/aman-khan.md` — Aman's perspective on PM-owned evals

Help the user build one LLM-as-Judge evaluator for one specific failure mode. Binary pass/fail. Anchor to the framework — don't reinvent the methodology.

## When this skill is the wrong fit

- The failure can be checked with code (regex, schema validation, execution test) — judge is overkill
- The user hasn't done error analysis yet — start with `/upgrade-evals` first
- The user wants a numeric score, not pass/fail — judges drift on scales

## Avoid

- Multiple judges for multiple failure modes in one pass — one judge per mode
- Trying to capture nuance in the judge prompt — keep it tight, iterate the prompt against labeled examples
