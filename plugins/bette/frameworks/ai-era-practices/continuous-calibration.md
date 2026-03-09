# Continuous Calibration (CC/CD) for AI Products

**Category:** AI-Era Practices
**Source:** Adapted from Lenny's Newsletter and AI product best practices
**Last Updated:** January 2025

## Overview

AI products need a fundamentally different development approach than traditional software. While traditional products use CI/CD (Continuous Integration/Continuous Deployment), AI products need CC/CD: **Continuous Calibration/Continuous Development**.

**The core difference:**
- **Traditional software:** Deterministic → Test once → Deploy → Works predictably
- **AI systems:** Non-deterministic → Need ongoing calibration → Deploy → Monitor → Adjust

## The Calibration Paradox

**You can't calibrate without shipping.**

**The mistake:** Building elaborate systems to perfectly calibrate AI behavior before launch.

**The reality:** You learn what quality means by shipping to users and seeing what they actually need.

**The approach:**
1. **Ship with low agency** (AI suggests, human decides)
2. **Learn from real usage** (what do users correct? what breaks?)
3. **Calibrate based on data** (adjust prompts, context, constraints)
4. **Increase agency gradually** (earn autonomy by proving reliability)
5. **Repeat continuously** (calibration never ends)

**Key insight:** Calibration happens through iteration with real users, not through pre-launch perfection.

## Why AI is Different

### Non-Determinism on Both Ends

**Input side:**
- Users interact through open-ended prompts, not buttons
- Infinite variations of how to ask the same thing
- Context matters enormously

**Output side:**
- AI responses vary even with identical inputs
- Quality fluctuates based on context, phrasing, edge cases
- "Correct" is often subjective

**Result:** You can't test once and assume it works forever.

### The Agency vs. Control Tradeoff

**Core tension:** Every increase in AI autonomy means surrendering human control.

```
Low Agency ←──────────────────→ High Agency
(Human decides)              (AI decides)

High Control ←──────────────→ Low Control
(Predictable)                (Unpredictable)
```

**Key insight:** "Every time you give an AI system more agency, you give up some control."

This requires intentional calibration, not just deployment.

## The CC/CD Framework

### Continuous Calibration

**Definition:** Ongoing adjustment of AI system behavior based on real-world performance.

**Not:**
- One-time tuning
- Set-and-forget deployment
- Traditional QA testing

**Instead:**
- Continuous monitoring
- Regular evaluation
- Iterative improvement
- Live performance tracking

### How It Works

**1. Start with Low Agency**

Don't launch with maximum autonomy.

```
Version 1: High Control, Low Agency
- AI suggests, human decides
- Human can override everything
- System learns from corrections

Version 2: Medium Control, Medium Agency
- AI decides simple cases, escalates complex ones
- Human oversight on important decisions
- Confidence thresholds determine autonomy

Version 3: Low Control, High Agency
- AI handles most decisions autonomously
- Human spot-checks and intervenes
- Only after proving reliability at lower levels
```

**Quote:** "You're not ready to give it high agency until you've thoroughly tested how it behaves when it fails at lower autonomy levels."

**2. Implement Evals at Each Level**

Before increasing agency:
- **Measure:** Success rate, error types, edge cases
- **Evaluate:** Quality, appropriateness, safety
- **Test:** Failure modes, hallucinations, bias

**See:** `/frameworks/ai/ai-evals.md` for comprehensive eval strategies

**3. Design Control Handoffs**

**Critical:** Users must be able to override the AI when it's wrong.

**Good handoff design:**
- "AI suggested X. Accept or edit?"
- Clear indication of AI confidence level
- Easy path to human override
- Learn from corrections

**Bad handoff design:**
- AI acts without confirmation
- No way to correct mistakes
- User doesn't know AI made the decision
- No feedback loop

**4. Monitor in Production**

**Track:**
- User satisfaction with AI outputs
- Correction/override rates
- Error patterns
- Quality degradation over time

**Alert on:**
- Sudden drops in quality
- Increased error rates
- New failure modes
- User frustration signals

**5. Calibrate Based on Data**

**Weekly/monthly:**
- Analyze production performance
- Identify new failure modes
- Add to eval dataset
- Retrain or adjust prompts
- Test before deploying changes

## Capability Versioning

**Traditional software versioning:** v1.0, v1.1, v2.0 (based on features)

**AI product versioning:** Should be based on **agency levels**, not just features.

**Example: AI Customer Support Bot**

**v1.0: Suggestion Mode (Low Agency)**
```
Capability:
- AI drafts responses
- Human reviews and edits before sending
- Human always decides

Control Level: High
Agency Level: Low
```

**v1.5: Assisted Mode (Medium Agency)**
```
Capability:
- AI handles simple questions automatically
- Escalates complex questions to human
- Human sets confidence thresholds

Control Level: Medium
Agency Level: Medium
```

**v2.0: Autonomous Mode (High Agency)**
```
Capability:
- AI handles most questions end-to-end
- Human spot-checks sample
- Only escalates true edge cases

Control Level: Low
Agency Level: High
```

**Key:** Don't skip from v1.0 to v2.0. Earn autonomy through proven reliability.

## The Calibration Loop

```
┌─────────────────────────────────────┐
│ 1. Deploy at Current Agency Level  │
└────────────┬────────────────────────┘
             │
┌────────────▼────────────────────────┐
│ 2. Monitor Performance in Prod     │
│    - Quality metrics               │
│    - User feedback                 │
│    - Error patterns                │
└────────────┬────────────────────────┘
             │
┌────────────▼────────────────────────┐
│ 3. Analyze & Learn                 │
│    - What's working?               │
│    - What's breaking?              │
│    - New edge cases?               │
└────────────┬────────────────────────┘
             │
┌────────────▼────────────────────────┐
│ 4. Calibrate System                │
│    - Update prompts                │
│    - Adjust thresholds             │
│    - Add guardrails                │
│    - Retrain if needed             │
└────────────┬────────────────────────┘
             │
┌────────────▼────────────────────────┐
│ 5. Test in Staging                 │
│    - Run evals                     │
│    - Validate improvements         │
│    - Check for regressions         │
└────────────┬────────────────────────┘
             │
┌────────────▼────────────────────────┐
│ 6. Consider Agency Increase        │
│    - Metrics improved?             │
│    - Ready for more autonomy?      │
│    - Or stay at current level?     │
└────────────┬────────────────────────┘
             │
             └──────────────┐
                           │
                    (Repeat continuously)
```

## Real-World Example

**Product:** AI-powered code review assistant

**Phase 1: Low Agency (Suggestion Mode)**

**Capability:**
- AI analyzes pull requests
- Suggests potential issues
- Developer reviews all suggestions
- Developer decides what to fix

**Metrics:**
- Suggestion accuracy: 70%
- False positive rate: 30%
- Developer adoption: 40% of suggestions acted on

**Learning:**
- AI over-flags style issues (low value)
- Misses some security vulnerabilities
- Developers ignore CSS suggestions

**Calibration:**
- Reduce style issue alerts
- Improve security rule prompts
- Focus on logic and security, not style

**Phase 2: Medium Agency (Assisted Mode)**

**Capability:**
- AI auto-comments on high-confidence issues
- Suggests fixes for medium-confidence issues
- Escalates low-confidence to developer review

**New metrics:**
- Auto-comment accuracy: 85%
- False positive rate: 15%
- Developer override rate: 10%

**Learning:**
- High-confidence security flags accurate
- Medium-confidence logic issues need improvement
- Some contextual false positives

**Calibration:**
- Tighten security rules
- Add context-awareness for logic checks
- Create escalation path for edge cases

**Phase 3: High Agency (Autonomous Mode)**

**Capability:**
- AI blocks PRs with security issues automatically
- Auto-fixes simple issues
- Logs all decisions for spot-checking

**Metrics:**
- Block accuracy: 95%
- Auto-fix success rate: 90%
- Developer complaints: <5%

**Only reached this phase after:**
- 6 months at low agency
- 4 months at medium agency
- Proven reliability at each level
- Strong eval performance

## Continuous Calibration Best Practices

### 1. Version Your Prompts

Track every prompt change like code:
```
v1.0: Initial prompt
v1.1: Added example for edge case X
v1.2: Reduced hallucinations in domain Y
v1.3: Improved tone for audience Z
```

**Why:** You need to A/B test and rollback if quality degrades.

### 2. Build a Golden Dataset

**Collect:**
- Known good responses
- Known failure cases
- Edge cases discovered in production
- Representative samples of all scenarios

**Use for:**
- Regression testing after changes
- Baseline performance measurement
- Training new team members
- Validating before agency increases

### 3. Monitor User Corrections

**Track when users:**
- Override AI decisions
- Edit AI outputs
- Reject AI suggestions
- Flag errors

**Learn:**
- What patterns does AI miss?
- Where is confidence miscalibrated?
- What new failure modes emerge?

**Apply:**
- Add to eval dataset
- Improve prompts
- Adjust thresholds

### 4. Set Quality Floors

**Define minimum acceptable:**
- Accuracy rate
- User satisfaction
- Error rate
- Hallucination rate

**Auto-alert when quality drops below threshold.**

**Action:** Roll back recent changes, investigate, fix before re-deploying.

### 5. Gradual Rollouts

**Don't deploy to 100% immediately:**

```
Day 1: 5% of traffic
Day 3: 10% (if quality holds)
Day 7: 25%
Day 14: 50%
Day 21: 100%
```

**Monitor at each step.** Roll back if quality degrades.

## Integration with Other Frameworks

### Teresa Torres' Continuous Discovery

**Discovery informs calibration:**
- Weekly user interviews reveal AI failure modes
- Opportunity solution trees include calibration improvements
- Discovery validates agency level appropriateness

### Aman Khan's AI Evals

**Evals enable calibration:**
- Define success criteria
- Measure current performance
- Test improvements before deploying
- Regression test after changes

### Prototype-First Development

**Prototype different agency levels:**
- Build low-agency version first
- Test with users
- Iterate toward higher agency
- Validate before production

### Four Risks (Marty Cagan)

**New AI-specific risks:**
- **Value:** Will users trust AI outputs?
- **Usability:** Can users override when AI is wrong?
- **Feasibility:** Can we maintain quality at scale?
- **Viability:** Can we afford inference costs + calibration overhead?

## Common Mistakes

❌ **Launching with high agency immediately**
- Users don't trust it
- Failure modes undiscovered
- No path to rollback gracefully

❌ **Set-and-forget after launch**
- AI quality degrades over time
- New edge cases emerge
- User needs evolve

❌ **No override mechanism**
- Users stuck with bad AI outputs
- Frustration builds
- No feedback loop to improve

❌ **Ignoring user corrections**
- Richest signal for improvement
- Shows where AI fails
- Reveals calibration opportunities

❌ **Increasing agency too fast**
- Skip learning at lower levels
- Miss failure modes
- Lose user trust when it breaks

## Questions to Ask

### Before launch:
- "What agency level are we starting at?"
- "How will users override the AI?"
- "What evals prove we're ready?"
- "What quality metrics determine success?"

### During operation:
- "Is quality stable or degrading?"
- "What new failure modes have emerged?"
- "Are users overriding frequently? Why?"
- "Should we increase or decrease agency?"

### When considering agency increase:
- "Have we proven reliability at current level?"
- "Do evals show consistent quality?"
- "Are users ready for more autonomy?"
- "What new risks does higher agency introduce?"

## Key Takeaways

1. **Start with low agency** - AI suggests, human decides
2. **Earn autonomy** - Prove reliability before increasing agency
3. **Design control handoffs** - Users must be able to override
4. **Monitor continuously** - AI quality changes over time
5. **Calibrate based on data** - Use prod feedback to improve
6. **Version by capability** - Track agency level, not just features
7. **Build eval infrastructure** - Test before deploying changes
8. **Learn from corrections** - User overrides show where to improve

## Operationalizing CC/CD

Use these commands to embed CC/CD in your workflow:

### Before Building

**`/spec --ai`** - Spec AI features with CC/CD thinking built in
- Agency Progression Plan (v1→v2→v3)
- Control Handoffs (override, escalation, feedback)
- Reference Dataset (golden examples before building)

**`/agency-ladder`** - Plan the autonomy progression
- Map v1→v2→v3 for any AI feature
- Define promotion criteria upfront
- Export for stakeholder alignment

### After Launch

**`/calibrate`** - Post-launch calibration workflow
- Document error patterns
- Review eval performance
- Make agency promotion decisions
- Quick health checks

### Related Commands

- `/ai-health-check` - Pre-launch readiness validation
- `/start-evals` - Set up evaluation infrastructure
- `/ai-cost-check` - Model unit economics

---

## Resources

**Conceptual:**
- Lenny's Newsletter: "Why your AI product needs a different approach"
- Continuous Calibration principles
- Agency vs. Control tradeoff

**Tactical:**
- Aman Khan: AI Evals framework (`/frameworks/ai/ai-evals.md`)
- Golden dataset creation
- Production monitoring strategies

**Source:**
- Aishwarya Naresh Reganti & Kiriti Badam: "Why your AI product needs a different development lifecycle" (Lenny's Newsletter, August 2025)

**Related:**
- CI/CD → CC/CD evolution
- Non-deterministic systems management
- Human-AI collaboration patterns

---

**Remember:** AI products aren't "ship and forget." They require ongoing calibration.

Start with low agency. Monitor continuously. Earn autonomy through proven reliability. Design for human override. Calibrate based on real-world performance.

CC/CD > CI/CD for AI products.
