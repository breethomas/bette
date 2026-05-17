# PM Memory Architecture

**Category:** AI-Era Practices
**Anchor sources:** Claude Code memory docs, Anthropic Auto Dream (May 2026), Managed Agents with Memory (April 2026)
**Last Updated:** May 2026

## Headline

Claude Code ships native memory. The unsolved problem isn't mechanics. It's **editorial discipline applied to memory.** What gets persisted, where it lives, how it's named, when it's promoted, what stays a one-line index entry vs. a deep topic file. PMs need this layer because the work is conversational and surfaces patterns across people, projects, and decisions that no auto-memory pass can curate.

This framework is the editorial layer on top of Claude Code's native primitives.

## Native primitives (what Anthropic ships)

For mechanics, read [`docs/memory-systems.md`](../../docs/memory-systems.md). Short version:

- **CLAUDE.md hierarchy.** Loads global (`~/.claude/CLAUDE.md`) → project (`./CLAUDE.md`) → subproject, with `CLAUDE.local.md` for personal/gitignored overrides.
- **`@path` imports.** Recursive up to 5 hops. Pulls referenced files into context deterministically.
- **Auto-memory** at `~/.claude/projects/<project>/memory/`. MEMORY.md plus topic files. MEMORY.md is always loaded (cap 200 lines / 25KB). Topic files load on demand via filename + frontmatter description matching.
- **Auto Dream** (May 2026). Between-session consolidation: dedupes contradictions, converts relative dates to absolute, rebuilds the topic-file index.
- **Hooks.** PreToolUse/PostToolUse hooks can warn on context bloat, log retrievals, track read patterns.

These cover mechanics. Not editorial decisions.

## The PM editorial layer

Five disciplines, in rough order of leverage.

### 1. Reference files load via `@imports`, not prose instruction

PMs maintain reference files that need to be in context every session: people directory, domain glossary, company systems. Don't rely on a MEMORY.md line that says "always load these." That depends on the model reading the instruction.

Use native `@imports` in CLAUDE.md:

```markdown
# Project CLAUDE.md

## Always-loaded reference
@./reference/people.md
@./reference/domains.md
@./reference/company.md
@./BACKLOG.md
@./GOALS.md
```

Deterministic. Claude Code pulls them in regardless of model attention budget. The MEMORY.md instruction becomes redundant.

### 2. MEMORY.md is an index of one-line pointers, not content

Every line costs your 200-line budget. Inline content gets silently truncated past line 200. The model has no idea content was cut.

Structure:

```markdown
# MEMORY.md (index)

## Reference files — always load
- bette/reference/people.md
- bette/reference/domains.md
- bette/reference/company.md

## Name disambiguation
- [Common name collisions](reference_name-disambiguation.md)

## Operating posture
- [VP-level operating](feedback_vp-level-operating.md): drive work down, go deep only to understand or coach

## Workflow preferences
- [Avoid em dashes](feedback_em-dashes.md)
- [No fabrication in briefs](feedback_no-fabrication-in-briefs.md)
- [No inferences in deliverables](feedback_no-inferences-homebot.md)
```

Each link points to a topic file. The topic file holds the content. The index is searchable; the content is loadable.

### 3. Topic file naming is a retrieval optimization

Auto-memory retrieval is filename + description matching, not semantic search. The model picks max 5 files per turn from filenames it scans. Bad names are invisible. Good names get pulled.

Pattern that works:

```
{type}_{slug}.md

types:
  feedback_*    user corrections and validated preferences
  project_*     ongoing work context, decisions, motivations
  reference_*   durable facts, glossaries, name resolutions
  user_*        who the user is, role, expertise, goals
```

`feedback_no-fabrication-in-briefs.md` gets retrieved when fabrication or brief writing comes up. `misc_notes_3.md` is invisible.

The one-line description in frontmatter is what the retrieval model reads. Make it specific.

### 4. Promotion rule: auto-memory → topic file → CLAUDE.md

Three altitudes, three lifetimes:

| Altitude | Lifetime | Cost | What lives here |
|---|---|---|---|
| **Auto-memory topic file** | Persistent, retrieved on relevance | Free until retrieved | Specific lessons, names, decisions, patterns |
| **MEMORY.md index** | Always loaded (capped at 200 lines) | 1 line of budget per entry | Pointer to topic file + 1-line hook |
| **CLAUDE.md** | Always loaded, every session | High. Every line costs across all future sessions. | Load-bearing rules that change *every response* |

Promotion rule: **a topic file gets promoted to CLAUDE.md only when the rule applies to nearly every response.** Most patterns stay as topic files. CLAUDE.md is for things that shape default behavior across all work. Communication style, attribution honesty, draft-routing, anti-fabrication.

A "preferences sprawl" CLAUDE.md is a memory leak.

### 5. The drafts pattern: route output, don't paste it

For any draftable artifact (Slack, email, exec update, MD&A, LinkedIn), write to a file first, then stage on clipboard:

```
1. Write to bette/drafts/<descriptive-kebab-case>.md
2. Run cat <file> | pbcopy
3. Tell the user it's copied and name the destination
```

Copying from terminal output carries visual line wraps into Slack/Notion as hard breaks. Piping the file through pbcopy delivers clean paragraph structure. Small pattern, compounds across every drafted artifact.

## PM-specific patterns worth naming

Editorial choices a PM has to make. Not in native memory.

### Disambiguation rules

When people share a first name or projects share an acronym, disambiguation belongs in `reference/people.md`, not scattered across topic files:

```markdown
- **Sean** (designer, direct report) vs **Sean Doran** (engineer, user messaging) vs **Sean O'Neill** (engineer, UI)
- **Nick Pendry** (Principal Eng, billing/auth) vs **Nick DeSantis** (QA/Eng, self-service tooling)
- **Mike Lynch** (Finance/Ops) vs **Mike Z** (Support) vs **Mike K** (Engineer, AI)
```

Without explicit disambiguation, the model conflates people across sessions. With it, the rule loads every session and the conflation stops.

### Transcript and external-tool artifacts

Granola, Otter, etc. mis-transcribe names, vendors, acronyms. Document corrections in `reference/`:

```markdown
- HeyGen = "Hyejin" transcript artifact
- Carmer = "Karma" transcript artifact
- Able Archer = "Orchard" / "day orchard" transcript artifact
```

One centralized correction list beats 30 topic files each fixing one error.

### Exec-facing guardrails

For execs you communicate with regularly, capture language rules in topic files:

```markdown
- Avoid "lagging indicator" with Ernie. He hears it as an excuse.
- Avoid "pre-PMF" language with Ernie. Reframe as "today vs tomorrow."
- Ernie features-over-intelligence. In live presentations, intelligence-layer lands, features get pushback.
```

Auto-memory can't write these for you. They emerge from observing the relationship and need deliberate persistence.

### Operating posture

Capture how the user actually operates so the model adjusts default behavior:

```markdown
- VP-level operating: drive work down to PMs, go deep only to understand or coach
- Iterative style: high-level plan > task-level detail > implement
- Direct feedback, no hedging
```

CLAUDE.md if it shapes every response. Load-bearing topic file if it's situational.

## Pitfalls and anti-patterns

- **MEMORY.md as a journal.** It's an index. Journal entries belong in dated session files or topic files.
- **Code patterns and architecture in memory.** Code is in the codebase. Git log is the history. Memory is for what isn't derivable from project state.
- **Fix recipes.** The fix is in the code; the commit message has context. Memory is for editorial patterns, not debug logs.
- **Memory growing without pruning.** Auto Dream helps but doesn't replace deliberate review. Periodically scan topic files.
- **CLAUDE.md preferences sprawl.** Every "from now on, do X" competes for attention every session. Most patterns belong in topic files.

## When to use this framework

- ✅ Setting up Claude Code memory for the first time as a PM
- ✅ Auditing an existing memory setup that's grown messy
- ✅ Onboarding a new PM to your team's memory conventions
- ✅ Deciding whether a new pattern goes in CLAUDE.md, MEMORY.md, or a topic file
- ❌ Replacing native primitives. Use the native system; this is the editorial layer on top.

## Resources

- [`docs/personalization.md`](../../docs/personalization.md) — practical companion to this framework
- [Claude Code memory docs](https://code.claude.com/docs/en/memory) — canonical reference for native primitives
- [`docs/memory-systems.md`](../../docs/memory-systems.md) — Bette's mechanics doc
- [Auto Dream blog](https://claudefa.st/blog/guide/mechanics/auto-dream) — between-session memory consolidation
- [Managed Agents with Memory](https://www.anthropic.com/engineering/managed-agents) — for agents beyond Claude Code
