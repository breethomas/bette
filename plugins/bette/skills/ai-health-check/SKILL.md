---
name: ai-health-check
description: Pre-launch health check that blocks you from shipping broken AI features. Grades 6 dimensions (model selection, data quality, cost, monitoring, failure UX, optimization).
---

# AI Health Check

Before you ship an AI feature, it needs to pass 6 checks.

Most AI products fail because PMs skip the basics: no cost model, broken failure UX, terrible data quality. This skill stops you from launching garbage.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AI HEALTH CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Before shipping an AI feature, it needs to pass 6 checks.

What AI feature are you preparing to launch?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/ai-health-check [feature-name]
```

**Examples:**
- `/ai-health-check "AI product recommendations"` - Audit specific feature
- `/ai-health-check "email composer AI"` - Manual description
- `/ai-health-check --pre-launch` - Full checklist for current sprint

## What Happens

1. Invokes the **ai-implementation-auditor** agent
2. Asks hard questions about your AI feature
3. Grades each of 6 dimensions: **Ready** / **Risk** / **Blocker**
4. Tells you if you can ship

## The 6 Dimensions

| Dimension | What It Checks |
|-----------|---------------|
| **Model Selection** | Did you try simple approaches first? |
| **Data Quality** | The thing you're probably ignoring |
| **Cost Modeling** | Can you afford this at scale? |
| **Production Monitoring** | How will you know if it breaks? |
| **Failure UX** | What happens when AI screws up? |
| **System Optimization** | Are you measuring the right things? |

## Verdict Logic

| Condition | Verdict |
|-----------|---------|
| Any Blocker | **DON'T SHIP** |
| 2+ Risks (no blockers) | **NEEDS WORK** |
| 0-1 Risks | **READY** |

## Sample Output

```
AI Health Check: Email Composer

Overall Readiness: NEEDS WORK (4/6 dimensions ready)

---

Ready: Model Selection, Production Monitoring, System Optimization
Risk: Data Quality, Failure UX
Blocker: Cost Modeling

VERDICT: DON'T SHIP YET

You have 1 blocker:
- No cost model -> Run /ai-cost-check RIGHT NOW

You have 2 risks:
- Data quality strategy undefined
- Failure UX is broken ("Something went wrong" isn't helpful)

---

What To Do Now:

Option A: Fix everything (RECOMMENDED)
1. Run /ai-cost-check (10 min)
2. Define data quality strategy (2 hours)
3. Build better failure UX (3 hours)
4. Rerun /ai-health-check

Option B: Ship with known risks
1. Fix the blocker only
2. Ship knowing data quality and failure UX are weak
3. Plan to fix in week 1
```

## Common Blockers

**Cost Modeling missing:**
> "You're about to launch with zero idea if this bankrupts you at scale."
> Run `/ai-cost-check` first.

**Failure UX broken:**
> "Something went wrong" tells users nothing. No confidence indicators = users don't know when to trust the AI.

**No monitoring plan:**
> "Launching without monitoring = flying blind."

## Philosophy (Chip Huyen)

- "Most AI failures are UX problems, not technical ones."
- "Data quality beats tool selection."
- "Fine-tuning should be your last resort."
- "The gap between a demo and a product is production engineering."

## Related Commands

- `/ai-cost-check` - Detailed cost modeling (run if cost dimension is blocked)
- `/start-evals` - Set up quality testing
- `/four-risks` - Overall feature risk assessment

---

**Best for:** Pre-launch validation of AI features
**Key insight:** "Fine-tuning is the last resort. Data quality beats tool selection. Most AI failures are UX problems."
