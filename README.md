# Bette

> "Attempt the impossible in order to improve your work." — Bette Davis

A PM operating system for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). 54 skills, 7 agents, 32 frameworks. One install.

Named after Bette Davis, who sued a studio because they wouldn't give her better roles.

---

## Who it's for

PMs using Claude Code who want repeatable workflows, not ad hoc prompting.

Strategic decisions. Meeting prep. Inbox triage. Backlog. AI evals. Spec writing.

Talk to it in plain English. Bette picks the workflow.

Opinionated. It'll push back.

---

## What it curates

Bette ships analytical frameworks. Tools for thinking.

Balfour's Four Fits diagnoses growth. Vohra's PMF Survey measures fit. Cagan's Four Risks evaluates before you build. These travel.

Bette does not ship process frameworks. Shape Up, Scrum, Kanban, OKRs. Process depends on your team, your stage, your customers, your politics. Your team is yours. Run it how it works.

---

## Install

```
/plugin marketplace add breethomas/bette
/plugin install bette@breethomas
```

Start a session. Say **"set me up"**.

---

## Get started

**Guided.** Say "set me up" and pick guided. Five minutes of questions. You get a preferences file, reference files, backlog, session bootstrap.

**Self-guided.** Say "set me up" and pick self-guided. Map and docs. Configure as you go.

---

## A session

```
catch me up
```
Email and Slack triage. Drafts. Backlog updates.

```
prep for my 1:1 with Sarah
```
Talk track from people file, recent meetings, open issues.

```
let's think through the pricing change
```
Sparring partner. Frameworks, evidence, decisions captured.

```
what should I focus on today?
```
Top three. From your backlog.

Type `/skills` for the full list. Slash commands like `/bette:strategy-session` work if you want them.

---

## Skills

### Think
Cagan, Torres, Verna, Balfour, Husain, Khan, others.

| Say | Get |
|---|---|
| "let's think through [problem]" | Conversational decision work |
| "write a spec for [feature]" | Specs at the right depth |
| "run four risks on [feature]" | Cagan's four-risk audit |
| "set up evals for [AI feature]" | First 20 test cases |
| "research competitors in [space]" | Parallel agent research |
| "plan the agency ladder" | v1, v2, v3 AI feature progression |
| "where's the broken fit?" | Balfour's Four Fits |
| "build a judge" | LLM-as-judge pipeline |
| "design the agent workflow" | Single vs multi-agent decision |

### Operate
Daily workflow.

| Say | Get |
|---|---|
| "catch me up" | Email and Slack triage |
| "process my meetings" | Transcripts to action items |
| "prep for my meeting with [name]" | Talk track |
| "process my backlog" | Categorized and prioritized |
| "weekly review" | What shipped, what didn't |
| "audit my Linear" | Workspace, project, or team check |

Better with Slack, Gmail, Notion, Linear connected. Works without.

### Work
For PMs who code.

| Say | Get |
|---|---|
| "run quality gates" | Pre-commit checklist |
| "write tests first" | Test suites before edits |

### Architect
Context engineering.

| Say | Get |
|---|---|
| "set me up" | First-use onboarding |
| "how should I structure my memory?" | PM memory architecture |

---

## Agents

| Agent | Job |
|---|---|
| Project health checker | Single project deep-dive |
| Linear workspace analyzer | Workspace methodology check |
| Team organization analyzer | Team conventions |
| Competitor researcher | One competitor, full depth |
| AI cost analyzer | AI feature economics |
| AI implementation auditor | Pre-launch readiness |
| Eval generator | Test cases and frameworks |

---

## What else

**32 frameworks** across discovery, planning, growth, execution, measurement, AI-era practices.

**14 thought leaders** (Cagan, Torres, Verna, Balfour, Cherny, Huyen, Rachitsky, Khan, Gupta, Vohra, Mehta, Bastow, Reforge, Linear Method).

**4 templates**: AI spec, lite PRD, Linear issue, competitive analysis.

**Architecture docs** in `docs/`: preferences, reference files, memory, context hygiene, skill architecture, personalization.

Bette is editorial discipline on top of Claude Code's native memory. Not a replacement. The PM memory architecture framework in `frameworks/ai-era-practices/` explains how.

---

## Integrations

Optional.

- Linear: `claude mcp add linear`
- Slack / Gmail / Notion: connect via Claude.ai → Integrations

---

## Maturity

Four levels. Ask Claude to audit your setup.

| Level | Looks like |
|---|---|
| Ad Hoc | No context. Sessions start cold. |
| Planned | Reference files exist. Sessions start warm. |
| Systematic | Skills define quality. The system knows your patterns. |
| Optimized | You steer. It drives. It knows you. |

Setup gets you to Planned in five minutes. The rest comes from daily use.

---

## History

Earlier versions lived across `bette-architect`, `bette-os`, `bette-work`. All archived. Everything's here now.

---

## Contributing

PRs welcome. New skills, frameworks, workflow improvements.

Skills are single markdown files. Lean loader pattern: load the framework and thought-leader profile, trust the model, no prescribed steps.

---

MIT. Built with Claude Code by [Bree Thomas](https://github.com/breethomas).

Fasten your seatbelts.
