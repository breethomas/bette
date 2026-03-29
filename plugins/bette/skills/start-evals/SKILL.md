---
name: start-evals
description: Start AI evals without overengineering. Create your first 20 test cases in a spreadsheet using PM-Friendly Evals approach.
---

# Start Evals

Launch your AI evaluation process using the **PM-Friendly Evals approach** (Aman Khan + Hamel Husain).

Start with 20 test cases in a spreadsheet. Scale when ready. Error analysis > automation.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 START EVALS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Start with 20 test cases. Scale when ready.

What AI feature are you evaluating?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/start-evals [feature-name]
```

**Examples:**
- `/start-evals "AI product recommendations"` - Generate test cases
- `/start-evals --create-project` - Create Linear project for tracking
- `/start-evals "customer support AI" --count 50` - Generate 50 test cases

## What Happens

1. Invokes the **eval-generator** agent
2. Asks about your AI feature and quality criteria
3. Generates 20 test cases (15 happy path + 5 edge cases)
4. Provides spreadsheet template and workflow
5. Optionally creates Linear project for tracking

## The Philosophy

**Good -> Better -> Best progression:**

| Stage | Test Cases | Process | Tool |
|-------|------------|---------|------|
| **Good** (Week 1) | 20 | Manual review | Spreadsheet |
| **Better** (Month 1-2) | 50-100 | LLM-as-judge | Weekly reviews |
| **Best** (Month 3+) | 200+ | Automated | CI/CD integration |

**Start here.** You're at "Good." Don't jump to automation.

## What You'll Get

```
AI Evals Starter Kit: Product Recommendations

HAPPY PATH (15 cases):

1. Input: "Recommend a laptop under $800 for college"
   Expected: Mid-range laptops with student-friendly features, under budget
   Pass criteria: All recommendations < $800, suitable for students

2. Input: "Best phone for photography"
   Expected: High-end phones with excellent cameras
   Pass criteria: Focus on camera quality, not price

...

EDGE CASES (5 cases):

16. Input: "Phone for elderly person"
    Expected: Simple, large screen, easy to use
    Pass criteria: Prioritizes simplicity over features
    Why it's tricky: Must understand implicit needs

...
```

## Week 1 Workflow (2-3 hours)

1. Copy test cases to spreadsheet (10 min)
2. Run your AI against each input (1-2 hours)
3. Record actual outputs
4. Mark pass/fail
5. Look for patterns in failures (30 min)

## After 1-2 Weeks

| Pass Rate | Action |
|-----------|--------|
| 80%+ | Add 10 more test cases |
| <80% | Fix issues, rerun |
| 50-100 cases | Graduate to "Better" approach |

## Common Questions

**Q: 20 seems like too few. Should I start with 100?**
A: No. 20 cases covering your core use case > 100 cases you never run.

**Q: How long does running 20 tests take?**
A: First time: 30-60 min. After that: 15-20 min per run.

**Q: Do I need special tools?**
A: No. Spreadsheet works great. Graduate to tools when manual gets painful.

## Ready to Scale?

| Signal | Next Step |
|--------|-----------|
| You have 50+ test cases or see production failures | `/upgrade-evals` — Systematic error analysis on real traces |
| You need more diverse test inputs | `/generate-test-data` — Dimension-based synthetic data |
| Your AI feature uses retrieval (search, knowledge base) | `/eval-rag` — Separate retrieval from generation evaluation |

## Related Commands

- `/upgrade-evals` - Error analysis on real traces (next step after this)
- `/build-judge` - LLM-as-Judge for subjective failure modes
- `/generate-test-data` - Diverse synthetic test inputs
- `/eval-rag` - RAG-specific retrieval + generation evaluation
- `/calibrate` - Ongoing post-launch calibration
- `/ai-health-check` - Full pre-launch readiness audit
- `/ai-cost-check` - Economic validation

---

**Framework:** PM-Friendly Evals (Aman Khan + Hamel Husain)
**Key insight:** "Error analysis is the most important activity. Start with 20 cases in a spreadsheet."
