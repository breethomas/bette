# CLAUDE.md Architecture

How to design layered context files that give AI the right information at the right time.

---

## The Layers

Context files form a hierarchy. Each layer adds specificity without repeating what's above it.

```
~/.claude/CLAUDE.md                    ← Global: who you are, how you work
  └── /project/CLAUDE.md              ← Project: what this project is, how it's structured
        └── /project/subdir/CLAUDE.md ← Directory: local rules for this area
```

Claude Code loads all matching CLAUDE.md files from global down to your current working directory. Each layer is additive — it inherits everything above it.

### Global (`~/.claude/CLAUDE.md`)

**What goes here:** Preferences and principles that apply to every project, every session.

- How you and the AI work together (planning protocol, iteration style)
- Communication preferences (tone, format, feedback style)
- Factual accuracy standards (research before answering, cite sources)
- Session management rules (when to save notes, where to save them)
- Tool-specific defaults (coding standards to load, writing style guides)

**What doesn't go here:**
- Project-specific context (that's the next layer)
- Information that changes frequently (put it in reference files instead)
- Large blocks of content (link to files, don't inline)

**Example structure:**

```markdown
# [Your Name]'s Global Claude Code Preferences

## How We Work Together
- Plan before implementing
- Ask clarifying questions one at a time
- Get approval on approach before execution

## Communication
- Direct feedback, no hedging
- Bullet points for summaries
- No emojis unless requested

## Truth and Research
- Never fabricate facts or sources
- State uncertainty explicitly
- Show reasoning for important decisions

## Session Management
- Save session notes after 2-3 major tasks
- [Where to save, what to capture]

## Task-Specific Loading
- For coding: load [coding standards path]
- For writing: load [style guide path]
```

### Project (`/project/CLAUDE.md`)

**What goes here:** Everything the AI needs to know about this specific project.

- What the project is and what it does
- Key files and directories to load
- Project-specific workflows and conventions
- Integration points (tools, APIs, services)
- What to query on demand vs. load every session

**What doesn't go here:**
- Your personal preferences (that's global)
- Deep reference content (put it in reference files, link from here)
- Implementation details that change with every PR

**Example structure:**

```markdown
# [Project Name]

## What This Is
[One paragraph: what the project does, who it's for]

## Context to Load
**Always read:**
- `reference/people.md` — who's who
- `reference/domains.md` — product areas and terminology
- `BACKLOG.md` — current priorities

**Read when relevant:**
- `strategy/framework.md` — for strategic work
- `docs/architecture.md` — for technical decisions

**Query on demand:**
- Notion (via MCP) — meeting notes, team docs
- Linear (via MCP) — issue tracking, project status

## Workflows
[Key workflows and how they're triggered]

## Directories
- `reference/` — persistent context files
- `drafts/` — work in progress
- `sessions/` — session notes
```

### Directory (`/project/subdir/CLAUDE.md`)

**What goes here:** Local rules that only apply within this directory.

- Specific file conventions for this area
- Relationships between files in this directory
- Workflows that only apply here
- Constraints on what the AI should or shouldn't do in this area

This layer is optional. Only create it when a directory has conventions that differ from the project level.

---

## Design Principles

### 1. Link, Don't Inline

CLAUDE.md files should be routing documents, not encyclopedias. Point to reference files, don't paste their contents.

**Bad:**
```markdown
## People
- Alice — Engineering lead, 5 years at company, owns auth...
- Bob — PM, started January, previously at Stripe...
[50 more entries]
```

**Good:**
```markdown
## Context to Load
- `reference/people.md` — who's who (roles, relationships)
```

### 2. Stable Content Only

CLAUDE.md files should change rarely. If content changes weekly, it belongs in a reference file that's loaded on demand, not baked into the project instructions.

- **Stable:** project structure, workflow descriptions, loading instructions
- **Volatile:** current priorities, team roster, active projects → reference files

### 3. Loading Instructions Are Explicit

Don't assume the AI will find the right files. Tell it exactly what to load and when.

```markdown
**Always read:**
- file1.md
- file2.md

**Read for [specific type of work]:**
- file3.md

**Query on demand:**
- [External source] — for [specific purpose]
```

### 4. Layer Boundaries Are Clear

Each layer should have a distinct purpose. If you're not sure which layer something belongs to, ask:

- Does this apply to ALL my projects? → Global
- Does this apply to THIS project? → Project
- Does this apply to THIS directory only? → Directory

### 5. Keep It Scannable

The AI reads these files at the start of every session. Dense paragraphs waste tokens and reduce comprehension. Use:
- Headers for sections
- Bullet points for lists
- Tables for structured reference
- Short sentences

---

## Common Patterns

### The Routing Pattern

Project CLAUDE.md acts as a router — it loads different context based on what you're doing.

```markdown
## Context Routing

When working on strategy:
- Load `strategy/CLAUDE.md`
- Load `strategy/framework.md`

When working on operations:
- Load `ops/CLAUDE.md`
- Load `reference/people.md`

When working on code:
- Load coding standards
- Load project architecture docs
```

### The Integration Pattern

For projects that use external tools (Notion, Linear, Slack), document how to query them.

```markdown
## Integrations

**Notion:** Knowledge base, past decisions, team docs. Query via MCP.
**Linear:** Issue tracking, cycle planning. Query for project status.
**Slack:** Team communication. Search for recent decisions.

Query on demand — don't load full contents into context.
```

### The Delegation Pattern

For large projects with heavy context, document what should be delegated to sub-agents vs. read directly.

```markdown
## Context Hygiene

**Read directly:** Files being edited, small reference files (< 200 lines)
**Delegate to sub-agent:** Transcripts, PDFs, large Notion pages, raw data

Rule: Read for editing, delegate for reference.
```

---

## Anti-Patterns

### The Kitchen Sink

Dumping everything into one CLAUDE.md. The AI gets overwhelmed, misses important instructions, and wastes tokens on irrelevant context.

**Fix:** Split into layers. Global for preferences, project for specifics, reference files for details.

### The Stale Instructions

CLAUDE.md references files that no longer exist, describes workflows that have changed, or includes outdated team information.

**Fix:** Review CLAUDE.md files quarterly. If a section hasn't been relevant in a month, remove it.

### The Novel

Multi-page CLAUDE.md with paragraphs of prose explaining every decision and its history.

**Fix:** CLAUDE.md is instructions, not documentation. Keep it terse. Link to docs for background.

---

*The best CLAUDE.md is the one you rarely need to update. Stable structure, dynamic reference files.*
