---
name: calibrate
description: Post-launch AI feature calibration workflow. Document error patterns, review eval performance, and decide on agency promotion. Based on CC/CD framework for continuous calibration of AI products.
---

# Calibrate - Post-Launch AI Feature Calibration

## Core Philosophy

**Calibration happens after launch, not before.**

The mistake: Building elaborate systems to perfectly calibrate AI behavior before launch.
The reality: You learn what quality means by shipping to users and seeing what they actually need.

**The Calibration Loop:**
1. Deploy at current agency level
2. Monitor performance in prod
3. Analyze and learn
4. Calibrate system
5. Test changes
6. Consider agency increase
7. Repeat

---

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CALIBRATE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Calibration happens after launch, not before.

What do you need?

  1. Document error patterns
     → Analyze failures, categorize, plan fixes

  2. Review eval performance
     → Are evals catching real issues? Missing patterns?

  3. Agency promotion decision
     → Is this feature ready for more autonomy?

  4. Quick calibration check
     → Is the system behaving as expected?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Parse intent from context:**
- If user mentions "errors" or "failures" or "bugs" → Flow 1
- If user mentions "evals" or "tests" or "coverage" → Flow 2
- If user mentions "promote" or "increase" or "V2" → Flow 3
- If user mentions "check" or "status" or "quick" → Flow 4

**Command-line shortcuts:**
- `/calibrate` → Show entry menu
- `/calibrate --errors` → Flow 1 (error patterns)
- `/calibrate --evals` → Flow 2 (eval review)
- `/calibrate --promote` → Flow 3 (agency promotion)
- `/calibrate --quick` → Flow 4 (quick check)

---

## Flow 1: Document Error Patterns

### Step 1: Gather Error Data

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ERROR PATTERN DOCUMENTATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Let's catalog what's going wrong.

Where are you seeing errors?
  • User feedback / complaints
  • Support tickets
  • Monitoring alerts
  • Manual review
  • User corrections / overrides

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Questions to ask:**
- "What specific failures have you observed?"
- "How often does this happen? (rare, occasional, frequent)"
- "What's the impact when it fails?"
- "Are there patterns in WHEN it fails?"

### Step 2: Categorize Errors

Categories must emerge from the errors you actually observe — not from a pre-defined list. Read the failures first, then group similar ones together. Pre-defined categories cause confirmation bias.

For the systematic process (reading traces, emergent categorization, failure rates), run `/upgrade-evals`. Flow 1 here is for quick ad-hoc error documentation when you don't need the full analysis.

### Step 3: Analyze Root Causes

For each error pattern, determine:
- **Likely reason:** Why is this happening?
- **Potential fix:** Prompt change? Context? Guardrail? Training data?
- **Priority:** P1 (critical), P2 (important), P3 (nice to fix)

### Output: Error Pattern Table

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ERROR PATTERN ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Analysis Date: [date]
Data Source: [where errors were observed]

| Error Pattern | Category | Likely Reason | Potential Fix | Priority |
|---------------|----------|---------------|---------------|----------|
| [description] | [type] | [why] | [how to fix] | P1 |
| [description] | [type] | [why] | [how to fix] | P2 |
| [description] | [type] | [why] | [how to fix] | P3 |

PATTERN ANALYSIS:
- Most common category: [X]
- Emerging pattern: [Y]
- Regression from last period: [Z]

RECOMMENDED ACTIONS:
1. [P1 action]
2. [P2 action]
3. [P3 action]

ADD TO EVALS:
- [ ] Add test case for [error pattern 1]
- [ ] Add test case for [error pattern 2]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Flow 2: Review Eval Performance

### Step 1: Current Eval State

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 EVAL PERFORMANCE REVIEW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Let's see if your evals are working.

Current state:
  • How many test cases do you have?
  • What's your pass rate?
  • When did you last update evals?
  • Are you seeing failures in prod that evals missed?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Questions to ask:**
- "Are current evals catching real issues?"
- "What new patterns have emerged since launch?"
- "Are you passing 100%?" (If yes, evals may be too easy)
- "How often do you run evals?"

### Step 2: Gap Analysis

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 EVAL GAP ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Check coverage across categories:

  □ Happy path - Common successful scenarios
  □ Edge cases - Unusual but valid inputs
  □ Adversarial - Intentional misuse attempts
  □ Boundary - Out of scope handling
  □ Regression - Previously fixed issues
  □ Production errors - Real failures observed

Missing categories = gaps in coverage
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Output: Eval Assessment

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 EVAL ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Test Cases: [count]
Pass Rate: [%]
Last Updated: [date]

COVERAGE ASSESSMENT:
| Category | Coverage | Status |
|----------|----------|--------|
| Happy path | [X] cases | ✅ Good |
| Edge cases | [X] cases | ⚠️ Needs work |
| Adversarial | [X] cases | ❌ Missing |
| Boundary | [X] cases | ✅ Good |
| Regression | [X] cases | ⚠️ Needs work |

EFFECTIVENESS:
- Catching real issues? [Yes/No/Partially]
- False positive rate: [%]
- Prod errors missed: [list]

RECOMMENDATIONS:
1. Add [X] test cases for [gap]
2. Update [Y] tests that are stale
3. Remove [Z] tests that are redundant

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Flow 3: Agency Promotion Decision

### Promotion Checklist

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AGENCY PROMOTION CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Considering: V[current] → V[target]

Let's verify readiness.

QUALITY METRICS
  □ Accuracy/quality stable for 4+ weeks?
  □ No new error patterns emerging?
  □ User corrections decreasing?

SAFETY & TRUST
  □ Confident in known failure modes?
  □ Override mechanism working well?
  □ User feedback positive?

OPERATIONAL READINESS
  □ Monitoring in place for new level?
  □ Rollback plan ready?
  □ Team aligned on promotion?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**For each item, ask:**
- "What's your evidence?"
- "How long have you observed this?"
- "What would change your answer?"

### Output: Promotion Verdict

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 PROMOTION VERDICT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Current: V[n] | Target: V[n+1]

VERDICT: [READY ✅ / NOT READY ❌ / NEEDS WORK ⚠️]

✅ PASSING:
- [criteria met with evidence]
- [criteria met with evidence]

❌ BLOCKING:
- [criteria not met + what's needed]
- [criteria not met + what's needed]

⚠️ RISKS IF PROMOTED NOW:
- [risk + mitigation needed]

RECOMMENDATION:
[Clear recommendation with reasoning]

NEXT STEPS:
1. [action if ready]
2. [action if not ready]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Flow 4: Quick Calibration Check

### Health Check

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 QUICK CALIBRATION CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Fast health check for [feature name]

  • Current quality metric: [X%]
  • Trend: [↑ improving / → stable / ↓ degrading]
  • Any alerts triggered? [Y/N]
  • User feedback signals: [positive/neutral/negative]
  • Override rate: [X%] (is this expected?)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Output: Health Status

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 CALIBRATION STATUS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Agency Level: V[n]
Check Date: [date]

STATUS: [HEALTHY ✅ / ATTENTION ⚠️ / DEGRADED ❌]

METRICS:
| Metric | Value | Trend | Status |
|--------|-------|-------|--------|
| Quality | [X%] | [→] | ✅ |
| Override rate | [X%] | [↓] | ✅ |
| User satisfaction | [X] | [→] | ⚠️ |

ALERTS:
- [any triggered alerts]

ACTION NEEDED:
- [none / specific action]

NEXT CHECK: [recommended cadence]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Calibration Cadence

**Weekly:** Quick check (Flow 4)
- Is quality stable?
- Any new alerts?
- User feedback signals?

**Monthly:** Eval review (Flow 2)
- Are evals catching real issues?
- New patterns to add?
- Stale tests to update?

**Quarterly:** Deep calibration
- Error pattern analysis (Flow 1)
- Agency promotion consideration (Flow 3)
- Strategic calibration review

---

## Challenge Patterns

**"Quality looks fine"**
→ "What's your correction rate? What's the trend? Fine compared to what baseline?"

**"No complaints"**
→ "Are users actually using it? Are they silently working around it?"

**"Ready to promote"**
→ "Show me the data. How long has quality been stable? What failure modes have you validated?"

**"Evals are passing"**
→ "100% pass rate? That might mean evals are too easy. When did you last add new test cases?"

---

## Integration with Other Commands

**Before /calibrate:**
- `/agency-ladder` - Define the ladder first
- `/spec --ai` - Ensure spec includes calibration plan

**Related:**
- `/ai-health-check` - Pre-launch validation
- `/start-evals` - Set up eval infrastructure
- `/upgrade-evals` - Systematic error analysis on real traces
- `/build-judge` - LLM-as-Judge for automating subjective evals
- `/eval-rag` - RAG-specific retrieval + generation evaluation

---

## Attribution

**Framework:** CC/CD (Continuous Calibration/Continuous Development)
**Source:** Aishwarya Naresh Reganti & Kiriti Badam (Lenny's Newsletter)
**Adaptation:** Post-launch calibration workflows

---

## Remember

- Calibration is continuous, not one-time
- Error patterns are the richest signal
- User corrections show where AI fails
- Evals must evolve with the product
- Promotion requires proven reliability
- 100% pass rate means evals are too easy
