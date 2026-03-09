---
name: focus
description: Surface today's top priorities. Use when user says "what should I focus on today", "what's my priority today", "what should I do today", or similar. Reads backlog and goals, checks recent meeting context, and surfaces maximum 3 focus items tied to strategic outcomes.
---

# What Should I Focus on Today?

Surface maximum 3 focus items for today, tied to strategic outcomes.

## Context Files

Read these first:
- `{Home Directory}/BACKLOG.md` — current items and priorities
- `{Home Directory}/GOALS.md` — what matters this quarter
- `{Strategy Directory}/initiatives/{Strategy Framework}` — strategic framework

## Workflow

### 1. Gather context

1. Read BACKLOG.md — look at P0 items and "This Week" sections
2. Read GOALS.md — what are the quarterly priorities?
3. If Notion Meeting Notes DB is configured (`{Notion Meeting Notes DB}`), delegate a sub-agent to query for meetings in the last 24 hours
4. Check calendar context if available

### 2. Surface focus items

- **Maximum 3 items** (P0 only)
- For each item, explain **why it matters** — tie to loops, pillars, or goals
- Flag blockers or dependencies
- Note what's deliberately NOT on the list today (and why)

### 3. Output

```
## Focus — [Date]

### 1. [Item]
Why: [Connection to strategic outcome]
Blocker: [if any]

### 2. [Item]
Why: [Connection to strategic outcome]
Blocker: [if any]

### 3. [Item]
Why: [Connection to strategic outcome]
Blocker: [if any]

### Not Today
- [Item] — [why it's not priority today]
```

## Sub-agent Delegation

When querying Notion for meeting notes, delegate to a sub-agent using the Task tool with subagent_type=Explore. Return only action items to the main context.
