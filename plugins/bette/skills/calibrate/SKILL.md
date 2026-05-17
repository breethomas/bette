---
name: calibrate
description: Post-launch AI feature calibration workflow. Document error patterns, review eval performance, and decide on agency promotion. Based on CC/CD framework for continuous calibration of AI products.
---

# Calibrate

Load these into context before responding:

- `frameworks/ai-era-practices/continuous-calibration.md` — CC/CD framework
- `thought-leaders/lenny-rachitsky.md` — Lenny's coverage of CC/CD

Help the user run a post-launch calibration on an AI feature. They may be documenting error patterns, reviewing eval performance against production, or deciding whether to promote agency. Adapt to what they need.

## When to load adjacent context

- The user is planning v1→v2→v3 promotion → also load context from `/agency-ladder` skill
- Eval quality is the question → also load `frameworks/ai/ai-evals.md`
- Cost/latency is changing the calculus → also load `frameworks/ai-era-practices/ai-unit-economics.md`

## Avoid

- Treating calibration as a one-time exercise — the CC framing is "continuous"
- Promoting agency without explicit eval and production evidence
