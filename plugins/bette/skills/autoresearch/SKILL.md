---
name: autoresearch
description: "Automated improvement loop for any PM artifact. Define what 'better' means, then let the agent iterate. Uses Karpathy's autoresearch pattern. Say 'autoresearch my [thing]', 'optimize this automatically', 'run the improvement loop'."
user-invocable: true
---

# Autoresearch

Karpathy's autoresearch pattern adapted for PM work (via Aakash Gupta). The insight: most PM artifacts can be improved iteratively if you can define "better" as a set of binary questions and let an agent loop against them.

## The Pattern

Three requirements must all be true:

1. **A clear metric.** "Better" is defined as 3-6 binary yes/no eval criteria.
2. **Automated measurement.** An eval script that scores outputs against those criteria.
3. **One mutable file.** A single artifact the agent can change per iteration.

If any requirement is missing, stop and fix that first. Without a clear metric, the loop produces motion, not improvement.

## Three-File Structure

```
artifact.md        # The mutable file. Agent rewrites this each iteration.
eval-criteria.md   # Read-only. Binary yes/no questions that define "better."
progress.log       # Append-only. Score history across iterations.
```

### eval-criteria.md

Each criterion is a yes/no question scored independently. Example for a pitch:

```markdown
1. Does the opening sentence state the problem in under 20 words?
2. Is every claim supported by a specific data point or source?
3. Does the recommendation section lead with what to do, not why?
4. Is the document under 800 words?
5. Can a reader get the core argument from the first paragraph alone?
```

Good criteria are: binary (no "somewhat"), observable (no "feels right"), stable (don't change mid-loop). The PM writes these. This is the hardest and most valuable step -- defining what "better" means is the real product work.

### The Loop (Ralph Wiggum Pattern)

Each iteration runs in a fresh Claude Code invocation. No context rot. Progress tracked in git commits and the progress log.

```bash
while :; do cat PROMPT.md | claude-code ; done
```

The prompt instructs the agent to:
1. Read the eval criteria (read-only).
2. Read the current artifact.
3. Read progress.log for prior scores and patterns.
4. Generate a candidate revision.
5. Evaluate the candidate against all criteria.
6. If score improves: commit the change, append to progress.log.
7. If score doesn't improve: revert, log the attempt, try a different approach.

Fresh context each iteration is the key design choice. The agent doesn't remember prior attempts except through the progress log. This prevents the agent from getting stuck in local optima of its own reasoning.

### PROMPT.md Template

```markdown
You are improving `artifact.md` against the eval criteria in `eval-criteria.md`.

Rules:
- Read eval-criteria.md first. These are your scoring rubric. Do not modify them.
- Read progress.log for prior scores and failed approaches.
- Read artifact.md. This is the file you will rewrite.
- Generate one candidate revision.
- Score it against every criterion (yes=1, no=0). Be honest.
- If total score > previous best: save artifact.md, git commit, append score to progress.log.
- If total score <= previous best: do NOT save. Append the attempt and score to progress.log with a note on why it didn't improve.
- After logging, exit. The next iteration will start fresh.
```

## What This Works On

Any PM artifact where "better" can be defined:

- **Prompts and skill files.** Eval: does the output match expected format, tone, completeness?
- **Email templates.** Eval: clarity, CTA prominence, word count, reading level.
- **Product copy.** Eval: specificity, active voice, jargon-free, length constraints.
- **Specs and PRDs.** Eval: completeness of sections, testability of requirements, ambiguity check.
- **Pitch decks.** Eval: answer-first structure, data backing, word count per slide.

## What This Does NOT Work On

- Artifacts where "better" is subjective and can't be decomposed into binary questions.
- Multi-file changes (the loop mutates one file).
- Work where the eval itself needs iteration -- stabilize the eval first, then run the loop.

## When to Stop

- Score hits maximum (all criteria pass). Done.
- Score plateaus across 3+ iterations with different approaches. The eval criteria may be conflicting or the artifact may be at its ceiling given constraints.
- Progress log shows the agent trying the same approach repeatedly. Intervene and adjust criteria or constraints.

## The Meta Point

This is the most "meta-app" skill: intent in, iterated outcome out. The PM's real contribution is writing the eval criteria -- that's where product judgment lives. The loop is mechanical. If the PM can't write clear eval criteria, the artifact's definition of "good" isn't clear enough to build toward, with or without automation.
