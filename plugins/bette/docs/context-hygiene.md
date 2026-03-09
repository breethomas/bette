# Context Hygiene

How to keep AI sessions productive as context grows.

---

## The Problem

AI context windows are large but not infinite. Every file you read, every tool result you pull in, every long response — it all accumulates. When context fills up, older information gets compressed or dropped. Quality degrades.

Context hygiene is the practice of being intentional about what enters your AI session.

## The Core Rule

**Read for editing. Delegate for reference.**

Before reading a file, ask: "Am I reading this to edit it, or to reference it?"

- **Editing:** Read it directly. You need the full content to make changes.
- **Reference:** Delegate to a sub-agent with a specific extraction prompt. Only the answer comes back, not the full content.

This one rule prevents most context bloat.

## What Bloats Context

### Large Files Read for Reference
Reading a 500-line document to find one fact wastes 499 lines of context.

**Instead:** Delegate to a sub-agent: "Extract the pricing decision from this document."

### Raw Tool Output
API calls, database queries, and MCP tool results often return far more data than you need.

**Instead:** Structure your queries to return only what's needed, or delegate the query to a sub-agent that summarizes before returning.

### Full Transcripts
Meeting transcripts are the worst offenders — they're long, mostly noise, and rarely need to be read in full.

**Instead:** Always delegate transcript processing: "Extract action items and decisions from this transcript."

### Accumulated Conversation History
Long sessions accumulate responses, tool results, and back-and-forth. The AI starts losing its grip on early context.

**Instead:** Restart sessions after 2-3 major tasks. Save state to session notes.

## The Delegation Pattern

Sub-agents (background tasks) are your context hygiene tool. They get their own context window, do the heavy reading, and return only what you asked for.

### How It Works

```
Main session (clean context)
  │
  ├── "Extract pricing discussion from transcript"
  │     └── Sub-agent reads full transcript → returns 5-line summary
  │
  ├── "Find architecture decision on Notion page"
  │     └── Sub-agent fetches page → returns the relevant section
  │
  └── "Summarize the key changes in this 400-line draft"
        └── Sub-agent reads draft → returns bullet summary
```

Main context stays clean. Sub-agents do the heavy lifting.

### When to Delegate

| Content | Size | Action |
|---------|------|--------|
| Transcripts | Any | Always delegate |
| PDFs | Any | Always delegate |
| Notion pages | > 200 lines | Delegate (unless editing) |
| Code files | > 200 lines | Read if editing, delegate if referencing |
| API/tool results | Large | Structure query to return less, or delegate |
| Drafts | > 200 lines | Read if editing, delegate if reviewing |

### When NOT to Delegate

- Files you're actively editing (you need the full content)
- Small files (< ~200 lines) used as working context
- Files the user explicitly asks to read
- Reference files loaded at session start (they're designed to be compact)

## Automation: Hooks

You can automate context hygiene checks using Claude Code hooks — scripts that run before tool calls and warn when you're about to bloat context.

### Example: File Size Warning

A hook on the Read tool that warns when reading large files:

```bash
#!/bin/bash
# Warn on files > 200 lines
FILE_PATH="$1"
LINE_COUNT=$(wc -l < "$FILE_PATH" 2>/dev/null || echo "0")
if [ "$LINE_COUNT" -gt 200 ]; then
  echo "CONTEXT HYGIENE: This file is $LINE_COUNT lines."
  echo "If reading for reference (not editing), delegate to a sub-agent."
fi
```

### Example: Transcript Guard

A hook that always warns when reading transcript files:

```bash
#!/bin/bash
# Always warn on transcript reads
FILE_PATH="$1"
if echo "$FILE_PATH" | grep -q "transcripts/"; then
  echo "CONTEXT HYGIENE: Transcript detected."
  echo "Delegate to sub-agent with extraction prompt."
fi
```

Hooks warn but don't block. This is intentional — sub-agents inherit hooks, so blocking would prevent the delegation pattern from working.

## Output Routing

When sub-agents process heavy content, their raw output can also bloat context if pulled back in full.

### The Problem

```
Main: "Process this transcript"
  └── Sub-agent: [returns 200 lines of extracted content]
Main: [200 lines now in main context anyway]
```

### The Fix

Have sub-agents write output to files instead of returning it directly:

```
Main: "Process this transcript, write results to drafts/digest.md"
  └── Sub-agent: [reads transcript, writes to file]
Main: [reads the file — same content, but controlled]
```

This gives you control over when and how much of the output enters main context. You can read the summary section without loading the full extraction.

---

## Session Lifecycle

### Start of Session
1. CLAUDE.md files load automatically (these should be compact)
2. Reference files load per CLAUDE.md instructions (designed for efficiency)
3. Memory files load automatically (keep MEMORY.md under 200 lines)

### During Session
4. Read files you're editing directly
5. Delegate heavy reads to sub-agents
6. Restart after 2-3 major tasks

### End of Session
7. Save session notes (what was done, what's next)
8. Update reference files if new context was discovered
9. Update memory if stable patterns emerged

---

## Measuring Context Health

Signs your context is healthy:
- AI remembers instructions from early in the session
- Responses stay consistent with established patterns
- No re-explanation needed

Signs your context is bloated:
- AI suggests approaches different from what you established
- Having to re-explain things covered earlier
- Response quality declining
- More back-and-forth to get correct output

When you notice bloat: save state, restart session, load clean context.

---

*Context is a budget. Spend it on what matters. Delegate the rest.*
