---
name: agency-ladder
description: Plan the v1→v2→v3 agency progression for AI features. Walk through mapping how autonomy increases over time, define promotion criteria, and generate artifacts for stakeholder alignment. Based on CC/CD framework.
---

# Agency Ladder - AI Autonomy Progression Planning

## Core Philosophy

**AI products earn autonomy. They don't start with it.**

Every increase in AI agency means surrendering human control. This tradeoff must be intentional, not accidental.

```
Low Agency ←──────────────────→ High Agency
(Human decides)              (AI decides)

High Control ←──────────────→ Low Control
(Predictable)                (Unpredictable)
```

**Key insight:** You're not ready to give high agency until you've thoroughly tested how the AI behaves at lower autonomy levels.

---

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AGENCY LADDER
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Every AI feature should earn autonomy, not start with it.

What are you working on?

  1. Planning a new AI feature
     → Build the ladder from scratch

  2. Reviewing an existing AI feature
     → Map current state, plan next level

  3. Deciding whether to increase agency
     → Promotion criteria check

  4. Workshop/conversation tool
     → Export ladder for stakeholder discussion

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Parse intent from context:**
- If user mentions "new feature" or "planning" → Flow 1
- If user mentions "existing" or "current" → Flow 2
- If user mentions "promote" or "increase" or "ready" → Flow 3
- If user mentions "stakeholder" or "present" or "export" → Flow 4

**Command-line shortcuts:**
- `/agency-ladder` → Show entry menu
- `/agency-ladder --review` → Flow 2 (existing feature)
- `/agency-ladder --promote` → Flow 3 (promotion check)
- `/agency-ladder --export` → Flow 4 (stakeholder artifact)

---

## Flow 1: Planning a New AI Feature

### Step 1: Understand the Feature

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STEP 1: UNDERSTAND THE FEATURE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Before mapping agency, let's understand what the AI is doing.

  • What task is the AI performing?
  • Who is the user?
  • What's the consequence of AI being wrong?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Questions to ask:**
- "What's the AI's job in one sentence?"
- "What's the worst thing that happens if the AI is wrong?"
- "How would a user currently do this without AI?"

### Step 2: Define V1 (Low Agency)

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STEP 2: DEFINE V1 (LOW AGENCY)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

V1 is where you start: AI suggests, human decides.

  • What's the minimum capability that tests your hypothesis?
  • How will users override when the AI is wrong?
  • What data will you collect to inform V2?

V1 Pattern: High Control, Low Agency
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**V1 questions:**
- "What's the simplest version where AI helps but human decides?"
- "What override mechanism exists?"
- "What are you testing with V1?"
- "How long will you run V1 before considering V2?"

### Step 3: Map V2 (Medium Agency)

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STEP 3: MAP V2 (MEDIUM AGENCY)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

V2 happens when V1 proves reliability.

  • What categories could AI handle autonomously?
  • What still needs human judgment?
  • What's the escalation path?

V2 Pattern: Medium Control, Medium Agency
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**V2 questions:**
- "What did you learn from V1 that enables V2?"
- "What confidence threshold triggers auto-action?"
- "What scenarios still need human review?"

### Step 4: Envision V3 (High Agency)

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STEP 4: ENVISION V3 (HIGH AGENCY)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

V3 is the end state: AI acts autonomously.

  • What does full autonomy look like?
  • What's the human's role at V3?
  • Is V3 even desirable for this feature?

V3 Pattern: Low Control, High Agency
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**V3 questions:**
- "What would it take to trust the AI completely?"
- "What's the human doing at V3? (spot-check, escalation only?)"
- "Should this feature ever reach V3?"

**Note:** Some features should never reach V3. That's a valid outcome.

### Step 5: Define Promotion Criteria

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 STEP 5: PROMOTION CRITERIA
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

What must be true to move from V(n) to V(n+1)?

  □ Quality metrics stable for how long?
  □ What user correction rate is acceptable?
  □ What error patterns must be resolved?
  □ What monitoring must be in place?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Promotion criteria categories:**
- **Quality:** Accuracy, success rate, user satisfaction
- **Safety:** Error patterns documented, failure modes understood
- **Operations:** Monitoring in place, rollback plan ready
- **Trust:** User corrections decreasing, feedback positive

### Output: Flywheel Table

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AGENCY LADDER COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# [Feature Name] - Agency Ladder

## Progression Overview

| Version | Capability | Control | Agency | What You're Testing |
|---------|------------|---------|--------|---------------------|
| V1 | [describe] | High | Low | [hypothesis] |
| V2 | [describe] | Medium | Medium | [hypothesis] |
| V3 | [describe] | Low | High | [hypothesis] |

## Flywheel

| Version | What You're Testing | What You Learn | What Feeds Next Loop |
|---------|---------------------|----------------|----------------------|
| V1 | [hypothesis] | [insights] | [data for V2] |
| V2 | [hypothesis] | [insights] | [data for V3] |
| V3 | [hypothesis] | [insights] | [calibration] |

## Control Handoffs

**Override mechanism:** [how users correct]
**Escalation path:** [when AI defers]
**Feedback capture:** [how corrections improve system]

## Promotion Criteria (V1→V2)

- [ ] [Metric 1] stable for [duration]
- [ ] [Metric 2] above [threshold]
- [ ] [Condition 3] resolved
- [ ] [Monitoring] in place

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

What next?

  1. Export to spec (/spec --ai)
  2. Set up post-launch calibration (/calibrate)
  3. Share with stakeholders
  4. Start building V1

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Flow 2: Reviewing an Existing AI Feature

### Step 1: Map Current State

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 MAPPING CURRENT STATE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Let's understand where this feature is today.

  • What's the AI currently doing?
  • How much human oversight exists?
  • What's working? What's failing?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Questions to determine current level:**
- "Does the AI act without human approval?" (If no → V1)
- "Does the AI handle some cases autonomously?" (If yes → V2)
- "Does the AI act autonomously most of the time?" (If yes → V3)

### Step 2: Identify Gaps

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 GAPS ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Based on the current state, here are potential gaps:

  □ Override mechanism exists?
  □ Quality metrics being tracked?
  □ Error patterns documented?
  □ Promotion criteria defined?
  □ Next level planned?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Output: Current State Assessment

Generate assessment showing:
- Current agency level (V1/V2/V3)
- What's working
- What's missing for CC/CD compliance
- Recommended next steps

---

## Flow 3: Promotion Check

### Promotion Criteria Checklist

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 PROMOTION CHECK: V[n] → V[n+1]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Let's see if this feature is ready for more autonomy.

QUALITY METRICS
  □ Accuracy/quality metrics stable for 4+ weeks?
  □ No new error patterns emerging?
  □ User corrections decreasing over time?

SAFETY & TRUST
  □ Confident in all known failure modes?
  □ Override mechanism working well?
  □ User feedback positive?

OPERATIONAL READINESS
  □ Monitoring in place for new agency level?
  □ Rollback plan if quality degrades?
  □ Team aligned on promotion decision?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Output: Promotion Assessment

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 PROMOTION ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Current Level: V[n]
Target Level: V[n+1]

VERDICT: [READY / NOT READY / NEEDS WORK]

✅ Passing:
- [criteria met]
- [criteria met]

❌ Blocking:
- [criteria not met]
- [criteria not met]

⚠️ Risks:
- [risk if promoted now]

RECOMMENDATION:
[Clear recommendation with reasoning]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Flow 4: Export for Stakeholder Discussion

Generate a presentation-ready artifact:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 AGENCY LADDER - [Feature Name]
 Stakeholder Discussion Document
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Why This Matters

AI products need a fundamentally different approach than
traditional software. We can't "ship and forget."

This document outlines how [feature] will earn autonomy
over time, with clear gates at each level.

## The Ladder

[Flywheel table from Flow 1]

## Current State

[Where we are today]

## Next Steps

[What we're asking stakeholders to approve]

## Risks & Mitigations

[Key risks at each level and how we address them]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Challenge Patterns

**"Let's just ship V3"**
→ "What happens when it fails? How do users recover? What failure modes are you willing to discover in production?"

**"Users will trust it"**
→ "How do you know? What's your evidence? Have you tested this with real users at lower agency?"

**"We'll figure out V2 later"**
→ "What must V1 prove to inform V2? If you don't know what you're testing, how will you know when to promote?"

**"It's just a small feature"**
→ "What's the consequence of AI being wrong? Even 'small' features can have significant trust implications."

---

## Integration with Other Commands

**Before /agency-ladder:**
- `/spec --ai` - Define what the AI is doing

**After /agency-ladder:**
- `/calibrate` - Post-launch calibration workflow
- `/ai-health-check` - Pre-launch validation

---

## Attribution

**Framework:** CC/CD (Continuous Calibration/Continuous Development)
**Source:** Aishwarya Naresh Reganti & Kiriti Badam (Lenny's Newsletter)
**Adaptation:** Agency ladder progression planning

---

## Remember

- Start with low agency, earn autonomy
- Each version tests a specific hypothesis
- Promotion requires proven reliability
- Some features should stay at V1 forever - that's valid
- Control handoffs must be designed, not assumed
