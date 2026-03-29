---
name: lno-prioritize
description: Find out if you're spending time on the wrong things. Categorize backlog by Leverage/Neutral/Overhead and challenge your time allocation.
---

# LNO Prioritize

**Most PMs waste time on overhead disguised as strategy.**

This skill categorizes your backlog by actual impact:
- **Leverage (L):** 10x impact - the work that actually matters
- **Neutral (N):** Regular work - do it well enough, move on
- **Overhead (O):** Busywork - minimize or automate

Then tells you if your time allocation is broken.

**Works with:**
- **Linear MCP** - Auto-analyzes and labels your issues
- **GitHub MCP** - Auto-analyzes and labels your issues
- **Manual** - Paste your issue list

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 LNO PRIORITIZATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Are you spending 60%+ time on Leverage work?
Most PMs aren't.

What do you want to analyze?

  1. Current sprint/cycle
     → I'll fetch and categorize all active issues

  2. Specific team or project
     → Focus on a subset of your backlog

  3. Paste issue list
     → I'll categorize what you provide

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## What This Does

Categorizes every issue, then challenges your priorities:
- Are you spending 60%+ time on Leverage work? (You should be)
- Is "strategy work" actually Overhead disguised as important?
- Which Neutral tasks can you delegate or do at B- quality?
- Which Overhead tasks can you eliminate entirely?

## Usage

```
/lno-prioritize
```

**Optional parameters:**
- `/lno-prioritize --team [team-name]` - Categorize specific team's issues
- `/lno-prioritize --project [project-name]` - Categorize specific project
- `/lno-prioritize --label` - Auto-add Linear labels (leverage/neutral/overhead)
- `/lno-prioritize --current-sprint` - Only analyze current sprint issues

## What Happens

1. **Fetches issues** from Linear or GitHub (if MCPs configured)
2. **Applies LNO framework**
3. **Categorizes each issue** based on:
   - Strategic importance
   - Impact potential
   - Time investment required
   - Compounding value
4. **Returns analysis** with:
   - Issue title and ID
   - LNO category assignment
   - Reasoning for categorization
   - Recommended time allocation
5. **Optionally updates source** with labels (if `--label` flag used and using Linear)

## Example Output

```
📊 LNO Prioritization Results

🚀 LEVERAGE (10x impact - be a perfectionist):
- [ENG-245] Rebuild recommendation engine
  Reason: Core product differentiator, compounds over time

- [ENG-198] Product strategy for Q2
  Reason: Foundational decision affecting all downstream work

📈 NEUTRAL (Regular impact - do good enough work):
- [ENG-301] Update onboarding flow copy
  Reason: Important but not transformational

- [ENG-276] Add analytics to checkout page
  Reason: Useful data but incremental improvement

⚙️ OVERHEAD (Minimal impact - do quickly):
- [ENG-312] Reformat PRD template
  Reason: Administrative work, no strategic value

- [ENG-288] Update Linear labels
  Reason: Organizational cleanup

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 YOUR TIME ALLOCATION IS BROKEN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Current backlog:
- 2 Leverage tasks (20%)
- 4 Neutral tasks (40%)
- 4 Overhead tasks (40%)

TARGET allocation:
- 60% Leverage (you're at 20% - way too low)
- 30% Neutral
- 10% Overhead (you're at 40% - way too high)

WHAT TO DO:
1. **Kill or delegate 3 of 4 Overhead tasks**
   - Reformatting templates? Not your job.
   - Linear labels? Automate it.

2. **Stop perfectionism on Neutral work**
   - Onboarding copy doesn't need to be perfect
   - Ship at B- quality and move on

3. **Focus on Leverage:**
   - Recommendation engine = your #1 priority
   - Q2 strategy = your #2 priority
   - Everything else can wait

Want me to create Linear issues to delegate/automate the Overhead work?
```

## Integration Options

**With Linear MCP:**
Automatically fetches Linear issues and can add L/N/O labels.

**With GitHub MCP:**
Automatically fetches GitHub issues and can add labels.

**Manual mode:**
Paste your issues and the skill will categorize them:
```
Apply the LNO framework to these issues: [paste issue list]
```

## Learn More

See the full LNO Prioritization framework at:
`frameworks/planning/lno-prioritization.md`

---

**Framework:** Aakash Gupta (based on Shreyas Doshi)
**Best for:** Sprint planning, backlog grooming, time management
**AI-era adaptation:** Focus on leverage work (vision, strategy) while AI handles neutral/overhead tasks
