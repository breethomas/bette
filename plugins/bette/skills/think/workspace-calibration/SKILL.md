---
name: workspace-calibration
description: Analyze Linear workspace health and usage patterns before jumping into backlog work. Like a pre-flight check for a new PM joining a team or organization.
---

# Workspace Calibration Skill

Analyze Linear workspace health and usage patterns before jumping into backlog work. Like a pre-flight check for a new PM joining a team or organization.

## Relationship to /linear-calibrate Command

**For reliable, structured analysis:** Direct users to run `/linear-calibrate`

This skill provides conversational context about Linear workspaces. For formal health checks with explicit thresholds and guaranteed output format, the `/linear-calibrate` command is more reliable.

**When this skill triggers:** Provide helpful context, then suggest:
> "For a formal health check with explicit pass/fail thresholds, run `/linear-calibrate`"

## When to Invoke

Auto-invoke this skill when:

- User is **new to a Linear workspace** and needs to understand how it's organized
- User asks about **workspace health**, structure, or organization
- User wants to understand **how this org uses Linear**
- User mentions **too many teams**, confusing structure, or workspace chaos
- User asks **"where do I start?"** with a large existing backlog
- Before running backlog commands like `/lno-prioritize` on an unfamiliar workspace

**Trigger phrases (must mention Linear explicitly):**
- "Help me understand this Linear workspace"
- "How is this org using Linear?"
- "Run a Linear workspace health check"
- "Analyze our Linear workspace"
- "Calibrate this Linear workspace"
- "Is our Linear workspace healthy?"
- "There are so many teams in Linear, where do I start?"

**Note:** Generic phrases like "workspace health check" may be interpreted as project/codebase checks. Always include "Linear" in the request.

## What This Skill Does

### CRITICAL: API Limits

**When calling Linear MCP tools, ALWAYS specify `limit: 250`** to avoid default truncation:
- `list_teams` defaults to 50 - use `limit: 250`
- `list_projects` defaults to 50 - use `limit: 250`
- `list_issues` defaults to 50 - use `limit: 250`
- `list_issue_labels` defaults to 50 - use `limit: 250`

If any result count equals 250, note there may be more items.

### 1. Workspace Discovery
Gather data about the workspace structure using Linear MCP tools:
- List all teams, their members, and activity
- Sample issues to understand quality patterns
- Analyze projects, cycles, labels
- Identify conventions and patterns

### 2. Health Assessment
Compare reality to Linear's methodology (see `references/linear-methodology.md`):
- Are teams structured as durable groups or labels-as-teams?
- Is issue quality good (clear titles, no user story format)?
- Are backlogs manageable or overwhelming?
- Are projects well-scoped with owners and dates?
- Is triage being used effectively?

### 3. Calibration Report
Produce actionable output:
- Health indicators (green/yellow/red) for each dimension
- Conventions guide ("Here's how this org uses Linear")
- Red flags requiring attention
- Recommendations for cleanup or improvement
- Context for future backlog work

---

## Calibration Process

### Step 1: Announce Intent

```
I'll analyze this Linear workspace to help you understand:
- How it's structured (teams, projects, workflows)
- What's healthy vs concerning
- How this org uses Linear compared to best practices
- Where to focus your attention

This takes a few minutes. I'll pull data across teams and issues.
```

### Step 2: Gather Data

Use Linear MCP tools to collect:

```
1. Teams
   - list_teams with limit: 250 (max)
   - If count = 250, flag as SEVERE: "Workspace may have 250+ teams - extreme proliferation"
   - For each active team: get_team for details
   - Note: member count, activity, naming patterns

2. Issues (sample)
   - list_issues with various filters:
     - Recent issues (last 30 days)
     - Stale issues (no update in 90 days)
     - Sample from multiple teams
   - Analyze: titles, descriptions, age distribution

3. Projects
   - list_projects: Get all projects
   - Note: leads, dates, status, issue counts

4. Cycles (if used)
   - list_cycles for active teams
   - Note: completion rates, carryover

5. Labels
   - list_issue_labels: Get all labels
   - Note: count, naming consistency, usage

6. Statuses
   - list_issue_statuses for key teams
   - Note: complexity, customization
```

### Step 3: Analyze Against Methodology

For each dimension, compare findings to Linear best practices:

**Team Structure:**
- Count teams, calculate members per team
- Identify teams with 0-3 members (potential labels-as-teams)
- Check for topic-named teams vs group/area-named teams
- Flag teams with no activity in 90 days

**Issue Quality:**
- Sample 50-100 issues across teams
- Check for user story format ("As a...")
- Analyze title quality (action-oriented vs vague)
- Note description patterns

**Backlog Health:**
- Calculate age distribution of open issues
- Identify staleness (% untouched in 60/90 days)
- Note backlog size per team

**Project Health:**
- Check for leads assigned
- Check for target dates
- Identify stale projects
- Note scope (issues per project)

**Workflow Complexity:**
- Count statuses per team
- Compare to Linear defaults
- Flag over-engineered workflows

### Step 4: Produce Calibration Report

**REQUIRED:** Always output the full structured report below. Do not summarize conversationally - the user needs the health indicators table and red flags to know where to focus.

Output this exact format:

```markdown
# Workspace Calibration Report

**Workspace:** [name]
**Date:** [date]
**Analyzed:** [X teams, Y issues sampled, Z projects]

---

## Executive Summary

[2-3 sentences: Overall health, key findings, top concerns]

---

## Health Indicators

| Dimension | Status | Finding |
|-----------|--------|---------|
| Team Structure | 🟢/🟡/🔴 | [summary] |
| Issue Quality | 🟢/🟡/🔴 | [summary] |
| Backlog Health | 🟢/🟡/🔴 | [summary] |
| Project Health | 🟢/🟡/🔴 | [summary] |
| Cycle Usage | 🟢/🟡/🔴 | [summary] |
| Workflow Complexity | 🟢/🟡/🔴 | [summary] |
| Triage Usage | 🟢/🟡/🔴 | [summary] |
| Label Hygiene | 🟢/🟡/🔴 | [summary] |

---

## How This Org Uses Linear

[Describe the patterns observed - team structure philosophy,
workflow conventions, project usage, cycle rhythm, etc.
This helps a new PM understand "how we do things here."]

### Teams
[List key teams with brief description of what they own]

### Conventions
- Issue titles: [pattern observed]
- Labels: [how they're used]
- Projects: [how they're scoped]
- Cycles: [if/how they're used]

---

## Red Flags

[List specific issues requiring attention]

1. **[Issue]**: [Details and why it matters]
2. **[Issue]**: [Details and why it matters]

---

## Recommendations

### Immediate (This Week)
1. [Specific action]
2. [Specific action]

### Near-Term (This Month)
1. [Specific action]
2. [Specific action]

### Consider (When Ready)
1. [Larger improvement]

---

## Gut-Check Questions

Before diving into backlog work, consider:

- [ ] Can you explain what each team owns in one sentence?
- [ ] Do you know where to file any given issue within 2 clicks?
- [ ] Are there teams that should be consolidated?
- [ ] Is there stale work that should be archived?

---

*Calibration powered by PM Thought Partner*
*Methodology: Linear Method (linear.app/method)*
```

### Step 5: Offer Next Steps

```
Your workspace is calibrated. Here's what I'd suggest:

1. [If red flags]: Address the [specific issue] first
2. [If healthy]: You're ready to run /lno-prioritize on [team]
3. [If context needed]: Want me to deep-dive on any dimension?

I now have context about how this org uses Linear. Future backlog
commands will account for your workspace patterns.
```

---

## Key Principles

### Compare to Methodology, Not Perfection
Linear's methodology is opinionated. Some orgs intentionally deviate. The goal is:
- Surface where reality differs from best practice
- Help user understand if deviations are intentional or drift
- Don't prescribe - inform and let user decide

### New PM Orientation
This skill is especially valuable for PMs joining an existing org:
- "Here's how this workspace is structured"
- "Here's what's healthy vs concerning"
- "Here's where to focus first"

### Set Up Future Work
Calibration provides context for subsequent commands:
- `/lno-prioritize` works better when you understand team structure
- `/four-risks` makes more sense when you know project conventions
- Backlog cleanup is informed by health assessment

---

## Integration with Other Skills

After calibration:
- **pm-frameworks skill**: Apply prioritization frameworks with workspace context
- **backlog-analysis skill** (future): Deep-dive on specific team/project backlogs
- Commands like `/lno-prioritize`, `/now-next-later`: Run with understanding of conventions

---

## Edge Cases

### No Linear MCP
If Linear MCP isn't configured:
```
I'd like to analyze your Linear workspace, but I don't have access.

To enable workspace calibration:
1. Get a Linear API key (Settings > Account > Security & Access)
2. Ask Claude "Set up the Linear MCP server"

Alternatively, you can describe your workspace structure and I'll
help you think through it manually.
```

### Very Large Workspace
For workspaces with 50+ teams or 10K+ issues:
```
This is a large workspace. I'll sample strategically rather than
analyzing everything:
- All teams (for structure analysis)
- 100-200 issues across key teams (for quality patterns)
- Active projects only (for project health)

This gives representative data without overwhelming the analysis.
```

### Recently Created Workspace
For new workspaces with minimal data:
```
This workspace is relatively new with limited history.

Instead of a full health check, I'll help you:
- Set up team structure following Linear best practices
- Establish conventions before patterns emerge
- Avoid common pitfalls (labels-as-teams, user story format, etc.)
```

---

## Reference Documents

- `references/linear-methodology.md` - Linear's recommended practices
- `references/health-indicators.md` - Detailed health dimensions and thresholds
