# Agent Workflow Design

**Category:** AI-Era Practices
**Anchor sources:** Anthropic Engineering — "Building agents with the Claude Agent SDK," "How we built our multi-agent research system," "Effective context engineering for AI agents"; Aakash Gupta — "Building multi-agent systems will be a must-have PM skill in 2026"
**Last Updated:** May 2026

## Headline

Most PM problems don't need an agent. They need a single AI call with the right context. Agents earn their cost when the work requires multi-step reasoning, tool use across boundaries, or parallel exploration of a problem space — and even then, the design decisions matter more than the model choice.

This framework names the patterns, the tradeoffs, and the decision points PMs face when designing agentic workflows.

## The first question: do you actually need an agent?

Aakash Gupta's framing is the right starting point: **the core PM skill in 2026 is knowing when to use an agent vs. a simpler AI-node workflow.** Most teams reach for agents too early. They build orchestrators for problems a single prompt could solve, then debate model selection while their evals tell them the problem isn't model capability — it's task design.

Use a single AI call when:
- The work fits in one round-trip (input in, output out)
- Tool use is bounded (one or two calls, deterministic)
- The output structure is known up front
- You don't need the model to plan before executing

Use an agent when:
- The work requires iterative reasoning (read result, decide next step)
- Tool use is open-ended (the model picks which tools and when)
- Sub-problems require their own context windows
- Parallel exploration would compress wall-clock time

Use multi-agent when:
- The work decomposes cleanly into independent strands
- Each strand benefits from its own clean context window
- The orchestrator can verify worker outputs without re-doing the work

The cost asymmetry matters: Anthropic's multi-agent research system used **~15× more tokens than equivalent chat**. It outperformed single-agent by ~90% on the right tasks. On the wrong tasks, it just burns money.

## The three patterns

### Pattern 1: Single AI call (no agent)

```
[Context + question] → [Single model call] → [Output]
```

The boring answer. Often the right one. Cheap, fast, easy to evaluate. Use this until you have evidence it's insufficient.

### Pattern 2: Single agent with tool use

```
[Context + objective] → [Agent loop: reason, call tool, observe, repeat] → [Output]
```

One model running an agent loop. Picks tools, observes results, decides next step. This is what Claude Code is doing when it reads files, runs grep, edits code. Most workflows live here.

When to choose this:
- The work needs multi-step reasoning but doesn't decompose into independent strands
- Tools are heterogeneous (read file, search web, call API) and the right sequence isn't knowable up front
- Context fits in one agent's working memory

### Pattern 3: Multi-agent (orchestrator-worker)

```
[Objective] → [Lead agent decomposes, plans, saves plan]
              → [Sub-agent A] [Sub-agent B] [Sub-agent C] (parallel)
              → [Lead agent synthesizes results]
              → [Output]
```

The pattern Anthropic uses for their multi-agent research system. Lead agent (typically larger model, e.g., Opus) plans and orchestrates. Sub-agents (typically smaller models, e.g., Sonnet) execute scoped tasks in parallel with isolated context windows.

When to choose this:
- Independent strands of work that don't need to coordinate mid-flight
- Parallel research, parallel analysis, parallel verification
- Token cost is justified by wall-clock compression or accuracy lift

When NOT to choose this:
- Tightly-coupled tasks (each step depends on the previous)
- The cost asymmetry isn't justified by accuracy or latency wins
- You haven't first measured what single-agent does on the same task

## Sub-agent specification (the load-bearing skill)

Anthropic's most repeated lesson from the multi-agent research system: **underspecified sub-agents duplicate or skip work.** Specifying a sub-agent well is the difference between a 90% accuracy lift and a 15× token bill with no improvement.

A sub-agent spec needs four things:

1. **Objective** — what is this sub-agent trying to accomplish, in one sentence? Sharp and bounded. "Research competitor pricing in [space]" — not "do research."
2. **Output format** — what shape does the result take? Structured markdown? JSON? A specific schema? The orchestrator will need to consume it; tell it how.
3. **Tool and source guidance** — which tools should it use, which sources should it prefer, which should it avoid? Don't make the sub-agent re-derive your search strategy.
4. **Clear boundaries** — what is the sub-agent explicitly NOT doing? Where does its scope end and the orchestrator's begin?

If a PM is designing a multi-agent workflow, the work is largely in writing these specs cleanly. Model choice, framework choice, infrastructure choice — all downstream of whether the specs are clean.

## Memory, context, and the attention budget

From Anthropic's "Effective context engineering for AI agents": context is a scarce attention budget, not a free resource. As workflows grow, you have three techniques to keep the budget intact:

1. **Compaction** — summarizing prior history into a compact representation. Used when conversation grows past a useful length.
2. **Structured note-taking** — sub-agents and orchestrators write to external memory files instead of keeping everything in-window. The plan goes in a file. Intermediate results go in files. Context window stays clean.
3. **Multi-agent architectures** — specialized sub-agents each get a clean window. The orchestrator never sees the full sub-agent transcript; only its condensed output.

These techniques compose. A multi-agent workflow with sub-agents writing structured notes and the orchestrator using compaction has a much higher effective ceiling than any single technique alone.

## When multi-agent is the wrong answer

Push back when:

- **The accuracy lift is unproven.** Run the single-agent baseline first. If it's good enough, ship that. Multi-agent is a 15× tax that needs to earn its keep.
- **The tasks are coupled.** If sub-agent B needs the result of sub-agent A to start, you're not running parallel agents — you're running a sequential pipeline. A single agent does this with less overhead.
- **The orchestrator can't verify worker output.** If the only way to know whether a sub-agent did good work is to redo the work, you've built a fragile system.
- **The team can't evaluate it.** Multi-agent systems are harder to debug, harder to evaluate, and harder to improve. If you don't have the eval discipline, scope down.

## Common failure modes

- **Sub-agent drift.** Worker spec was ambiguous, two sub-agents did overlapping work, one missed its strand entirely.
- **Orchestrator over-trust.** Lead agent treated sub-agent output as ground truth when it should have spot-checked.
- **Context bleed.** Orchestrator passed too much of its own context into sub-agents, contaminating the clean-window benefit.
- **Tool grab-bag.** Sub-agent had access to too many tools, picked the wrong ones, blew its budget on irrelevant calls.
- **Eval void.** Workflow ships without an eval suite. First production failure is a mystery; second is the same mystery louder.
- **Premature optimization.** Multi-agent design before the single-agent baseline existed.

## A PM decision tree

```
Is this a one-shot task?
├── Yes → single AI call
└── No → does the work decompose into independent strands?
    ├── No → single agent with tool use
    └── Yes → does the accuracy/latency win justify ~15× token cost?
        ├── No → single agent, or split into discrete calls
        └── Yes → multi-agent orchestrator-worker
            └── Are sub-agent specs sharp (objective, format, tools, boundaries)?
                ├── No → fix specs before building anything
                └── Yes → build, with an eval suite
```

## When to use this framework

- Designing a new AI feature and choosing the architecture
- Diagnosing why an existing agentic workflow is unreliable or expensive
- Writing the spec for a sub-agent (the load-bearing artifact most teams skip)
- Pushing back on "let's make it multi-agent" when single-agent hasn't been measured

## Resources

- [Building agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) — Anthropic's canonical engineering post on the agent loop
- [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) — orchestrator-worker pattern in production
- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — compaction, structured notes, attention budget
- [Claude Code Advanced Patterns: Subagents, MCP, and Scaling](https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents,%20MCP,%20and%20Scaling%20to%20Real%20Codebases.pdf) — Anthropic PDF with concrete patterns
- Aakash Gupta — "Building multi-agent systems will be a must-have PM skill in 2026" ([Medium](https://aakashgupta.medium.com/building-multi-agent-systems-will-be-a-must-have-pm-skill-in-2026-30e52fd732cb))
- Aakash Gupta — "AI Agents for PMs: The Ultimate Guide in 2026" ([Product Growth](https://www.news.aakashg.com/p/ai-agents-pms))
