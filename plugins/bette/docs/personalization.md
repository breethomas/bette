# Personalization

Bette is opinionated about content but neutral about delivery. The plugin curates *which* frameworks (Balfour, Vohra, Verna, etc.) and *which* thought leaders. It doesn't prescribe how the model should explain those frameworks to you, how chatty it should be, or how much hand-holding you want.

That layer is yours. It lives in your `CLAUDE.md` files.

## The principle

A skill loads the canonical framework and trusts the model to apply it. Whether the model explains the framework like you've never seen it, applies it surgically without restating it, or coaches you through a half-known concept depends on:

1. **The question you asked** — the model reads it and calibrates depth.
2. **Your `CLAUDE.md`** — durable personalization that loads every session.

Most users don't need to touch any of this. The model calibrates well from the question alone. But if you want a consistent operating posture, write it down once.

## Where personalization lives

Claude Code's `CLAUDE.md` hierarchy loads three levels at session start:

| File | Scope | Use for |
|---|---|---|
| `~/.claude/CLAUDE.md` | Global, all projects | Your default posture, communication style, attribution rules |
| `<project>/CLAUDE.md` | This project only | Project-specific roles, north star, always-loaded reference imports |
| `<subdir>/CLAUDE.md` | This subdirectory | Workflow-specific rules (loaded on demand) |

For Bette personalization specifically, put it in `~/.claude/CLAUDE.md` — these are preferences that apply to all your Claude Code work, not just Bette.

## Common knobs

Copy what fits, adapt as needed.

### Seniority signaling

If you don't want frameworks re-explained every time:

```markdown
## How I work
I've been PMing for [N] years. Don't explain frameworks back to me when I invoke them — apply them directly. If a framework reference is genuinely unclear or ambiguous in my question, ask one clarifying question instead of lecturing.
```

If you're learning frameworks alongside the model:

```markdown
## How I work
I'm building product sense. When I invoke a framework I haven't used much, explain its core moves briefly before applying it. Treat my questions as opportunities to teach, not just answer.
```

### Communication style

```markdown
## Communication preferences
- Direct feedback, no hedging
- Bullet points over paragraphs for status and feedback
- No emojis unless I explicitly ask
- No trailing summaries — I can read the diff or output
```

### Attribution and fabrication

```markdown
## Truth standards
- Never fabricate facts, quotes, data, or sources
- Distinguish clearly between facts, analysis, and opinion
- If uncertain, say "I cannot confirm this" — don't guess
- Cite sources transparently. No vague "studies show"
```

### Voice for drafted artifacts

When the model drafts Slack messages, emails, LinkedIn posts, or exec updates on your behalf:

```markdown
## Voice for drafts
- Match recipient's language and framing, not Claude's defaults
- Plain text by default — no markdown tables, no code blocks unless I ask
- "Running by you" is not the same as giving a directive — get the intent right
```

### Output routing

If you want drafted artifacts written to files instead of pasted in chat:

```markdown
## Draft routing
For any draftable artifact (Slack, email, exec update, LinkedIn, meeting notes):
1. Write to drafts/<descriptive-kebab-case>.md
2. Run `cat <file> | pbcopy` to stage on clipboard
3. Tell me it's copied and name the destination

Why: copying from terminal output carries visual line wraps into Slack/Notion as hard breaks. The file pipe delivers clean paragraph structure.
```

### Iterative style

If you prefer plan-then-implement over jump-to-code:

```markdown
## Working style
- Plan at the high level first, then task level, then implement
- Multiple review rounds work well
- Ask one clarifying question at a time so I can give complete answers
- Get approval on the approach before implementation
```

## What NOT to put in CLAUDE.md

A few rules to keep CLAUDE.md from becoming a dumping ground:

- **Things that change weekly or monthly** — current backlog, in-progress decisions, this week's priorities. Those belong in `BACKLOG.md`, project files, or auto-memory topic files.
- **One-off task instructions** — if it's "for this thing," not "every time," it's not CLAUDE.md material.
- **Framework restatements** — the skill already loads the framework. Don't duplicate it in your CLAUDE.md.
- **Code patterns, file paths, architecture** — those live in the codebase. CLAUDE.md is for what isn't derivable from current project state.
- **Anything you'd describe as "preferences" — but only if those preferences apply to nearly every response.** If a rule applies to one workflow, it belongs in a memory topic file. If it applies to every workflow, CLAUDE.md.

A `CLAUDE.md` that fills up with one-off rules is a memory leak. Every line in CLAUDE.md costs attention budget across every session that ever loads it.

## Composition rules

When multiple `CLAUDE.md` files load, they don't conflict — they compose. Global rules apply everywhere. Project rules apply within the project. Subdir rules apply within the subdir.

If two layers say genuinely contradictory things, the more specific layer wins (subdir > project > global). But this rarely matters in practice; most rules at different layers operate on different scopes.

## See also

- `frameworks/ai-era-practices/pm-memory-architecture.md` — the editorial discipline framework that explains how personalization fits into the broader memory system (reference files, topic files, the promotion rule between layers)
- `docs/memory-systems.md` — Claude Code memory mechanics (retrieval, the 200-line budget, auto-memory)
- `docs/claude-md-architecture.md` — the underlying file hierarchy

## When to use this doc

- Setting up Bette for the first time and wondering "where do my personal preferences go?"
- Auditing a `CLAUDE.md` that's grown messy
- Onboarding a new PM to your team's conventions and wondering what should be shared vs. personal
