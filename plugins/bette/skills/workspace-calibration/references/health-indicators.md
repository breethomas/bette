# Workspace Health Indicators

Dimensions to analyze when calibrating a Linear workspace.

> **Note:** For canonical thresholds with exact pass/fail values, see `/linear-calibrate` command. This document provides narrative guidance and context.

---

## 1. Team Structure

**What to analyze:**
- Total team count
- Members per team (active users)
- Team naming patterns
- Activity distribution across teams

**Healthy signals:**
- 4-15 teams for most orgs (scales with company size)
- Each team has 4+ active members
- Teams named after durable groups or product areas
- Work distributed across teams (not concentrated in 1-2)

**Warning signals:**
- 16-30 teams = review needed; 31+ teams = problem (likely labels-as-teams)
- Many teams with 0-3 members (ghost teams)
- Teams named after topics ("Bugs", "Tech Debt", "Ideas")
- Many teams with zero activity in 90 days (>25% stale = problem)

**Gut-check questions:**
- Can you explain what each team owns in one sentence?
- Are these real squads or "labels-as-teams"?
- Could you consolidate to 8-15 without losing anything?
- Does a new PM know where to file any given issue within 2 clicks?

---

## 2. Issue Quality

**What to analyze:**
- Title patterns (clear vs vague)
- User story format usage
- Description completeness
- Scope clarity

**Healthy signals:**
- Action-oriented titles (verb + subject + context)
- No "As a user, I want..." format
- Issues have clear, concrete outcomes
- Minimal but sufficient descriptions

**Warning signals:**
- Vague titles ("Fix bug", "Update page", "Improvements")
- User story format everywhere
- Issues that are really epics (need breaking down)
- Missing descriptions on complex issues

**Patterns to detect:**
- Titles starting with "As a..."
- Single-word titles
- Titles that are questions
- Issues with no description and vague titles

---

## 3. Backlog Health

**What to analyze:**
- Total open issues
- Age distribution (how old are open issues?)
- Recent activity (touched in last 30/60/90 days)
- Issues per team/project

**Healthy signals:**
- Most open issues touched within 30 days
- Backlog size manageable (not thousands of stale items)
- Regular archiving of abandoned work
- Clear prioritization (not everything is "high")

**Warning signals:**
- 100+ issues untouched for 90+ days
- Backlogs with 500+ items per team
- No clear prioritization pattern
- Duplicate or overlapping issues

**Staleness thresholds:**
- 🟢 Green: <20% issues untouched 60+ days
- 🟡 Yellow: 20-40% issues untouched 60+ days
- 🔴 Red: >40% issues untouched 60+ days

---

## 4. Project Health

**What to analyze:**
- Projects with/without leads
- Projects with/without target dates
- Active vs stale projects
- Project scope (issues per project)

**Healthy signals:**
- All projects have assigned leads
- Projects have start/target dates (even approximate)
- Projects are time-bound (not indefinite)
- Reasonable scope (10-50 issues typically)

**Warning signals:**
- Projects without owners (>30% missing = problem)
- Projects with no dates (>50% missing = problem)
- Projects with 100+ issues (too big)
- Projects with 0 activity for 60+ days
- Projects named as ongoing work ("Maintenance", "Bugs")

**Project count thresholds:**
- 🟢 Green: 1-50 projects (manageable)
- 🟡 Yellow: 51-150 projects (sprawling)
- 🔴 Red: 151+ projects (audit and archive needed)

---

## 5. Cycle Usage

**What to analyze:**
- Which teams use cycles
- Cycle length and consistency
- Completion rates
- Carryover patterns

**Healthy signals:**
- Teams have consistent cycle rhythm
- 1-2 week cycles
- Reasonable completion rates (60-80%)
- Carryover is intentional, not just overflow

**Warning signals:**
- No cycles (no planning rhythm)
- Inconsistent cycle lengths
- Very low completion rates (<40%)
- Massive carryover every cycle

**Note:** Some teams intentionally don't use cycles (continuous flow). This isn't necessarily unhealthy - just different.

---

## 6. Workflow Complexity

**What to analyze:**
- Number of statuses per team
- Custom vs default workflows
- Status usage distribution

**Healthy signals:**
- Using Linear defaults or minimal customization
- 4-6 statuses total
- Clear progression (not circular)
- All statuses actually used

**Warning signals:**
- 10+ statuses (over-engineered)
- Mimicking Jira complexity
- Statuses that are never used
- Confusing status names

---

## 7. Triage Usage

**What to analyze:**
- Is triage enabled?
- Volume in triage
- Time-to-triage (how long do items sit?)
- Triage → accepted ratio

**Healthy signals:**
- Triage enabled and actively used
- Items reviewed within 1-2 days
- Clear ownership of triage duty
- Most items accepted or declined (not lingering)

**Warning signals:**
- Triage disabled or ignored
- 50+ items sitting in triage
- Items in triage for weeks
- No clear triage process

---

## 8. Label Hygiene

**What to analyze:**
- Total label count
- Label naming consistency
- Labels vs teams overlap
- Label usage distribution

**Healthy signals:**
- Minimal labels (10-25 = healthy)
- Consistent naming (no "Bug" vs "bug" vs "Bugs")
- Labels complement teams (not duplicate)
- Most labels actually used

**Warning signals:**
- 26-50 labels = getting complex; 51+ labels = sprawl
- Inconsistent naming conventions
- Labels that should be teams
- Many labels with <5 issues

---

## 9. Cross-Team Patterns

**What to analyze:**
- Projects spanning multiple teams
- Dependencies between teams
- Shared views usage
- Initiative structure

**Healthy signals:**
- Cross-team projects have clear ownership
- Dependencies are tracked (blocking/blocked)
- Shared views for leadership visibility
- Initiatives group related work

**Warning signals:**
- Cross-team work with no coordination
- Hidden dependencies (not tracked)
- No workspace-level visibility
- Siloed teams with no shared context

---

## Calibration Output Summary

After analysis, produce ratings for each dimension. For the full structured report format with exact thresholds, run `/linear-calibrate`.

| Dimension | Threshold | Status | Key Finding |
|-----------|-----------|--------|-------------|
| Team Count | 4-15 🟢 / 16-30 🟡 / 31+ 🔴 | 🟢/🟡/🔴 | [summary] |
| Team Sizes | 4+ 🟢 / 2-3 🟡 / 0-1 🔴 | 🟢/🟡/🔴 | [summary] |
| Stale Teams | <10% 🟢 / 10-25% 🟡 / >25% 🔴 | 🟢/🟡/🔴 | [summary] |
| Project Count | 1-50 🟢 / 51-150 🟡 / 151+ 🔴 | 🟢/🟡/🔴 | [summary] |
| Project Ownership | <10% 🟢 / 10-30% 🟡 / >30% 🔴 missing | 🟢/🟡/🔴 | [summary] |
| Project Dates | <20% 🟢 / 20-50% 🟡 / >50% 🔴 missing | 🟢/🟡/🔴 | [summary] |
| Backlog Staleness | <20% 🟢 / 20-40% 🟡 / >40% 🔴 | 🟢/🟡/🔴 | [summary] |
| Label Count | 10-25 🟢 / 26-50 🟡 / 51+ 🔴 | 🟢/🟡/🔴 | [summary] |
| Issue Quality | <10% 🟢 / 10-25% 🟡 / >25% 🔴 problems | 🟢/🟡/🔴 | [summary] |

Plus:
- Top 3 recommendations (Immediate / Near-Term / Maintenance)
- Conventions guide (how this org uses Linear)
- Red flags requiring attention with "Ask Claude" follow-up prompts
