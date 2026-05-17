# Bette

> "Attempt the impossible in order to improve your work." — Bette Davis

A PM operating system for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). 55 skills, 7 autonomous agents, 31 PM frameworks. One install.

Named after Bette Davis, who sued a studio because they wouldn't give her better roles.

---

## Who is this for?

Product managers using Claude Code who want repeatable workflows instead of ad hoc prompting. Strategic decisions, meeting prep, inbox triage, backlog management, AI evals, spec writing.

You don't memorize commands. Just say what you need in plain English. Bette picks the right workflow.

It's opinionated. Expect challenges to fuzzy thinking, requests for evidence, and pressure to talk to users.

---

## Install

```
/plugin marketplace add breethomas/bette
/plugin install bette@breethomas
```

Start a new session. Say **"set me up"**.

---

## Get Started

Two paths. Same system.

**Guided:** Say "set me up" and pick guided. Five minutes of questions. You get a preferences file, reference files, backlog, and a session bootstrap.

**Self-guided:** Say "set me up" and pick self-guided. You get the map and docs. Configure as you go.

---

## What does a session look like?

```
catch me up
```
Triages email and Slack saves. Drafts replies. Updates the backlog.

```
prep for my 1:1 with Sarah
```
Talk track from your people file, recent meetings, and open issues.

```
let's think through the pricing change
```
Sparring partner mode. Frameworks, evidence requests, decision capture.

```
what should I focus on today?
```
Top priorities from your backlog. No more than three.

Just talk to it. Slash commands exist (`/bette:strategy-session`) if you want them. Type `/skills` to see everything.

---

## Skills

### Think
Strategic sparring grounded in Cagan, Torres, Verna, Balfour, Singer, Husain, and others.

| Say this | What happens |
|---|---|
| "let's think through [problem]" | Conversational decision work |
| "write a spec for [feature]" | Specs at the right depth |
| "shape this work" | Shape Up: appetite, solution, risks |
| "run four risks on [feature]" | Cagan's value / usability / feasibility / viability |
| "set up evals for [AI feature]" | First 20 test cases |
| "research competitors in [space]" | Parallel agent analysis |
| "plan the agency ladder" | v1 → v2 → v3 AI feature progression |
| "where's the broken fit?" | Balfour's Four Fits |
| "build a judge for [AI feature]" | LLM-as-judge pipelines |

### Operate
Daily workflow.

| Say this | What happens |
|---|---|
| "catch me up" | Email + Slack triage |
| "process my meetings" | Transcripts to action items |
| "prep for my meeting with [name]" | Talk track |
| "process my backlog" | Categorize and prioritize |
| "weekly review" | What got done, what didn't |
| "audit my Linear" | Workspace, project, or team-level check |

Works better with Slack, Gmail, Notion, Linear connected. Skills handle missing integrations gracefully.

### Work
For PMs who code.

| Say this | What happens |
|---|---|
| "run quality gates" | Pre-commit checklist |
| "write tests first" | Test suites before modifying code |

### Architect
Context engineering.

| Say this | What happens |
|---|---|
| "set me up" | First-use onboarding |
| "check my setup" | Audit against the maturity model |
| "how should I structure my memory?" | PM memory architecture, editorial discipline on top of native Claude Code primitives |

---

## Agents

| Agent | What it does |
|---|---|
| Project health checker | Single project deep-dive |
| Linear workspace analyzer | Workspace methodology check |
| Team organization analyzer | Team conventions |
| Competitor researcher | One competitor, full depth |
| AI cost analyzer | AI feature economics |
| AI implementation auditor | Pre-launch readiness, 6 dimensions |
| Eval generator | AI test cases and frameworks |

---

## What else is in the box

**31 frameworks** across discovery, planning, growth, execution, measurement, and AI-era practices. Continuous discovery, Shape Up, growth loops, LNO, AI unit economics, PM memory architecture, more.

**15 thought leader profiles** (Cagan, Torres, Verna, Balfour, Cherny, Singer, Huyen, Rachitsky, Khan, others).

**4 templates**: AI product spec, lite PRD, Linear issue, competitive analysis.

**Architecture docs** in `docs/`. Covers preferences files, reference files, memory systems, context hygiene, skill architecture, and personalization (how to tune Bette to your seniority and style via CLAUDE.md).

Bette positions itself as editorial discipline on top of Claude Code's native memory primitives (CLAUDE.md hierarchy, @imports, auto-memory, Auto Dream), not a replacement. The PM memory architecture framework in `frameworks/ai-era-practices/` is where that gets articulated.

---

## Connecting Your Tools

Optional. Set up when ready.

- **Linear**: `claude mcp add linear`
- **Slack / Gmail / Notion**: connect via Claude.ai → Integrations

---

## Maturity Model

Say "check my setup" to see where you are.

| Level | What it looks like |
|---|---|
| **Ad Hoc** | No context. Every session starts cold. |
| **Planned** | Reference files exist. Sessions start warm. |
| **Systematic** | Skills define quality standards. System knows your patterns. |
| **Optimized** | You steer. The system drives. It knows you. |

Setup gets you to Planned in five minutes. Systematic comes from daily use. Optimized is when the system needs less from you, not more.

---

## History

Earlier in Bette's evolution, this material lived across companion repos (`bette-architect`, `bette-os`, `bette-work`). Those are archived. All current canonical thinking is in this repo.

---

## Contributing

PRs welcome. New skills, framework additions, workflow improvements.

Each skill is a single markdown file. Follow the lean loader pattern: pull in the canonical framework and thought-leader profile, trust the model to apply them, no prescribed workflows.

---

MIT License. Built with Claude Code by [Bree Thomas](https://github.com/breethomas).

Fasten your seatbelts.
