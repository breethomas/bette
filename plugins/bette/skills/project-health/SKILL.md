---
name: project-health
description: Deep-dive health check on a single Linear project. Produces assessment with 7 dimensions - On Track / At Risk / Stalled.
---

# Project Health Check

Analyze a single Linear project against execution best practices. Produces a health assessment: On Track / At Risk / Stalled.

## Prerequisites

- Linear MCP must be configured
- Run `/linear-calibrate` first to identify projects worth investigating

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 PROJECT HEALTH CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Deep-dive health check on a specific Linear project.

Which project do you want to analyze?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/project-health [project-name]
```

**Examples:**
- `/project-health AI Video`
- `/project-health "HBN for Agent Customers"`

## What Happens

1. Invokes the **project-health-checker** agent with your project name
2. Agent fetches project details and all issues from Linear
3. Applies 7 health dimensions with status-aware thresholds
4. Generates structured health assessment

## Health Dimensions

| Dimension | What It Measures |
|-----------|------------------|
| Ownership | Does the project have a lead assigned? |
| Timeline | Are start and target dates set? Is it overdue? |
| Progress | Completion percentage and recent activity |
| Scope Clarity | Description length (>300 chars = clear scope) |
| Issue Distribution | Right number of issues (5-100 is healthy) |
| Blockers | Percentage of open issues that are blocked |
| Staleness | Days since last activity |

## Overall Rating

| Condition | Status |
|-----------|--------|
| Any red dimension | **Stalled** |
| 2+ yellow (no red) | **At Risk** |
| 0-1 yellow | **On Track** |

## After the Report

Options:
1. **Fix a specific red flag** - I can help update the project
2. **See blocked issues** - Detail on what's stuck
3. **Review issues missing descriptions** - Quality cleanup
4. **Run on another project** - `/project-health [other-name]`

## Relationship to Other Commands

```
/linear-calibrate        → Workspace-level (flags "497 projects, 86% missing dates")
         ↓
/project-health [name]   → THIS COMMAND - deep-dive on flagged projects
         ↓
/issue-audit [team]      → Team workflow analysis
```

---

*Part of PM Thought Partner Linear analysis suite*
