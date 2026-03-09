---
name: slack-inbox
description: Process saved Slack items. Use when user says "process my saved Slack items", "Slack inbox", "what's saved in Slack", "triage my Slack saves", "process my Slack", or similar. Pulls saved items, categorizes them, drafts responses, and adds action items to backlog. Interactive triage — discusses each item with the PM.
---

# Slack Inbox

Process saved Slack items in one pass. Pull saved items, read thread context, categorize, and triage interactively.

## Context Files

Read these first:
- `{Home Directory}/BACKLOG.md` — current priorities (to avoid duplicating existing items)
- `{Home Directory}/reference/people.md` — who's who (for name resolution in messages)
- `{Home Directory}/slack/.processed-saved` — already-processed saved items (create file if it doesn't exist)

## Slack Configuration

- **PM's Slack user ID:** `{Slack User ID}`
- **CRITICAL:** Always use `detailed` format for Slack search. The `concise` format crashes the MCP.
- **Drafts only:** Use `slack_send_message_draft` (never `send_message`). PM reviews before sending.
- **Draft limit:** One draft per channel. If `draft_already_exists` error, tell {PM Name} and skip.
- **Slack formatting:** Use Slack mrkdwn — single `*bold*`, `_italic_`, backtick for code. NOT standard markdown.

## Priority Hierarchy

@mentions of {PM Name} always rank highest:
1. @mentions where {PM Name} hasn't replied
2. Direct questions to {PM Name}
3. Action items (things to do outside Slack)
4. Decisions pending input
5. FYI / general awareness

## Workflow

### 1. Gather saved items (delegate to sub-agent)

Delegate the Slack search to a sub-agent using the Task tool (`subagent_type: general-purpose`). The sub-agent should:

1. Search Slack with `mcp__claude_ai_Slack__slack_search_public_and_private` using query `is:saved`, format `detailed`, sorted by timestamp descending
2. For each result, extract: message text (first 200 chars), author name, channel name, channel_id, message_ts, thread reply count, permalink
3. Return a structured numbered list with clear field labels

### 2. Filter already-processed items

Read `{Home Directory}/slack/.processed-saved`. For each saved item from step 1, check if `channel_id:message_ts` exists in the file. Remove matches — only present unprocessed items.

If no unprocessed items remain, tell {PM Name} "No new saved items to process" and stop.

### 3. Enrich with thread context (delegate to sub-agent)

For items that have thread replies (reply_count > 0), delegate thread reads to a sub-agent. Ask the sub-agent to check whether user `{Slack User ID}` has replied in each thread.

Batch thread reads into a single sub-agent call (up to 10 threads).

### 4. Categorize each item

- **Respond** — Someone asked a question, @mentioned {PM Name}, or the thread needs input. {PM Name} has NOT already replied.
- **Action** — Contains a to-do that happens outside Slack.
- **FYI** — Informational. Saved for awareness but no action needed.
- **Stale** — Old enough or resolved enough that it's no longer relevant.

### 5. Present interactively

Present items grouped by category, most actionable first. Then ask: "Want to walk through these one by one, or should I handle the obvious ones and just bring you the judgment calls?"

### 6. Process each item based on direction

**Respond:** Draft a response, show it for approval, then create via `slack_send_message_draft`.
**Action:** Append to `{Home Directory}/BACKLOG.md` with Slack permalink.
**FYI:** Mark as processed.
**Stale:** Confirm before marking as processed.

### 7. Update tracking (REQUIRED)

**Before ending this workflow, Claude MUST append all processed item identifiers to `{Home Directory}/slack/.processed-saved`** — one `channel_id:message_ts` per line. Deferred items (no decision made) should NOT be added.

### 8. Summary

After processing: [N] responses drafted, [N] items added to backlog, [N] marked FYI/stale, [N] deferred.

## Sub-agent Delegation Rules

All Slack search and read operations MUST go through sub-agents. This keeps raw Slack API output out of main context.

**Exception:** `slack_send_message_draft` calls can stay in main context.

## Error Handling

- If `is:saved` returns no results: "No saved items found."
- If `detailed` format fails: Do NOT retry with `concise`. Report the error.
- If thread read fails: skip it, continue with the rest.
- If draft creation fails: show the draft text so {PM Name} can copy-paste manually.

## Output Style

- Interactive — walk through items, don't dump a list
- Be opinionated about categories
- Keep message previews short (1-2 sentences)
- For draft responses, match {PM Name}'s communication style
