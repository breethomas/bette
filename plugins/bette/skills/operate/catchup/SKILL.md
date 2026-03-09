---
name: catchup
description: Catch up on all inbound messaging. Use when user says "catch me up", "what did I miss", "morning catchup", "process my inbox", "what's waiting for me", or similar. Orchestrates email inbox, Slack saved items, and optionally Slack channel catchup. Presents a consolidated view.
---

# Catchup

Catch {PM Name} up on everything missed across all messaging channels. Orchestrate email and Slack triage in one pass.

## Context Files

Read these first:
- `{Home Directory}/BACKLOG.md` — current priorities
- `{Home Directory}/reference/people.md` — who's who
- `{Home Directory}/GOALS.md` — current goals (for connecting items to priorities)

## Workflow

### 1. Determine scope

Check if {PM Name} specified what to catch up on:

- **"Catch me up"** / **"what did I miss"** (no qualifier) → Run email + Slack saved items. Ask if they also want Slack channels.
- **"Catch me up on everything"** → Run email + Slack saved + ask which Slack channels.
- **"Catch me up on email"** → Run email only (invoke `/email-inbox` directly).
- **"Catch me up on Slack"** → Run Slack saved + ask about channels (invoke `/slack-inbox` and optionally `/slack-catchup`).

Default scope (no qualifier): **Email inbox + Slack saved items.** Slack channels are opt-in.

### 2. Fan out to sub-agents

Run email and Slack processing in parallel using the Agent tool. Each agent runs independently and writes results to a file.

**Email agent:**
Launch an Agent (`subagent_type: general-purpose`) with this prompt:

> You are processing {PM Name}'s Gmail inbox. Follow these steps:
>
> 1. Read `{Home Directory}/reference/people.md` for name resolution
> 2. Read `{Home Directory}/email/.processed-inbox` (create if it doesn't exist) for already-processed IDs
> 3. Call `mcp__claude_ai_Gmail__gmail_get_profile` to confirm the account
> 4. Search Gmail with `mcp__claude_ai_Gmail__gmail_search_messages` using query `is:starred OR (is:unread -category:promotions -category:social -category:updates)`, maxResults 30
> 5. Filter out any messageIds already in `.processed-inbox`
> 6. For remaining items, read threads with `mcp__claude_ai_Gmail__gmail_read_thread` to get conversation context
> 7. Categorize each item as: Respond (waiting on {PM Name}), Action (to-do outside email), FYI (informational), or Stale (old/resolved)
> 8. Write results to `{Home Directory}/drafts/catchup-email.md` in this format:
>
> ```
> # Email Inbox — [Date]
>
> [N] emails to triage
>
> ## Respond ([count])
> 1. From: [Sender name (role from people.md)] — [relative time]
>    Subject: [subject]
>    > [Snippet]
>    Thread: [message count]. [Waiting on {PM Name}: yes/no]
>    messageId: [id]
>    threadId: [id]
>
> ## Action ([count])
> ...
>
> ## FYI ([count])
> ...
>
> ## Stale ([count])
> ...
> ```
>
> Prioritize: direct emails to {PM Name} > exec team/direct reports > others. Be opinionated about categories.
> End your response with: EMAIL_FILE: {Home Directory}/drafts/catchup-email.md

**Slack agent:**
Launch an Agent (`subagent_type: general-purpose`) with this prompt:

> You are processing {PM Name}'s saved Slack items. Follow these steps:
>
> 1. Read `{Home Directory}/reference/people.md` for name resolution
> 2. Read `{Home Directory}/slack/.processed-saved` (create if it doesn't exist) for already-processed items
> 3. Search Slack with `mcp__claude_ai_Slack__slack_search_public_and_private` using query `is:saved`, response_format `detailed`, sort `timestamp`, sort_dir `desc`
> 4. Filter out any `channel_id:message_ts` pairs already in `.processed-saved`
> 5. For remaining items with thread replies, read threads with `mcp__claude_ai_Slack__slack_read_thread` to get context. Check if {PM Name} (user ID {Slack User ID}) has already replied.
> 6. Categorize each item as: Respond (@mention or question, {PM Name} hasn't replied), Action (to-do outside Slack), FYI (informational), or Stale (old/resolved)
> 7. Write results to `{Home Directory}/drafts/catchup-slack.md` in this format:
>
> ```
> # Slack Saved Items — [Date]
>
> [N] saved items to triage
>
> ## Respond ([count])
> 1. [Author] in #[channel] — [relative time]
>    > [Message preview — first 1-2 sentences]
>    Thread: [reply count]. {PM Name} replied: [yes/no]
>    channel_id: [id], message_ts: [ts]
>
> ## Action ([count])
> ...
>
> ## FYI ([count])
> ...
>
> ## Stale ([count])
> ...
> ```
>
> Priority: @mentions of {PM Name} > direct questions > action items > decisions > FYI.
> End your response with: SLACK_FILE: {Home Directory}/drafts/catchup-slack.md

### 3. Present consolidated view

After both agents complete, read the output files and present a unified summary:

```
## Catchup — [Date]

### Email: [N] items
- [X] need a response
- [Y] have action items
- [Z] FYI/stale

### Slack: [N] items
- [X] need a response
- [Y] have action items
- [Z] FYI/stale

### Respond First ([total across both channels])

**Email:**
1. [Sender] — [subject] — [relative time]
   > [snippet]

**Slack:**
2. [Author] in #[channel] — [relative time]
   > [message preview]

### Actions to Capture ([total])
3. [Source: Email/Slack] — [brief description]
4. ...

### FYI / Stale ([total])
5. [Source] — [brief description] — [why it's FYI/stale]
```

Then ask: "Want to walk through the respond items first? I can draft replies for email and Slack as we go."

### 4. Interactive triage

Walk through items with {PM Name}, starting with "Respond" category across both channels:

**For email items:**
- Read the full thread if needed (delegate to sub-agent for long threads)
- Draft a reply via `mcp__claude_ai_Gmail__gmail_create_draft`
- Show draft text for approval before creating

**For Slack items:**
- Read the full thread if needed (delegate to sub-agent)
- Draft a reply via `mcp__claude_ai_Slack__slack_send_message_draft`
- Use Slack mrkdwn format (single `*bold*`, `_italic_`)
- Handle `draft_already_exists` gracefully

**For action items (both channels):**
- Append to `{Home Directory}/BACKLOG.md` under appropriate priority section
- Format: `- **[Brief description]** — [context]. [Source: Gmail/Slack permalink if available]`

**For FYI/stale items:**
- Mark as processed after confirmation

### 5. Slack channel catchup (optional)

If {PM Name} opted in to channel catchup, ask which channels. Then invoke `/slack-catchup` with the specified channels.

If not specified, suggest: "Want me to also catch you up on any Slack channels? Just name them, or say skip."

### 6. Update tracking (REQUIRED)

**Before ending this workflow, Claude MUST update both tracking files:**

1. Append processed email messageIds to `{Home Directory}/email/.processed-inbox` — one messageId per line
2. Append processed Slack items to `{Home Directory}/slack/.processed-saved` — one `channel_id:message_ts` per line

Only add items that were actually triaged. Deferred items stay off the list.

### 7. Final summary

```
## Catchup Complete

- Email: [N] drafted, [N] to backlog, [N] cleared
- Slack: [N] drafted, [N] to backlog, [N] cleared
- Deferred: [N] items (will appear next catchup)

Drafts to review:
- Gmail: [N] drafts waiting in Gmail
- Slack: [N] drafts waiting in Slack "Drafts & Sent"
```

## Error Handling

- If Gmail MCP is not connected: skip email, note it, proceed with Slack only
- If Slack MCP is not connected: skip Slack, note it, proceed with email only
- If both are unavailable: tell {PM Name} neither integration is available
- If one agent fails: present results from the successful one, note the failure, offer to retry
- If a draft file wasn't written by a sub-agent: report what happened and offer to run that channel manually

## Output Style

- Start with the big picture (how many items across channels), then drill into details
- Be opinionated about what matters most — {PM Name} wants Claude's judgment
- Keep it moving — don't belabor FYI items
- Match {PM Name}'s voice for all drafts: direct, concise, no fluff
- Cross-reference items when the same topic appears in both email and Slack
