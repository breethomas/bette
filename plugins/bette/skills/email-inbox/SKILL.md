---
name: email-inbox
description: Process the PM's email inbox. Use when user says "process my email", "email inbox", "what's in my email", "triage my email", "check my email", or similar. Pulls starred/unread emails, categorizes them, drafts replies, and adds action items to backlog. Interactive triage — discusses each item with the user.
---

# Email Inbox

Process {PM Name}'s inbox in one pass. Pull starred and unread emails, categorize, and triage interactively.

## Context Files

Read these first:
- `{Home Directory}/BACKLOG.md` — current priorities (to avoid duplicating existing items)
- `{Home Directory}/reference/people.md` — who's who (for name resolution)
- `{Home Directory}/email/.processed-inbox` — already-processed email IDs (create file if it doesn't exist)

## Email MCP Configuration

**Primary: Superhuman MCP** (`mcp__claude_ai_Superhuman_Mail__*`). Superhuman is {PM Name}'s email client; prefer it for every operation so read-statuses, drafts, and actions stay in sync with what {PM Name} sees in Superhuman.

- **List / search:** `mcp__claude_ai_Superhuman_Mail__query_email_and_calendar` (cross-search with calendar) or `list_threads`
- **Read:** `get_message` (single), `get_thread` (conversation)
- **Draft:** `create_or_update_draft` — always draft, never send automatically
- **Follow-up signals:** `get_read_statuses` — check whether recipients have opened {PM Name}'s earlier outbound emails (useful for prioritizing who to re-ping)
- **Inbox hygiene:** `unsubscribe` (for newsletter-style FYI items), `trash_thread` (for stale items), `mark_spam` (for obvious spam)

**Fallback: Gmail MCP** (`mcp__claude_ai_Gmail__*`) only if Superhuman MCP is disconnected. Gmail retains granular label CRUD, which Superhuman exposes read-only — if {PM Name} asks to add or rename labels mid-triage, use Gmail for that specific operation.

- **Drafts only:** never auto-send. {PM Name} reviews and sends from Superhuman.
- **Plain text default:** use plain text unless asked for HTML formatting.

## Priority Hierarchy

1. Emails where {PM Name} is directly addressed (To:, not just CC'd)
2. Emails from exec team, direct reports, or key stakeholders (reference people.md)
3. Emails requiring a decision or response
4. Action items (things to do outside email)
5. FYI / newsletters / automated notifications

## Workflow

### 1. Gather inbox items (delegate to sub-agent)

Delegate the search to a sub-agent using the Agent tool (`subagent_type: general-purpose`). The sub-agent should:

1. Query Superhuman with `query_email_and_calendar` for starred + unread mail (exclude promotions/social/updates categories), maxResults 30
2. If Superhuman is unavailable, fall back to Gmail `gmail_search_messages` with query `is:starred OR (is:unread -category:promotions -category:social -category:updates)`
3. For each result, extract: messageId, threadId, subject, from, to, date, snippet (first 200 chars), labels
4. Return a structured numbered list with clear field labels

### 2. Filter already-processed items

Read `{Home Directory}/email/.processed-inbox`. For each email from step 1, check if the `messageId` exists in the file. Remove matches — only present unprocessed items.

If no unprocessed items remain, tell {PM Name} "No new emails to process" and stop.

### 3. Enrich with thread context (delegate to sub-agent)

For emails that are part of a conversation, delegate `get_thread` reads to a sub-agent. Batch thread reads into a single sub-agent call (up to 10 threads). If more than 10 unprocessed items, use multiple sub-agent calls.

### 4. Categorize each item

- **Respond** — Someone emailed {PM Name} directly and is waiting for a reply. The thread is open and {PM Name} hasn't responded to the latest message. Highest priority.
- **Action** — Contains a to-do that happens outside email (review a doc, follow up on something, make a decision).
- **FYI** — Informational. {PM Name} was CC'd, or it's a status update, newsletter, or notification that needs no action.
- **Stale** — Old (> 2 weeks), already resolved, or no longer relevant.

### 5. Present interactively

Present items grouped by category, most actionable first. Then ask: "Want to walk through these one by one, or should I handle the obvious ones (draft responses, add backlog items, mark stale as processed) and just bring you the judgment calls?"

### 6. Process each item

**Respond items:**
1. Read the full thread if needed (delegate to sub-agent for long threads)
2. If {PM Name} has sent earlier outbound mail in this thread, consider checking `get_read_statuses` before drafting — if the recipient hasn't opened the previous message, the reply strategy may differ (e.g., forward + nudge vs. assume context)
3. Draft a response matching {PM Name}'s voice: direct, concise, no fluff
4. Show the draft text before creating it
5. After approval, create draft via `mcp__claude_ai_Superhuman_Mail__create_or_update_draft` (Gmail `gmail_create_draft` as fallback)
6. Tell {PM Name} the draft is in Superhuman drafts — review and send from there

**Action items:**
1. Append to `{Home Directory}/BACKLOG.md` under the appropriate priority section
2. Format: `- **[Brief description]** — [context from email].`
3. Confirm what was added

**FYI items:**
1. Mark as processed (no other action by default)
2. If it's a newsletter or subscription-style sender, offer `unsubscribe` as a one-shot clean-up
3. If {PM Name} wants to save the context, offer to add a note to the relevant person file or backlog

**Stale items:**
1. Confirm before marking as processed
2. Offer `trash_thread` if {PM Name} wants the thread out of the inbox, not just out of the triage queue
3. If {PM Name} disagrees with "stale", recategorize

### 7. Update tracking (REQUIRED)

**Before ending this workflow, Claude MUST append all processed email messageIds to `{Home Directory}/email/.processed-inbox`** — one messageId per line.

This includes ALL items that were presented and triaged. Do not skip this step. If an item was deferred (no decision made), do NOT add it to the processed list.

### 8. Summary

After processing all items:
- [N] responses drafted (check Superhuman drafts to review and send)
- [N] items added to backlog
- [N] items marked FYI/stale
- [N] items unsubscribed / trashed
- [N] items deferred (will appear next time)

## Sub-agent Delegation Rules

All email search and read operations MUST go through sub-agents. This keeps raw email API output out of main context.

**Exception:** `create_or_update_draft`, `unsubscribe`, `trash_thread`, `mark_spam`, and `get_read_statuses` calls can stay in main context — they are small write/read operations.

## Error Handling

- If search returns no results: "No starred or unread emails found. Inbox is clear."
- If thread read fails: skip it, note it was unreadable, continue with the rest.
- If draft creation fails: show the draft text so {PM Name} can copy-paste manually.
- If Superhuman MCP is not connected: retry with Gmail MCP; if both are down, tell {PM Name} and suggest checking MCP settings.

## Output Style

- Interactive — walk through items, don't just dump a list
- Be opinionated about categories — {PM Name} wants Claude's judgment
- Keep snippets short (1-2 sentences)
- For draft responses, match {PM Name}'s communication style: direct, no hedging, concise
- Reference people.md for sender context
