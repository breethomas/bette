# The Four Big Risks

**Author:** Marty Cagan
**Category:** Discovery
**Last Updated:** January 2025

## Overview

Marty Cagan's framework identifies four critical risks that every product idea faces. Product discovery is fundamentally about addressing these risks before building and shipping a product.

**In the AI era (2025+):** These four risks are MORE critical than ever. AI introduces new dimensions to each risk—probabilistic behavior, explainability challenges, uncertain economics, and evolving regulations. The good news? The framework is perfectly suited to handle these challenges if you apply it rigorously.

## The Four Risks

### 1. Value Risk
**"Will customers buy this or choose to use it?"**

- Most fundamental risk - the #1 reason products fail
- Does this actually solve a real problem?
- Would customers pay for it (or use it if free)?
- Is it significantly better than alternatives?

**AI product considerations:**
- **Avoid AI for AI's sake** - Don't add AI just for marketing or competitive parity
- **Prove demonstrable value** - AI must solve the problem measurably better than existing solutions
- **Set clear expectations** - Clearly communicate what AI can/can't do to avoid disappointment
- **Account for probabilistic nature** - Customers must understand AI won't be 100% accurate every time
- **Test with real use cases** - AI demos can be misleading; test with actual customer workflows

**How to address:**
- Customer discovery interviews (focus on problem, not AI solution)
- Problem validation with target users
- Demand testing (would they switch from current solution?)
- Prototype testing showing AI capabilities AND limitations
- Concierge tests to validate value before building AI

### 2. Usability Risk
**"Can users figure out how to use it?"**

- Can users understand the product?
- Can they accomplish their goals efficiently?
- Is the UX intuitive for your target audience?

**AI product considerations:**
- **Explainability vs. accuracy tradeoff** - More accurate models are often less explainable; balance based on user needs
- **Managing uncertainty** - How do you communicate confidence levels? When does AI say "I don't know"?
- **Setting realistic expectations** - Users must understand capabilities AND limitations upfront
- **Trust and transparency** - Users need to understand why AI made a decision, especially for high-stakes decisions
- **Speed vs. accuracy balance** - Faster responses may be less accurate; what's acceptable for your use case?
- **Error recovery** - When AI gets it wrong (and it will), can users easily correct it?
- **Progressive disclosure** - Don't overwhelm users with AI complexity; reveal details when needed

**How to address:**
- Usability testing with prototypes (including error states and edge cases)
- User testing sessions with diverse skill levels
- Test explainability features - do users understand AI outputs?
- A/B testing different transparency approaches
- Observe user reactions when AI makes mistakes

### 3. Feasibility Risk
**"Can we build this with the time, skills, and technology we have?"**

- Technical capability and constraints
- Timeline and resources required
- Dependencies on other systems or teams
- Performance, scale, and reliability concerns

**AI product considerations:**
- **Probabilistic vs. deterministic behavior** - AI is fundamentally non-deterministic; same inputs may yield different outputs
- **Acceptable error rates** - What's tolerable? (News feed: 5% errors OK; medical dosing: 0.1% may be too high)
- **Training data quality and bias** - Do you have enough quality data? What biases exist? Can you address them?
- **Model accuracy vs. cost tradeoff** - Better models cost more to run; what's your acceptable balance?
- **Infrastructure requirements** - Can your systems handle AI workloads (compute, storage, latency)?
- **Model degradation over time** - AI models can degrade as data distributions change; how will you monitor?
- **Vendor lock-in risks** - Relying on third-party AI APIs? What's your contingency plan?
- **Evaluation and testing** - How do you test probabilistic systems? Traditional unit tests don't work

**How to address:**
- Technical spike work with actual AI models (not just demos)
- Proof-of-concept with production-like data volumes
- Cost modeling at scale (not just prototype costs)
- Engineering feasibility reviews including AI expertise
- Architecture discussions on monitoring, evaluation, and model updates
- Data quality audits before committing to build

### 4. Business Viability Risk
**"Does this solution work for our business?"**

- Does it fit our business model?
- Can we support/maintain it?
- Does it comply with legal/regulatory requirements?
- Does it align with our brand and strategy?
- Is it viable from sales, marketing, finance, legal perspectives?

**AI product considerations:**

**This is often the most complex risk for AI products. Key challenges:**

- **Unit economics uncertainty** - AI costs can be unpredictable at scale; do you understand your cost per interaction/user?
- **Copyright and data provenance** - Where did training data come from? Do you have rights to use it? What about AI outputs?
- **Legal liability for probabilistic decisions** - Who's responsible when AI makes a mistake? Insurance? Indemnification?
- **Regulatory compliance** - AI regulations are rapidly evolving (EU AI Act, etc.); can you stay compliant?
- **Ethical implications** - Bias, fairness, transparency, environmental impact - does your company have a stance?
- **Competitive moats** - AI models are increasingly commoditized; where's your defensibility?
- **Support and debugging** - How do you troubleshoot probabilistic systems? What's your support burden?
- **Vendor dependencies** - If using third-party models, what's your risk if pricing changes or service is discontinued?

**How to address:**
- Stakeholder reviews (include legal, ethics, finance early)
- Business case analysis with realistic AI cost projections
- Legal/compliance review (don't skip this for AI products!)
- Financial modeling at scale including worst-case scenarios
- Ethical review - what could go wrong? How will you respond?
- Competitive analysis - why won't Google/OpenAI/etc. just do this?
- Support plan for when AI fails in production

## The Discovery Process

```
Product Ideas
     ↓
Rapid testing of all four risks
     ↓
High-confidence solution
     ↓
Build & Ship
```

## Key Principles

### 1. Address Risks Before Building
Don't wait until after launch to discover problems. Discovery is about quickly and cheaply testing ideas.

### 2. Value Risk is Usually Highest
Most product failures are because no one wanted it, not because it was hard to build or use.

### 3. Test with Real Target Users
Your team's opinions don't count. Test with actual customers in your target market.

### 4. Use Prototypes, Not Production Code
Test ideas with high-fidelity prototypes that require minimal engineering time.

## Discovery Techniques by Risk Type

### For Value Risk:
- Customer discovery interviews
- Concierge tests (manual delivery)
- Landing page tests
- Fake door tests
- Wizard of Oz tests

### For Usability Risk:
- Prototype testing
- Usability testing sessions
- Cognitive walkthroughs
- Task analysis

### For Feasibility Risk:
- Technical spikes
- Proof-of-concept code
- Architecture reviews
- Reference projects

### For Business Viability Risk:
- Stakeholder reviews
- Business model canvas
- Unit economics analysis
- Legal reviews

## Questions to Ask

### Assessing Value Risk:
- "What problem does this solve for customers?"
- "How do they solve this problem today?"
- "Would they pay for a better solution?"
- "What evidence do we have that customers want this?"
- "What would make them switch from their current solution?"

### Assessing Usability Risk:
- "Can target users complete key tasks without help?"
- "What are the most common points of confusion?"
- "Is the learning curve acceptable for our market?"
- "Does this work for our least tech-savvy users?"

### Assessing Feasibility Risk:
- "What's the hardest technical challenge here?"
- "What could block us from delivering this?"
- "Are there dependencies on other teams?"
- "What would we need to learn or build that's new?"
- "What performance/scale concerns exist?"

### Assessing Business Viability Risk:
- "Does this fit our business model?"
- "Can sales sell it? Can marketing market it?"
- "What are the support implications?"
- "Are there legal/regulatory issues?"
- "Does this align with company strategy?"

## Common Patterns

**Early-stage products:** Value risk is highest - focus there first
**Mature products:** Usability and business viability often more important
**Technical products:** Feasibility risk may be higher than usual
**Regulated industries:** Business viability (compliance) is critical

## Integration with Other Frameworks

Works well with:
- **Teresa Torres' Continuous Discovery** - Use four risks to prioritize what to test
- **Assumption Mapping** - Categorize assumptions by risk type
- **Lean Startup** - Four risks inform what experiments to run
- `/frameworks/ai/fine-tuning-vs-rag.md` - Strategic decision that impacts feasibility and viability risks for AI products

## Anti-Patterns to Avoid

❌ **Building first, testing later** - Most expensive way to address risks
❌ **Assuming you are the user** - Your opinion on usability doesn't count
❌ **Ignoring business viability** - Engineering can build it but business can't support it
❌ **Only testing one risk** - All four must be addressed
❌ **Testing with the wrong users** - Must be target customers, not friends/family

## When to Use This Framework

- ✅ Evaluating new product ideas
- ✅ Planning discovery activities
- ✅ Prioritizing what to test first
- ✅ Deciding if you're ready to build
- ✅ Conducting pre-mortems on ideas

## Practical Application

**Example 1: AI-powered customer support chatbot**

1. **Value Risk (Test First):**
   - Question: Will customers actually use a chatbot vs. waiting for human support?
   - Test: Wizard of Oz test - human pretends to be AI for 100 support conversations
   - Validate: Are customers satisfied? Do they complete their tasks? Would they use this again?

2. **Usability Risk:**
   - Question: Can users get answers without frustration? Do they understand when chatbot doesn't know something?
   - Test: Prototype with 20 real customer scenarios including edge cases
   - Measure: Task completion rate, time to resolution, user satisfaction

3. **Feasibility Risk (AI-specific):**
   - Question: What accuracy rate can we achieve? What's acceptable? (90%? 95%? 99%?)
   - Test: POC with real support tickets using different models (GPT-4, Claude, fine-tuned model)
   - Measure: Accuracy, cost per interaction, response time, hallucination rate
   - Critical: Test with production-like data volume, not cherry-picked examples

4. **Business Viability Risk (Most Complex for AI):**
   - Economics: At 10K daily interactions with GPT-4, what's cost vs. human support savings?
   - Legal: Who's liable if chatbot gives wrong information? Need legal review
   - Ethics: What biases exist in training data? How do we handle sensitive customer data?
   - Support: When chatbot fails, what's escalation path? Can we debug issues?
   - Test: Full cost modeling + legal review + ethical assessment

**Order of testing:** Value → Usability → Feasibility → Business Viability

**AI insight:** For AI products, Business Viability often takes longer to assess than Feasibility. Budget time for legal/ethical review.

---

**Example 2: Traditional mobile app for restaurant reservations** (showing framework applies to non-AI products too)

1. **Value Risk (Highest):**
   - Test: Show prototype to diners and restaurant owners
   - Question: Would diners actually use this vs. calling? Would restaurants adopt it?
   - Method: Concierge test - manually handle reservations for 3 restaurants

2. **Usability Risk:**
   - Test: Can users complete a reservation in 60 seconds?
   - Method: Prototype testing with 10 target users

3. **Feasibility Risk:**
   - Test: Can we integrate with existing restaurant systems?
   - Method: Technical spike with 2 different POS systems

4. **Business Viability Risk:**
   - Test: Will restaurants pay our commission? Can we scale customer support?
   - Method: Financial modeling + discussions with restaurant owners

**Order of testing:** Value → Usability → Feasibility → Business Viability

## Resources

**Core framework:**
- Book: "Inspired: How to Create Tech Products Customers Love" by Marty Cagan
- Website: [svpg.com](https://svpg.com)
- Article: "Four Big Risks" at Silicon Valley Product Group

**AI-specific applications:**
- Article: ["AI Product Management"](https://www.svpg.com/ai-product-management/) by Marty Cagan & Marily Nika
- See also: `/frameworks/ai/production-ai-systems.md` (Chip Huyen) for technical feasibility considerations
- See also: `/frameworks/ai/ai-evals.md` for testing probabilistic systems
