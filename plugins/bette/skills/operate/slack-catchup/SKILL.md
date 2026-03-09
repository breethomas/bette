---
name: slack-catchup
description: Summarize what was missed in Slack channels. Use when user says "catch me up on [channel]", "what did I miss in [channel]", "summarize [channel]", "what's happening in [channel]", "catch up on Slack", or similar. Reads channel history, extracts decisions, blockers, and items needing attention. Writes summary to drafts/.
context: fork
model: sonnet
---

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Before executing, find and read the CLAUDE.md file in the project root (the directory containing BACKLOG.md and GOALS.md). Locate the Config table and resolve all `{Key}` placeholders in this skill to their configured values.

If no Config table is found, abort and report: "Cannot resolve config variables. Ensure CLAUDE.md has a Config table with {Home Directory}, {PM Name}, and other required keys."


# Slack Catchup

Summarize what {PM Name} missed in one or more Slack channels. Read recent messages, extract what matters, filter noise, and write a structured summary.

## Context Files

Read these first:
- `{Home Directory}/reference/people.md` — who's who (for identifying key participants)
- `{Home Directory}/reference/domains.md` — product domains, acronyms (for understanding context)
- `{Home Directory}/GOALS.md` — current priorities (to flag things that connect to goals)

## Slack Configuration

- **PM's Slack user ID:** `{Slack User ID}`
- **CRITICAL:** Always use `detailed` format for all Slack MCP calls. The `concise` format crashes the MCP.

## Priority Hierarchy

@mentions of {PM Name} always rank highest:
1. @mentions (`{Slack User ID}`) where they haven't responded
2. Questions directed at product that {PM Name} should weigh in on
3. Decisions made without {PM Name}'s input
4. Blockers or escalations
5. Status updates and progress
6. General discussion (filtered as noise)

## Workflow

### 1. Resolve channels

`$ARGUMENTS` may contain:
- **Channel name(s):** "pm-team", "#team-ai and #pm-team"
- **Topic:** "AI stuff", "pricing discussions" — search for matching channels
- **Nothing:** Ask which channels to catch up on

### 2. Determine time range

Parse from `$ARGUMENTS` if specified:
- "since yesterday" → last 24 hours
- "this week" → since Monday
- "last few days" → last 72 hours
- No time specified → default to last 24 hours

### 3. Read channel messages

For each channel, use `mcp__claude_ai_Slack__slack_read_channel` with `detailed` format, limit 100 per page. Paginate up to 200 messages if needed.

### 4. Read key threads

Focus thread reads on:
- Any thread that @mentions {PM Name}
- Threads with 3+ replies
- Threads from key people (reference people.md)

Skip bot messages, automated notifications, and social conversation.

### 5. Extract and categorize

**Needs Attention:** @mentions, questions needing input, pending decisions, blockers
**Decisions Made:** Conclusions, directions set, commitments made
**Status & Progress:** What shipped, cycle work updates, PRs merged
**Connected to Goals:** Anything that ties to GOALS.md or the strategic framework

### 6. Write summary to file

Write to: `{Home Directory}/drafts/slack-catchup-[YYYY-MM-DD].md`

```
# Slack Catchup — [Date]

Channels reviewed: [list]
Time range: [range]
Messages reviewed: [count]

## Needs Your Attention
- **[@mention]** [Author] in #[channel] asked: "[question]" [permalink]

## Decisions Made (Without You)
- **#[channel]:** [Decision summary] — decided by [who]. [permalink]

## Status & Progress
- **#[channel]:** [What shipped or moved] [permalink]

## Connected to Goals
- [Item] ties to [specific goal] — [how]

## Noise Filtered
[N] total messages reviewed. [K] items surfaced above.
```

### 7. Return file path

Your final message MUST include:
```
CATCHUP_FILE: {Home Directory}/drafts/slack-catchup-[YYYY-MM-DD].md
```

## Output Guidelines

- Write full summary to the file (this is the primary output)
- Be aggressive about filtering noise — signal, not a transcript
- Always include permalinks
- For "Needs Attention" items, be specific about what to do
- For "Decisions Made" items, note strategic alignment or conflict
- When attributing, reference people.md for role context
- If a channel is quiet (< 5 messages), note "Quiet — nothing notable"
