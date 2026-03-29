---
name: slack-find
description: Find a specific Slack message or conversation. Use when user says "find the Slack message about", "hunt down the message from [name] about", "find what [name] said about", "where did someone say [topic] in Slack", "find that Slack thread", or similar. Searches public and private channels, resolves names from people.md, and presents results with action options.
---

# Slack Find

Find a specific Slack message or conversation based on natural language description. Search, present results, and offer actions.

## Context Files

Read this first:
- `{Home Directory}/reference/people.md` — who's who (for name resolution and disambiguation)

## Slack Configuration

- **PM's Slack user ID:** `{Slack User ID}`
- **Search tool:** `mcp__claude_ai_Slack__slack_search_public_and_private` (searches all channels, DMs, Group DMs)
- **CRITICAL:** Always use `detailed` format. The `concise` format crashes the MCP.

## Workflow

### 1. Parse the request

The PM will describe what they're looking for in natural language. Extract:

- **Person** — "from Sarah", "what Jay said", "message from Austin"
- **Topic/keywords** — "about the migration", "about domain renewal", "the API contract"
- **Channel** — "in #product", "in the #engineering channel" (optional, often not specified)
- **Time range** — "last week", "from yesterday", "in January" (optional)

### 2. Resolve names

If a person is mentioned:

1. Look up in `{Home Directory}/reference/people.md` for full name
2. Check for disambiguation — if multiple people share a first name, ask which one
3. Use the full name in the `from:` search filter (Slack search handles first/last name matching)
4. Only fall back to `mcp__claude_ai_Slack__slack_search_users` if the name is not in people.md

### 3. Build search query

Construct a Slack search query using available operators:

- `from:[full name]` — filter by sender
- `in:[channel-name]` — filter by channel (no # prefix)
- `before:YYYY-MM-DD` / `after:YYYY-MM-DD` — date range
- Keywords — topic words, unquoted for broad match or `"quoted"` for exact phrase
- `has:link` / `has:file` — if a link or file is mentioned

### 4. Search Slack

Use `mcp__claude_ai_Slack__slack_search_public_and_private` with the constructed query, format `detailed`.

**Refinement strategy (up to 3 attempts):**
- If too many results (> 10): add date filters or more specific keywords
- If too few results (0): remove the `from:` filter, broaden keywords, or try alternative phrasing
- If wrong results: adjust keywords based on what came back

Tell {PM Name} what query was used so they can help refine if needed.

### 5. Present results

```
## Slack Search: "[what was asked for]"

Query used: `[the Slack search query]`
Results: [N] messages found

### 1. [Author] in #[channel] — [date/time]
> [Message text — first 2-3 sentences]
Thread: [N] replies / No thread
[Permalink]

### 2. [Author] in #[channel] — [date/time]
> [Message text — first 2-3 sentences]
Thread: [N] replies / No thread
[Permalink]
```

If more than 5 results, present the top 5 most relevant and note there are more.

Then ask: "Is one of these what you're looking for? I can:"
- **Read the full thread** (if it has replies)
- **Draft a response** (creates a Slack draft for review)
- **Add to backlog** (captures as a BACKLOG.md item with permalink)
- **Search again** (with different terms)

### 6. Handle follow-up actions

**Read full thread:**
- If short (< 20 replies), use `mcp__claude_ai_Slack__slack_read_thread` directly
- If long (20+ replies), delegate to a sub-agent with extraction prompt
- After presenting the thread, re-offer: draft response or add to backlog

**Draft a response:**
- Ask {PM Name} what they want to say (or suggest a response based on context)
- Use `mcp__claude_ai_Slack__slack_send_message_draft` with appropriate `thread_ts` if replying to a thread
- Use Slack mrkdwn format (single `*bold*`, `_italic_`, backtick code)
- Show the draft text before creating it
- Handle `draft_already_exists` gracefully — suggest clearing the existing draft

**Add to backlog:**
- Append to `{Home Directory}/BACKLOG.md` under the appropriate priority section
- Format: `- **[Brief description]** — [context from Slack thread]. [Slack permalink]`
- Confirm what was added

**Search again:**
- Ask for refinement ("different keywords? different person? different time range?")
- Rebuild query and search again

## Error Handling

- If search returns no results: suggest alternative search terms, try removing filters, expand the date range.
- If `detailed` format fails: do NOT retry with `concise`. Report the error.
- If name is ambiguous: present options and ask to clarify before searching.
- If draft creation fails: show the draft text so the PM can copy-paste manually.

## Output Style

- Quick and focused — the PM is hunting for a specific message, not browsing
- Present just enough context to identify the right message (2-3 sentences per result)
- Always include the permalink so the PM can jump to it in Slack
- Be proactive about suggesting follow-up actions
- Show the query used so the PM can help refine if results aren't right
