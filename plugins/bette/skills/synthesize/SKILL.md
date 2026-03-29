---
name: synthesize
description: Strategic analysis of meeting transcripts. Use when user says "synthesize", "what decisions came out of", "run this against our strategy", "what does this mean for my domains", "analyze this transcript", or similar. Extracts decisions, maps to strategic framework, and identifies domain impact. Not for daily action items (that's /digest).
context: fork
model: sonnet
---

## Config Resolution

This skill uses `{variables}` from the project CLAUDE.md Config table. Before executing, find and read the CLAUDE.md file in the project root (the directory containing BACKLOG.md and GOALS.md). Locate the Config table and resolve all `{Key}` placeholders in this skill to their configured values.

If no Config table is found, abort and report: "Cannot resolve config variables. Ensure CLAUDE.md has a Config table with {Home Directory}, {PM Name}, and other required keys."


# Synthesize

Run strategic analysis on meeting transcripts. Extract what matters — decisions, strategic implications, domain impact.

## Context Files

Read these first:
- `{Home Directory}/reference/people.md` — who's who (verify all attributions against this)
- `{Home Directory}/reference/domains.md` — product domains, PM owners, architecture layers
- `{Home Directory}/reference/company.md` — systems, methodology, compliance
- `{Strategy Directory}/initiatives/{Strategy Framework}` — strategic framework

## Workflow

### 1. Identify transcripts

{PM Name} will either:
- Name specific meetings ("synthesize the exec meeting from this morning")
- Point to a time range ("synthesize my meetings from today")
- Provide transcripts directly

Find matching transcripts in `{Transcript Directory}` by filename (format: `YYYY-MM-DD_HHMM_Meeting_Title.md`).

If no match found, ask {PM Name} to clarify. Do not guess.

### 2. Determine which lenses to run

{PM Name} may request a specific lens or all three. If not specified, run all three.

**The three lenses:**
- **Decisions** — what was decided, by whom, implications
- **Strategic mapping** — connection to your strategic framework
- **Domain impact** — which product domains are affected

### 3. Read and analyze

Read each transcript fully. Then apply the requested lenses:

#### Lens 1: Decisions

For each decision surfaced:
- **What was decided** — one sentence, plain language
- **Who decided** — verify against people.md. If uncertain, say "from the transcript" not a guessed name
- **What it changes** — what shifts as a result (priorities, timelines, ownership, direction)
- **Open threads** — anything left unresolved or needing follow-up

Only surface actual decisions. "We discussed X" is not a decision. "We agreed to do Y by Z date" is.

#### Lens 2: Strategic Mapping

Map transcript content against the strategic framework (`{Strategy Directory}/initiatives/{Strategy Framework}`):

- **Value prop alignment** — Which value proposition does this support? How?
- **Growth loop impact** — Does this accelerate or slow a core growth loop?
- **Strategic priority** — Does this align with current strategic priorities or diverge?
- **Tensions** — Anything that contradicts or challenges the current strategy? Flag it directly.

_Customize these mapping dimensions to match your strategic framework._

Skip sections that don't apply. Not every meeting touches every part of the framework.

#### Lens 3: Domain Impact

Map transcript content against the domain reference:

- For each affected domain, note:
  - **Domain** — name and PM owner (from domains.md)
  - **What changed** — new information, shifted priorities, new dependencies
  - **Action needed** — does the PM owner need to know or do something?

Only include domains actually affected. Don't stretch to fill every domain.

### 4. Write to file

Write the full analysis to: `{Home Directory}/drafts/synthesis-[YYYY-MM-DD]-[brief-topic].md`

Use this format:

```
# Synthesis — [Topic/Meeting Name(s)]
**Date:** [date]
**Transcripts analyzed:** [count]
- [meeting names with times]

## Decisions
[If this lens was run]

### [Decision 1 title]
- **Decided:** [what]
- **By:** [who — verified against people.md]
- **Changes:** [what shifts]
- **Open threads:** [unresolved items, or "None"]

## Strategic Mapping
[If this lens was run]

### Value Prop Alignment
[which value prop, how]

### Growth Loop Impact
[which loop, accelerate or slow]

### Strategic Priority
[alignment or divergence]

### Tensions
[anything that challenges current strategy, or "None identified"]

## Domain Impact
[If this lens was run]

### [Domain Name] (Owner: [PM])
- **What changed:** [specifics]
- **Action needed:** [what the PM should know or do]
```

### 5. Return file path

Your final message MUST include:
```
SYNTHESIS_FILE: {Home Directory}/drafts/synthesis-[YYYY-MM-DD]-[topic].md
```

## Guardrails

- **No fabrication.** Never invent details not in the source transcripts.
- **Speaker attribution is unreliable.** Do NOT trust transcript speaker labels as ground truth. Attribute to roles when possible. Qualify with "(per transcript — verify)" when a specific name matters.
- **Verify names against people.md.** If a name isn't in the reference file, flag it as unrecognized.
- **High-level framing.** Use domain charter vocabulary from domains.md.
- **Conservative extraction.** Signal over noise. If something is ambiguous or minor, leave it out.
- **Concise first draft.** Keep bullets tight. {PM Name} will ask to expand if needed.
