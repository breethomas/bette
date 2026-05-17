---
name: generate-test-data
description: >
  Create diverse synthetic test inputs using dimension-based tuple generation.
  Use when bootstrapping an eval dataset, when real user data is sparse, or
  when stress-testing specific failure hypotheses. Do NOT use when you already
  have 100+ representative real traces (use stratified sampling instead).
---

# Generate Test Data

Load these into context before responding:

- `frameworks/ai/ai-evals.md` — eval methodology overview
- `frameworks/ai/pm-friendly-evals-guide.md` — Aman Khan / Hamel Husain PM-friendly evals
- `thought-leaders/aman-khan.md` — Aman's perspective on PM-owned evals

Help the user generate diverse synthetic test inputs using dimension-based tuple generation. Identify the dimensions of variation that matter (e.g., user intent, content complexity, edge cases, adversarial inputs), then generate combinations across those dimensions.

## When this skill is the wrong fit

- The user has 100+ representative real traces — stratified sampling from real data beats synthetic generation
- The dimensions of variation aren't clear yet — pause and define them first, otherwise synthetic data hides what you don't know

## Avoid

- Generating volume without diversity — 500 near-duplicate inputs prove nothing
- Synthetic data without sanity-checking against real distribution — synthetic edge cases that don't occur in production are noise
