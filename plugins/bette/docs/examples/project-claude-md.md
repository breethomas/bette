# Example: Project CLAUDE.md

An annotated example of a project-level CLAUDE.md for an AI-powered PM operating system.

---

```markdown
# [Project Name] — [One Line Description]

[Project name] is [what it does]. Claude reads this context to help
[who it helps] with [what kind of work].

---

## Core Principle
                                          # ← Lead with the philosophy.
                                          #   This shapes AI behavior
                                          #   more than specific rules.

Don't over-structure. [Name] captures raw context with minimal
organization. Claude does the pattern matching, prioritization,
and connection to goals.
                                          # ← This tells the AI: don't demand
                                          #   perfect inputs. Work with messy.

---

## Context to Load

**Always read:**                          # ← Loaded every session.
- `BACKLOG.md` — brain dump inbox         #   Keep this list short.
- `GOALS.md` — what matters this quarter
- `reference/people.md` — who's who
- `reference/domains.md` — product areas
- `reference/company.md` — systems, meetings

**Read for strategic context:**           # ← Loaded when doing strategy work.
- `../strategy/framework.md`

**Query on demand:**                      # ← NOT loaded. Queried when needed.
- Notion (via MCP) — meeting notes, docs
- Linear (via MCP) — issues, projects

---

## Skills
                                          # ← The skill menu. AI uses this
                                          #   for routing. Human uses it
                                          #   as a reference.

| Command | What It Does |
|---------|-------------|
| `/catchup` | Catch up on all inbound messaging |
| `/digest` | Process daily meeting transcripts |
| `/backlog` | Process and prioritize backlog items |
| `/focus` | Surface today's top 3 priorities |
| `/prep-1on1 [name]` | Prep talk track for 1:1 |
| `/exec-update` | Draft Tuesday exec update |

Skills auto-invoke from natural language — no command required.
                                          # ← Important for voice-to-text.
                                          #   "Prep for my 1:1 with Carol"
                                          #   should just work.

---

## Context Hygiene
                                          # ← Rules for what enters context.
                                          #   This section prevents bloat.

**Transcripts:** Never read raw into main context.
Always delegate to a sub-agent with an extraction prompt.

**Large files (> 200 lines):** If referencing (not editing),
delegate to sub-agent.

**Notion pages:** Default to delegating. Only fetch directly
if updating the page.

Rule: Read for editing, delegate for reference.

---

## Integrations

**Notion:** Knowledge base, past decisions, team docs.
**Linear:** Issue tracking, project status, cycle planning.

---

## Directories
                                          # ← Map of what lives where.
                                          #   AI uses this to find things.

- `reference/` — persistent context (loaded every session)
- `people/` — direct report files (loaded for 1:1 prep)
- `transcripts/` — meeting transcripts (always delegate)
- `sessions/` — session notes
- `drafts/` — work in progress

---

## Session Management

- Don't rely on chat history across sessions
- Update files during session so context persists
- Suggest saving state after 2-3 major tasks
- Persist tracking state before ending workflows
                                          # ← Critical: skills that process
                                          #   inputs must save their progress.
                                          #   Don't rely on the human to ask.

---

## The Filter
                                          # ← Decision framework for the AI.
                                          #   When prioritizing or recommending,
                                          #   always run through this filter.

When [name] asks about priorities, always filter through:
1. Does this support [strategic goal 1]?
2. Does this support [strategic goal 2]?
3. Does this prevent [critical system] from breaking?
4. Does this build the team [name] needs?

If none of the above: ask why [name] is doing this.
```

---

## Key Design Choices

**"Always read" is small.** Five files, all compact reference files. This is the minimum context for any session.

**Skills are a table, not paragraphs.** Scannable, complete, and the AI can pattern-match natural language to the right skill.

**Context hygiene has its own section.** This is important enough to be explicit. Without it, the AI will read everything and bloat context.

**The Filter is decision-making infrastructure.** It turns "what should I prioritize?" from a subjective question into a structured evaluation. The AI applies this filter automatically.
