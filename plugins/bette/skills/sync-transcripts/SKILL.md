---
name: sync-transcripts
description: Sync meeting transcripts and process them. Use when user says "sync my transcripts", "process my morning meetings", "process my most recent meetings", "process today's meetings", or any request for meetings from TODAY. Runs the backup script first, then triggers the daily digest workflow.
---

# Sync My Transcripts

Pull latest transcripts, then run the daily digest.

## When to Use This Skill

**This skill runs the transcript backup FIRST.** Use when:
- "sync my transcripts"
- "process my morning meetings"
- "process my most recent meetings"
- "process today's meetings"
- "what happened in my [meeting name] meeting?" (if meeting was today)
- Any request for meetings from TODAY

**Do NOT use this skill when:**
- "Daily digest" — use `/digest` instead (assumes transcripts already exist)
- "Process yesterday's meetings" — use `/digest` instead
- Requests for meetings from previous days — use `/digest` instead

## Workflow

### 1. Run transcript backup

```bash
{Transcript Backup Script}
```

Wait for sync to complete. This pulls the latest meeting transcripts into `{Transcript Directory}`.

If no backup script is configured, skip this step and note that transcripts should be manually placed in the transcript directory.

### 2. Run daily digest

After sync completes, invoke the `/digest` skill to process newly synced transcripts.

The digest skill handles all downstream updates:
- `.processed` tracking file
- `INDEX.md` transcript index (tags, series, chronological table)

If the digest skill is not available as a direct invocation, run the digest workflow manually:
1. Read `.processed` tracking file
2. List new transcripts from last 48 hours
3. Filter to unprocessed only
4. Extract and categorize (to-dos, meeting topics, coaching notes, strategic insights)
5. Output consolidated digest
6. Update `.processed` file
7. Update `INDEX.md` — add new entries with content-based tags and series
