---
name: backlog
description: Process and prioritize the PM's backlog. Use when user says "process my backlog", "clean up my backlog", "what's on my backlog", or similar. Reads BACKLOG.md, categorizes each item, cross-references with goals, and suggests priorities. Interactive — discusses items with the PM.
---

# Process My Backlog

Read the backlog, categorize items, cross-reference with goals, and prioritize. This is interactive — discuss with {PM Name} and get input on ambiguous items.

## Context Files

Read these first:
- `{Home Directory}/BACKLOG.md` — the inbox
- `{Home Directory}/GOALS.md` — what matters this quarter
- `{Strategy Directory}/initiatives/{Strategy Framework}` — strategic framework

## Workflow

### 1. Read and categorize

For each item in BACKLOG.md, determine:
- Is this an **action item**? (who, what, by when)
- Is this a **decision to make**?
- Is this a **question to answer**?
- Is this a **meeting topic** for someone?
- Is this a **strategic thread** to pull?
- Is this a **project** that needs its own tracking?

### 2. Cross-reference with goals

- Does this connect to quarterly priorities in GOALS.md?
- Does it advance the primary strategic objective?
- Does it strengthen a core growth loop?
- Does it protect current revenue or stability?
- Does it build the team or capabilities needed?

Surface any items that don't connect to goals — ask: should {PM Name} be doing this?

### 3. Suggest priorities

- **P0** = today
- **P1** = this week
- **P2** = soon
- **P3** = someday

### 4. Discuss and clarify

Ask clarifying questions for ambiguous items. This is a conversation — don't just dump a list.

### 5. Clean up

After {PM Name} confirms, clear processed items from BACKLOG.md (move to appropriate place or mark done).

## Sub-agent Delegation

When querying Notion or Linear during this workflow (e.g., to check context on a backlog item), delegate the search to a sub-agent using the Task tool with subagent_type=Explore. Return only the summary to the main context.

## Output Style

- Present items grouped by category, then by priority
- Flag items that don't connect to goals
- Be direct about what should be dropped or delegated
