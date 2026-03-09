# Skill Architecture

How to design AI workflows that stay coherent as they scale.

---

## What Are Skills?

Skills are reusable AI workflows — markdown files that define a task, its context requirements, and its execution pattern. When triggered (by command or natural language), the AI loads the skill and follows its instructions.

Skills turn "ask the AI to do the thing" into "invoke a workflow that does the thing consistently."

```
User: "prep for my 1:1 with Carol"
  → Skill loads: prep-1on1
  → Loads: people/carol.md, recent meeting notes, Linear issues
  → Produces: structured talk track
```

## Skill Types

### Interactive Skills (Non-Forked)

Run in the main session. The AI reads context, does the work, and you interact with the results in real time.

**Use for:**
- Workflows that need back-and-forth (backlog triage, inbox processing)
- Quick tasks (add to backlog, surface priorities, draft a message)
- Anything where you want to steer as it runs

**Characteristics:**
- Stay in main context window
- Can ask you questions mid-execution
- Results are immediately visible
- Context cost: whatever they read stays in your session

**Examples:** backlog processing, focus/priority surfacing, exec update drafting, message drafting

### Isolated Skills (Forked)

Run in a sub-agent with their own context window. They do heavy processing independently and return results.

**Use for:**
- Workflows that read large amounts of content (transcripts, Notion pages, PDFs)
- Processing that doesn't need mid-stream interaction
- Anything that would bloat main context

**Characteristics:**
- Get their own context window (main stays clean)
- Can't ask you questions mid-execution
- Results must be written to files (not returned directly — see output routing below)
- Context cost: only the final output enters main context

**Examples:** meeting digest, transcript synthesis, 1:1 prep, performance review draft, coaching notes

### Orchestrator Skills

Coordinate multiple sub-skills, often running them in parallel.

**Use for:**
- Workflows that fan out to multiple sources (catch up on email + Slack + channels)
- Multi-step processes where each step is independent

**Characteristics:**
- The orchestrator stays in main context
- Each sub-task runs as a forked skill or sub-agent
- Results are consolidated and presented

**Examples:** morning catchup (email + Slack in parallel), weekly review

---

## Design Decisions

### Forked or Not?

Ask two questions:

1. **Does this skill need to read large content?** (Transcripts, full Notion pages, PDFs, long threads)
   - Yes → Fork it
   - No → Keep it interactive

2. **Does this skill need mid-stream interaction?** (Asking the user to confirm, choose, or steer)
   - Yes → Keep it interactive
   - No → Fork it

If both answers are "yes" (needs large reads AND interaction), fork the heavy reading to a sub-agent and keep the interaction in the main skill.

### Output Routing

Forked skills face a problem: when they return results to the main session, the output can get compressed if it's long. Critical details get lost.

**The fix:** Forked skills write output to files, then the main session reads the file.

```
Forked skill: "Process transcript, write digest to drafts/digest.md"
  └── Sub-agent reads transcript, writes structured output to file
Main session: Reads drafts/digest.md, presents to user
```

This guarantees the full output survives, regardless of context compression.

### Context Requirements

Every skill should declare what context it needs:

```markdown
## Context
**Always load:**
- reference/people.md
- reference/domains.md

**Load for this skill:**
- people/[name].md (for the specific person)
- Recent meeting transcripts (delegate to sub-agent)

**Query on demand:**
- Linear: recent issues assigned to [person]
- Notion: meeting notes from last 2 weeks
```

This prevents skills from loading everything and keeps context focused.

---

## Skill File Structure

A skill is a markdown file with a predictable structure:

```markdown
# Skill Name

[One line: what this skill does]

## Trigger
[When this skill should activate — commands and natural language patterns]

## Context
[What files and sources to load]

## Process
[Step-by-step instructions for the AI]

## Output
[What the skill produces and where it goes]

## Examples
[Example inputs and expected outputs]
```

### Trigger Design

Skills should be invocable by command AND natural language:

```markdown
## Trigger
- Command: `/prep-1on1 [name]`
- Natural language: "prep for my 1:1 with [name]", "get ready for [name]"
```

Natural language triggers are important for voice-to-text workflows (dictation). If users speak their requests, the AI should recognize the intent without requiring exact commands.

---

## Scaling Patterns

### The Skill Menu

As skills accumulate, document them in your project CLAUDE.md as a lookup table:

```markdown
## Skills

| Command | What It Does |
|---------|-------------|
| `/digest` | Process daily meeting transcripts |
| `/prep-1on1 [name]` | Prep talk track for 1:1 |
| `/backlog` | Process and prioritize backlog |
| `/focus` | Surface today's top 3 priorities |
```

This serves double duty: the AI uses it for routing, and you use it as a reference.

### Skill Dependencies

Some skills depend on others or share context:

```
/sync-transcripts → runs backup → then triggers /digest
/catchup → fans out to /email-inbox + /slack-inbox in parallel
```

Document these dependencies in the skill file so the AI (and future you) understands the chain.

### Shared Reference

Multiple skills often need the same context (people.md, domains.md). Rather than listing them in every skill, establish a "base context" in your CLAUDE.md that loads for all skills, and only specify additional context per-skill.

---

## Anti-Patterns

### The Monolith Skill

One skill that does everything: reads transcripts, processes email, updates the backlog, drafts messages, and files issues.

**Fix:** Break into focused skills. One skill, one job. Orchestrate with a parent skill if needed.

### The Leaky Fork

A forked skill that returns its full processing into main context, defeating the purpose of isolation.

**Fix:** Write output to files. Main session reads the file.

### The Context Hog

A skill that loads every reference file, every meeting note, and every related document "just in case."

**Fix:** Declare minimum context. Load additional context only when the skill determines it's needed.

### The Silent Skill

A skill that does work but doesn't persist state. Next time it runs, it starts from scratch.

**Fix:** Skills that process inputs (transcripts, emails, Slack items) must update tracking files (e.g., `.processed`) before completing. State persistence is the skill's responsibility, not the user's.

---

*Skills are habits encoded. Design them well and your AI gets more useful every day.*
