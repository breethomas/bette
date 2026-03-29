---
name: log-meeting
description: Log notes from a meeting with someone. Use when user says "log 1:1 with [name]", "capture notes from [name]", "save meeting notes for [name]", or similar. Captures topics discussed, commitments, and follow-ups. Writes to the person's file.
---

# Log Meeting Notes

Capture notes from a meeting and update the person's file. Takes a person name as argument.

## Argument

`$ARGUMENTS` = person name (e.g., "chris", "Chris Johnson", "taylor")

Normalize the name to find the right file:
- Check `{People Directory}/` for matching filename (lowercase)
- If full name given, match against `{Home Directory}/reference/people.md`

## Workflow

### 1. Load context

Read `{People Directory}/[name].md` — review the current topics and recent history.

### 2. Capture notes

Ask {PM Name} what was discussed (or they'll paste/dictate the notes). Capture:
- Topics discussed
- Commitments made (by {PM Name} and by them)
- Follow-ups needed
- Key decisions

### 3. Update person file

1. Append new entry under `## 1:1 Notes` with today's date
2. Update `## 1:1 Topics (Next Meeting)` — check off items discussed, add new ones surfaced
3. Add any wins to `## Wins & Accomplishments`
4. If escalation needed, add to `{Home Directory}/BACKLOG.md`

### 4. Confirm

Show {PM Name} the updates before writing to confirm accuracy.

## Output Style

- Interactive — ask for notes, confirm before writing
- Keep entries concise but complete
- Use consistent date format (YYYY-MM-DD)
