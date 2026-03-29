---
name: email-find
description: Find a specific email or conversation. Use when user says "find the email about", "find the email from [name]", "where's that email about", "search my email for", or similar. Searches Gmail, resolves names from people.md, and presents results with action options.
---

# Email Find

Find a specific email or conversation based on natural language description. Search, present results, and offer actions.

## Context Files

Read this first:
- `{Home Directory}/reference/people.md` — who's who (for name resolution and disambiguation)

## Gmail Configuration

- **Search tool:** `mcp__claude_ai_Gmail__gmail_search_messages`
- **Read tools:** `mcp__claude_ai_Gmail__gmail_read_message`, `mcp__claude_ai_Gmail__gmail_read_thread`
- **Draft tool:** `mcp__claude_ai_Gmail__gmail_create_draft`

## Workflow

### 1. Parse request

Extract from natural language:

- **Person** — "from Sarah", "email from Austin", "what Jamie sent"
- **Topic/keywords** — "about the quarterly report", "about the contract"
- **Time range** — "last week", "from yesterday", "in January" (optional)
- **Has attachment** — "the one with the spreadsheet", "with the PDF" (optional)

### 2. Resolve names

If a person is mentioned:

1. Look up in `{Home Directory}/reference/people.md` for full name and context
2. Check disambiguation notes for people who share first names
3. If ambiguous, ask {PM Name} to clarify before searching
4. Use the resolved email or full name in the Gmail `from:` search filter

### 3. Build search query

Construct a Gmail search query using available operators:

- `from:sender@example.com` or `from:name` — filter by sender
- `to:recipient@example.com` — filter by recipient
- `subject:meeting` — filter by subject line
- `has:attachment` — if an attachment was mentioned
- `after:YYYY/M/D` / `before:YYYY/M/D` — date range
- `"exact phrase"` — exact phrase match
- Keywords — topic words for broad match

### 4. Search Gmail

Use `mcp__claude_ai_Gmail__gmail_search_messages` with the constructed query, maxResults 10.

**Refinement strategy (up to 3 attempts):**
- If too many results (> 10): add date filters or more specific keywords
- If too few results (0): remove the `from:` filter, broaden keywords, or try alternative phrasing
- If wrong results: adjust keywords based on what came back

Tell {PM Name} what query was used so they can help refine if needed.

### 5. Present results

```
## Email Search: "[what was asked for]"

Query used: `[the Gmail search query]`
Results: [N] emails found

### 1. From: [Sender] — [date]
   Subject: [subject line]
   > [Snippet — first 2-3 sentences]
   Thread: [message count] messages / Single email

### 2. From: [Sender] — [date]
   Subject: [subject line]
   > [Snippet]
   Thread: [message count] messages / Single email
```

If more than 5 results, present the top 5 most relevant and note there are more.

Then ask: "Is one of these what you're looking for? I can:"
- **Read the full thread** (if it's a conversation)
- **Read the full message** (if it's a single email)
- **Draft a reply** (creates a Gmail draft for review)
- **Add to backlog** (captures as a BACKLOG.md item)
- **Search again** (with different terms)

### 6. Handle follow-up actions

**Read full thread:**
- Short threads (< 10 messages): read directly
- Long threads (10+): delegate to sub-agent for summary
- After presenting, re-offer: draft reply or add to backlog

**Draft a reply:**
- Ask what to say (or suggest a response based on context)
- Use `mcp__claude_ai_Gmail__gmail_create_draft`
- Show draft text for approval before creating
- Use `contentType: "text/plain"` by default

**Add to backlog:**
- Append to `{Home Directory}/BACKLOG.md` under the appropriate priority section
- Format: `- **[Brief description]** — [context from email].`

## Error Handling

- If search returns no results: suggest alternative search terms, try removing filters.
- If thread read fails: offer to try reading individual messages instead.
- If name is ambiguous: present options and ask to clarify before searching.
- If draft creation fails: show the draft text for manual copy-paste.
- If Gmail MCP is not connected: report and suggest checking MCP settings.

## Output Style

- Quick and focused — hunting for a specific email, not browsing
- Present just enough context to identify the right email
- Be proactive about suggesting follow-up actions
- Show the query used for refinement
- Reference people.md for sender context
