# Personalization

Bette is opinionated about content, neutral about delivery. The plugin curates *which* frameworks (Balfour, Vohra, Verna) and *which* thought leaders. It doesn't prescribe how the model explains them, how chatty it should be, or how much hand-holding you want.

That layer is yours. It lives in your `CLAUDE.md` files.

## The principle

A skill loads the canonical framework and trusts the model to apply it. How the model uses it depends on two things:

1. **The question you asked.** The model reads it and calibrates depth.
2. **Your `CLAUDE.md`.** Durable personalization that loads every session.

Most users don't need to touch any of this. The model calibrates well from the question alone. If you want a consistent operating posture, write it down once.

## Where personalization lives

Claude Code's `CLAUDE.md` hierarchy loads three levels at session start:

| File | Scope | Use for |
|---|---|---|
| `~/.claude/CLAUDE.md` | Global, all projects | Default posture, communication style, attribution rules |
| `<project>/CLAUDE.md` | This project only | Project-specific roles, north star, always-loaded reference imports |
| `<subdir>/CLAUDE.md` | This subdirectory | Workflow-specific rules (loaded on demand) |

Put Bette personalization in `~/.claude/CLAUDE.md`. These preferences apply to all your Claude Code work, not just Bette.

## Common knobs

Copy what fits.

### Seniority signaling

If you don't want frameworks re-explained:

```markdown
## How I work
I've been PMing for [N] years. Don't explain frameworks back to me when I invoke them. Apply them directly. If a reference is genuinely ambiguous, ask one clarifying question instead of lecturing.
```

If you're learning frameworks alongside the model:

```markdown
## How I work
I'm building product sense. When I invoke a framework I haven't used much, explain its core moves briefly before applying it. Treat my questions as opportunities to teach.
```

### Communication style

```markdown
## Communication preferences
- Direct feedback, no hedging
- Bullet points over paragraphs for status and feedback
- No emojis unless I explicitly ask
- No trailing summaries. I can read the diff.
```

### Attribution and fabrication

```markdown
## Truth standards
- Never fabricate facts, quotes, data, or sources
- Distinguish facts, analysis, and opinion
- If uncertain, say "I cannot confirm this." Don't guess.
- Cite sources transparently. No vague "studies show."
```

### Voice for drafted artifacts

When the model drafts Slack messages, emails, LinkedIn posts, or exec updates:

```markdown
## Voice for drafts
- Match recipient's language and framing, not Claude's defaults
- Plain text by default. No markdown tables, no code blocks unless I ask.
- "Running by you" is not a directive. Get the intent right.
```

### Output routing

If you want drafts written to files instead of pasted in chat:

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
- Ask one clarifying question at a time
- Get approval on the approach before implementation
```

## What NOT to put in CLAUDE.md

- **Things that change weekly or monthly.** Backlog, in-progress decisions, this week's priorities. Those belong in `BACKLOG.md`, project files, or auto-memory topic files.
- **One-off task instructions.** If it's "for this thing," not "every time," it's not CLAUDE.md material.
- **Framework restatements.** The skill already loads the framework. Don't duplicate.
- **Code patterns, file paths, architecture.** Those live in the codebase.
- **Preferences that apply to one workflow.** Those go in a topic file. CLAUDE.md is for what applies to every workflow.

A `CLAUDE.md` full of one-off rules is a memory leak. Every line costs attention budget across every session.

## Composition rules

Multiple `CLAUDE.md` files compose. Global rules apply everywhere. Project rules apply within the project. Subdir rules apply within the subdir.

If two layers contradict, the more specific layer wins (subdir > project > global). Rarely matters in practice.

## See also

- `frameworks/ai-era-practices/pm-memory-architecture.md` — the editorial discipline framework
- `docs/memory-systems.md` — Claude Code memory mechanics
- `docs/claude-md-architecture.md` — the underlying file hierarchy

## When to use this doc

- Setting up Bette for the first time and wondering where personal preferences go
- Auditing a `CLAUDE.md` that's grown messy
- Onboarding a new PM and deciding what's shared vs. personal
