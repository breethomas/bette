---
name: issue-audit
description: Understand how a team organizes work in Linear. Helps PMs onboarding to new teams learn conventions, see examples, and know what questions to ask.
---

# Issue Audit

Understand how a team organizes and writes issues in Linear. Helps PMs onboarding to new teams learn conventions, see examples, and know what questions to ask.

## Prerequisites

- Linear MCP must be configured

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ISSUE AUDIT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Learn how a team organizes work in Linear.
Helps you onboard faster and follow team conventions.

Which team do you want to analyze?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/issue-audit [team name]
```

**Examples:**
- `/issue-audit Customer Experience`
- `/issue-audit Platform`
- `/issue-audit "Data Engineering"`

## What Happens

1. Invokes the **team-organization-analyzer** agent with your team name
2. Agent fetches team structure: workflow states, labels, cycles
3. Samples 9 issues (3 active, 3 completed, 3 backlog)
4. Analyzes patterns and infers conventions

## What You'll Learn

- **Workflow**: How issues flow through states (Triage -> Done)
- **Labels**: What taxonomy the team uses (Type, Area, Priority)
- **Cycles**: Whether they use sprints and cadence
- **Patterns**: How they write issues (descriptions, titles, hierarchy)
- **Conventions**: What a new PM should follow

## Sample Size Philosophy

9 issues is intentional - enough to observe patterns without overwhelming. The agent:
- Won't apologize for limited data
- Reports specific observations ("5 of 9 have descriptions")
- Infers conventions from patterns
- Offers concrete drill-down prompts

## After the Report

Explore further:
- "Show me issue [ID]" - Full details on any sample
- "Show me 3 parent issues" - See epic structure
- "Show me issues labeled [X]" - Filter by label
- "Run /issue-audit on [other team]" - Compare patterns

## Relationship to Other Commands

```
/linear-calibrate        → Workspace-wide health (30,000 ft view)
         ↓
    ┌────┴────┐
    ↓         ↓
/project-health       /issue-audit
[project]             [team]
(execution health)    (organization patterns) ← THIS COMMAND
```

- `/linear-calibrate` flags workspace-level issues
- `/project-health` checks if a specific project is on track
- `/issue-audit` helps PM understand how a team works

---

*Part of PM Thought Partner Linear analysis suite*
