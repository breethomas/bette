# Issues Not User Stories

**Category:** AI-Era Practices
**Source:** Linear Method
**Last Updated:** January 2025

## Overview

User stories have become cargo cult ritual in product development - ceremony that feels good but wastes time and resources. Modern teams write clear, direct issues instead.

**The shift:**
- **Old:** "As a [persona], I want [action], so that [benefit]"
- **New:** "Add export button to dashboard" - clear, direct, actionable

## The Problem with User Stories

### 1. Time-Consuming Overhead
- Time-consuming to write and read
- Creates unnecessary process overhead
- Forces ceremony where clarity would suffice

### 2. Silos Engineers into Mechanical Roles
- Engineers code to issue requirements instead of thinking about UX holistically
- Removes them from product thinking
- Creates "just ship what's in the ticket" mentality

### 3. Brings Product Details to Task Level
- Product-level context doesn't belong in individual tasks
- Creates scope creep in issues
- Confuses what needs to be done with why the product exists

### 4. Doesn't Match How Teams Actually Communicate
- No one talks like this in real conversations
- Forces artificial language
- Slows down communication

**From Linear:** "User stories have become a cargo cult ritual that feels good but wastes a lot of resources and time."

## The Better Approach: Clear, Direct Issues

### Core Principles

**1. Describe Tangible Outcomes**
Issues should specify what needs to be built (code, design, document)

**Good examples:**
- "Add export to CSV button on analytics dashboard"
- "Fix pagination bug in user list"
- "Design mobile navigation for settings"

**Bad examples:**
- "As a user, I want to export data so that I can analyze it offline"
- "Users need better navigation"
- "Improve analytics"

**2. Write Clearly and Directly**
- Title states what the task is
- Description includes relevant context (optional but helpful)
- No ceremony, just clarity

**3. Authors Write Their Own Issues**
- The person doing the work understands it best
- Forces deeper thinking about the problem
- Creates ownership

**4. Keep UX Discussions at Product Level**
- Engage full teams (designers, engineers, customers) before writing code
- Don't bury product strategy in task-level issues
- Separate "what to build" (product) from "how to build it" (issues)

## How to Write Good Issues

### Issue Title Format

**Pattern:** [Action] + [What] + [Optional: Where/Context]

**Examples:**
- "Add dark mode toggle to settings"
- "Fix: Dashboard crashes on mobile Safari"
- "Refactor authentication middleware"
- "Design: New user onboarding flow"
- "Update pricing page copy"

### When to Include Description

**Include description when:**
- Context isn't obvious from title
- There are specific requirements
- You need to link to related work
- Edge cases need clarification

**Keep it brief:**
- Few sentences max
- Link to design/specs if needed
- Acceptance criteria if helpful
- Don't repeat what's in the title

### Example: User Story vs. Issue

**User Story (ceremonial):**
```
Title: User Export Functionality
As a data analyst,
I want to export dashboard data to CSV,
So that I can perform offline analysis in Excel.

Acceptance Criteria:
- Given I'm on the analytics dashboard
- When I click the export button
- Then I receive a CSV file with all visible data
- And the file is named with the current date
```

**Issue (direct):**
```
Title: Add CSV export button to analytics dashboard

Description:
Button should export currently visible data as CSV.
Filename format: analytics-export-YYYY-MM-DD.csv

Design: [link to Figma]
Ref: Users requesting this in #feedback
```

**What changed:**
- ❌ Removed persona theater ("As a data analyst")
- ❌ Removed obvious motivation ("so that I can analyze")
- ✅ Clear title stating what to build
- ✅ Relevant context in description
- ✅ Links to design and context

## When User Stories Might Still Make Sense

**Rare cases where the format helps:**
- Teaching non-technical stakeholders about user needs
- Workshop exercises to build empathy
- Early product exploration (before you know what to build)

**But even then:**
- Don't put them in engineering issues
- Use them for discovery, not task management
- Translate to clear issues when work begins

## Integration with Modern PM Practices

### Works With Prototype-First Development
- Build prototype → Show team → Write clear issues for production
- No need for user story ceremony when you have working example
- "Build the dashboard export feature" (with prototype link) > long user story

### Aligns With Linear Method
**Direction Setting:**
- Define product vision (why we're building)
- Set goals and priorities

**Building:**
- Write clear issues for what to build
- Engineers understand context from product vision, not from each issue
- Ship continuously

**The separation:**
- Product vision = Why we exist, what problems we solve
- Issues = Specific things to build

### Supports AI-Era Speed
- AI can generate code from clear instructions
- "Add export button" is clearer than user story for AI tools
- Less ceremony = faster execution

## Common Objections Answered

### "But user stories keep us user-focused!"
**Response:** No, talking to actual users keeps you user-focused.

User stories are theater that makes you feel user-focused while potentially building the wrong thing.

**Better:**
- Talk to users weekly (Teresa Torres)
- Prototype and test with users
- Make product decisions informed by real user needs
- Write clear issues to implement those decisions

### "How will engineers know the 'why'?"
**Response:** From product context, not from every issue.

**Better approach:**
- Product vision explains the why
- Roadmap shows priorities
- Team discussions provide context
- Issues describe what to build

Engineers shouldn't need to re-read "why" in every ticket. They should understand product direction.

### "What about acceptance criteria?"
**Response:** Include it when helpful, but keep it concise.

**Good acceptance criteria:**
- Clear, testable conditions
- Focused on this specific task
- Not restating the obvious

**Example:**
```
Title: Add CSV export to dashboard

Acceptance criteria:
- Exports currently visible data only
- Includes column headers
- Works with filtered views
- File size limit: 10MB
```

No need for "Given/When/Then" ceremony - just the actual criteria.

## Best Practices

### 1. Make Titles Scannable
Team should understand what's being worked on from issue list view alone.

**Good:**
- "Add two-factor authentication"
- "Fix: Login fails on Safari"
- "Design mobile checkout flow"

**Bad:**
- "User authentication improvements"
- "Bug fix"
- "Update designs"

### 2. Use Labels/Tags for Context
Instead of embedding context in title:
- Priority: P0, P1, P2
- Type: Bug, Feature, Design, Tech Debt
- Area: Auth, Dashboard, API

### 3. Link to Relevant Context
- Design files
- Related issues
- Customer feedback
- Product specs

Don't duplicate information - link to it.

### 4. Break Down Appropriately
- Each issue should be completable in reasonable time (hours to few days)
- If too big, break into smaller issues
- Don't need sub-tasks with user story format for each

### 5. Let People Write Their Own
- Engineers write implementation issues
- Designers write design issues
- PMs write exploratory/research issues

Whoever's doing the work understands it best.

## Real-World Examples

### Feature Work

**Bad (User Story):**
```
As a user, I want to receive email notifications when someone comments on my post, so that I can stay engaged with discussions.
```

**Good (Issue):**
```
Title: Add email notifications for post comments

Description:
Send email when someone comments on user's post.
Include: commenter name, comment preview, link to post

Settings: User can disable in notification preferences
Frequency: Real-time (not batched)

Design: [Figma link]
```

### Bug Fix

**Bad:**
```
As a user, when I try to upload an image larger than 5MB, I want to see a helpful error message instead of a generic failure, so that I understand what went wrong.
```

**Good:**
```
Title: Fix: No error message for large image uploads

Description:
Images >5MB fail silently. Show error: "Image must be under 5MB. Please resize and try again."

Repro: Upload 10MB image in profile settings
Browser: All browsers
```

### Design Work

**Bad:**
```
As a mobile user, I want the navigation to be easier to use on small screens, so that I can access all features comfortably.
```

**Good:**
```
Title: Design mobile navigation for <768px screens

Description:
Current nav doesn't work on mobile. Design hamburger menu or bottom nav.

Requirements:
- Access to all main sections
- Account/settings
- Search
- Notifications

Research: [User feedback link]
```

## The Mindset Shift

**From:** "How do I write a good user story?"
**To:** "What needs to be built and why?"

**From:** Following a format
**To:** Communicating clearly

**From:** Ceremony and process
**To:** Clarity and action

## Resources

- Linear Method: [linear.app/method](https://linear.app/method)
- "Write Issues Not User Stories": [linear.app/method/write-issues-not-user-stories](https://linear.app/method/write-issues-not-user-stories)

**Grounded in:**
- Linear's product development philosophy
- Modern software team practices
- Reducing ceremony, increasing clarity

---

**Remember:** The goal is clear communication and efficient execution, not following a template.

Write what needs to be built. Skip the ceremony. Ship faster.
