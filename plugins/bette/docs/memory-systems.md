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

**MEMORY.md is prime real estate.** It's loaded every session, so every line costs tokens. Keep it under 200 lines — anything past that gets truncated.

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

When a section of MEMORY.md grows too large, extract it into a topic file and link from MEMORY.md.

```markdown
## Integration Gotchas
See [integrations.md](integrations.md) for detailed tool-specific notes.
Key issues:
- Slack: always use detailed format
- Notion: don't overwrite pages being actively edited
```

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

MEMORY.md has a hard limit. When you're approaching it:
1. Move detailed sections to topic files
2. Compress multi-line entries to single lines
3. Remove anything that's now covered by CLAUDE.md or reference files
4. Delete entries that haven't been relevant in 30+ days

---

*Memory is a garden, not a landfill. Plant what grows. Pull what's dead.*
