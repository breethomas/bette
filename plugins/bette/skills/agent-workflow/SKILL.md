---
name: agent-workflow
description: Design AI agent workflows — single agent vs multi-agent vs single-call, orchestrator-worker patterns, sub-agent specification, context engineering. Anchored to Anthropic's Claude Agent SDK guidance and Aakash Gupta's multi-agent PM framing. Use when scoping a new AI feature, deciding architecture for an agentic workflow, debugging an unreliable agent system, or writing sub-agent specs.
---

# Agent Workflow Design

Load these into context before responding:

- `../../frameworks/ai-era-practices/agent-workflow-design.md` — canonical framework (single AI call vs single agent vs multi-agent, orchestrator-worker pattern, sub-agent specification, cost tradeoffs)
- `../../thought-leaders/boris-cherny.md` — Claude Code lead's perspective on agent design
- `../../thought-leaders/aakash-gupta.md` — Aakash's PM-shaped framing on when to use agents

Help the user design or audit an agent workflow. They may be choosing an architecture for a new AI feature, debugging an existing agentic system, writing sub-agent specs, or pushing back on "let's make it multi-agent" before single-agent has been measured. Adapt to where they are.

## When to load adjacent context

- Cost is the constraint → also load `../../frameworks/ai-era-practices/ai-unit-economics.md`
- Evals come up → also load `../../frameworks/ai/ai-evals.md`
- Memory and context architecture matters → also load `../../frameworks/ai-era-practices/pm-memory-architecture.md`

## Avoid

- Recommending multi-agent without confirming single-agent has been measured
- Treating model selection as the primary lever (sub-agent specification is more load-bearing)
- Hand-waving "use sub-agents" without specifying objective, output format, tool guidance, and boundaries
