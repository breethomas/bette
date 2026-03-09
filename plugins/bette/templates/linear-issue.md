# Linear Issue Guide

**Philosophy:** Write what needs to be done. Make it clear. Move on.

The goal is shared understanding, not following a format.

---

## The Only Rule

**Title should make it obvious what you're doing.**

That's it. Everything else is optional.

---

## Title Format

**Pattern:** `[Action] + [What] + [Optional: Where]`

**Good:**
- `Add CSV export to dashboard`
- `Fix: Login fails on Safari`
- `Design mobile navigation`
- `Refactor auth middleware`

**Bad:**
- `Export feature` (vague)
- `Bug` (what bug?)
- `Updates` (what updates?)

---

## When to Add a Description

**Add description when:**
- Context isn't obvious
- There are specific requirements
- Edge cases need clarification
- You need to link to designs/specs

**Skip description when:**
- Title says it all
- Task is straightforward
- Team already understands context

---

## Description Elements (Use What You Need)

### Context
Why we're doing this. 1-2 sentences.

### Requirements
- Specific things to build/fix
- Edge cases to handle

### Acceptance Criteria
- [ ] Testable conditions
- [ ] When is this "done"?

### Links
Design, prototype, related issues, specs

### Notes
Anything else that helps

---

## Quick Examples

### Simple Task
**Title:** `Add dark mode toggle to settings`

**Description:**
```
Toggle in settings page, saves preference, applies across app.

Design: [Figma link]
```

That's enough!

---

### Bug Fix
**Title:** `Fix: Dashboard crashes on date filter`

**Description:**
```
Steps to reproduce:
1. Open dashboard
2. Select date range > 1 year
3. Click apply
4. Crash

Browser: Safari only
Priority: P1 - affects 20% of users
```

---

### Needs More Context
**Title:** `Implement AI email subject suggestions`

**Description:**
```
Generate 3 subject line options based on email body.
Show above subject field after user types 50+ chars.

Requirements:
- 3 distinct suggestions
- <2 second response
- Graceful failure if API down
- User can dismiss

Design: [Figma]
Prototype: [link]
Evals: [link to eval dataset]

Cost: ~$0.01 per generation
```

---

## Labels > Long Descriptions

Use labels to add context without writing paragraphs:

**Priority:** `P0` `P1` `P2` `P3`

**Type:** `feature` `bug` `design` `tech-debt` `docs`

**Area:** `auth` `dashboard` `api` `mobile` `ai`

**Status:** `blocked` `needs-design` `needs-review`

---

## Common Mistakes

### ❌ User Story Theater
```
As a user, I want to export data,
so that I can analyze it offline.
```

**Why it's bad:** Ceremonial, wastes time, not how people talk.

**Instead:** `Add CSV export to dashboard`

---

### ❌ Vague Titles
```
Dashboard improvements
```

**Why it's bad:** Doesn't tell you what's being worked on.

**Instead:** `Add loading states to dashboard cards`

---

### ❌ PRD in the Issue
```
[10 paragraphs explaining product strategy,
market research, competitive analysis...]

Therefore we need an export button.
```

**Why it's bad:** Product context belongs in PRDs/vision docs, not tasks.

**Instead:** Link to PRD. Describe the specific task.

---

## Real-World Examples

### Feature Work

**Title:** `Add email notifications for post comments`

**Description:**
```
Send email when someone comments on user's post.

Include:
- Commenter name
- Comment preview (first 100 chars)
- Link to post

Settings: User can disable in notification preferences
Frequency: Real-time (not batched)

Design: [Figma]
```

---

### Design Task

**Title:** `Design mobile navigation for settings`

**Description:**
```
Current left sidebar doesn't work on mobile (<768px).

Requirements:
- Access all 6 settings sections
- Matches design system
- Consider: bottom nav, hamburger, or tabs

Context: 40% of settings traffic is mobile

User research: [link]
```

---

### AI Feature

**Title:** `Build evals for email subject line AI`

**Description:**
```
Create automated eval system for subject line generation.

Test dataset:
- 50 diverse email examples
- Mix of: sales emails, marketing, support, internal

Success criteria:
- 70%+ rated "good" by human reviewers
- No inappropriate/offensive suggestions
- Diverse suggestions (not all same style)

Related: Implementing feature in #234
```

---

### Tech Debt

**Title:** `Refactor auth middleware error handling`

**Description:**
```
Current middleware doesn't handle edge cases cleanly.
Makes debugging difficult.

Focus areas:
- Token expiration
- Invalid format
- Missing credentials
- Rate limiting

Requirements:
- Specific error codes for each case
- Better logging
- Maintain backward compatibility

Related issues: #234, #567, #891
```

---

## Issue Hierarchy

**Large work = Epic/Initiative**

Example Epic: "Improve mobile experience"

**Small work = Issues under that epic:**
- `Design mobile navigation`
- `Fix mobile keyboard overlap`
- `Optimize images for mobile`

---

## Who Writes Issues?

**The person doing the work** (when possible):
- Engineers write implementation issues
- Designers write design issues
- PMs write exploratory/research issues

They understand it best. They own it.

---

## Tips

### Keep Scope Tight
One issue = one clear outcome.
Completable in hours to few days, not weeks.

### Link Liberally
Link to designs, specs, prototypes, related work.
Don't copy-paste everything.

### Update as You Go
Mark blockers, add learnings, update estimates.

### Close with Evidence
Link to PR, note what shipped, add follow-ups.

---

## The Spirit of It

**Traditional:** Follow the user story format exactly.

**Modern:** Communicate clearly so work gets done.

**Questions to ask yourself:**
- Can someone read the title and know what I'm doing?
- Does my description help or just add ceremony?
- Am I writing for clarity or following a template?

Write for clarity. Skip the ceremony.

---

## More Examples

See `frameworks/ai-era-practices/issues-not-stories.md` for the full philosophy and more examples.

---

**Remember:** The goal is clear communication, not perfect formatting.

If your team understands what needs to be done, you succeeded.
