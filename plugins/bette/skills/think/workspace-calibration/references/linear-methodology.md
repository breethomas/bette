# Linear Methodology Reference

Source: [linear.app/method](https://linear.app/method) and [linear.app/docs](https://linear.app/docs)

## Core Philosophy

Linear emphasizes building quality software by focusing on foundational practices. Their core belief: "The quality of a product is driven by both the talent of its creators and how they feel while they're crafting it."

This means: minimize process overhead, keep things simple, ship frequently.

---

## Conceptual Model

**Hierarchy:** Workspace → Teams → Issues

- **Workspace**: Container for all issues, teams, and concepts for one company
- **Teams**: Groups of people who work together frequently, OR product areas
- **Issues**: The fundamental unit of work (only title and status required)

**Cross-cutting concepts:**
- **Projects**: Group issues toward time-bound deliverables (can span teams)
- **Cycles**: Sprint-like timeboxes (per-team)
- **Views**: Dynamic filters for discovering/organizing work

---

## Teams

### What Teams Should Be
- **Durable groups** who work together frequently
- OR **product areas** (not topics, not bug categories)
- Examples: "Growth", "Core App", "Platform", "Mobile"

### What Teams Should NOT Be
- Topics (e.g., "Billing Bugs")
- Temporary initiatives
- Labels-as-teams (creating a team for every category)

### Best Practices
- **Start small**: "If you aren't sure how to split up your teams, start with one or two"
- **Add as needed**: Easy to add teams later, copy settings, move issues
- Issues are team-bound (can't span teams, though projects can)
- Each team can have its own workflow/statuses and cycles

### Red Flags
- 60+ teams in a workspace (likely misusing teams as categories)
- Many teams with 0-3 members
- Teams with no activity for 90+ days
- Teams named after topics instead of groups/areas

---

## Issues (Not User Stories)

### Linear's Position
"User stories have become a cargo cult ritual that feels good but wastes a lot of resources and time."

Modern teams don't need user stories because:
- Customers can articulate requirements directly
- Common features have established patterns
- Strong teams understand their users deeply

### What Makes a Good Issue
1. **Clear, direct title**: Scannable, states exactly what needs doing
   - Good: "Fix calendar loading bug on mobile"
   - Bad: "Calendar issues" or "As a user, I want to see my calendar load faster"

2. **Concrete task with defined outcome**: Specific deliverable (code, design, document)

3. **Minimal but sufficient description**: Only what's necessary to execute
   - Quote customer feedback directly rather than summarizing

### What Issues Should NOT Contain
- User story format ("As a X, I want Y, so that Z")
- Vague exploration without clear scope
- Large features that need breaking down first

### Key Principle
"Write your own issues. This forces deeper thinking about problems."

---

## Projects

### What Projects Are
- Units of work with **clear outcome** or **planned completion date**
- Like launching a feature
- Can span multiple teams
- Comprise issues and optional documents

### Best Practices
- **Require a project lead** for clear ownership
- **Set start and end dates** (even approximate ones)
- **Organize around outcomes**, not features
  - Good: "Improve trial conversion"
  - Bad: "Pricing page revamp"
- Use milestones to subdivide into meaningful stages

### For Ongoing Work
- Create projects without target dates, OR
- Break into smaller, time-boxed projects, OR
- Use custom "Maintenance" status

---

## Cycles

### What Cycles Are
- Sprint-like timeboxes
- Automated and repeating
- Per-team (not workspace-wide)

### Best Practices
- **Start with 1-2 week cycles**
- Run consistently (same length each time)
- Issues automatically roll over if not completed
- Use for planning rhythm, not release themes

---

## Triage

### What Triage Is
- Special inbox for incoming issues
- Reviews work before adding to your workflow
- Particularly valuable for issues from integrations or other teams

### Actions
- **Accept**: Move to default status
- **Mark as duplicate**: Merge into existing issue
- **Decline**: Cancel with explanation
- **Snooze**: Hide temporarily

### Best Practices
- Establish rotating ownership for triage
- Request clarification before accepting unclear issues
- Configure to require priority before issues leave triage

---

## Backlog Management

### Best Practices
- **Keep backlogs lean** through consistent weekly triage
- **Archive stale issues** regularly (untouched for 90+ days)
- Clutter breeds confusion and missed priorities

### Signs of Unhealthy Backlog
- Hundreds of issues with no recent activity
- Issues without clear scope or owner
- Duplicate or overlapping issues
- Issues that are really "ideas" not actionable work

---

## Workflow & Statuses

### Linear's Default
Triage → Backlog → In Progress → In Review → Done

### Best Practices
- **Start with defaults**: Only customize when genuine workflow pain emerges
- "Resist the temptation to mirror complex Jira configurations"
- Simpler is better

---

## Prioritization: Enablers & Blockers

### Definitions
- **Enablers**: Add new functionality, make product more valuable
- **Blockers**: Gaps or friction preventing users from adopting

### Key Principle
"Growth comes from investing energy on the right enablers and removing critical blockers."

### Questions to Ask
1. **Is this timely?** Will it help achieve goals this week/month?
2. **Does it compound?** Consider future effects and complexity costs
3. **What's the sequence?** What must come first?

---

## Labels

### Best Practices
- Keep minimal and consistent
- Avoid variations ("Bugs" vs "Bug" vs "bug")
- Use as swimlanes for organizing views
- Don't create labels that should be teams (or vice versa)

---

## Integration Patterns

### Recommended
- **GitHub/GitLab**: Auto-update status when PRs merge
- **Slack**: Create issues from conversations, post updates
- Connect support tools for customer feedback → triage

---

## Signs of a Healthy Linear Workspace

1. **Clear team structure**: Each team has obvious ownership and 4+ active members
2. **Clean backlogs**: Issues have recent activity, clear scope
3. **Consistent cycles**: Regular rhythm, reasonable carryover
4. **Projects with dates**: Clear start/end, assigned leads
5. **Simple workflows**: Using defaults or minimal customization
6. **Active triage**: Incoming work is reviewed and routed
7. **Good issue hygiene**: Clear titles, no user story format, minimal stale issues

## Signs of an Unhealthy Linear Workspace

1. **Team proliferation**: 30+ teams, many with 0-3 members
2. **Stale backlogs**: Hundreds of issues untouched for months
3. **No cycles**: Work has no rhythm or planning cadence
4. **Projects without owners/dates**: Vague initiatives floating indefinitely
5. **Over-engineered workflows**: 10+ statuses mimicking Jira
6. **Triage ignored**: Issues pile up without review
7. **Poor issue quality**: Vague titles, user story format, no clear scope
