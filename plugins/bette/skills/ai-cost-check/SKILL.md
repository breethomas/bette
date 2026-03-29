---
name: ai-cost-check
description: Calculate AI feature costs and challenge if you actually need it. Invokes ai-cost-analyzer agent for detailed economics modeling.
---

# AI Cost Check

Before you build an AI feature, answer two questions:
1. **Do you actually need this feature?**
2. **Can you afford it?**

Most PMs skip #1 and regret #2 later.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AI COST CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AI features have marginal costs that scale with usage.
Model this BEFORE building, not after launch.

What AI feature are you considering?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/ai-cost-check [feature-name]
```

**Examples:**
- `/ai-cost-check "product recommendations"` - Calculate recommendation costs
- `/ai-cost-check "email composer"` - Model email generation economics
- `/ai-cost-check --compare` - Compare cost across different models

## What Happens

1. Invokes the **ai-cost-analyzer** agent
2. **Challenges the premise first** - Do you have evidence users want this?
3. **Models the economics** - Cost per request, cost at scale, % of revenue
4. **Provides a verdict** - Sustainable, viable but expensive, or unsustainable
5. **Shows optimization paths** - Caching, model selection, prompt optimization

## The Philosophy

AI products have marginal costs that scale with usage. Every user interaction costs money. Model this BEFORE building, not after launch when you're hemorrhaging cash.

## Cost Thresholds

| AI Cost as % of Revenue | Status | Recommendation |
|-------------------------|--------|----------------|
| <15% | Sustainable | Build it |
| 15-30% | Viable | Build with optimization plan |
| >30% | Unsustainable | Don't build (or fundamentally rethink) |

## What You'll Get

```
FEATURE DETAILS:
- Model: GPT-4 Turbo
- Calls per recommendation: 1
- Input: 1,500 tokens
- Output: 300 tokens

COST BREAKDOWN:
Per request: $0.024
Per user/month: $2.16

| Scale | Monthly Cost | Your Revenue | AI % of Revenue |
|-------|-------------|--------------|-----------------|
| 100   | $216        | $2,000       | 10.8%           |
| 10K   | $21,600     | $200,000     | 10.8%           |

VERDICT: Sustainable at 10.8% of revenue

OPTIMIZATION PATHS:
1. Caching (saves 40-60%): $8,640/month at 10K users
2. Model selection (saves 70%): Use GPT-3.5 for simple cases
```

## Model Price Reference (January 2025)

| Model | Input | Output |
|-------|-------|--------|
| GPT-4 Turbo | $0.01/1K | $0.03/1K |
| GPT-4o | $0.005/1K | $0.015/1K |
| GPT-3.5 Turbo | $0.0005/1K | $0.0015/1K |
| Claude 3.5 Sonnet | $0.003/1K | $0.015/1K |
| Claude 3 Haiku | $0.00025/1K | $0.00125/1K |

## Related Commands

- `/ai-health-check` - Full pre-launch readiness audit
- `/four-risks` - Includes viability (business model) risk
- `/pmf-survey` - Validate willingness to pay

---

**Key insight:** "Most AI features are solutions looking for problems. Validate the problem before modeling costs."
