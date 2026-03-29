---
name: session-check
description: >
  Check if it's time to save session notes and restart. Prevents context rot.
  Use when user says 'session check', 'should I restart', 'save session notes',
  'context getting stale'.
user-invocable: true
---

# Session Check

Assess current session health, suggest saving notes if appropriate, and help create session notes for a clean handoff.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 SESSION CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Let me assess the current session.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then immediately perform the assessment (do not wait for user input).

## Context

Context rot is real. AI assistants lose coherence over long sessions. Managing sessions is as important as managing the work itself. This skill helps the user decide whether to continue or restart, and captures state cleanly either way.

Reference: `docs/core-principles.md` (Session Management section) for the full framework.

## Workflow

### Step 1: Assess Session Health

Evaluate these signals by reviewing the conversation so far:

**Task count:**
- How many distinct tasks or features has the user completed this session?
- 1 task: session is fresh
- 2-3 tasks: consider saving notes
- 4+ tasks: strongly recommend restart

**Context signals:**
- Has Claude had to re-read files it already read earlier?
- Has Claude suggested approaches that contradict earlier decisions?
- Has the user had to re-explain things covered earlier?
- Are responses getting longer or more verbose (a sign of context pressure)?

**Work type:**
- Coding sessions: more context-intensive, restart sooner
- Writing/editing sessions: can run longer
- Mixed sessions: restart sooner

### Step 2: Report the Assessment

Present the assessment clearly:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 SESSION HEALTH

 Tasks completed:     [N]
 Context pressure:    [Low / Medium / High]
 Recommendation:      [Continue / Save notes & continue / Save notes & restart]

 [Reasoning in 1-2 sentences]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Recommendation logic:**

- **Continue** — 1 task done, no context pressure signals, work is coherent
- **Save notes & continue** — 2-3 tasks done, session is still coherent but should capture state as insurance
- **Save notes & restart** — 4+ tasks done, OR context pressure signals present, OR user reports quality decline

### Step 3: Generate Session Notes

If the recommendation is to save notes (or the user asks for them regardless), generate session notes.

**Determine save location:**

1. Check if the project has a session notes convention:
   - Look for `.claude/sessions/` directory
   - Look for `docs/sessions/` or `docs/dev-sessions/` directory
   - Look for a `dev-log.md` file
2. If found, use the existing convention
3. If not found, ask the user:

```
Where should I save session notes?

Options:
- .claude/sessions/[date]-[description].md (Claude convention)
- docs/sessions/[date]-[description].md (team convention)
- dev-log.md (append to running log)
- Somewhere else?
```

**Generate the notes using this template:**

```markdown
# [Date] - [Brief Description of Work]

## Done
- [Completed task 1 — specific, not vague]
- [Completed task 2]
- [Completed task 3]

## Current State
- [What's working / deployed / merged]
- [What's in progress but not finished]
- [What's broken or blocked]

## Next
1. [Most immediate task]
2. [Following task]
3. [Task after that]

## Patterns / Decisions
- [Key decision made and why]
- [Pattern established for future reference]
- [Convention chosen and rationale]

## Resume Prompt
> [Exact text the user can paste to start the next session with full context.
> Include: files to read, where work left off, what to do next.]
```

**Notes quality rules:**
- "Done" items must be specific. "Worked on feature" is bad. "Added user auth endpoint with JWT validation" is good.
- "Current State" must distinguish between done, in-progress, and broken.
- "Next" items must be actionable. "Continue working" is bad. "Write tests for the auth middleware" is good.
- "Resume Prompt" must be self-contained. A fresh Claude session with only this prompt should be able to pick up cleanly.

### Step 4: Save and Confirm

1. Write the session notes to the determined location
2. Confirm:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 SESSION NOTES SAVED

 Location: [file path]

 [If restart recommended:]
 Restart when ready. Paste the Resume Prompt to pick up
 where you left off.

 [If continue recommended:]
 Notes saved as insurance. Keep going — session is still healthy.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Proactive Invocation

Claude should suggest this skill after completing 2-3 major tasks in any session, even if the user does not invoke it. Use a light touch:

```
We've completed [N] tasks this session. Want to save session
notes before continuing? (/session-check)
```

Do not nag. Suggest once. If the user declines, continue working.

## Rules

- Do the assessment automatically when invoked. Do not ask the user to self-report on session health.
- Base the assessment on observable signals from the conversation, not guesses.
- Session notes must be concrete and specific, not generic summaries.
- The Resume Prompt is the most important part of the notes. A new session with only that prompt should work.
- Never recommend restarting during the first task of a session.
- If the user is in the middle of something, suggest finishing the current task before saving notes.
