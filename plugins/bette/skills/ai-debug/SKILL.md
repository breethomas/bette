---
name: ai-debug
description: Diagnose why an AI feature is underperforming, hallucinating, or behaving inconsistently. Uses 4D audit to work backwards from symptoms to root cause.
---

# AI Debug

Figure out **why an existing AI feature is broken**.

**Works with:**
- **Linear MCP** - Pull issue/bug details
- **Manual** - Describe the symptoms

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AI DEBUG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

When AI fails, teams blame the model.
But 90% of failures are context failures.

What's going wrong?

  1. Provide a Linear issue ID
  2. Describe the symptoms

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/ai-debug                 # Describe symptoms manually
/ai-debug LIN-123         # Start from Linear bug/issue
```

## What It Does

Works backwards from symptoms to root cause using the 4D audit:

| Symptom | Likely Root Cause | Focus Area |
|---------|-------------------|------------|
| Hallucinations | Missing domain context, no grounding | D2, D4 |
| Inconsistency | Vague job definition, missing rules | D1, D4 |
| Generic outputs | Missing user/environment context | D2 |
| Wrong tone/format | Missing constraints, no examples | D1, D4 |
| Slow responses | Too much context, bad discovery | D2, D3 |
| High costs | Dumping everything in prompt | D2, D3 |
| Demo vs prod mismatch | Discovery strategy broken | D3, D4 |

**Key insight:** When AI fails, teams blame the model. But 90% of failures are context failures.

## The 4D Audit

### D1: Was the Job Defined?
- Can you articulate exactly what the model should produce?
- Is there a written spec for inputs, outputs, constraints?
- Do engineers and PMs agree on what "good" looks like?

### D2: Is Context Right?
- What context is the model actually receiving?
- Walk through the 6 layers: Intent, User, Domain, Rules, Environment, Exposition
- Is context structured or dumped as raw text?
- Is there too much context (token bloat)?

### D3: Is Context Fetched Reliably?
- How is each piece of context being fetched at runtime?
- What happens when a data source is unavailable?
- Is there visibility into what context is used per request?

### D4: Are Failures Being Caught?
- Are there pre-checks before calling the model?
- Are there post-checks validating output?
- What's the fallback UX when things break?
- Is there a feedback loop capturing failures?

## Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CONTEXT AUDIT COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [Name]
Symptoms: [What was reported]

  D1 Demand:      [CLEAR / GAP / CRITICAL]
  D2 Data:        [CLEAR / GAP / CRITICAL]
  D3 Discovery:   [CLEAR / GAP / CRITICAL]
  D4 Defense:     [CLEAR / GAP / CRITICAL]

Primary Issue: [Root cause summary]

RECOMMENDED FIXES (prioritized):
1. [Highest impact fix]
2. [Second fix]
3. [Third fix]

Quick Win: [Smallest change that would help]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Workflow

1. Collect symptoms (what's going wrong)
2. Map symptoms to likely causes using the table above
3. Audit each D dimension with diagnostic questions
4. Identify root cause and prioritize fixes
5. Offer to add findings to Linear or export

**Questions to ask at each step:**
- "What specific behavior are you seeing?"
- "What should it be doing instead?"
- "When did this start happening?"
- "Does it happen every time or intermittently?"

---

**Framework:** 4D Context Canvas (Aakash Gupta & Miqdad Jaffer)
**Best for:** Debugging hallucinations, inconsistency, performance issues in AI features
