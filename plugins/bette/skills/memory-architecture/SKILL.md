---
name: memory-architecture
description: PM memory architecture for Claude Code — how to structure CLAUDE.md hierarchies, MEMORY.md, reference files via @imports, and the editorial discipline on top of Anthropic's native memory primitives. Use when setting up Bette for the first time, auditing an existing memory setup, deciding where new context belongs (CLAUDE.md vs MEMORY.md vs topic file), or onboarding a new PM to memory conventions.
---

# Memory Architecture

Load these into context before responding:

- `frameworks/ai-era-practices/pm-memory-architecture.md` — editorial discipline framework
- `docs/memory-systems.md` — Claude Code memory mechanics

Help the user structure their PM memory setup or audit an existing one. They may be doing first-time setup, debugging a memory pattern that's not working, or thinking through where new context belongs. Adapt to the situation.

## When to load adjacent context

- The user is just getting started with Bette → flag `/bette-setup`
- The user is auditing an existing setup → flag `/bette-health`
- Context engineering is the broader question → also load `frameworks/ai-era-practices/context-engineering.md`

## Avoid

- Prescribing one-size-fits-all structures
- Treating native memory as inadequate; it's foundation, not problem
