---
name: prep-meeting
description: Prepare a talk track for a meeting with someone. Use when user says "prep for meeting with [name]", "prep my 1:1", "get ready for [name]", or similar. Gathers context from people files, Notion, and Linear, then builds a structured conversation plan.
context: fork
model: sonnet
---

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Before executing, find and read the CLAUDE.md file in the project root (the directory containing BACKLOG.md and GOALS.md). Locate the Config table and resolve all `{Key}` placeholders in this skill to their configured values.

If no Config table is found, abort and report: "Cannot resolve config variables. Ensure CLAUDE.md has a Config table with {Home Directory}, {PM Name}, and other required keys."


# Prep for Meeting with $ARGUMENTS

Prepare a structured talk track for {PM Name}'s meeting with **$ARGUMENTS**.

## Name Resolution

The person is: **$ARGUMENTS**

Normalize to find the right file:
- Check `{People Directory}/` for a matching filename (lowercase)
- If full name given, match against `{Home Directory}/reference/people.md`

## Workflow

### 1. Load person context

1. Read `{People Directory}/$ARGUMENTS.md` (lowercase the name) — background, meeting history, relationship notes
2. Read `{Home Directory}/GOALS.md` — what matters this quarter
3. Read `{Home Directory}/BACKLOG.md` — any items related to $ARGUMENTS

### 2. Query recent context

Use MCP tools to gather fresh context:

**Notion:** Search for recent meeting notes mentioning $ARGUMENTS
```
mcp__notion__notion-search --query "$ARGUMENTS meeting" --query_type "internal"
```

**Linear:** Search for their recent work
```
mcp__linear__list_issues --query "$ARGUMENTS" --limit 10
```

Look for: shipped work, in-progress items, blockers, cycle commitments.

### 3. Surface key items

From all gathered context, identify:
- **Open items from last meeting** — what was committed to, what's still pending
- **Recent wins** — what shipped or went well since last meeting
- **Decisions needed** — anything requiring alignment or input
- **Points to raise** — things to bring up based on recent context
- **Strategic alignment** — how their work connects to GOALS.md priorities

### 4. Build talk track and write to file

Build a structured conversation plan (not just bullet points).

**Write the full talk track to:** `{Home Directory}/drafts/prep-meeting-$ARGUMENTS-[YYYY-MM-DD].md`

Use this format:

```
# Meeting Prep: $ARGUMENTS — [Date]

## Open from Last Time
- [item] — status: [resolved/pending/needs discussion]

## Talk Track

1. **[Topic]**
   - Context: [what you know]
   - Ask: [specific question to ask]
   - Goal: [what this conversation should accomplish]

2. **[Topic]**
   - Context: [what you know]
   - Ask: [specific question]
   - Goal: [what to accomplish]

3. **[Topic]**
   ...

## Points to Raise
- [Specific topic + context + why it matters]

## Wins to Acknowledge
- [Specific win + impact]

## Recent Work (Linear)
- [issue] — [status]
- ...

## Watch For
- [Anything to pay attention to during the conversation]
```

### 5. Return file path

Your final message MUST include:
```
PREP_FILE: {Home Directory}/drafts/prep-meeting-$ARGUMENTS-[YYYY-MM-DD].md
```

## Output Guidelines

- Write full talk track to the file (this is the primary output)
- Talk track format, not bullet dump — {PM Name} wants a conversation plan
- Be specific with points to raise (examples, not generalities)
- Tie topics to GOALS.md where relevant
- Be thorough in the file — it will be read back by the main agent and presented to {PM Name}
- If person file doesn't exist, note that and build what you can from Notion/Linear
