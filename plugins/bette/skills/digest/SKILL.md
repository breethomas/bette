---
name: digest
description: Process daily digest of meetings and action items. Use when user says "daily digest", "process yesterday's meetings", "what happened in my meetings", or similar. Reads unprocessed transcripts from last 48 hours, extracts action items, meeting topics, coaching notes, and strategic insights. Returns consolidated digest for review.
context: fork
model: sonnet
---

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Before executing, find and read the CLAUDE.md file in the project root (the directory containing BACKLOG.md and GOALS.md). Locate the Config table and resolve all `{Key}` placeholders in this skill to their configured values.

If no Config table is found, abort and report: "Cannot resolve config variables. Ensure CLAUDE.md has a Config table with {Home Directory}, {PM Name}, and other required keys."


# Daily Digest

Process unprocessed meeting transcripts and return a consolidated digest.

## Context Files

Read these first:
- `{Home Directory}/BACKLOG.md` — current priorities
- `{Home Directory}/GOALS.md` — quarterly goals
- `{Home Directory}/reference/people.md` — who's who
- `{Strategy Directory}/initiatives/{Strategy Framework}` — strategic framework

## Workflow

### 1. Identify unprocessed transcripts

1. Read `{Transcript Directory}/.processed` to get list of already-processed filenames
2. List all transcripts in `{Transcript Directory}` from the **last 48 hours only** (by filename date, format: `YYYY-MM-DD_HHMM_Meeting_Title.md`)
   - Transcripts older than 48 hours are either already processed or stale — skip them
   - If the PM wants to process an older transcript, they'll ask specifically
3. Filter to unprocessed only (not in `.processed`)
4. If no unprocessed transcripts found, report that and stop

### 2. Enrich with calendar context

If Google Calendar MCP is available, pull calendar events for the date(s) covered by unprocessed transcripts and match them to transcripts by time.

1. **Determine dates** from unprocessed transcript filenames (format: `YYYY-MM-DD_HHMM_Title.md`)
2. **Pull calendar events** for each date using the Google Calendar MCP:
   - `gcal_list_events(timeMin="YYYY-MM-DDT00:00:00", timeMax="YYYY-MM-DDT23:59:59", condenseEventDetails=false)`
   - Request full details (`condenseEventDetails=false`) to get attendee lists
3. **Match transcripts to events** by comparing transcript start time (from filename) to event start time. Match if within a 15-minute window.
4. **Build enrichment map** — for each matched transcript, capture:
   - Attendee list (names and emails from calendar)
   - Meeting description/agenda (from event description)
   - Organizer
5. **Flag mismatches** for the digest output:
   - Calendar events with no matching transcript (meetings attended but transcription may have missed)
   - Transcripts with no matching calendar event (ad hoc conversations)

**If Google Calendar MCP is NOT available:** Skip this step entirely. Note in the digest output that calendar enrichment was not available, so attendee lists are based on transcript detection only.

### 3. Read and extract

For each unprocessed transcript, read the full content and extract into these categories. **When calendar enrichment is available, include the attendee list and meeting description in the extraction context** — this improves speaker attribution and action item routing.

**To-dos for backlog:**
- Action items {PM Name} committed to
- Follow-ups mentioned
- Deadlines discussed
- Decisions that need to be made

**Meeting topics by person:**
- Things to discuss with specific people in upcoming meetings
- Tag by person name
- Look for person files in `{People Directory}/` to identify who has a tracking file

**Coaching notes:**
- Feedback on {PM Name}'s communication and leadership
- Missed opportunities or moments to note
- Use this lens: "From this transcript, give {PM Name} specific notes on what could have been done better to be a stronger colleague and product leader. What was done or missed, why it matters, and how to improve next time. Be concrete — include example wording or behaviors. Supportive and direct tone."
- Context: {PM Name} is a {PM Role}

**Strategic insights:**
- Connections to the strategic framework (`{Strategy Directory}/initiatives/{Strategy Framework}`)
- Growth loop impact — anything that accelerates or slows core loops
- Strategic priority alignment or divergence
- Anything that validates or challenges current strategy

### 4. Consolidate and write to file

Consolidate into a single digest organized by section (not by meeting). Be conservative — only surface items with clear signal, avoid noise.

**Write the full digest to:** `{Home Directory}/drafts/digest-[YYYY-MM-DD].md`

Use this format:

```
# Daily Digest — [Date]

## Meetings Processed

| Time | Meeting | Attendees | Source |
|------|---------|-----------|--------|
| 10:00 | [meeting name] | [names] | Calendar + Transcript |
| 09:31 | [meeting name] | [names] | Transcript only |

### Coverage Gaps
- **No transcript:** [calendar event name] at [time] with [attendees]
- **No calendar event:** [transcript name] at [time] — ad hoc or from another calendar

## To-Dos for Backlog
- [item] (from: [meeting name])
- ...

## Meeting Topics by Person
**[Person]:** [items]
**[Person]:** [items]
**Other:** [person]: [items]

## Coaching Notes
[1-3 notes, each one paragraph]

## Strategic Insights
- [insight and connection to strategic framework]
```

**Notes:**
- Use calendar attendee names when available. Fall back to transcript participant detection for unmatched transcripts.
- Only include Coverage Gaps section if there are actual gaps to report.

### 5. Update tracking (REQUIRED)

**Before ending this workflow, Claude MUST append all processed filenames to `{Transcript Directory}/.processed`** — one filename per line. Do not skip this step.

### 6. Update transcript index (REQUIRED)

**Add each newly processed transcript to `{Transcript Directory}/INDEX.md`.**

For each processed transcript:

1. **Parse filename** for date, time, and title
2. **Assign tags** by inferring from transcript content — look for product terms, domain names, project names, and recurring themes based on the PM's domain context and `reference/domains.md`
3. **Infer series** from title and content — identify recurring meeting patterns (e.g., team standups, 1:1s with specific people, cross-functional syncs)
4. **Add a row** to the "Full Index" table in INDEX.md (maintain chronological order)
5. **If the transcript belongs to a recurring series**, add its date to that series section at the top
6. **Update the transcript count** in the header and the "Last updated" date

Do not rewrite the entire file — read it, add the new entries, and write back.

### 7. Return file path

Return the full path to the digest file so the main agent can read and present it to {PM Name}.

Your final message MUST include:
```
DIGEST_FILE: {Home Directory}/drafts/digest-[YYYY-MM-DD].md
```

## Speaker Attribution

Meeting transcripts frequently mislabel who is speaking, especially in multi-person calls. Do NOT trust transcript speaker labels as ground truth.

**Use calendar attendee lists to improve attribution:**
- When a transcript matches a calendar event, the attendee list tells you who was actually in the room.
- Cross-reference attendee names with `reference/people.md` for role context.

**General attribution rules:**
- Attribute to **roles or context** rather than trusting speaker labels (e.g., "engineering raised concern about X" not "[Name] said X").
- When a specific name matters, only attribute if the content makes it unambiguous.
- For coaching notes, focus on {PM Name}'s behavior rather than attributing specific statements to other participants.
- If uncertain who said something, use "from the transcript" rather than guessing a name.

## Output Guidelines

- Write full digest to the file (this is the primary output)
- {PM Name} reviews and decides what to action (copy to BACKLOG.md, add to people files, etc.)
- Group related items across meetings
- Be thorough in the file — it will be read back by the main agent and presented to {PM Name}
