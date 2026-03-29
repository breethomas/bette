---
name: coach-me
description: Generate coaching notes on recent meetings. Use when user says "coach me on my meetings", "give me feedback on my meetings", "meeting coaching", "how did I do in my meetings", or similar. Reads recent transcripts and provides specific, direct feedback on communication and leadership.
context: fork
model: sonnet
---

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Before executing, find and read the CLAUDE.md file in the project root (the directory containing BACKLOG.md and GOALS.md). Locate the Config table and resolve all `{Key}` placeholders in this skill to their configured values.

If no Config table is found, abort and report: "Cannot resolve config variables. Ensure CLAUDE.md has a Config table with {Home Directory}, {PM Name}, and other required keys."


# Coach Me on My Meetings

Read recent meeting transcripts and generate coaching feedback for {PM Name}.

## Context

{PM Name} is a {PM Role}. They want direct, specific feedback on their communication and presence in meetings. Assume the PM may not have picked up on subtle social or emotional cues.

## Workflow

### 1. Find transcripts

- If a specific meeting is mentioned in `$ARGUMENTS`, find that transcript
- Otherwise, check `{Transcript Directory}` for meetings in the last 24 hours (files named `YYYY-MM-DD_HHMM_Meeting_Title.md`)
- If no recent transcripts found, report that and suggest running `/sync-transcripts` first

### 2. Read and analyze

Read the full transcript content for each meeting. For each meeting, generate **3 coaching notes** using this lens:

> From this transcript, give {PM Name} three specific notes on what could have been done better to be a stronger colleague and product leader. For each note, write one paragraph: what was done or missed, why it matters for the other person or team, and how to improve next time. Be concrete — include example wording or behaviors. Supportive and direct tone.

Look for:
- **Communication clarity** — Did {PM Name} state their point clearly? Was there ambiguity?
- **Active listening** — Did they acknowledge others' points? Build on or dismiss?
- **Decision-making** — Were decisions made clearly? Were owners and next steps explicit?
- **Inclusion** — Did they create space for quieter voices? Did anyone get talked over?
- **Strategic framing** — Did they connect tactical work to strategic goals?
- **Emotional intelligence** — Were there moments where someone's concern wasn't fully addressed?

### 3. Write coaching notes to file

**Write the full coaching notes to:** `{Home Directory}/drafts/coaching-[YYYY-MM-DD].md`

Use this format:

```
# Meeting Coaching — [Date]

## [Meeting Name] ([Time])

**Note 1: [Short label]**
[One paragraph: what happened, why it matters, how to improve. Include specific wording or behavior examples.]

**Note 2: [Short label]**
[One paragraph]

**Note 3: [Short label]**
[One paragraph]

---

## [Next Meeting Name] ([Time])
...
```

### 4. Return file path

Your final message MUST include:
```
COACHING_FILE: {Home Directory}/drafts/coaching-[YYYY-MM-DD].md
```

## Speaker Attribution

Meeting transcripts frequently mislabel who is speaking, especially in multi-person calls. Do NOT trust transcript speaker labels as ground truth.

- Focus coaching notes on **{PM Name}'s behavior** — what they said, how they responded, what they missed. They know who they were talking to.
- When referencing what others said, attribute to **role or context** rather than trusting speaker labels.
- If uncertain who said something, use "from the transcript" rather than guessing a name.

## Output Guidelines

- Write full coaching notes to the file (this is the primary output)
- Be direct, not gentle — {PM Name} wants real feedback
- Always include specific examples (quote or paraphrase from transcript)
- Focus on actionable improvements, not just observations
- Be thorough in the file — it will be read back by the main agent and presented to {PM Name}
