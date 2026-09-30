# PM Who Codes - Role Clarity & Philosophy

*Revised September 2026. The team norms still hold. The "Working with Claude" section changed because the models did (see [Revisit with New Models](../core-principles.md)). The pre-commit checklist lives in [quality-gates.md](quality-gates.md).*

## Your Role as PM Who Codes

**You're a product manager who codes, not a software engineer.**

This distinction matters:
- **Goal:** Ship features quickly while respecting engineering quality
- **Strength:** Product thinking, prototyping, getting things done
- **Limitation:** Not a professional software engineer
- **Responsibility:** Don't create more work for the team than the feature is worth

## Core Principles

### 1. Consistency > Personal Preference

When working in existing codebases:
- **Study similar code first** - Find components/patterns that match what you're building
- **Match patterns exactly** - Spacing, naming, structure, everything
- **Don't innovate on architecture** - Use what's already there
- **Ask before deviating** - If you think you need a new pattern, ask first

### 2. CI Must Pass Locally First

**The #1 Problem to Solve: Pushing PRs that fail CI/CD**

Non-negotiable rule:
- Run ALL the same checks locally that CI will run
- Don't commit until everything passes
- Don't push until you've verified in the actual environment
- If a check can't run locally, say so before opening the PR, not after it fails

If Claude suggests committing without passing checks → **STOP and run checks first**

### 3. Quality > Speed

Shipping fast is good. Shipping sloppy code is not.

Before pushing code, ask:
- **Is this creating more work than it saves?**
- **Will this be easy for the team to maintain?**
- **Did I follow their patterns or force my own?**

If the answer to any is "no" → **refactor before pushing**

### 4. Test Before Ship

Untested code is broken code you haven't discovered yet.

Minimum testing:
- **Manual testing:** Does it actually work in the real environment? See it in the simulator or browser, not just in passing tests
- **Automated tests:** Follow project conventions (some require tests, some don't)
- **Edge cases:** What breaks this? Test those scenarios

### 5. Know When to Ask

You're not expected to know everything. Ask before:
- Creating new architectural patterns
- Deviating from established conventions
- Making decisions that affect the team
- Shipping something you're not confident about

**It's better to ask than to create work for others cleaning up your code.**

### 6. AI Changes Go Through Evals

**Prompts, AI tools and model changes affect what users see immediately, and they fail quietly.** The AI can "work" and still do the wrong thing, and fixing one behavior can break another.

Before and after any change to a prompt, tool definition, model or model setting:
1. **Run the eval suite first** to get a baseline
2. **Add an eval case for the bug** before fixing it, so you can see it fail
3. **Check related cases,** not just the one that broke
4. **Run the full suite after,** and more than once when behavior is intermittent
5. **Put the before and after scores in the PR**

Use [prompt-engineering.md](prompt-engineering.md) for how to approach the change. The evals are how you know it worked.

### 7. Discover Before Building

**Before adding new code, scripts, or workflows, search for existing patterns.**

This applies to:
- **Cross-cutting concerns** - timezone, auth, user context, logging
- **Operational workflows** - migrations, deployments, scripts, one-time tasks
- **Common utilities** - helpers, formatters, validators

Before proposing a solution:

1. **Ask "how does the team currently do this?"**
2. **Search for existing patterns** - grep for related terms, check bin/, lib/tasks/, terraform/
3. **Look at similar past work** - git log, existing migrations, deploy configs
4. **Check infrastructure files** - Terraform, CI/CD, Dockerfiles

**Red flags that you're about to duplicate:**
- Building a new script for a one-time operation
- Adding a new bin/ command or rake task
- "I'll create a helper to..."
- Adding a new field to pass context from client to server
- Building new middleware for a common concern

**Instead:**
- "How does the codebase currently handle this?"
- "Is there an existing workflow for running migrations?"
- "What's the team's pattern for X?"
- Search before architecting, script before building

### 8. Plan Big Work in Phases

**For multi-day or multi-step work, create a punch list document.**

Structure it by dependencies:
1. **Environment/infrastructure first** - fix what blocks accurate testing
2. **Bug fixes second** - clear blockers before polish
3. **Polish third** - UI, UX improvements
4. **Testing last** - verify everything works

Update the document as you work:
- Mark items complete with dates
- Add findings/decisions inline
- Create issues for deferred items

A punch list keeps you focused and gives visibility into progress.

### 9. Clean Up Before Milestones

**Before major pushes (releases, submissions), do a housekeeping pass.**

Remove:
- Stale documentation that no longer reflects reality
- Test artifacts and simulation files from past debugging
- Commented-out code and abandoned experiments

Keep:
- The source of truth (actual prompts, current configs)
- Session notes and decision logs
- Active test scenarios

The best time to clean up is before shipping, not after.

### 10. Verify Before Claiming

**Better models are still confidently wrong sometimes.** A claim about the code, the data or how the product behaves gets checked against the source before it goes into a PR, a doc, user-facing copy or a decision.

- **Code claims:** read the code or run it. "The forecast uses the real bank balance" means someone opened the calculator
- **Data claims:** query it. "Only 2 active users have a bank connected" comes from a query, not a guess
- **Product claims in copy:** every feature a page promises should exist in the app that users will actually have
- **Label inferences as inferences.** "Probably" and "I haven't checked" are fine. Presenting a guess as fact is not

If Claude states something important without showing where it came from → **ask how it knows**

### 11. Review Before Every PR

**Every PR goes through the project's reviewer agents before it opens and before it merges.**

- Run them in the order the project defines. If the project has none, at minimum check the change against the spec, then for bugs, performance and security
- Fix blocking findings before merging, or write down why not
- Note in the PR that the reviewers ran
- No exceptions for "small" PRs. Skipped reviews are how a string of merged PRs ends up needing reviews after the fact

## Working with Claude

Claude is your pair programmer, but you're responsible for:
- **Directing the approach** - "Match the existing pattern in X component"
- **Verifying quality** - Run checks, test thoroughly
- **Making judgment calls** - "Is this good enough or should I ask the team?"

Claude will help you write code. You ensure it's responsible code.

### Spec First, Then Let It Run

Current models can build a whole feature in one go. What they need is a clear target, not tiny tasks.

1. **Describe the work** in plain language
2. **Agree on a short spec:** what we're building, why it matters, how it works, done when, not this time
3. **Let Claude build the whole slice** against that spec
4. **Review at checkpoints:** the spec, the working result in the real app, and the diff before the PR

Break work up by what can ship on its own, not by what fits in a prompt.

### Session Notes, Not Session Restarts

Long sessions are fine on current models. How far one can go depends on the model's context window: when it fills, older context gets summarized automatically, and the summary loses detail. So restart based on how the session is going, not on a task count. Restarting on a schedule throws away useful context.

- **Write session notes after each meaningful chunk:** what changed, what's live, what's next, decisions and why
- **Notes are for resuming,** by you, a new session or a parallel one, not for wiping context
- **Restart only when Claude loses the thread:** it repeats questions, contradicts decisions you already made, or forgets constraints

### Write Down Decisions, Not Everything

Project CLAUDE.md files, skills and specs now carry most of the context Claude needs. You don't have to re-explain the codebase in markdown before every task.

What still needs writing down:
- **Decisions and why** - in the spec or session notes
- **Things only you know** - product context, team agreements, what was tried and dropped
- **Anything a future session would get wrong without it**

### Parallel Sessions

Running several sessions at once is normal now. Keep them from stepping on each other:
- **One worktree and branch per session** - don't share a checkout between sessions
- **Shared notes get appended, never overwritten** - read the file, then add your section
- **Watch shared local resources** - a local database on one port serves every session that uses it
- **Coordinate through messages** - ask the other session instead of changing its work

## When Working Solo vs. With Team

### Solo Projects
- Focus on maintainability - future you should understand this
- Keep it lean - simple > clever
- Document why, not just what
- Test enough to be confident it works

### Team Projects
- Follow their workflow religiously
- Use their tools and conventions
- Run their quality checks
- Respect their architectural decisions
- Don't create cleanup work for senior engineers

## Success Metrics

You're doing this right when:
- PRs pass CI on first push
- Code reviews focus on product decisions, not code quality issues
- Senior engineers aren't cleaning up after you
- AI changes ship with before-and-after eval results
- Your code is maintainable 6 months later
- You're shipping quality code that creates value

---

*This is not about being a perfect engineer. It's about being a responsible one.*
