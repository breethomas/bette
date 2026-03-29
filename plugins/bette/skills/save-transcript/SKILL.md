---
name: save-transcript
description: Save a meeting transcript from clipboard/paste. Use when user pastes a meeting transcript, says "save this transcript", "save transcript from [meeting]", "log this transcript", or similar. Writes a properly formatted markdown file to the transcripts directory.
---

# Save Transcript

Take pasted transcript content and save it as a properly formatted markdown file.

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Resolve `{Transcript Directory}` and `{PM Name}` from the Config table before executing.

## Workflow

### 1. Get the content

{PM Name} will either:
- Paste transcript text directly into the chat
- Say "save this transcript" after pasting content
- Provide a meeting name and then paste

If no content has been pasted yet, ask: "Paste the transcript and I'll save it."

### 2. Extract meeting metadata

From the pasted content or conversation context, determine:
- **Meeting title** — ask if not obvious from the content
- **Date and time** — look for timestamps in the pasted content, ask if not found
- **Participants** — extract from the transcript if present

If the date/time isn't clear, ask: "When was this meeting? I need the date and approximate start time."

### 3. Write the file

Save to `{Transcript Directory}/` using this naming convention:

**Filename:** `YYYY-MM-DD_HHMM_Meeting_Title.md`
- Date and time from the meeting (not when it's being saved)
- Meeting title with spaces replaced by underscores
- No special characters in the filename

**File format:**

```
# [Meeting Title]

**Date:** YYYY-MM-DD
**Time:** HH:MM
**Participants:** [names if known]

---

[Full transcript content as pasted]
```

### 4. Confirm

Report:
- File saved: `[filename]`
- Location: `{Transcript Directory}/[filename]`
- Ready for `/digest` to pick up

## Output Style

- Fast and simple — this should take 10 seconds
- Only ask questions if date/time or meeting title can't be inferred
- Don't edit or summarize the transcript content — save it as-is
