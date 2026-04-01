# Memory Systems

What to persist across sessions and what to let die.

---

## The Problem

Every AI session starts fresh. Without a memory system, you re-explain context, lose insights, and repeat mistakes. But saving everything creates noise that drowns out signal.

The goal: **persist what makes the next session better. Discard what doesn't.**

## How Memory Works in Claude Code

Claude Code provides an auto-memory directory that persists across conversations. The main file (`MEMORY.md`) is loaded into every session automatically. Additional topic files can be created and linked from MEMORY.md.

```
~/.claude/projects/[project-path]/memory/
  MEMORY.md           ← Always loaded (keep under 200 lines)
  debugging.md        ← Topic file, loaded on demand
  patterns.md         ← Topic file, loaded on demand
  integrations.md     ← Topic file, loaded on demand
```

**MEMORY.md is prime real estate.** It's loaded every session, so every line costs tokens. Keep it under 200 lines -- anything past that gets silently truncated. The AI has no idea lines were cut.

### How Retrieval Works

Each turn, a separate model call scans all memory file names and descriptions, then picks the 5 most relevant to load. This is filename-based matching, not semantic search or embeddings. This means:

- **File names matter.** `feedback_testing.md` gets retrieved when testing comes up. `misc_notes_3.md` never does.
- **Description frontmatter matters.** The one-line description in each topic file is what the retrieval model reads to decide relevance.
- **Max 5 files per turn.** If you have 30 topic files, 25 are invisible on any given turn. Name them well.

### MEMORY.md as Index, Not Content

MEMORY.md should be an index of one-line pointers to topic files -- not a place to store content directly. Every multi-line block in MEMORY.md is eating your 200-line budget.

**Bad** (content inlined, 10 lines for one topic):
```markdown
## Pricing Model
- APU = Active Portal User
- Four corners applies to the client experience
- SaaS continues as the pedal tone
- Middle Earth is the transitional state
```

**Good** (pointer, 1 line):
```markdown
- [Pricing model](project_pricing-model.md) -- APU definition, four corners, SaaS pedal tone
```

The content lives in the topic file where it has room to breathe. MEMORY.md stays lean.

### Compaction and Memory

Auto-compaction fires at ~167,000 tokens. When it does, it compresses everything into a ~50,000-token summary and retains only 5 files in full. Every file read, reasoning chain, and intermediate decision is discarded.

Memory files are not affected by compaction -- they persist on disk. But if your MEMORY.md is bloated with inlined content, it's wasting tokens in the summary budget too. A lean MEMORY.md means more room for actual work context to survive compaction.

## What to Save

### Stable Patterns (High Value)
Conventions confirmed across multiple interactions:
- "Bree prefers bullet points over paragraphs"
- "This codebase uses factory pattern for services"
- "Slack MCP: always use response_format: detailed — concise format crashes"

### Solved Problems (High Value)
Solutions to issues you'll hit again:
- "Date calculations: anchor to known date, step through day by day — no approximating"
- "Notion callout insertion: insert_content_after near callouts can land inside them"

### Key Decisions (Medium Value)
Architectural or workflow decisions that affect future sessions:
- "Forked skills must write output to drafts/ — fork output gets compressed"
- "Intelligence layer is the product term; semantic layer is engineering's term"

### Name Disambiguation (Medium Value)
When the AI consistently confuses people or terms:
- "Sean (designer) vs Sean Doran (engineer) vs Sean O'Neill (engineer)"

## What NOT to Save

### Session-Specific Context
Current task details, in-progress work, temporary state. This is what session notes are for — they live in the project, not in memory.

### Unverified Conclusions
Don't save something as fact after reading one file. Verify against project docs before writing to memory.

### Duplicates of CLAUDE.md
If it's already in a CLAUDE.md file, don't also put it in memory. One source of truth.

### Speculative Notes
"I think this might be related to X" — either confirm it or don't save it.

---

## Memory Organization

### MEMORY.md Structure

Organize semantically by topic, not chronologically.

```markdown
# Project Memory

## Reference Files — Always Load
[What files to load at session start]

## Name Disambiguation
[People and terms that confuse the AI]

## Workflow Preferences
[How the human likes to work — confirmed patterns]

## Integration Gotchas
[Tool-specific issues and workarounds]

## Key Decisions
[Architectural choices that affect future work]

## Strategic Context
[Important background the AI needs for decision-making]
```

### Topic Files

When a section of MEMORY.md grows past 3-4 lines, extract it into a topic file and replace with a one-line pointer.

**Topic file naming convention:**
```
{type}_{topic}.md

Types: user, feedback, project, reference
Examples: feedback_testing.md, project_pricing-model.md, user_role-context.md
```

**Topic file frontmatter** (required for retrieval):
```markdown
---
name: Pricing model
description: APU definition, four corners, SaaS pedal tone, transitional state
type: project
---

[content here]
```

The `description` field is what the retrieval model reads to decide whether to load this file. Make it specific enough to match relevant queries.

**MEMORY.md pointer:**
```markdown
- [Pricing model](project_pricing-model.md) -- APU definition, four corners, SaaS pedal tone
```

One line. Under 150 characters. The description in the pointer and the frontmatter should be similar but don't need to be identical.

---

## Correction Loops

**When the AI gets something wrong from memory, fix it at the source.**

This is critical. If you correct the AI in conversation but don't update the memory file, the same mistake will repeat in the next session.

```
Session 1: AI says "Liza is VP Finance"
You correct: "Liza is Chief of Staff"
→ MUST update MEMORY.md immediately
→ Next session starts with correct information
```

Build this into your CLAUDE.md:

```markdown
When the user corrects something stated from memory, update or remove
the incorrect entry immediately. A correction means the stored memory
is wrong — fix it at the source before continuing.
```

## Explicit Saves

When you want the AI to remember something specific:

> "Always use bun, never npm"
> "Never auto-commit without asking"
> "Remember that Carol prefers async communication"

These should be saved immediately — no need to wait for multiple interactions to confirm the pattern.

Similarly, when you want to forget:

> "Stop remembering the old API endpoint"
> "Remove the note about Sean's project — it's done"

The AI should find and remove the entry.

---

## Memory Hygiene

### Regular Cleanup

Memory files accumulate. Schedule periodic reviews:
- **Monthly:** Scan MEMORY.md for stale entries
- **After major changes:** Remove notes about completed projects, departed people, resolved issues
- **When memory feels noisy:** If the AI is loading irrelevant context, trim

### Staleness Signals

An entry is probably stale when:
- It references a project that's been shipped or cancelled
- It mentions a person who's left the company
- The workaround it describes has been properly fixed
- The decision it records has been reversed

### The 200-Line Budget

MEMORY.md has a hard limit of 200 lines. Content past line 200 is silently truncated -- the AI sees clean input and has no idea it was cut. This is not a soft guideline; it's a hard ceiling.

**Target 80-120 lines.** This leaves room for growth without constant pruning.

When approaching the budget:
1. Extract multi-line blocks to topic files (most common fix)
2. Compress remaining entries to one-liners under 150 characters
3. Remove anything duplicated in CLAUDE.md or reference files (one source of truth)
4. Delete entries for completed projects, departed people, or resolved issues
5. Check for dead links -- topic files that were deleted but still referenced

### The 25KB Byte Cap

A separate 25KB byte limit covers edge cases with long lines. If individual entries are very long (URLs, code snippets), they can hit this before the 200-line limit. Keep entries concise.

---

*Memory is a garden, not a landfill. Plant what grows. Pull what's dead.*
