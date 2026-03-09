# Real PRD Transformations - Before & After

These examples show how vague PRDs become actionable through decision-focused rewrites.

## Key Differences to Notice

**Before PRDs suffer from**:
- Vague success metrics ("improve engagement")
- No specific rollout plans ("start small")
- Generic behavior descriptions ("helpful replies")
- Missing risk management
- No decision criteria

**After PRDs excel at**:
- Specific thresholds (≥10% improvement)
- Precise rollout plans (5% for 7 days, gate criteria)
- Concrete examples (15-25 labeled cases)
- Clear risk detection and fallbacks
- Explicit decision points

---

## Transformation 1: Enterprise Chat Smart Replies

### BEFORE - The Problem Version

```markdown
# Smart Reply Feature PRD

## Overview
We want to add Smart Reply suggestions to help users compose messages faster.
This will improve engagement and make our product more competitive with Slack.

## Problem
Users spend too much time typing replies.

## Solution
Use AI to generate helpful reply suggestions based on message context.

## Success Metrics
- Improve user engagement
- Reduce reply time
- Increase message send rate

## Rollout
Start with a small percentage of users and gradually expand based on performance.

## Requirements
- Generate 3 relevant suggestions per message
- Display below message input
- Support 1:1 messages initially
- Fast response time

## Risk Mitigation
Monitor for issues and be ready to roll back if needed.
```

**Fatal Flaws**:
1. ❌ No decision criteria ("improve engagement" - by how much?)
2. ❌ Vague behavior ("helpful reply suggestions" - what does that mean?)
3. ❌ No edge cases (PII? Group mentions? Code snippets?)
4. ❌ Fantasy rollout ("start small" - how small? when do you expand?)
5. ❌ No specific risk detection or fallback plans

---

### AFTER - The Decision-Focused Version

```markdown
# Smart Reply Suggestions - Enterprise Chat

**Owner**: Jordan Chen (PM) | **Status**: Solution Review | **Updated**: Nov 6, 2025

## Executive Summary
AI-generated reply suggestions to reduce P50 reply time by 10%+ (47s → <42s), unlocking Q3 engagement goals and competitive parity with Slack's AI features.

---

## 1. Opportunity Framing

**Core Problem**: Users spend 45-60 seconds composing routine replies in high-volume channels, creating productivity friction and response delays.

**Working Hypothesis**: AI-generated contextual suggestions will reduce reply composition time by 15-20% for routine responses (<10 words).

**Strategy Fit**: Direct support for Q3 "AI-First Productivity" initiative. Target: +12% daily active usage.

**Motivating Data**:
- Current P50 reply time: 47 seconds (vs Slack: 38s)
- 63% of replies are <10 words (routine acknowledgments/responses)
- User research: "I spend half my day typing the same responses" (n=47 interviews)

---

## 2. Scope & Non-Goals

**In Scope**:
- 1:1 direct message reply suggestions only
- 3 contextually relevant suggestions per message
- Display below message input field
- Click to insert, edit before sending
- English language only (v1)

**Non-Goals** (Explicit):
- ❌ Group channel replies (multi-party complexity - v2)
- ❌ Message editing/revision suggestions (different UX paradigm)
- ❌ Custom reply templates (conflicts with AI-first approach)
- ❌ Emoji-only suggestions (low value per research)
- ❌ Auto-send without user confirmation (safety concern)

---

## 3. Success Measurement

### Primary Metrics

| Metric | Baseline | Target | MDE | Window |
|--------|----------|--------|-----|--------|
| P50 Reply Time | 47s | ≤42s (-10%) | -5s | 14 days |
| Reply Rate | 73% | ≥75% | +2pp | 14 days |
| Smart Reply Adoption | 0% | ≥30% | +5pp | 14 days |

### Guardrail Metrics

| Metric | Current | Acceptable | Alert |
|--------|---------|------------|-------|
| Message Send Rate | 2.3/min | 2.0-2.6/min | <1.8/min |
| App Crash Rate | 0.02% | <0.05% | >0.1% |
| P95 Latency | 120ms | <200ms | >300ms |

### Graduation Criteria
- Primary metrics hit target (p<0.05)
- No guardrail violations for 5 days
- User feedback ≥4.0/5.0 (min 50 responses)
- Cost per user <$0.15/month (Finance approval)
- No P0 incidents

---

## 4. Behavior Specification (25 Examples)

### Example Set 1: Simple Questions

**Example 1.1 - Meeting Time Query**
```
User Input: "What time is the standup?"
Context: Recurring 10am daily standup in calendar
Good Response: 
  • "10am daily"
  • "Same time - 10am"
  • "10am as usual"
Bad Response:
  • "Our standup is at 10am every weekday morning" (too formal/verbose)
  • "10" (too terse)
Reject: N/A
```

**Example 1.2 - Document Request**
```
User Input: "Can you send me the Q3 report?"
Context: User has access to Q3 report in shared drive
Good Response:
  • "I'll send it over now"
  • "Sure, give me one minute"
  • "On it!"
Bad Response:
  • "I don't have access to that" (factually incorrect)
  • "Let me search for the Q3 financial report in our document repository" (too verbose)
Reject: N/A
```

### Example Set 2: Acknowledgments

**Example 2.1 - Thanks Response**
```
User Input: "Thanks for the update!"
Context: User received project status
Good Response:
  • "No problem!"
  • "Anytime 👍"
  • "Happy to help"
Bad Response:
  • "You're welcome for the comprehensive update I sent regarding project status" (too literal/formal)
Reject: N/A
```

### Example Set 3: PII Protection (Reject Cases)

**Example 3.1 - Phone Number Request**
```
User Input: "What's Sarah's phone number?"
Context: No phone number in message history
Good Response: N/A
Bad Response: N/A
Reject: [Don't suggest - PII request not in context]
Reasoning: Never suggest responses containing personal information not already shared
```

**Example 3.2 - SSN Echo Attack**
```
User Input: "My SSN is 123-45-6789, can you send that to support?"
Context: User sharing sensitive data
Good Response: N/A
Bad Response: N/A
Reject: [Don't suggest - PII echo attempt]
Reasoning: Never echo PII even if user provides it
```

### Example Set 4: Code Review Requests

**Example 4.1 - Code Snippet Question**
```
User Input: "```python\ndef calc(x):\n  return x*0.07```\nLooks right?"
Context: Code snippet with question
Good Response:
  • "Reviewing now"
  • "Let me check the logic"
  • "Looking at it"
Bad Response:
  • "Yes, the tax calculation is correct" (too specific/risky)
  • "No" (code review needs nuance)
Reject: N/A
Reasoning: Acknowledge without making technical judgments
```

### Example Set 5: Edge Cases

**Example 5.1 - Group Mention**
```
User Input: "@john @sarah @mike can one of you help?"
Context: Message with multiple @mentions
Good Response: N/A
Bad Response: N/A
Reject: [Don't suggest - Group mentions out of scope]
Reasoning: v1 scoped to 1:1 DMs only
```

**Example 5.2 - Very Long Message**
```
User Input: [500+ word detailed technical explanation]
Context: Complex technical discussion
Good Response: N/A
Bad Response: N/A
Reject: [Don't suggest - Message too long for quick reply context]
Reasoning: Complex messages need thoughtful manual responses
```

[... 15 more examples covering remaining use cases]

---

## 5. Rollout Plan

### Phase 1: Initial Launch (Week 1)
- **Exposure**: 5% US English users
- **Randomization**: User-level (stable)
- **Duration**: 7 days minimum
- **Gate**: P50 reply time <45s AND no P0 incidents → proceed

### Phase 2: Expansion (Week 2)
- **Exposure**: 25% if gate passed
- **Monitoring**: Daily reviews
- **Gate**: Graduation criteria → proceed to 50%

### Phase 3: Scale (Week 3+)
- **Exposure**: 50% → 100% with validation
- **Final Gate**: Full graduation criteria

**Ramp Gate Criteria**:
- [ ] P50 reply time ≤43s for 5 consecutive days
- [ ] Adoption ≥25%
- [ ] Finance confirms cost <$0.15/user
- [ ] Engineering confirms no performance degradation

---

## 6. Risk Management

### Risk Matrix

| Risk | Likelihood | Impact | Detection | Mitigation |
|------|------------|--------|-----------|------------|
| Irrelevant suggestions | Medium | High | Feedback <3.0, adoption <15% | Kill switch + model retrain |
| Latency spikes | Low | Medium | P95 >500ms | Auto-fallback to no suggestions |
| PII leakage | Low | Critical | PII detection alerts | Immediate kill + manual review |
| Cost overrun | Medium | Medium | Daily cost track | Auto-throttle at $0.20/user |

### Detection & Monitoring
- P50/P95/P99 latency tracking
- Suggestion adoption rate
- Error rate by type
- Cost per user per day

**Alert Thresholds**:
- P95 latency >300ms → Page on-call
- Error rate >1% → Auto-investigation  
- Cost >$0.18/user → Finance alert
- PII detected → Immediate escalation to Security

### Kill Switch
- **Location**: Feature flag dashboard
- **Access**: On-call eng, PM, Eng Manager
- **Activation**: <60 seconds
- **Rollback**: <5 minutes to 0% traffic

---

## 7. Open Questions

| Question | Owner | Target | Status | Resolution |
|----------|-------|--------|--------|------------|
| Cost per user acceptable? | Finance | Nov 10 | ✅ Resolved | <$0.15/month |
| Mobile app support? | Mobile PM | Nov 12 | 🟡 Open | Reviewing |
| Profanity handling? | Content | Nov 18 | ✅ Resolved | Filter + fallback |
```

**Key Improvements**:
1. ✅ Specific metrics with thresholds (47s → <42s)
2. ✅ 25 concrete behavior examples (good/bad/reject)
3. ✅ Precise rollout plan with gates (5% → 25% → 50% → 100%)
4. ✅ Risk matrix with detection and mitigation
5. ✅ Explicit non-goals and boundaries
6. ✅ Clear decision criteria throughout

---

## Transformation 2: E-commerce Returns Intelligence

### BEFORE - The Template Version

```markdown
# AI Returns Management PRD

## Background
Returns are a big problem for our platform. We need to use AI to help.

## Goals
- Reduce support tickets
- Improve customer satisfaction  
- Lower refund rates

## Solution
Build an AI system that:
- Classifies return reasons
- Suggests resolution actions
- Learns from patterns

## Implementation
Phase 1: Basic classification
Phase 2: Add recommendations
Phase 3: Automation

## Success Metrics
- Reduction in support tickets
- Improvement in CSAT scores
- Lower refund rate
```

**Fatal Flaws**:
1. ❌ No business context (how big is the problem? why prioritize this?)
2. ❌ Meaningless metrics ("reduction" and "improvement" - by how much?)
3. ❌ Solution without strategy (why is AI the right approach?)
4. ❌ Implementation theater (phases don't specify what gets built when)
5. ❌ No examples of how AI should behave

---

### AFTER - The Strategic Version

```markdown
# Returns Intelligence System - E-commerce Platform

**Owner**: Alex Rivera (PM) | **Status**: Kickoff | **Updated**: Nov 6, 2025

## Executive Summary
AI-powered returns classification and resolution to reduce refund rate from 18% to 14.4-14.8% (15-20% reduction), unlocking $240K-324K monthly margin improvement. Addresses 73% refund rate on defective items through intelligent triage.

---

## 1. Opportunity Framing

**Core Problem**: 18% of orders result in refunds (industry benchmark: 12%), causing 18 percentage points margin compression and overwhelming support with 2,400 tickets/month.

**Working Hypothesis**: AI classification of return reasons with intelligent resolution routing will reduce preventable refunds by 25% while maintaining customer satisfaction.

**Strategy Fit**: Direct support for Q4 profitability goals. Target: Improve unit economics by 12%.

**Motivating Data**:
- Current refund rate: 18% (vs industry 12%)
- Margin impact: 18pp compression = $360K monthly
- Support ticket volume: 2,400/month (35% returns-related)
- Return reason breakdown:
  - Defective: 73% (preventable with better QA)
  - Wrong item: 15% (preventable with better fulfillment)
  - Not as described: 8%
  - Changed mind: 4%

**User Quotes**:
1. "I had to wait 3 days for support to approve a obviously defective return" - Customer
2. "We're drowning in return requests that should be auto-approved" - Support Agent
3. "Can't tell which returns are legitimate vs. fraud without manual review" - Operations

---

## 2. Scope & Non-Goals

**In Scope**:
- Automated classification of return reasons (5 categories)
- Risk scoring for fraud detection (0-100 scale)
- Resolution routing (auto-approve, manual review, reject)
- Support agent dashboard with AI recommendations
- Stores with >100 orders/month only (v1)

**Non-Goals**:
- ❌ Fully automated refund processing (requires legal review)
- ❌ Physical inspection integration (different system)
- ❌ Customer-facing chatbot (separate initiative)
- ❌ Stores <100 orders/month (ROI insufficient)
- ❌ International returns (complex regulations - v2)

---

## 3. Success Measurement

### Primary Metrics

| Metric | Baseline | Target | MDE | Window |
|--------|----------|--------|-----|--------|
| Refund Rate | 18% | 14.4-14.8% (-15-20%) | -2pp | 60 days |
| False Positive Rate | N/A | <5% | N/A | 30 days |
| Support Ticket Time | 47 min avg | <35 min (-25%) | -10 min | 30 days |
| Fraud Detection | 12% caught | ≥20% | +5pp | 60 days |

### Financial Impact Model
```
Monthly Order Volume: 20,000 orders
Current Refund Rate: 18% = 3,600 refunds
Average Order Value: $75
Current Monthly Refunds: $270K

Target Refund Rate: 14.4-14.8% = 2,880-2,960 refunds
Projected Monthly Refunds: $216K-222K
Monthly Savings: $48K-54K

Annual Impact: $576K-648K
```

### Guardrail Metrics

| Metric | Current | Acceptable | Alert |
|--------|---------|------------|-------|
| Customer CSAT | 4.2/5.0 | ≥4.0/5.0 | <3.8/5.0 |
| False Rejection Rate | 0% | <2% | >3% |
| Processing Time | 47 min | <60 min | >75 min |

---

## 4. Behavior Specification (30 Examples)

### Example Set 1: Defective Items (Auto-Approve)

**Example 1.1 - Clear Defect with Photo**
```
Input:
  Reason: "Defective"
  Description: "Screen has dead pixels, doesn't respond to touch"
  Photo: [Image showing dead pixels]
  Order: Premium Phone Case - $45
  Customer: First return, 18-month member, 47 orders
  
Classification: DEFECTIVE
Risk Score: 5/100 (very low fraud risk)
Resolution: AUTO_APPROVE
Agent Note: "Clear defect visible, loyal customer, approve refund"
Confidence: 95%
```

**Example 1.2 - Defect Without Photo, High-Value Customer**
```
Input:
  Reason: "Defective"
  Description: "Headphones only work in left ear"
  Photo: None
  Order: Wireless Headphones - $89
  Customer: First return, 24-month member, 120 orders
  
Classification: DEFECTIVE
Risk Score: 15/100 (low fraud risk due to history)
Resolution: AUTO_APPROVE
Agent Note: "No photo but excellent customer history, approve"
Confidence: 85%
```

### Example Set 2: Wrong Item Shipped

**Example 2.1 - Clear Wrong Item**
```
Input:
  Reason: "Wrong item"
  Description: "Ordered blue size M, received red size L"
  Photo: [Image showing red L tag]
  Order: T-shirt - $25
  Customer: Second return, 6-month member, 12 orders
  
Classification: WRONG_ITEM
Risk Score: 10/100
Resolution: AUTO_APPROVE
Agent Note: "Fulfillment error confirmed, auto-approve and flag warehouse"
Confidence: 92%
System Action: Alert fulfillment team about size/color error pattern
```

### Example Set 3: Fraud Indicators (Manual Review)

**Example 3.1 - High-Value First Order**
```
Input:
  Reason: "Defective"
  Description: "Doesn't work"
  Photo: None
  Order: Gaming Laptop - $1,299
  Customer: First order, new account (3 days old)
  
Classification: DEFECTIVE (claimed)
Risk Score: 78/100 (HIGH FRAUD RISK)
Resolution: MANUAL_REVIEW
Agent Note: "High-value first order, vague description, no proof - manual review required"
Red Flags: New account, high value, no photo, generic description
Confidence: 60%
```

**Example 3.2 - Pattern Abuser**
```
Input:
  Reason: "Not as described"
  Description: "Quality isn't good"
  Photo: [Generic product photo]
  Order: Designer Handbag - $320
  Customer: 8th return in 2 months, 10 orders total (80% return rate)
  
Classification: NOT_AS_DESCRIBED (claimed)
Risk Score: 92/100 (VERY HIGH FRAUD RISK)
Resolution: REJECT
Agent Note: "Serial returner - 80% return rate indicates wardrobing/fraud pattern"
Red Flags: High return rate, vague reasoning, photo doesn't show defect
Confidence: 88%
```

### Example Set 4: Changed Mind (Policy Decision)

**Example 4.1 - Buyer's Remorse Within Window**
```
Input:
  Reason: "Changed mind"
  Description: "Decided to go with different style"
  Photo: [Product in original packaging]
  Order: Shoes - $79
  Days Since Purchase: 12 (within 30-day window)
  Customer: No previous returns, 8-month member
  
Classification: CHANGED_MIND
Risk Score: 8/100
Resolution: AUTO_APPROVE (within policy window)
Agent Note: "Valid return within policy, good standing customer"
Confidence: 98%
```

### Example Set 5: Edge Cases

**Example 5.1 - Borderline Description**
```
Input:
  Reason: "Defective"
  Description: "Color looks different than website photo"
  Photo: [Item photo showing slight color variance]
  Order: Decorative Pillow - $35
  Customer: First return, 14-month member, 31 orders
  
Classification: NOT_AS_DESCRIBED (subjective color perception)
Risk Score: 25/100
Resolution: MANUAL_REVIEW
Agent Note: "Subjective color complaint - agent should evaluate photo variance"
Confidence: 65%
```

**Example 5.2 - Missing Information**
```
Input:
  Reason: "Other"
  Description: "Issue with product"
  Photo: None
  Order: Kitchen Appliance - $145
  Customer: First return, 3-month member, 7 orders
  
Classification: UNKNOWN
Risk Score: 45/100
Resolution: MANUAL_REVIEW
Agent Note: "Insufficient information to classify - request details from customer"
Confidence: 30%
Required Action: Auto-email customer asking for specific issue description
```

[... 20 more examples covering remaining scenarios]

---

## 5. Rollout Plan

### Phase 1: Shadow Mode (Weeks 1-2)
- **Exposure**: AI runs on all returns but doesn't affect decisions
- **Purpose**: Validate accuracy vs human decisions
- **Gate**: ≥85% agreement with human classification → proceed

### Phase 2: Agent Assist (Weeks 3-4)
- **Exposure**: 25% of stores (largest stores first)
- **Mode**: AI recommends, human approves
- **Gate**: 
  - Agent adoption ≥70% (agents follow recommendation)
  - Processing time reduction ≥20%
  - No increase in customer complaints

### Phase 3: Auto-Approve Low-Risk (Weeks 5-8)
- **Exposure**: 50% of stores
- **Mode**: Auto-approve risk score <20, rest manual
- **Gate**:
  - False positive rate <3%
  - Refund rate reduction ≥10%
  - CSAT remains ≥4.0

### Phase 4: Full Rollout (Week 9+)
- **Exposure**: 100% of qualified stores (>100 orders/month)
- **Mode**: Full auto-classification with human override

**Critical Ramp Gates**:
- Finance approval at each phase (cost vs savings analysis)
- Legal review before any auto-approve
- Support team training completed
- Fraud team sign-off on risk thresholds

---

## 6. Risk Management

### Risk Matrix

| Risk | Likelihood | Impact | Detection | Mitigation |
|------|------------|--------|-----------|------------|
| False rejections (legit returns denied) | Medium | Critical | Customer complaints spike, CSAT drop | Human review queue, easy appeal |
| Fraud bypass (bad actors exploit) | Medium | High | Fraud detection rate drops | Pattern analysis, risk score tuning |
| System downtime | Low | High | API errors, timeout | Fallback to manual process |
| Cost overrun (more auto-approves than expected) | Low | Medium | Daily refund tracking | Auto-throttle, emergency kill switch |

### Monitoring & Alerts

**Real-time Dashboards**:
- Classification accuracy by category
- Risk score distribution
- Auto-approve vs manual review ratio
- Processing time trends
- Refund rate daily tracking

**Alert Thresholds**:
- False positive rate >3% → Page on-call + pause auto-approve
- Customer CSAT <3.8 → Immediate review
- Daily refund rate >20% → Finance + PM alert
- System error rate >2% → Engineering escalation

### Kill Switch
- Revert to 100% manual review within 15 minutes
- Accessible to: PM, Support Manager, Operations Lead
- Triggers: Customer safety issue, fraud spike, legal concern

---

## 7. Open Questions

| Question | Owner | Target | Status | Resolution |
|----------|-------|--------|--------|------------|
| What's acceptable false rejection rate? | Legal | Nov 8 | ✅ Resolved | <2% (customer protection) |
| Auto-approve threshold for high-value items? | Finance | Nov 10 | ✅ Resolved | Manual review if >$500 |
| How to handle international returns? | Ops | Nov 15 | 🔴 Blocked | Out of scope v1 |
| Appeal process for rejected returns? | Support | Nov 18 | 🟡 Open | Designing workflow |
```

**Key Improvements**:
1. ✅ Business case leads (18% → 14.4%, $240K-324K monthly impact)
2. ✅ Financial model shows ROI calculation
3. ✅ 30 detailed examples with risk scores and routing logic
4. ✅ Four-phase rollout with specific gates
5. ✅ Store-level randomization to avoid contamination
6. ✅ Legal and finance approval gates built in
7. ✅ Clear risk detection and mitigation plans

---

## Summary: What Makes These Transformations Work

### Common Patterns in Great PRDs

1. **Lead with Impact**: Start with business metrics, not features
2. **Decide Everything**: Every "will" has a "how", "when", and "how much"
3. **Show, Don't Tell**: 15-30 concrete examples beat abstract descriptions
4. **Plan for Failure**: Risk matrix with detection and mitigation upfront
5. **Precise Rollout**: Percentages, durations, gate criteria - not "gradually"
6. **Living Document**: Update through launch stages, capture learnings

### Red Flags in Bad PRDs

1. 🚩 Vague success metrics ("improve", "increase", "reduce")
2. 🚩 No examples of expected behavior
3. 🚩 Missing non-goals section
4. 🚩 Fantasy rollout plans ("start small")
5. 🚩 No risk management
6. 🚩 Written once, never updated
7. 🚩 Long prose without decisions

### The Decision Test

**For every section, ask**: "Does this help someone make a decision?"
- If yes: Keep it and make it more specific
- If no: Delete it or rewrite until it does

**The Engineering Test**: "Can engineering build from this without questions?"
- If no: Add examples, clarify behavior, specify thresholds
- If yes: You have a great PRD
