# Bette

> "Attempt the impossible in order to improve your work." — Bette Davis

One plugin. One install. A PM operating system built on Claude Code.

Named after Bette Davis — who sued a studio because they wouldn't give her better roles.

---

## Install

```
/plugin marketplace add breethomas/bette
/plugin install bette@breethomas
```

Start a new session. Run `/bette:bette-setup` to get started.

---

## Get Started

Two paths. Same system.

### "Set me up"

Run `/bette:bette-setup` and choose guided setup. Bette asks about your role, team, and tools, then generates your entire context architecture:

- Global CLAUDE.md (your preferences and working style)
- Project directory with reference files (people, domains, systems)
- Backlog, goals, and session management
- SessionStart hook for automatic bootstrap

Takes about 5 minutes. Gets you from zero to a working PM operating system.

### "I'll configure myself"

Run `/bette:bette-setup` and choose self-guided. You get the module map and docs. Enable what you want, configure your own CLAUDE.md, wire your own integrations.

---

## What's Inside

### Think — frameworks that sharpen decisions (30 skills)

Strategic sparring grounded in frameworks from Marty Cagan, Teresa Torres, Elena Verna, Brian Balfour, Ryan Singer, Hamel Husain, and more.

| Skill | What It Does |
|-------|-------------|
| `/bette:strategy-session` | Work through any product decision conversationally |
| `/bette:spec` | Write specs at the right depth — quick issues to full AI feature specs |
| `/bette:shape-up` | Shape work using Shape Up methodology |
| `/bette:four-risks` | Run Cagan's value/usability/feasibility/viability assessment |
| `/bette:start-evals` | Set up AI evals — first 20 test cases |
| `/bette:competitive-research` | Systematic competitor analysis with parallel agents |
| `/bette:agency-ladder` | Plan v1→v2→v3 AI feature agency progression |

And 23 more. Run `/skills` to see everything.

### Operate — run your day without losing the plot (23 skills)

Daily workflows for inbox triage, meeting prep, backlog management, and strategic synthesis.

| Skill | What It Does |
|-------|-------------|
| `/bette:catchup` | Catch up on all inbound — email + Slack in one pass |
| `/bette:digest` | Process daily meeting transcripts into action items |
| `/bette:prep-meeting` | Prep talk track for any meeting |
| `/bette:backlog` | Process and prioritize your backlog |
| `/bette:focus` | Surface today's top 3 priorities |
| `/bette:weekly-review` | Run weekly review |
| `/bette:synthesize` | Extract decisions and insights from transcripts |

And 16 more. These skills work best with MCP integrations (Slack, Gmail, Notion, Linear).

### Work — guardrails that keep quality high (3 skills)

For PMs who code. Quality gates, test-first patterns, and session management.

| Skill | What It Does |
|-------|-------------|
| `/bette:quality-gates` | Interactive pre-commit checklist |
| `/bette:test-first` | Generate test suites before modifying code |
| `/bette:session-check` | Check if it's time to save notes and restart |

### Architect — set up and maintain your foundation (2 skills)

Context engineering — the infrastructure that makes everything else work.

| Skill | What It Does |
|-------|-------------|
| `/bette:bette-setup` | First-use onboarding — generate your context architecture |
| `/bette:bette-health` | Audit your setup against the maturity model |

---

## Agents

Seven specialized agents handle research and analysis autonomously.

| Agent | What It Does |
|-------|-------------|
| `project-health-checker` | Single project deep-dive (On Track / At Risk / Stalled) |
| `linear-workspace-analyzer` | Workspace health against Linear methodology |
| `team-organization-analyzer` | Team conventions and patterns |
| `competitor-researcher` | Individual competitor analysis |
| `ai-cost-analyzer` | AI feature economics and viability |
| `ai-implementation-auditor` | Pre-launch readiness (6 dimensions) |
| `eval-generator` | Create AI test cases |

---

## Connecting Your Tools

Bette's operate skills are most powerful with MCP integrations. These are optional — set them up when you're ready:

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

| Level | What It Looks Like |
|-------|-------------------|
| **Ad Hoc** | Prompting AI, accepting output, hoping it works |
| **Planned** | CLAUDE.md exists, reference files, quality gates |
| **Systematic** | Layered context, patterns captured, session management |
| **Optimized** | AI manages routine execution within guardrails |

Run `/bette:bette-health` to see where you are and what to do next.

---

## Architecture Docs

Want to understand WHY things work the way they do? The companion repos explain the architecture:

- **[bette-architect](https://github.com/breethomas/bette-architect)** — Context engineering: CLAUDE.md design, reference files, memory systems, skill architecture
- **[bette-think](https://github.com/breethomas/bette-think)** — PM frameworks and thought leader profiles
- **[bette-work](https://github.com/breethomas/bette-work)** — Quality principles, maturity model, session management
- **[bette-os](https://github.com/breethomas/bette-os)** — Daily workflow patterns and operational design

---

## Philosophy

This plugin won't just agree with you. It will:

- Ask for evidence before accepting assumptions
- Suggest prototypes over PRDs
- Challenge you to talk to users
- Push back when thinking is fuzzy

**Opinionated. Curated. AI-era first.**

---

## Contributing

Bette is open source. PRs welcome — especially new skills, framework additions, and workflow improvements.

---

MIT License. Built with Claude Code by [Bree Thomas](https://github.com/breethomas).

Fasten your seatbelts.
