# Bette

> "Attempt the impossible in order to improve your work." — Bette Davis

A PM operating system built on [Claude Code](https://docs.anthropic.com/en/docs/claude-code). 57 skills, 7 autonomous agents, and 24 PM frameworks in one install.

Named after Bette Davis — who sued a studio because they wouldn't give her better roles.

---

## Who is this for?

Product managers using Claude Code who want more than ad hoc prompting. Bette gives you repeatable workflows for the work you actually do: strategic decisions, meeting prep, inbox triage, backlog management, AI evals, and spec writing.

You don't need to memorize commands. Just tell Claude what you need in plain English. Bette recognizes what you're asking for and activates the right workflow.

It's opinionated. It will ask for evidence, challenge fuzzy thinking, suggest prototypes over PRDs, and push you to talk to users.

---

## Install

In Claude Code, type:

```
/plugin marketplace add breethomas/bette
/plugin install bette@breethomas
```

Start a new session. Then just say: **"set me up"**

---

## Get Started

Two paths. Same system.

### "Set me up"

Say **"set me up"** or **"configure bette"** and choose guided setup. Bette asks about your role, team, and tools, then generates your entire context architecture:

- A preferences file (your working style, what you care about)
- Reference files (your people, your domains, your systems)
- Backlog, goals, and session management
- Automatic bootstrap so every session starts with context

Takes about 5 minutes. Gets you from zero to a working PM operating system.

### "I'll configure myself"

Say **"set me up"** and choose self-guided. You get the module map and docs. Enable what you want, configure your own setup, wire your own integrations.

---

## What does a session look like?

Morning:
```
catch me up
```
Bette triages your email and Slack saved items, surfaces action items, drafts replies, and updates your backlog.

Before a 1:1:
```
prep for my 1:1 with Sarah
```
Bette pulls context from your people file, recent meeting notes, and open issues. Builds a talk track with topics, questions, and follow-ups.

Working through a product decision:
```
let's think through the pricing change
```
Bette becomes a strategic sparring partner. Asks clarifying questions, applies frameworks, challenges assumptions, captures decisions.

End of day:
```
what should I focus on tomorrow?
```
Bette reads your backlog, checks your goals, and surfaces the top 3 things that matter.

Just talk to it. Bette figures out which workflow to run.

> **Power users:** Every skill also has a slash command (like `/bette:strategy-session`). Type `/skills` to see the full list. But you never have to use them.

---

## Skills (57)

### Think — frameworks that sharpen decisions (30)

Strategic sparring grounded in frameworks from Marty Cagan, Teresa Torres, Elena Verna, Brian Balfour, Ryan Singer, Hamel Husain, and more.

| Say this | What happens |
|----------|-------------|
| "let's think through [problem]" | Work through any product decision conversationally |
| "write a spec for [feature]" | Specs at the right depth — quick issues to full AI feature specs |
| "shape this work" | Shape Up methodology — appetite, solution, risks |
| "run four risks on [feature]" | Cagan's value/usability/feasibility/viability assessment |
| "set up evals for [AI feature]" | AI evaluation suite — first 20 test cases |
| "research competitors in [space]" | Systematic competitor analysis with parallel agents |
| "plan the agency ladder for [feature]" | v1 → v2 → v3 AI feature progression |
| "help me design the context architecture" | Layered context engineering for AI workflows |
| "write a PRD for [feature]" | PRDs with before/after examples |
| "build a judge for [AI feature]" | LLM-as-judge evaluation pipelines |

And 20 more. Type `/skills` to see everything.

### Operate — run your day without losing the plot (22)

Daily workflows for inbox triage, meeting prep, backlog management, and strategic synthesis.

| Say this | What happens |
|----------|-------------|
| "catch me up" | Triage email + Slack in one pass |
| "process my meetings" | Transcripts into action items, decisions, follow-ups |
| "prep for my meeting with [name]" | Talk track with topics, context, and questions |
| "process my backlog" | Categorize, prioritize, connect to goals |
| "what should I focus on today?" | Top 3 priorities tied to strategic outcomes |
| "weekly review" | What got done, what didn't, what's coming |
| "synthesize [meeting/transcript]" | Extract decisions and insights |

And 15 more. These work best with integrations (Slack, Gmail, Notion, Linear) but don't require them.

### Work — guardrails that keep quality high (3)

For PMs who code. Quality gates, test-first patterns, and session management.

| Say this | What happens |
|----------|-------------|
| "run quality gates" | Interactive pre-commit checklist |
| "write tests first" | Generate test suites before modifying code |
| "should I save and restart?" | Check if it's time for session notes |

### Architect — set up and maintain your foundation (2)

Context engineering — the infrastructure that makes everything else work.

| Say this | What happens |
|----------|-------------|
| "set me up" | First-use onboarding — generate your context architecture |
| "check my setup" | Audit against the maturity model |

---

## Agents

Seven specialized agents handle research and analysis autonomously. Skills invoke these as needed, or you can ask for them directly.

| Agent | What It Does |
|-------|-------------|
| Project health checker | Single project deep-dive (On Track / At Risk / Stalled) |
| Linear workspace analyzer | Workspace health against Linear methodology |
| Team organization analyzer | Team conventions and patterns |
| Competitor researcher | Individual competitor analysis (runs in parallel) |
| AI cost analyzer | AI feature economics and viability |
| AI implementation auditor | Pre-launch readiness (6 dimensions) |
| Eval generator | Create AI test cases and evaluation frameworks |

---

## What else is in the box

Beyond skills and agents, Bette includes reference material that skills draw from automatically.

**24 PM frameworks** organized by discipline: discovery, planning, growth, execution, measurement, and AI-era practices. Includes continuous discovery, Shape Up, growth loops, LNO prioritization, AI unit economics, and more.

**15 thought leader profiles** capturing methodologies from Marty Cagan, Teresa Torres, Elena Verna, Brian Balfour, Boris Cherny, Ryan Singer, Chip Huyen, Lenny Rachitsky, and others. Skills reference these when applying frameworks.

**4 templates** for common PM artifacts: AI product specs, lightweight PRDs, Linear issues, and competitive analysis.

**Architecture docs and examples** covering context engineering patterns: how to structure your preferences file, reference files, memory systems, and context hygiene.

---

## Connecting Your Tools

Bette works on its own, but gets more powerful with integrations. These are optional — set them up when you're ready:

**Linear** (issue tracking):
```
claude mcp add linear
```

**Slack** (messaging):
Connect via Claude.ai settings → Integrations → Slack

**Gmail** (email):
Connect via Claude.ai settings → Integrations → Gmail

**Notion** (knowledge base):
Connect via Claude.ai settings → Integrations → Notion

Skills gracefully handle missing integrations — they'll tell you what to connect when needed.

---

## The Maturity Model

Bette includes a maturity model for AI-assisted PM work. Say **"check my setup"** to see where you are.

| Level | What It Looks Like |
|-------|-------------------|
| **Ad Hoc** | No context. Every session starts cold. |
| **Planned** | Reference files exist. The AI starts warm. |
| **Systematic** | Skills define quality standards. The system knows your patterns. |
| **Optimized** | You steer, the system drives. It knows you. |

Most people start at Ad Hoc. Setup gets you to Planned in five minutes. Systematic comes from using the system daily. Optimized is where the system needs less instruction from you, not more — because your preferences are so well-captured.

---

## Architecture and Design

The architecture docs are included in the plugin under `docs/`. For deep dives into the design philosophy, the companion repos break out each component:

- **[bette-architect](https://github.com/breethomas/bette-architect)** — Context engineering: preferences design, reference files, memory systems, skill architecture
- **[bette-think](https://github.com/breethomas/bette-think)** — PM frameworks and thought leader profiles
- **[bette-work](https://github.com/breethomas/bette-work)** — Quality principles, maturity model, session management
- **[bette-os](https://github.com/breethomas/bette-os)** — Daily workflow patterns and operational design

---

## Companion Plugins

Bette handles PM workflows. For codebase comprehension — understanding architecture, dependencies, and what a change impacts without reading code — pair it with:

- **[Understand Anything](https://github.com/Lum1104/Understand-Anything)** — Turns any codebase into an interactive knowledge graph. Built for product and design teams who need to understand systems without reading source code.

---

## Contributing

Bette is open source. PRs welcome — especially new skills, framework additions, and workflow improvements.

Each skill is a single markdown file with a header and instructions. Look at any existing skill for the pattern. New skills should follow the "lean" pattern: triggers, context requirements, quality standards, output format. Trust the model for execution.

---

MIT License. Built with Claude Code by [Bree Thomas](https://github.com/breethomas).

Fasten your seatbelts.
