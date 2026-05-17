---
name: bette-setup
description: "Set up your PM operating system. Run this first after installing Bette. Generates CLAUDE.md, reference files, and session bootstrap. Use when user says 'set me up', 'configure bette', 'bette setup', 'get started with bette'."
user-invocable: true
---

# Bette Setup

First-use onboarding for the Bette PM operating system. This skill generates the context architecture that powers all other Bette skills.

## Entry Point

Present two paths:

**Path 1: "Set me up"** — Guided onboarding. Claude asks questions and generates everything.
**Path 2: "I'll configure myself"** — Points to the module map and docs.

Ask which path before proceeding.

---

## Path 1: Guided Onboarding

Ask the following questions **one at a time**. Wait for each answer.

1. **Role:** "What's your role? (PM, designer, founder, engineer, other)" — PM gets full setup; others get a simplified variant.
2. **Team:** "Do you manage people? If so, how many direct reports?" — If yes, generate `people/` with a file per report.
3. **Tools:** "Which tools does your team use? (Slack, Notion, Linear, GitHub, Jira, others)" — informs which MCPs to mention.
4. **Coding:** "Do you write code? Solo, team codebase, or not at all?" — If yes, include work-module references.
5. **Workspace location:** "Where should I create your workspace? Default: `~/bette-workspace/`."

### Step 1: Generate Global CLAUDE.md

Write `~/.claude/CLAUDE.md`. Customize sections by role.

```markdown
# [User's Name]'s Claude Code Preferences

## How We Work

- Bette is the PM operating system layered on Claude Code
- Plan before implementation — discuss strategy, then execute
- Ask clarifying questions one at a time
- Direct feedback, no hedging, no emojis

## Truth and Research

- Never fabricate facts, quotes, data, or sources
- If uncertain, state it explicitly
- Distinguish facts, analysis, and opinion
- Challenge ideas with evidence

## Communication

- Bullet points for feedback and summaries
- Concise, direct, no filler
- No emojis unless explicitly requested

## Draft Output Routing (load-bearing)

When asked for any draftable artifact (Slack message, email, exec update, MD&A, LinkedIn post, meeting notes):

1. Write to `[WORKSPACE]/drafts/<descriptive-kebab-case>.md`
2. Run `cat <file> | pbcopy`
3. Tell the user it's copied and name the destination

Why: copying from terminal output carries visual line wraps into Slack/Notion as hard breaks. Piping through pbcopy delivers clean paragraph structure.

## Session Management

- After 2-3 major tasks, suggest saving session notes
- Save to `[WORKSPACE]/sessions/YYYY-MM-DD-description.md`
- Capture: what was accomplished, current state, what's next
```

Role customizations:
- **PM:** Add prioritization filter pointer, exec update format
- **Designer:** Design review and critique format
- **Founder:** Investor update format, decision log
- **Engineer:** Code review prefs, PR conventions, ADR pattern

### Step 2: Generate Project Workspace

Create at the workspace path:

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
  [people/]   # only if user has direct reports
```

**[WORKSPACE]/CLAUDE.md** — uses native `@imports` so reference files load deterministically (not via prose instruction):

```markdown
# Bette Workspace

Bette is [user's name]'s operating system. This file loads every session.

## Always-loaded reference

@./reference/people.md
@./reference/domains.md
@./reference/company.md
@./BACKLOG.md
@./GOALS.md

## Draft output routing

For any draftable artifact: write to `drafts/<kebab-case>.md`, then `cat <file> | pbcopy`, then tell the user where to paste. See global CLAUDE.md for rationale.

## Session management

- Don't rely on chat history across sessions — update files during the session
- If a session runs long, suggest saving state to `sessions/`
```

**[WORKSPACE]/BACKLOG.md:**

```markdown
# Backlog

Brain dump here. No structure required.

---

## P0 — This Week

## P1 — Soon

## P2 — When There's Space

---

## Completed

## Waiting / Someday
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
- TODO

### Goal 3
- TODO

---

## The Filter

[Replace with your own strategic filter. The questions below are examples — rewrite them around what actually matters for your org and product.]

When prioritizing, ask:
1. [Strategic question relevant to your top goal]
2. [Strategic question relevant to your product or customer]
3. [Strategic question relevant to your team]

If none apply, ask why you're doing it.
```

**Reference files** — create with a `# Title`, `**Last updated:**` line, and TODO-stub sections:

- `reference/people.md` — sections: Leadership, Direct Reports (or Key Collaborators if no reports). One line per person: `Name — Role. Key context.`
- `reference/domains.md` — sections: Domain Map (table: Domain | Owner | Scope), Acronyms & Terms.
- `reference/company.md` — sections: Technical Systems, Methodology, Meeting Cadences.

If user manages people, create `people/<name>.md` per direct report with sections: Background, Coaching Notes, 1:1 Log, Wins.

### Step 3: SessionStart Hook

Add to `~/.claude/settings.json`. Read first, merge if it exists.

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup|resume",
        "hooks": [
          { "type": "command", "command": "[WORKSPACE]/scripts/session-start.sh" }
        ]
      }
    ]
  }
}
```

### Step 4: Session Start Script

Copy `/Users/bree.thomas@homebot.ai/Work/bette/scripts/session-start.sh` to `[WORKSPACE]/scripts/session-start.sh`, replace `__BETTE_WORKSPACE__` with the workspace path, and `chmod +x`.

### Step 5: Marker File

Write `~/.claude/.bette-configured`:

```
configured: [today's date]
workspace: [WORKSPACE path]
role: [user's role]
```

### Step 6: Confirm to the User

Print a summary of files created, then:

```
Next steps:
1. Restart your Claude Code session to activate the SessionStart hook
2. Fill in the TODO placeholders in reference/ and GOALS.md
3. Try: "What's on my backlog?" or "Help me set my goals"

About auto-memory:
Claude Code maintains an auto-memory directory at
~/.claude/projects/<project>/memory/MEMORY.md that loads every session
and persists patterns across conversations. Run /memory-architecture
to learn the editorial discipline (what gets persisted where, naming
conventions, promotion rules).

Learn more:
- frameworks/ai-era-practices/pm-memory-architecture.md — canonical framework
- docs/personalization.md — tune Bette to your seniority and style
- docs/memory-systems.md — how native memory primitives work
```

---

## Path 2: Self-Guided Configuration

Print:

```
Bette Module Map
================

Run /skills to see the current list of available skills, grouped by
THINK (frameworks), OPERATE (daily ops), and WORK (coding guardrails).
Counts and contents shift between releases — /skills is the source of truth.

Setup: bette-setup (this skill), bette-health

How to connect MCPs:
  claude mcp add slack -- npx @anthropic/claude-code-slack-mcp
  claude mcp add notion -- npx @anthropic/claude-code-notion-mcp
  claude mcp add linear -- npx @anthropic/claude-code-linear-mcp

Learn more:
- frameworks/ai-era-practices/pm-memory-architecture.md
- docs/personalization.md
- docs/memory-systems.md

Auto-memory: Claude Code maintains ~/.claude/projects/<project>/memory/MEMORY.md
that loads every session. Run /memory-architecture for the editorial discipline.

Docs: github.com/breethomas/bette-architect
```

Then write `~/.claude/.bette-configured`:

```
configured: [today's date]
workspace: self-guided
role: unknown
```

---

## Error Handling

- `~/.claude/CLAUDE.md` exists: ask before overwriting; offer merge or replace.
- `~/.claude/settings.json` has hooks: merge, do not replace.
- Workspace directory exists: ask before overwriting files.
- `~/.claude/.bette-configured` exists: tell user Bette is configured; ask if they want to reconfigure.
