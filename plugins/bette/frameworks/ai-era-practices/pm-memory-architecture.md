# PM Memory Architecture

**Category:** AI-Era Practices
**Anchor sources:** Claude Code memory docs, Anthropic Auto Dream (May 2026), Managed Agents with Memory (April 2026)
**Last Updated:** May 2026

## Headline

Claude Code now ships native memory. The unsolved problem isn't memory mechanics — it's **editorial discipline applied to memory.** What gets persisted, where it lives, how it's named, when it's promoted, and what stays a one-line index entry vs. a deep topic file. PMs need this layer because the work is conversational, context-laden, and surfaces patterns across people / projects / decisions that no auto-memory pass can curate for them.

This framework is the editorial layer on top of Claude Code's native primitives.

## Native primitives (what Anthropic ships)

For mechanics — how MEMORY.md retrieval works, how topic files load, how MEMORY.md gets truncated past 200 lines — read [`docs/memory-systems.md`](../../docs/memory-systems.md). The short version:

- **CLAUDE.md hierarchy** — loads global (`~/.claude/CLAUDE.md`) → project (`./CLAUDE.md`) → subproject (`./.claude/CLAUDE.md` or nested), with `CLAUDE.local.md` for personal/gitignored overrides
- **`@path` imports** — recursive up to 5 hops; pulls referenced files into context deterministically (not via prose instruction)
- **Auto-memory** at `~/.claude/projects/<project>/memory/` — MEMORY.md plus topic files. MEMORY.md is always loaded (cap 200 lines / 25KB). Topic files load on demand via filename + frontmatter description matching.
- **Auto Dream** (May 2026) — between-session consolidation: dedupes contradictions, converts relative dates to absolute, rebuilds the topic-file index.
- **Hooks** — PreToolUse/PostToolUse hooks can warn on context bloat, log retrievals, track read patterns.

These primitives cover *mechanics*. They do not cover editorial decisions.

## The PM editorial layer (where this framework lives)

Five disciplines, in rough order of leverage:

### 1. Reference files load via `@imports`, not via prose instruction

PMs maintain reference files that need to be in context every session — people directory, domain glossary, company-specific systems and meetings. Don't rely on a MEMORY.md line that says "always load these alongside BACKLOG.md and GOALS.md." That depends on the model reading the instruction.

Use native `@imports` in CLAUDE.md instead:

```markdown
# Project CLAUDE.md

## Always-loaded reference
@./reference/people.md
@./reference/domains.md
@./reference/company.md
@./BACKLOG.md
@./GOALS.md
```

This is deterministic — Claude Code pulls them in regardless of model attention budget. The MEMORY.md instruction becomes redundant.

### 2. MEMORY.md is an index of one-line pointers, not content

Every line in MEMORY.md costs your 200-line budget. Inline content there is expensive and gets silently truncated past line 200 (the model has no idea content was cut).

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
- [VP-level operating](feedback_vp-level-operating.md) — drive work down, go deep only to understand or coach

## Workflow preferences
- [Avoid em dashes](feedback_em-dashes.md)
- [No fabrication in briefs](feedback_no-fabrication-in-briefs.md)
- [No inferences in deliverables](feedback_no-inferences-homebot.md)
```

Each link points to a topic file. The topic file holds the actual content. The index is searchable; the content is loadable.

### 3. Topic file naming is a retrieval optimization

Auto-memory retrieval is filename + description matching — not semantic search. The model picks max 5 files per turn from filenames it scans. Bad names are invisible. Good names get pulled.

Pattern that works:

```
{type}_{slug}.md

types:
  feedback_*    — user corrections and validated preferences
  project_*     — ongoing work context, decisions, motivations
  reference_*   — durable facts, glossaries, name resolutions
  user_*        — who the user is, role, expertise, goals
```

Example: `feedback_no-fabrication-in-briefs.md` gets retrieved when fabrication or brief writing comes up. `misc_notes_3.md` is invisible.

The one-line description in each topic file's frontmatter is what the retrieval model reads to decide relevance. Make it specific, not generic.

### 4. Promotion rule: auto-memory → topic file → CLAUDE.md

Three altitudes, three lifetimes:

| Altitude | Lifetime | Cost | What lives here |
|---|---|---|---|
| **Auto-memory topic file** | Persistent, retrieved on relevance | Free until retrieved | Specific lessons, names, decisions, patterns |
| **MEMORY.md index** | Always loaded (capped at 200 lines) | 1 line of budget per entry | Pointer to topic file + 1-line hook |
| **CLAUDE.md** | Always loaded, every session | High — every line costs across all future sessions | Load-bearing rules that change *every response*, not just one type |

Promotion rule: **a topic file gets promoted to CLAUDE.md only when the rule applies to nearly every response, not just one workflow.** Most patterns stay as topic files. CLAUDE.md is reserved for things that genuinely shape the model's default behavior across all work — communication style, attribution honesty, draft-routing patterns, anti-fabrication rules.

A "preferences sprawl" CLAUDE.md is a memory leak.

### 5. The drafts pattern: route output, don't paste it

For any draftable artifact (Slack message, email, exec update, MD&A, LinkedIn post), the model should write to a file first, then stage it on the clipboard:

```
1. Write to bette/drafts/<descriptive-kebab-case>.md
2. Run cat <file> | pbcopy
3. Tell the user it's copied and name the destination
```

Why this matters: copying from terminal output carries visual line wraps into Slack/Notion as hard breaks. Piping the file through pbcopy delivers clean paragraph structure. This is a small mechanical pattern that compounds — applies to every drafted artifact, not just skill outputs.

## PM-specific patterns worth naming

These patterns aren't in native memory — they're editorial choices a PM has to make:

### Disambiguation rules

When multiple people share a first name or projects share an acronym, disambiguation belongs in `reference/people.md` (or equivalent), not scattered across topic files:

```markdown
- **Sean** (designer, direct report) vs **Sean Doran** (engineer, user messaging) vs **Sean O'Neill** (engineer, UI)
- **Nick Pendry** (Principal Eng, billing/auth) vs **Nick DeSantis** (QA/Eng, self-service tooling)
- **Mike Lynch** (Finance/Ops) vs **Mike Z** (Support) vs **Mike K** (Engineer, AI)
```

Without explicit disambiguation, the model conflates people across sessions. With it, the rule loads on every session and the conflation stops.

### Transcript and external-tool artifacts

If you process meeting transcripts (Granola, Otter, etc.), tools mis-transcribe names, vendors, and acronyms. Document the corrections in `reference/` as durable facts:

```markdown
- HeyGen = "Hyejin" transcript artifact
- Carmer = "Karma" transcript artifact
- Able Archer = "Orchard" / "day orchard" transcript artifact
```

Same logic: one centralized correction list beats 30 topic files each fixing one error.

### Exec-facing guardrails

For execs you communicate with regularly, capture language rules in topic files:

```markdown
- Avoid "lagging indicator" with Ernie — he hears it as an excuse
- Avoid "pre-PMF" language with Ernie — reframe as "today vs tomorrow"
- Ernie features-over-intelligence — in live presentations, intelligence-layer lands, features get pushback
```

These are exactly the kind of editorial patterns auto-memory can't write for you. They emerge from observing the relationship over time and need deliberate persistence.

### Operating posture

Capture how the user actually operates so the model adjusts default behavior:

```markdown
- VP-level operating — drive work down to PMs, go deep only to understand or coach
- Iterative style — high-level plan > task-level detail > implement
- Direct feedback, no hedging
```

This is the kind of meta-rule that goes in CLAUDE.md if it shapes every response, or as a load-bearing topic file if it's situational.

## Pitfalls and anti-patterns

- **Treating MEMORY.md as a journal.** It's an index. Journal entries belong in dated session files or topic files, not in the always-loaded slot.
- **Saving code patterns and architecture in memory.** Code is in the codebase. Git log is the history. Memory is for what *isn't* derivable from current project state.
- **Saving fix recipes.** The fix is in the code; the commit message has context. Memory is for editorial patterns, not debug logs.
- **Memory growing without pruning.** Auto Dream helps but doesn't replace deliberate review. Periodically scan topic files: still relevant? Update or remove.
- **CLAUDE.md preferences sprawl.** Every "from now on, do X" added to CLAUDE.md is one more thing competing for attention every session. Most patterns belong in topic files where they load on relevance.

## When to use this framework

- ✅ Setting up Claude Code memory for the first time as a PM
- ✅ Auditing an existing memory setup that's grown messy
- ✅ Onboarding a new PM to your team's memory conventions (team OS adjacent)
- ✅ Deciding whether a new pattern goes in CLAUDE.md, MEMORY.md, or a topic file
- ❌ Replacing native primitives — use the native system; this is the editorial layer on top

## Resources

- [`docs/personalization.md`](../../docs/personalization.md) — how to tune Bette to your seniority and style via CLAUDE.md (the practical companion to this framework)
- [Claude Code memory docs](https://code.claude.com/docs/en/memory) — canonical reference for native primitives
- [`docs/memory-systems.md`](../../docs/memory-systems.md) — Bette's mechanics doc, complements this framework
- [Auto Dream blog](https://claudefa.st/blog/guide/mechanics/auto-dream) — between-session memory consolidation
- [Managed Agents with Memory](https://www.anthropic.com/engineering/managed-agents) — for agents beyond Claude Code itself
