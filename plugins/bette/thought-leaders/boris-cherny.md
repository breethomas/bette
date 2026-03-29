# Boris Cherny

**Focus:** Claude Code architecture, behavioral CLAUDE.md design, self-improving AI workflows

**Known For:** Creating Claude Code at Anthropic, pioneering the "expectations doc" style of CLAUDE.md that treats AI like a junior engineer who needs a manager

## Core Philosophy

Boris Cherny's insight is that the gap between "Claude Code works" and "Claude Code works the way my team needs it to" is almost entirely a configuration problem. The `.claude/` directory is a protocol for giving Claude structured context about your project, your team, and your rules.

His CLAUDE.md reads less like a project README and more like an engineering manager's expectations document. Instructions like "ask yourself: would a staff engineer approve this?" and "don't keep pushing if something goes sideways" are the kind of feedback you'd give a real teammate after their first few PRs. They work because Claude responds well to role-framing.

## Key Contributions

### The Behavioral CLAUDE.md

Most CLAUDE.md files describe WHAT the project is. Cherny's describes HOW to be a good engineer. Two complementary approaches:

- **Project identity:** commands, architecture, conventions, landmines
- **Behavioral rules:** plan mode defaults, verification standards, self-improvement loops

The most effective setup combines both. Project identity tells Claude what the codebase is. Behavioral rules tell Claude how to operate within it.

**Key behavioral sections from Cherny's own CLAUDE.md:**

**Plan Mode Default:**
- Enter plan mode for any non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately
- Write detailed specs upfront to reduce ambiguity

**Subagent Strategy:**
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis
- One task per subagent for focused execution

**Self-Improvement Loop:**
- After ANY correction from the user, update `tasks/lessons.md`
- Write rules that prevent the same mistake
- Ruthlessly iterate on lessons until mistake rate drops
- Review lessons at session start for relevant project

**Verification Before Done:**
- Never mark a task complete without proving it works
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

**Core Principles:**
- Simplicity First: make every change as simple as possible
- No Laziness: find root causes, no temporary fixes
- Demand Elegance: for non-trivial changes, pause and ask "is there a more elegant way?"

### The Self-Improvement Loop

The most underrated pattern in Cherny's setup. Claude writes its own mistakes to `tasks/lessons.md` and reviews them at the start of each session. This creates a feedback loop where Claude gets measurably better at your codebase over time -- not through model fine-tuning, but through accumulated context.

**The mechanism:**
1. User corrects Claude
2. Claude writes the correction to lessons.md with the pattern that caused the mistake
3. Next session, Claude reads lessons.md before starting work
4. Mistake rate drops over time

This is institutional memory built one correction at a time. It compounds.

### Task Management via Plain Files

Cherny uses plain markdown files as state: `tasks/todo.md` and `tasks/lessons.md`. No tooling required. No integrations to set up. Claude reads them, writes to them, and tracks its own progress.

**The workflow:**
1. Plan First: write plan to `tasks/todo.md` with checkable items
2. Verify Plan: check in before starting implementation
3. Track Progress: mark items complete as you go
4. Explain Changes: high-level summary at each step
5. Document Results: add review section to `tasks/todo.md`
6. Capture Lessons: update `tasks/lessons.md` after corrections

Simple enough to start using today.

### The .claude/ Directory as Protocol

Cherny frames the `.claude/` directory not as a config folder but as a protocol with distinct components, each serving a specific purpose:

| Component | Purpose |
|-----------|---------|
| **CLAUDE.md** | What the project is, how to work in it |
| **Rules** (`.claude/rules/`) | Standards scoped to paths -- loads only when relevant |
| **Skills** (`.claude/skills/`) | Workflows and knowledge, invocable on demand |
| **Subagents** (`.claude/agents/`) | Specialists with isolated context windows |
| **Settings** (`.claude/settings.json`) | Permissions, hooks, plugins |
| **Hooks** | Deterministic enforcement -- don't rely on the model to remember |

**The key insight:** CLAUDE.md is the highest-leverage file. Get that right first. Everything else is refinement for scale, safety, and specialization.

## Core Principles

### 1. Treat Claude Like a Junior Engineer, Not a Tool

Role-framing works. "Would a staff engineer approve this?" produces better output than "write good code." Set expectations the way you'd set them for a new hire.

### 2. Enforce Deterministically When You Can

Hooks run scripts at lifecycle events (before tool use, after file edits, at session start). If a rule matters enough to put in CLAUDE.md, ask: could a hook enforce this automatically? Auto-formatting after edits, test validation before commits, command auditing -- these shouldn't depend on the model remembering.

### 3. Keep Context Lean, Push Overflow to Subagents

Most developers underuse subagents because they don't think to ask for them. Making "use subagents liberally" a standing instruction means Claude defaults to keeping the main context window clean instead of filling it with exploration output.

### 4. Path-Scope Your Rules

As CLAUDE.md grows, split instructions into `.claude/rules/` files with glob frontmatter. A rule scoped to `src/api/**/*.ts` only loads when Claude works on API files. Context stays relevant. Instructions don't get buried.

### 5. Configuration Is the Product

Five parallel Claude instances don't need five different prompts. They need one well-configured `.claude/` directory. The configuration IS the multiplier.

## How This Applies to PM Workflows

Cherny's patterns were built for engineering, but the principles transfer directly:

### Behavioral CLAUDE.md for PMs

Instead of "plan mode for 3+ step tasks," a PM might write:
- Always check How Homebot Grows before prioritization recommendations
- When drafting exec communications, lead with the decision, not the analysis
- Flag when a request conflicts with stated goals

Same pattern: role-framing + behavioral expectations + quality standards.

### Self-Improvement Loop for PM Skills

The lessons.md pattern maps directly to Bette's memory system. After a correction:
- Save the feedback to memory (what to do differently)
- Memory gets loaded at session start (just like lessons.md)
- Behavior improves across sessions

The Bette approach is more sophisticated (typed memories, topic files, indexed in MEMORY.md) but the mechanism is identical: persistent corrections that compound.

### Path-Scoped Rules for PM Domains

PMs working across multiple domains can use `.claude/rules/` to scope instructions:
- `rules/exec-updates.md` -- pyramid structure, no implementation details
- `rules/meeting-notes.md` -- capture decisions and action items, not discussion
- `rules/linear-issues.md` -- follow team conventions, link to context

Rules activate when the work matches. Context stays lean.

### Hooks for PM Quality Gates

- PreToolUse hook on file reads: warn about large files (context hygiene)
- PostToolUse hook on writes: check for banned phrases in exec docs
- SessionStart hook: load daily priorities automatically

Bette already implements the first one. The others are available patterns.

## Integration with Other Frameworks

**Karpathy's Autoresearch:**
- Cherny's self-improvement loop is the manual version of what autoresearch automates
- Both rely on the same insight: define what good looks like, then iterate toward it
- Cherny's loop improves the operator (Claude's behavior). Autoresearch improves the artifact (the skill file)

**Bette's Context Architecture:**
- Cherny's layered `.claude/` maps to Bette's CLAUDE.md hierarchy (global, project, directory)
- Bette's reference files (people.md, domains.md) are the durable layer Cherny describes
- Bette's skills are the evolvable layer -- lean workflows that get shorter as models improve

**Linear Method:**
- Cherny's task management via plain files (todo.md, lessons.md) mirrors Linear's philosophy: simple tools, clear ownership, momentum over ceremony

## When to Apply Cherny's Patterns

- When Claude keeps making the same mistake across sessions (self-improvement loop)
- When CLAUDE.md is getting long and instructions are being ignored (split into rules)
- When you want deterministic enforcement, not just suggestions (hooks)
- When context is bloating your session (subagent strategy)
- When onboarding a team to Claude Code (the .claude/ directory as shared protocol)

## Common Misconceptions

- **"CLAUDE.md is a README"** -- It's an expectations document. READMEs describe; CLAUDE.md instructs.
- **"More instructions = better output"** -- Past a point, instructions get buried. Split into scoped rules and keep CLAUDE.md lean.
- **"Hooks are for engineers only"** -- Any deterministic check can be a hook. PMs use them for context hygiene and quality gates.
- **"Subagents are advanced"** -- They're the default for any task that produces a lot of intermediate output. Make them a standing instruction, not a special case.

## Quotes to Remember

> "The gap between 'Claude Code works' and 'Claude Code works the way my team needs it to' is almost entirely a configuration problem."

> "CLAUDE.md is the single most important file in the entire system."

> "If Claude keeps ignoring a rule despite it being in CLAUDE.md, the file is probably too long and the instruction is getting buried."

> "Hooks are ideal for enforcing rules deterministically -- rather than relying on the model to remember to do it."

> "The first tells Claude what your project is. The second tells Claude how to be a good engineer. The most effective setup combines both."

## Further Learning

**Start here:**
- Boris Cherny's public CLAUDE.md (shared via Linas Beliunas, Mar 2026)
- Claude Code documentation on skills, hooks, and subagents
- Anthropic's Claude Code architecture guides

**Context:**
- Boris Cherny is the creator of Claude Code at Anthropic
- His setup demonstrates production-grade `.claude/` configuration
- The behavioral CLAUDE.md pattern has been widely adopted since being shared publicly

## Related Thinkers

- **Andrej Karpathy** -- autoresearch automates what Cherny's self-improvement loop does manually
- **Aakash Gupta** -- adapted Karpathy's autoresearch for PM workflows, complementing Cherny's behavioral approach
- **Linear Method** -- shares the philosophy of plain files as state, simplicity over tooling

---

**In the context of this PM Thought Partner:**

Cherny's contribution is the architecture underneath everything Bette does. The layered CLAUDE.md, the self-improvement loop (realized as Bette's memory system), the subagent strategy (forked skills), and the quality gates (hooks) -- these are all Cherny patterns adapted for PM work.

His core insight matters most: Claude's behavior is a configuration problem. The better your context architecture, the more reliable your AI workflows become. Bette is proof of that thesis applied to product management.
