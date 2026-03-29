---
name: save-notion
description: Save content from the current session to Notion. Use when user says "save to Notion", "put this in Notion", or similar. Creates a subpage under the PM's configured Notion page.
---

# Save to Notion

Save content from the current session to a Notion page.

## Argument

`$ARGUMENTS` = optional title or topic for the page. If not provided, infer from the content being saved.

## Destination

All saves go to `{Notion Default Parent Page}` — the PM's configured Notion page.

If `{Notion WIP Page}` is also configured and the PM says "save to WIP", use that instead. Otherwise ignore — one destination is fine.

## Workflow

### 1. Identify content

Take the content from the current session — digest, notes, summary, analysis, or whatever the PM wants to persist.

### 2. Create Notion page

Use Notion MCP to create a subpage:
```
mcp__notion__notion-create-pages with parent {"page_id": "<destination_page_id>"}
```

**Title format:** `[Type] — [Topic] ([Date])`
- Examples:
  - "Digest — Cycle Planning (Jan 7, 2026)"
  - "Analysis — Engagement Pricing Options (Feb 3, 2026)"
  - "Meeting Prep — Chris Johnson (Feb 7, 2026)"

### 3. Confirm

Report the URL of the created page to {PM Name}.
