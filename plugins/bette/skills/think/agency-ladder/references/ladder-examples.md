# Agency Ladder Examples

Reference examples for different types of AI features.

---

## Example 1: AI Customer Support Bot

### The Ladder

| Version | Capability | Control | Agency | What You're Testing |
|---------|------------|---------|--------|---------------------|
| V1 | AI drafts responses, human reviews before sending | High | Low | Response quality, tone accuracy |
| V2 | AI handles simple questions automatically, escalates complex | Medium | Medium | Auto-response accuracy, escalation judgment |
| V3 | AI handles most questions end-to-end | Low | High | Long-term quality stability |

### Flywheel

| Version | What You're Testing | What You Learn | What Feeds Next Loop |
|---------|---------------------|----------------|----------------------|
| V1 | Can AI draft helpful responses? | Common question patterns, tone issues | Categories safe for auto-response |
| V2 | Can AI handle routine questions? | Escalation accuracy, confidence calibration | Edge cases requiring human |
| V3 | Can AI maintain quality at scale? | Quality consistency, new edge cases | Ongoing calibration |

### Promotion Criteria V1→V2

- [ ] Auto-response accuracy >85% over 4 weeks
- [ ] Customer satisfaction maintained
- [ ] No critical errors in review sample
- [ ] Confidence thresholds calibrated

---

## Example 2: AI Code Review Assistant

### The Ladder

| Version | Capability | Control | Agency | What You're Testing |
|---------|------------|---------|--------|---------------------|
| V1 | AI suggests potential issues, dev reviews all | High | Low | Detection accuracy, false positive rate |
| V2 | AI auto-comments on high-confidence issues | Medium | Medium | Comment quality, dev sentiment |
| V3 | AI blocks PRs with security issues | Low | High | Block accuracy, trust level |

### Flywheel

| Version | What You're Testing | What You Learn | What Feeds Next Loop |
|---------|---------------------|----------------|----------------------|
| V1 | Can AI find real issues? | True vs false positives, dev preferences | Categories safe for auto-comment |
| V2 | Are auto-comments helpful? | Developer workflow impact, dismiss patterns | When blocking is acceptable |
| V3 | Can AI be a gatekeeper? | Trust at scale, edge case discovery | Continuous calibration |

### Promotion Criteria V1→V2

- [ ] True positive rate >80%
- [ ] Developer action rate >50%
- [ ] Zero security issues missed
- [ ] Developer feedback positive

---

## Example 3: AI Content Writer

### The Ladder

| Version | Capability | Control | Agency | What You're Testing |
|---------|------------|---------|--------|---------------------|
| V1 | AI generates first draft, human edits substantially | High | Low | Draft usefulness, voice alignment |
| V2 | AI generates near-final content, human edits lightly | Medium | Medium | Publish-readiness, factual accuracy |
| V3 | AI generates and publishes with minimal review | Low | High | Quality consistency, brand safety |

### Flywheel

| Version | What You're Testing | What You Learn | What Feeds Next Loop |
|---------|---------------------|----------------|----------------------|
| V1 | Does AI save time vs blank page? | Common edits, voice issues | Templates and guidelines |
| V2 | Is output publishable? | Quality distribution, outliers | Confidence for auto-publish |
| V3 | Can AI own the content pipeline? | Scale effects, audience response | Ongoing calibration |

### Promotion Criteria V1→V2

- [ ] Edit rate <30% of content
- [ ] Factual accuracy >95%
- [ ] Voice consistency score >80%
- [ ] Editor feedback positive

---

## Example 4: AI Recommendation Engine (E-commerce)

### The Ladder

| Version | Capability | Control | Agency | What You're Testing |
|---------|------------|---------|--------|---------------------|
| V1 | AI shows "You might also like" suggestions | High | Low | Click-through rate, relevance |
| V2 | AI personalizes homepage layout | Medium | Medium | Engagement lift, user satisfaction |
| V3 | AI controls entire shopping experience | Low | High | Revenue impact, long-term retention |

### Flywheel

| Version | What You're Testing | What You Learn | What Feeds Next Loop |
|---------|---------------------|----------------|----------------------|
| V1 | Are recommendations relevant? | User preference signals | Personalization depth |
| V2 | Does personalization increase engagement? | Optimal layout patterns | Full experience ownership |
| V3 | Can AI drive business outcomes? | Revenue correlation, user segments | Continuous optimization |

### Important Note

**V3 may not be desirable.** Some users prefer control over their experience. Consider whether full AI ownership aligns with user expectations.

---

## Example 5: AI Scheduling Assistant

### The Ladder

| Version | Capability | Control | Agency | What You're Testing |
|---------|------------|---------|--------|---------------------|
| V1 | AI suggests meeting times, user confirms | High | Low | Availability accuracy, preference learning |
| V2 | AI sends invites with user's standing approval | Medium | Medium | Booking accuracy, conflict handling |
| V3 | AI manages calendar autonomously | Low | High | Trust level, boundary respect |

### Flywheel

| Version | What You're Testing | What You Learn | What Feeds Next Loop |
|---------|---------------------|----------------|----------------------|
| V1 | Does AI understand my schedule? | Preference patterns, edge cases | Auto-booking rules |
| V2 | Can AI book on my behalf? | Conflict resolution, guest preferences | Full calendar ownership |
| V3 | Can AI manage my time? | Work-life boundaries, priority learning | Ongoing calibration |

### Promotion Criteria V1→V2

- [ ] Suggestion acceptance >80%
- [ ] No double-bookings for 4 weeks
- [ ] User explicitly opts into auto-booking
- [ ] Clear override mechanism in place

---

## Example 6: AI Financial Advisor

### The Ladder

| Version | Capability | Control | Agency | What You're Testing |
|---------|------------|---------|--------|---------------------|
| V1 | AI explains options, user decides everything | High | Low | Advice quality, comprehension |
| V2 | AI suggests actions, user approves | High | Low | Recommendation accuracy, trust |
| V3 | AI executes approved strategies | Medium | Medium | Execution quality, risk management |

### Important Note

**High-stakes domains may never reach traditional V3.** For financial, medical, and legal applications, human approval loops may be required by regulation or prudent practice.

---

## Anti-Patterns

### Anti-Pattern 1: No V1

**Problem:** Team ships V3 directly ("Let's just automate it")

**Result:**
- Failure modes undiscovered
- Users don't trust the system
- No data to calibrate
- Difficult to diagnose issues

**Fix:** Always start with V1, even if brief

### Anti-Pattern 2: Infinite V1

**Problem:** Feature stays at V1 forever ("We'll promote later")

**Result:**
- Never learn if higher agency is viable
- Miss opportunity to reduce human workload
- Competitors move ahead

**Fix:** Define promotion criteria upfront, set timeline for evaluation

### Anti-Pattern 3: Forced V3

**Problem:** Business pressure to skip V2 ("We need it to scale")

**Result:**
- Quality issues at scale
- User trust erosion
- Expensive rollback

**Fix:** Frame V1/V2 as risk mitigation, not delay

---

## Key Principles

1. **Start where users are comfortable** - Don't force autonomy

2. **Each version has a hypothesis** - Know what you're testing

3. **Promotion is earned** - Data must support the move

4. **V3 isn't always the goal** - Some features should stay at V1/V2

5. **Control handoffs are product decisions** - Design them deliberately
