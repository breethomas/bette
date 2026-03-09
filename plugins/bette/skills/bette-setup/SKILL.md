---
name: bette-setup
description: "Set up your PM operating system. Run this first after installing Bette. Generates CLAUDE.md, reference files, and session bootstrap. Use when user says 'set me up', 'configure bette', 'bette setup', 'get started with bette'."
user-invocable: true
---

# Bette Setup

First-use onboarding for the Bette PM operating system. This skill generates the context architecture that powers all other Bette skills.

## Entry Point

Present two paths to the user:

**Path 1: "Set me up"** — Full guided onboarding. Claude asks questions and generates everything.
**Path 2: "I'll configure myself"** — Shows the module map and points to docs.

Ask the user which path they prefer before proceeding.

---

## Path 1: Guided Onboarding

Ask these questions **one at a time** (wait for each answer before asking the next). Keep the conversation natural — do not dump all questions at once.

### Step 1: Gather Context

**Question 1 — Role:**
"What's your role? (PM, designer, founder, engineer, or something else)"

Based on the answer, adapt the templates below. PMs get the full operational setup. Other roles get a simplified version focused on their workflow.

**Question 2 — Team:**
"Do you manage people? If so, how many direct reports?"

If yes: create people/ directory with a file per direct report (placeholder content). If no: skip people/ directory entirely.

**Question 3 — Tools:**
"Which tools does your team use? (Slack, Notion, Linear, GitHub, Jira, others)"

Record the answers — these determine which MCP integrations to mention in the generated CLAUDE.md and which operate-module skills are relevant.

**Question 4 — Coding:**
"Do you write code? Solo projects, team codebase, or not at all?"

If they code: include the work module (coding guardrails, quality gates) in their setup. If not: skip work module references.

**Question 5 — Workspace location:**
"Where should I create your workspace? Default is ~/bette-workspace/"

Use their answer or the default for all file generation below.

### Step 2: Generate Global CLAUDE.md

Create `~/.claude/CLAUDE.md` with the following structure. Customize based on answers above.

```markdown
# [User's Name]'s Claude Code Preferences

## How We Work Together

- Claude is a PM operating system called Bette
- Plan before implementation — discuss strategy, then execute
- Ask clarifying questions one at a time
- Direct feedback, no hedging, no emojis

## Planning Protocol

- Discuss overall strategy before making changes
- Get approval on approach before implementation
- Check understanding after completing each task

## Truth and Research

- Never fabricate facts, quotes, data, or sources
- If uncertain, state it explicitly
- Distinguish between: facts, analysis, and opinion
- Challenge ideas with evidence — push back when appropriate

## Communication

- Bullet points for feedback and summaries
- Concise, direct language
- No emojis unless explicitly requested

## Session Management

- After completing 2-3 major tasks, suggest saving session notes
- Session notes go in [WORKSPACE]/sessions/YYYY-MM-DD-description.md
- Capture: what was accomplished, current state, what's next
```

**Customizations by role:**
- **PM:** Add sections for "The Filter" (prioritization framework), meeting prep patterns, exec update format
- **Designer:** Add sections for design review workflow, critique format
- **Founder:** Add sections for investor update format, decision log, strategic planning
- **Engineer:** Add sections for code review preferences, PR conventions, architecture decision records

### Step 3: Generate Project Workspace

Create the following directory structure at the workspace path:

```
[WORKSPACE]/
  CLAUDE.md
  BACKLOG.md
  GOALS.md
  reference/
    people.md
    domains.md
    company.md
  sessions/
  drafts/
```

**[WORKSPACE]/CLAUDE.md** — Project-level context:

```markdown
# Bette Workspace

Bette is [user's name]'s operating system. Claude reads this context to help manage day-to-day operations.

## Context to Load

**Always read:**
- `BACKLOG.md` — Brain dump inbox
- `GOALS.md` — What matters this quarter
- `reference/people.md` — Who's who (roles, relationships)
- `reference/domains.md` — Product domains, acronyms
- `reference/company.md` — Systems, meetings, methodology

## Session Management

- Don't rely on chat history across sessions
- Update files during the session so context persists
- If a session runs long, suggest saving state

## The Filter

When prioritizing, ask:
1. Does this move the top goal forward?
2. Does this unblock someone?
3. Does this prevent something from breaking?
4. Does this build the team?

If none of the above: ask why we're doing this.
```

**[WORKSPACE]/BACKLOG.md:**

```markdown
# Backlog

Brain dump here. No structure required. Just capture.

---

## P0 — This Week

## P1 — Soon

## P2 — When There's Space

---

## Completed

---

## Waiting / Someday

---
```

**[WORKSPACE]/GOALS.md:**

```markdown
# Goals

**Last updated:** [today's date]

---

## This Quarter

### Goal 1
- TODO: Define your top goal

### Goal 2
- TODO: Define your second goal

### Goal 3
- TODO: Define your third goal

---

## The Filter

When prioritizing, ask:
1. Does this move the top goal forward?
2. Does this unblock someone?
3. Does this prevent something from breaking?
4. Does this build the team?

If none of the above: why am I doing this?
```

**[WORKSPACE]/reference/people.md:**

```markdown
# People Reference

Quick lookup for Claude. One line per person.

**Last updated:** [today's date]

---

## Leadership

- TODO: Add leadership team members (Name — Role. Key context.)

## Direct Reports

[If user has direct reports, create one entry per report:]
- TODO: [Name] — Role. Key context. See `people/[name].md`.

[If user has no direct reports, replace with:]
## Key Collaborators

- TODO: Add people you work with regularly

---
```

**[WORKSPACE]/reference/domains.md:**

```markdown
# Domains Reference

Quick lookup for Claude. Product areas, acronyms, ownership.

**Last updated:** [today's date]

---

## Domain Map

| Domain | Owner | Scope |
|--------|-------|-------|
| TODO | TODO | TODO |

## Acronyms & Terms

- TODO: Add team-specific acronyms and terminology

---
```

**[WORKSPACE]/reference/company.md:**

```markdown
# Company & Systems Reference

Quick lookup for Claude. Terminology, systems, and cadences.

**Last updated:** [today's date]

---

## Technical Systems

- TODO: Add key systems and tools (Name — What it does.)

## Methodology

- TODO: Add how your team works (Agile, Shape Up, Kanban, etc.)

## Meeting Cadences

- TODO: Add recurring meetings (Name — When. What it covers.)

---
```

If the user manages people, also create `[WORKSPACE]/people/` with one file per direct report:

```markdown
# [Name]

**Role:** [from user's answer]
**Started:** TODO

---

## Background

TODO: Key context about this person

## Coaching Notes

## 1:1 Log

## Wins

---
```

### Step 4: Generate SessionStart Hook

Add a hook to `~/.claude/settings.json`. Read the file first — if it exists, merge into the existing structure. If it does not exist, create it.

The hook to add (merge into the `hooks` object):

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup|resume",
        "hooks": [
          {
            "type": "command",
            "command": "[WORKSPACE]/scripts/session-start.sh"
          }
        ]
      }
    ]
  }
}
```

Replace `[WORKSPACE]` with the actual workspace path.

### Step 5: Create Session Start Script

Copy the template from `/Users/bree.thomas@homebot.ai/Work/bette/scripts/session-start.sh` to `[WORKSPACE]/scripts/session-start.sh`.

Then customize it:
- Replace `__BETTE_WORKSPACE__` with the actual workspace path
- Make it executable: `chmod +x [WORKSPACE]/scripts/session-start.sh`

### Step 6: Create Marker File

Create `~/.claude/.bette-configured` with content:

```
configured: [today's date]
workspace: [WORKSPACE path]
role: [user's role]
```

### Step 7: Tell the User

Print a summary of everything that was created:

```
Bette is set up. Here's what was created:

Global config:
  ~/.claude/CLAUDE.md — Your preferences and working style
  ~/.claude/settings.json — SessionStart hook (loads Bette context automatically)
  ~/.claude/.bette-configured — Setup marker

Workspace ([WORKSPACE]/):
  CLAUDE.md — Project context (loaded every session)
  BACKLOG.md — Brain dump inbox
  GOALS.md — Quarterly goals template
  reference/people.md — Team directory (fill in TODOs)
  reference/domains.md — Product areas and acronyms (fill in TODOs)
  reference/company.md — Systems and cadences (fill in TODOs)
  sessions/ — Session notes directory
  drafts/ — Working documents directory
  [people/ — Direct report files (if applicable)]

Next steps:
1. Restart your Claude Code session to activate the SessionStart hook
2. Fill in the TODO placeholders in reference/ files
3. Try: "What's on my backlog?" or "Help me set my goals"
```

---

## Path 2: Self-Guided Configuration

Show the user the module map and point them to docs.

Print this:

```
Bette Module Map
================

THINK (26 skills) — PM frameworks, active now
  Strategy: pyramid, minto, scqa, issue-trees, hypothesis-driven
  Analysis: five-whys, impact-mapping, wardley-map, jobs-to-be-done
  Prioritization: rice-scoring, moscow, opportunity-scoring, kano
  Planning: shape-up-pitch, user-story-mapping, assumption-mapping
  Communication: stakeholder-map, decision-log, status-update, exec-brief
  Product: product-brief, competitive-analysis, launch-checklist, retro

OPERATE (23 skills) — Daily operations, need MCP connections
  Comms: catchup, email-inbox, email-find, slack-inbox, slack-find, slack-catchup
  Meetings: digest, sync-transcripts, prep-1on1, log-1on1, coach-me, synthesize
  Planning: backlog, focus, weekly-review
  People: prep-review
  Publishing: save-notion, pyramid
  Health: bette-health

WORK (3 skills) — Coding guardrails, for PMs who code
  quality-gate, session-log, pr-review

Setup: bette-setup (this skill), bette-health

How to explore:
  /skills — See all available skills
  /bette:bette-health — Audit your current context architecture

How to connect MCPs:
  claude mcp add slack -- npx @anthropic/claude-code-slack-mcp
  claude mcp add notion -- npx @anthropic/claude-code-notion-mcp
  claude mcp add linear -- npx @anthropic/claude-code-linear-mcp

Docs: github.com/breethomas/bette-architect
```

After showing the map, still create the marker file at `~/.claude/.bette-configured` with:

```
configured: [today's date]
workspace: self-guided
role: unknown
```

---

## Error Handling

- If `~/.claude/CLAUDE.md` already exists, ask the user before overwriting. Offer to merge or replace.
- If `~/.claude/settings.json` already has hooks, merge the new SessionStart hook — do not replace existing hooks.
- If the workspace directory already exists, ask the user before overwriting any files.
- If `~/.claude/.bette-configured` already exists, tell the user Bette is already configured and ask if they want to reconfigure.
