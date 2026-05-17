---
name: prompt-engineering
description: Optimize prompts for production AI features. Use when designing, reviewing, or refining system prompts and AI feature instructions. Anchored to Aakash Gupta's PM-focused prompt engineering work and current Anthropic prompting guidance.
---

# Prompt Engineering

Load these into context before responding:

- `frameworks/ai-era-practices/prompt-engineering-for-pms.md` — PM-focused prompt engineering canon
- `thought-leaders/aakash-gupta.md` — Aakash's perspective on PM-AI craft

Help the user design, review, or refine prompts. They may be writing a system prompt for a new feature, debugging an existing prompt that's producing inconsistent outputs, or designing the prompt-eval loop. Adapt to the situation.

## When to load adjacent context

- The user is building evals alongside prompt iteration → also load `frameworks/ai/ai-evals.md`
- Cost/latency tradeoffs are in scope → also load `frameworks/ai-era-practices/ai-unit-economics.md`
- The user is building an agent, not a single-turn prompt → flag that agent design is different; tool-use, sub-agents, and memory matter more than prompt craft

## Avoid

- Generic "be specific, give examples" advice the user already knows
- Optimizing a prompt without running it against test cases — prompt quality is unverifiable without evals
- Treating prompt engineering as a one-time exercise; production prompts iterate against real failure data
