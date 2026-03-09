# PRD Framework

**Primary Source:** Aakash Gupta, Product Growth Newsletter
**Enhancements:** Modern AI-era best practices from leading tech companies (OpenAI, etc.)
**Context:** Modern approach to PRDs - shorter, more insightful, focused on quality over completeness, enhanced with AI-specific requirements and decision-forcing frameworks

## Core Philosophy

**PRDs are about decisions, not documentation.**

Modern PRDs are not 10-page documents. They're:
- **Shorter but more insightful**
- **Decision-focused** - Every section decides something
- **Specific, not generic** - "≥10%" not "improve"
- **Designed to excite teams** not just inform them
- **Living documents** that evolve through 5 stages
- **Works alongside AI prototyping** - When building fast becomes easy (thanks to AI), knowing what to build becomes even more important

## The 8/10 Rule

**Don't aim for 10/10** unless you have an exec review.

- 8/10 PRD: 1-2 days of work
- 10/10 PRD: 2+ weeks of work by senior PM

The Pareto principle applies. Get to 8/10 and ship. Reserve 10/10 for critical executive reviews.

## Modern Product Development Flow

**Old flow (linear):** PRD → Design → Build → Test

**New flow (cyclical):** Idea → Quick Prototype → PRD → Refined Prototype → Ship

### How PRDs and Prototypes Work Together

**Prototypes as discovery tools:**
- Use AI tools (Cursor, Replit, v0) to mock up 3 different approaches in an afternoon
- Each prototype teaches something about the problem space
- PRD captures learnings and sets direction

**PRDs as prototype constraints:**
- PRD provides guardrails for prototyping
- Answers: What edge cases? What metrics? How does this fit strategy?

**The feedback loop:**
- Iterate between prototypes and PRDs multiple times
- Each prototype informs the PRD
- Each PRD update guides the next prototype

## The 5 Stages of a PRD

### Stage 1: Planning
**Purpose:** Explore the problem space during planning cycle

**What to include:**
- **Problem:** Clearly defined user problem
- **Metrics:** Relevant data about this problem
- **Qualitative Evidence:** Customer quotes, user behaviors, anecdotes
- **Next Steps:** What else you need to know

**Output:** Speclet that documents the problem and why it matters

### Stage 2: Kickoff
**Purpose:** Move from problem to solution

**What to include:**
- **Potential Solution:** Wireframe or mock (even napkin sketch)
- **Success Metrics:** North-star, secondary, guardrail metrics
- **Impact Sizing:** Model out how this will move metrics

**The Middle Ground:**
PM should put together a napkin drawing, but design team should be willing to blow it up. This prevents both extremes: PM leaving everything to design OR PM constraining the solution space too much.

### Stage 3: Solution Review
**Purpose:** After solution exploration, lock in details

**What to include:**
- **Edge cases:** All the scenarios you now know about
- **Roll-out plan:** Experiment? Gradual? All at once?
- **Non-functional requirements:** Performance, security, etc.
- **Tracking requirements:** What telemetry eng needs to add
- **Go-to-market strategy:** How to make this successful
- **Risks and mitigation:** What could go wrong, how to prevent

**Reality Check:** 90% of teams don't really explore solution space. If that's you, you'll add these sections right after Stage 2. But if your team wrestles with the problem space, these details come after design exploration.

### Stage 4: Launch Readiness
**Purpose:** Final iteration before launch

**What happens:**
- Engineering reviews and comments extensively
- PM updates PRD based on eng feedback
- Team discovers edge cases they missed
- Final polish on everything

**Key:** This is about iteration, not adding new sections. Update content from Stage 3 based on what you learned.

### Stage 5: Impact Review
**Purpose:** Connect PRD to results

**What to include:**
- Link to results review document at top of PRD
- Anyone looking back knows what happened

**Why:** Future you (or others) will come back to understand why this was built. Having results linked makes that much easier.

## AI-Specific PRD Requirements

For AI/ML features, add these critical elements to your PRD:

### Behavior Contract with Examples (MANDATORY)
The defining characteristic of AI PRDs: **tons of concrete examples**

Include 15-25 labeled examples showing:
- **Good responses:** What the AI should do
- **Bad responses:** Common failure modes
- **Reject cases:** When AI should refuse/defer

**Format for each example:**
```
User Input: [specific query or scenario]
Good Response: [desired AI behavior]
Bad Response: [what to avoid]
Reject: [when to refuse]
```

**Reference model:** OpenAI's Model Spec is the gold standard - filled with concrete examples, not abstract principles.

### Principles and Instructions
- Clear guidelines for AI behavior
- Specific risks and how to avoid them
- Guardrails and safety measures

### Edge Cases and Red-Team List
- Adversarial inputs
- PII/sensitive data handling
- Performance degradation scenarios
- Code snippets, special characters, multi-language inputs

### Validation Mechanisms
- **Offline Golden Set:** Test data for validation
- **Human Review Rubric:** Qualitative checks with specific criteria
- **Online Metrics:** Specific KPIs with thresholds (not "improve X")

### Safety and Fallbacks
- **Detection:** How to spot failures
- **Fallback & Kill Switch:** Recovery mechanisms with owners
- **Legal/Security Review:** PII handling, compliance requirements

## Quality Content Over Completeness

### What Makes Content "Quality"?

**User Evidence:**
- ❌ "Users want faster email composition"
- ✅ "From 15 interviews, 87% said 'writing takes too long.' 60% already use ChatGPT separately. Quote: 'I rewrite the same emails 10x.'"

**Impact Sizing:**
- ❌ "This will improve engagement"
- ✅ "If we reduce composition time 50% (8min → 4min), we estimate 20% increase in emails sent. Addressable: 10K users. Target: 3K adoption Q1."

**Competition:**
- ❌ "Competitors exist"
- ✅ "Grammarly has AI writing but not email-specific. Superhuman is fast but no AI. Gap: No one has great AI composition inside email client."

**Metrics:**
- ❌ "Track engagement and usage"
- ✅ "North-star: Email composition time. Secondary: Emails sent/day. Guardrails: Email quality (response rate), manual editing time, AI cost/email"

## The Checklist Approach

Instead of rigid templates, use checklists by stage:

### Planning Checklist
- [ ] Problem clearly defined
- [ ] Current state documented
- [ ] Metrics identified
- [ ] Qualitative evidence included
- [ ] Competition surveyed
- [ ] User insight identified
- [ ] Next steps outlined

### Kickoff Checklist
- [ ] Potential solution outlined
- [ ] Metrics to measure defined
- [ ] Impact sizing model created
- [ ] Counter metrics identified

### Solution Review Checklist
- [ ] Edge cases identified
- [ ] Roll-out plan defined
- [ ] XFN requirements outlined
- [ ] Tracking requirements specified
- [ ] GTM strategy outlined
- [ ] Risks and mitigations documented

### Launch Readiness Checklist
- [ ] Eng concerns addressed
- [ ] Design complete
- [ ] Estimated and tasked
- [ ] GTM teams enabled
- [ ] Test plan ready
- [ ] Corner cases handled

### Impact Review Checklist
- [ ] Results linked
- [ ] Stats validated
- [ ] Continuous monitoring defined
- [ ] Improvements identified

## Common Mistakes

### 1. No Impact Sizing
Don't just say "this will improve engagement." Model it out:
- How many users are addressable?
- What adoption rate do you expect?
- How will this move input metrics?
- How does that translate to output metrics?

### 2. Weak User Evidence
Including a link to a research doc ≠ user evidence. Pull the most salient quotes and findings directly into the PRD.

### 3. Missing Counter Metrics
Features rarely have only upside. If users do X, they're not doing Y. Measure the tradeoffs.

### 4. Excessive Delegation
"Design will figure out the UX" is abdicating product thinking. Create a mock (even rough) to ensure you've thought through the edge cases.

### 5. Looking Complete But Being Vacuous
Having every section filled out means nothing if the content is generic. "Ensure legal compliance" is not a legal requirement. "@Legal to confirm details on GDPR for email AI" is.

## Critical Antipatterns

### Antipattern 1: Prose Without Decisions
**Symptom:** Long paragraphs explaining context with no actionable outcomes

**Fix:** Every paragraph should end with a decision or a specific example

### Antipattern 2: Metric Theater
**Symptom:** "Improve engagement", "Increase satisfaction", "Reduce costs"

**Fix:** "P50 engagement time increases ≥15%", "NPS increases from 42 to 48+", "Server costs decrease $12K/month"

### Antipattern 3: Implementation Fantasy
**Symptom:** "Start small, then ramp" or "Three-phase approach"

**Fix:** "Week 1: 5% US users, Week 2: Graduate if p<0.05 and +10% metric, Week 3: Scale to 25%"

### Antipattern 4: Vibe-Based Behavior (for AI features)
**Symptom:** "Generate helpful replies" or "Provide good recommendations"

**Fix:** 25 labeled examples showing good/bad/reject cases with specific inputs and outputs

### Antipattern 5: One-and-Done Documentation
**Symptom:** PRD written once, never updated, gathering dust

**Fix:** Update PRD at each stage, link to results, annex learnings from production

## What Makes an 8/10 vs 10/10?

### 8/10 PRD includes:
- Market data and user quotes
- Clear metrics and success criteria
- Wireframe or mock
- Impact sizing model
- Risk assessment
- Go-to-market plan

**Time:** 1-2 days

### 10/10 PRD adds:
- Company-specific internal data
- Detailed financial model
- Working prototype
- Solution testing (usability tests on prototype)
- Feature-level metrics tied to company revenue model

**Time:** 2+ weeks by experienced PM

### When to go for 10/10:
- Exec review presentation
- Major product bet (top 3 priorities for quarter)
- Entering new market
- High-risk / high-investment feature

### When 8/10 is perfect:
- Standard features on roadmap
- Iterative improvements
- Validated problem space
- Experienced product trio

## Practical Tips

**Start with User Evidence:**
Begin your PRD with the most compelling user quote or data point. Get people excited from sentence one.

**Remix Templates, Don't Follow Them:**
If your company has a template, use 80% of it and add 20% specific to your feature. Remove sections that don't apply.

**Just Start Writing:**
Don't overthink it. The PRD builds up over stages. Start with what you know in Stage 1, add more in Stage 2, etc.

**CRITICAL: Don't Use LLMs for First Drafts**

**Why:** LLMs create verbose, decision-free documentation that says nothing. You'll get generic prose that looks complete but is vacuous.

**Instead:**
- Write the first draft yourself with clear decisions
- Use LLM as copilot to improve and finesse
- Think of AI as teammate, not ghostwriter
- You make the decisions, AI helps you communicate them better

**Quality Check:**
Before finalizing, ask:
- Would this excite me to build?
- Is the user evidence specific and compelling?
- Does the impact sizing feel credible?
- Have I identified what might go down (counter metrics)?
- Does every section make a decision (not just describe)?

## References

**Primary Framework:**
- [PRDs: A Modern Guide](https://www.productgrowth.com/p/product-requirements-documents) - Aakash Gupta
- Includes 2 example PRDs (6/10 and 8/10) with detailed critique

**AI-Specific Enhancements:**
- OpenAI Model Spec - Gold standard for AI behavior specification with concrete examples
- Modern AI-era PRD practices from leading tech companies
- Decision-forcing frameworks and antipatterns
- AI prototyping integration (Cursor, Replit, v0)

---

**Best for:** Feature planning, team alignment, reducing ambiguity
**When to use:** Any feature you want to measure results for
**Anti-pattern:** Creating 10-page documents no one reads
**Modern approach:** Shorter, more insightful, quality over completeness, decisions over documentation
