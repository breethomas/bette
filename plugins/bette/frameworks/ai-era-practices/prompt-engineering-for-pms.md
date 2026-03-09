# Prompt Engineering for Product Managers

**Category:** AI-Era Practices
**Source:** Adapted from Aakash Gupta, Reforge, and AI product best practices
**Last Updated:** January 2025

## Overview

Prompt engineering isn't a technical implementation detail—it's **product strategy in disguise**. Every instruction you write into a system prompt is a product decision about behavior, tone, constraints, and user experience.

As a PM, you can't outsource this work to engineering. You understand user intent better than anyone, and prompt changes enable iteration speeds that engineering sprints can't match.

## ⚠️ What This Framework Is NOT About

**This framework is NOT about building a "prompt library."**

The future of AI products isn't collecting perfect prompts—it's building systems that give AI the right context, tools, and feedback loops to solve problems iteratively.

**Two related but different skills:**

**Context Engineering** (see [context-engineering.md](context-engineering.md))
- Designing the environment AI operates in
- Data, tools, memory, constraints, feedback loops
- Systems thinking > one-shot prompting
- **This is the strategic skill**

**Prompt Engineering** (this framework)
- Writing effective instructions within that context
- Product decisions about behavior and tradeoffs
- Iteration and testing methodology
- **This is a tactical skill within the bigger system**

**The hierarchy:**
```
Context Engineering (the system)
  ↓
Prompt Engineering (the instructions)
  ↓
Output (what users see)
```

**Key insight:** Great prompts with bad context fail. Okay prompts with great context work. Perfect is both, but prioritize context.

**If you're choosing where to start, read [context-engineering.md](context-engineering.md) first.**

## Why PMs Own Prompt Engineering

### 1. User Understanding

**You know what users actually want.**

Engineers know how to structure code. Data scientists know model capabilities. But **PMs understand user intent**—and that's what prompts encode.

**Example:**
```
Bad prompt (technical focus):
"Generate a summary of the input text using extractive methods."

Good prompt (user intent focus):
"Write a 2-3 sentence summary that captures the key takeaway
a busy executive would care about. Focus on insights, not details."
```

The difference? Understanding **why** users need summaries and **how** they'll use them.

### 2. Iteration Speed

**Changing a prompt takes minutes. Waiting for an engineering sprint takes weeks.**

As a PM, you can:
- Test different prompt approaches in hours
- A/B test variations with real users
- Respond to user feedback immediately
- Iterate toward quality before involving eng

**This matches AI-era reality:** Prototype-first development means testing prompts before building production systems.

### 3. Product Strategy Embedded in Prompts

**Every prompt instruction is a product decision:**

| Prompt Choice | Product Decision |
|--------------|------------------|
| "Be concise" vs "Be comprehensive" | Depth vs breadth tradeoff |
| "Suggest 3 options" vs "Recommend 1 best option" | User agency vs system confidence |
| "If uncertain, say so" vs "Always provide an answer" | Accuracy vs helpfulness balance |
| "Use friendly tone" vs "Use professional tone" | Brand voice and positioning |
| "Prioritize safety over usefulness" | Risk tolerance |

**These are product calls, not engineering decisions.**

### 4. Pattern Recognition from User Feedback

**User complaints often reveal prompt opportunities, not model limitations.**

When users say:
- "The AI is too verbose" → Prompt constraint issue
- "It doesn't understand my industry" → Context/examples needed
- "Results feel generic" → Prompt lacks specificity
- "It's sometimes wrong but sounds confident" → Calibration instruction needed

**PMs are best positioned to translate user feedback into prompt improvements.**

## The Core Mental Model: Quality First, Cost Second

**Source:** Aakash Gupta's framework

Don't optimize for efficiency before you have quality. Instead:

### Phase 1: Hill Climb Up Quality

**Goal:** Get it working well, regardless of cost.

**Approach:**
- Write verbose, detailed prompts
- Include many examples
- Over-specify context
- Prioritize accuracy over token efficiency
- Test extensively with real scenarios

**Mindset:** "What does the AI need to produce excellent outputs?"

**Example:**
```
Phase 1 prompt (quality-focused):
You are an expert customer support agent for [Product].
Your goal is to help users solve problems quickly and empathetically.

Context about our product:
- [Detailed product description]
- [Common use cases]
- [Known issues and solutions]

When responding:
1. Always acknowledge the user's frustration
2. Provide step-by-step solutions
3. If you're unsure, say so and escalate
4. Use a warm, helpful tone
5. Avoid jargon

Examples of good responses:
[3-5 detailed examples]

Now, respond to this user query: {query}
```

**This is long and token-heavy, but it works.**

### Phase 2: Down Climb Cost

**Goal:** Reduce tokens and latency while maintaining quality.

**Approach:**
- Remove redundant instructions
- Condense examples
- Test minimal viable prompts
- Measure quality degradation
- Find the efficiency frontier

**Mindset:** "What can I remove without hurting quality?"

**Example:**
```
Phase 2 prompt (cost-optimized):
You're a [Product] support expert. Help users solve problems
with empathy and clarity. Escalate if uncertain.

Examples:
[2 concise examples]

Query: {query}
```

**Key principle:** Never start with Phase 2. Optimize cost only after proving quality.

## Prompt Engineering as Context Engineering

**Prompts are part of a broader context system:**

```
┌─────────────────────────────────────┐
│  System Prompt (Instructions)      │ ← Behavior, tone, constraints
│  ↓                                  │
│  User Input (The query)            │ ← What user asked
│  ↓                                  │
│  Retrieved Context (RAG)           │ ← Relevant data from your system
│  ↓                                  │
│  Few-Shot Examples (In prompt)     │ ← Show, don't just tell
│  ↓                                  │
│  Model Output                      │ → AI response
└─────────────────────────────────────┘
```

**Aakash's insight:** Prompts handle **85% of the heavy lifting** compared to RAG or fine-tuning.

### When to Use Each Approach

**Prompting alone:**
- Behavior and tone guidance
- Output format specification
- General instructions
- Constraint definition
- **→ Start here, cheapest and fastest**

**Prompting + RAG:**
- Need specific factual information
- User data or domain knowledge required
- Context changes per user/query
- **→ Add when prompts alone miss information**

**Fine-tuning:**
- Consistent style across all outputs
- Domain-specific language patterns
- High volume justifies cost
- Prompting + RAG plateaued
- **→ Only when necessary, expensive and slow**

**Key insight:** Most PMs over-invest in RAG/fine-tuning before exhausting prompt improvements.

## Prompt Patterns PMs Should Know

These are timeless patterns, not tool-specific syntax.

### 1. Role Definition

**Give the AI a clear identity and purpose.**

```
Good: "You are an experienced product manager helping
a startup prioritize their roadmap."

Bad: "Help prioritize this roadmap."
```

**Why it works:** Context about expertise and audience shapes responses.

### 2. Chain-of-Thought

**Ask the AI to show its reasoning before answering.**

```
Good: "Before providing recommendations, first analyze:
1. What problem is the user trying to solve?
2. What constraints do they have?
3. What options exist?
Then provide your recommendation."

Bad: "Provide a recommendation."
```

**Why it works:** Reasoning steps improve quality and let you debug failures.

### 3. Few-Shot Examples

**Show examples of good outputs, don't just describe them.**

```
Good:
"Here are examples of good summaries:

Input: [Long article about AI]
Output: AI models are getting cheaper and more accessible,
enabling new product categories. Key opportunity: integrate
AI into existing products using off-the-shelf models.

Input: [Long article about pricing]
Output: Most startups undercharge because they fear losing
customers. Better: find high-willingness-to-pay segments and
charge them appropriately.

Now summarize this article: [new article]"

Bad: "Provide a concise summary."
```

**Why it works:** Examples communicate format, tone, and quality better than instructions.

### 4. Constraint Specification

**Explicitly state boundaries and limitations.**

```
Good: "Provide 3-5 recommendations. Each should be:
- Actionable within 2 weeks
- No more than $5k budget
- Focused on retention, not acquisition
If you can't provide recommendations meeting these
constraints, explain why."

Bad: "Give me some recommendations."
```

**Why it works:** Prevents generic or off-target responses.

### 5. Calibration Instructions

**Tell the AI how to handle uncertainty.**

```
Good: "If you're confident in your answer, provide it directly.
If somewhat uncertain, offer 2-3 possibilities.
If very uncertain, say 'I don't have enough information to
answer this reliably' and suggest what additional context
would help."

Bad: "Answer the question."
```

**Why it works:** Matches confidence to response style, builds user trust.

**See also:** `/frameworks/ai-era-practices/continuous-calibration.md` for agency vs control tradeoffs.

### 6. Output Format Control

**Specify structure, length, and format.**

```
Good: "Respond in this format:
**Problem:** [1 sentence]
**Recommendation:** [2-3 sentences]
**Rationale:** [3-5 bullet points]
**Risks:** [1-2 potential downsides]"

Bad: "Tell me what to do."
```

**Why it works:** Consistent format improves usability and downstream processing.

## Prompts as Product Strategy

**Every prompt encodes product decisions. Be intentional about tradeoffs.**

### Tradeoff 1: Helpfulness vs Accuracy

**More helpful = more hallucination risk**

```
Helpful-biased prompt:
"Always provide an answer, even if you need to extrapolate."
→ Users get responses, but some may be wrong

Accuracy-biased prompt:
"Only answer if you're confident. If uncertain, say so."
→ Users get "I don't know" more often, but fewer errors
```

**Product decision:** Which failure mode is worse for your users?

### Tradeoff 2: Brevity vs Completeness

**Concise responses are faster to read but might miss nuance**

```
Brevity-biased prompt:
"Respond in 1-2 sentences maximum."
→ Fast to consume, might oversimplify

Completeness-biased prompt:
"Provide comprehensive explanation with examples."
→ Thorough, but takes longer to read
```

**Product decision:** What's your users' context? Busy executive vs researcher learning?

### Tradeoff 3: User Agency vs System Confidence

**AI can suggest options or make decisions**

```
Agency-preserving prompt:
"Suggest 3-5 options with pros/cons. Let the user decide."
→ User maintains control, but requires more effort

Confidence-driven prompt:
"Recommend the single best option and explain why."
→ Faster for user, but AI might be wrong
```

**Product decision:** How much do users trust the AI? How high-stakes is the decision?

**See also:** `/frameworks/ai-era-practices/continuous-calibration.md` for managing agency levels.

### Tradeoff 4: Generic vs Opinionated

**AI can be neutral or encode product opinions**

```
Neutral prompt:
"Explain both sides of this debate fairly."
→ Balanced, but potentially wishy-washy

Opinionated prompt:
"We believe [position]. Explain this perspective
while acknowledging counterarguments."
→ Reflects product values, but might alienate some users
```

**Product decision:** Is your product opinionated or a neutral platform?

## Iterating on Prompts: The Process

**Prompt engineering is product iteration at high speed.**

### 1. Define Success Criteria

**Before writing prompts, know what "good" looks like.**

- What makes a response excellent vs mediocre vs bad?
- What failure modes are unacceptable?
- What edge cases must you handle?

**Document these as evals.**

**See:** `/frameworks/ai/ai-evals.md` for comprehensive eval design.

### 2. Start with Verbose Prompt

**Phase 1: Quality first.**

- Write detailed instructions
- Include context and examples
- Over-specify constraints
- Test with real scenarios

### 3. Test Against Evals

**Measure quality systematically.**

- Run prompt against eval dataset
- Track success rate, failure modes
- Identify patterns in failures

### 4. Iterate Based on Failures

**Fix failure modes one at a time.**

When the AI:
- Misunderstands intent → Add clarifying instructions
- Produces wrong format → Specify format more explicitly
- Hallucinates → Add "say if uncertain" instruction
- Is too verbose → Add length constraints
- Misses context → Add examples or RAG

### 5. Version Your Prompts

**Track every change like code.**

```
v1.0: Initial prompt
v1.1: Added constraint to reduce verbosity
v1.2: Added few-shot examples for edge case X
v1.3: Improved calibration instructions to reduce hallucinations
v1.4: Optimized for cost (removed redundant context)
```

**Why:** A/B test versions, rollback if quality degrades.

### 6. Optimize for Cost (Phase 2)

**Only after proving quality.**

- Remove redundant instructions
- Condense examples
- Test minimal viable prompt
- Measure quality impact
- Find efficiency frontier

### 7. Monitor in Production

**Prompts drift as usage evolves.**

Track:
- User satisfaction with outputs
- Override/correction rates
- New failure modes
- Edge cases discovered

**Calibrate continuously.**

**See:** `/frameworks/ai-era-practices/continuous-calibration.md`

## Integration with Other Frameworks

### Teresa Torres' Continuous Discovery

**User interviews reveal prompt opportunities:**

Weekly conversations uncover:
- "The AI doesn't understand my workflow" → Add context about user workflows
- "Responses feel robotic" → Adjust tone instructions
- "It misses the point of my question" → Improve intent classification

**Discovery informs prompting, prompting enables discovery prototypes.**

### Aman Khan's AI Evals

**Evals validate prompt quality:**

- Define success criteria for AI responses
- Build eval dataset of scenarios
- Test prompt changes against evals
- Measure improvement/regression
- Only deploy if evals pass

**Prompts are hypotheses. Evals are the test.**

**See:** `/frameworks/ai/ai-evals.md`

### Marty Cagan's Four Risks

**Prompts address multiple risks:**

- **Value risk:** Does prompt produce outputs users want?
- **Usability risk:** Can users understand AI responses?
- **Feasibility risk:** Can we maintain prompt quality at scale?
- **Viability risk:** Are token costs sustainable?

**Prototype prompts to test risks before building.**

### Continuous Calibration (CC/CD)

**Prompts evolve with agency levels:**

**Low agency (AI suggests):**
```
"Provide 3-5 options with pros/cons.
Let the human decide."
```

**Medium agency (AI recommends):**
```
"Recommend the best option and explain why.
Mention alternatives if close call."
```

**High agency (AI decides):**
```
"Make the best decision and execute.
Log rationale for human review."
```

**Earn autonomy by proving quality at each level.**

### Prototype-First Development

**Prompts ARE prototypes:**

Instead of:
- Writing 10-page spec about desired AI behavior
- Waiting for eng to implement
- Testing after it's built

Do this:
- Write prompt (5 minutes)
- Test with real scenarios (30 minutes)
- Iterate based on results (1 hour)
- Show working prototype to stakeholders
- Align before building production system

**This is the AI-era PM workflow.**

## Common Mistakes

### ❌ Treating Prompts as Eng Work

**Problem:** "I wrote a spec, now eng will implement the prompt."

**Better:** PMs should write initial prompts, then collaborate with eng on production implementation.

**Why:** You understand user intent, iterate faster, and prompts are product decisions.

### ❌ Optimizing for Cost Too Early

**Problem:** "Let's make prompts as short as possible to save tokens."

**Better:** Prove quality first (verbose prompts), then optimize cost.

**Why:** Cheap prompts that produce bad outputs are worthless.

### ❌ Under-Specifying Context

**Problem:** "The AI should just figure out what users want."

**Better:** Give AI rich context: role, constraints, examples, format.

**Why:** Models need explicit instructions. Vague prompts → vague outputs.

### ❌ No Examples in Prompts

**Problem:** "I described what I want in the instructions."

**Better:** Show 2-5 examples of excellent outputs.

**Why:** Examples communicate better than descriptions.

### ❌ Not Versioning Prompts

**Problem:** "We keep tweaking the prompt but don't track changes."

**Better:** Version every prompt change, A/B test, rollback if needed.

**Why:** Need to diagnose quality degradation and compare versions.

### ❌ Ignoring User Corrections

**Problem:** "Users edit AI outputs, but we don't analyze why."

**Better:** Track patterns in user corrections → Update prompts.

**Why:** User edits show where prompts fail. Fix the root cause.

### ❌ Skipping Evals

**Problem:** "We test prompts manually with a few examples."

**Better:** Build systematic eval dataset, test all changes.

**Why:** Manual testing misses edge cases and doesn't scale.

## Practical Examples for PMs

### Example 1: Roadmap Prioritization Assistant

**User need:** Help PMs prioritize features based on impact and effort.

**v1.0: Quality-first prompt (verbose)**
```
You are an experienced product manager helping prioritize
features for a roadmap.

Context:
- This is a B2B SaaS product in the [domain] space
- Users are primarily [persona]
- Current goals: [growth/retention/expansion]
- Team size: [X engineers, Y designers]
- Timeline: Next quarter

When evaluating features:
1. Assess potential user impact (high/medium/low)
2. Estimate engineering effort (small/medium/large)
3. Consider strategic alignment with goals
4. Identify dependencies or risks
5. Recommend priority tier (Now/Next/Later)

Provide recommendations in this format:
**Feature:** [Name]
**Impact:** [Assessment + reasoning]
**Effort:** [Assessment + reasoning]
**Priority:** [Now/Next/Later]
**Rationale:** [Why this priority?]

Examples:
[3 examples of well-prioritized features]

Now, evaluate these features: {feature_list}
```

**v1.3: Cost-optimized prompt (after validating quality)**
```
You're a PM helping prioritize features.

For each feature, assess:
- Impact (high/med/low)
- Effort (small/med/large)
- Priority (Now/Next/Later)

Format:
**Feature:** [Name]
**Impact:** [Assessment + why]
**Effort:** [Assessment + why]
**Priority:** [Tier + rationale]

Features: {feature_list}
```

**Improvement:** Reduced tokens by ~60%, maintained quality.

### Example 2: Customer Feedback Analyzer

**User need:** Categorize and summarize support tickets.

**v1.0: Initial prompt**
```
Categorize this support ticket and suggest a response.
```

**Problem:** Too vague. AI produces generic categories and responses.

**v2.0: Improved with context and examples**
```
You're analyzing support tickets for [Product].

Categorize each ticket:
- Bug Report
- Feature Request
- How-to Question
- Billing Issue
- Account Access

For each category, suggest:
- Priority (high/medium/low)
- Recommended response
- If escalation needed

Examples:
User: "The app crashes when I upload images larger than 5MB"
Category: Bug Report
Priority: High
Response: [Example response acknowledging, asking for details]
Escalate: Yes, to engineering

User: "How do I export my data?"
Category: How-to Question
Priority: Low
Response: [Example with steps]
Escalate: No

Now analyze: {ticket}
```

**Improvement:** Specificity → Better categorization and responses.

**v2.3: Added calibration after hallucination issues**
```
[Same as v2.0, but added:]

Important: Only suggest responses if you're confident.
If the issue is unclear or requires specific account access,
mark as "Needs human review" and explain why.
```

**Improvement:** Reduced incorrect auto-responses by 40%.

### Example 3: Product Strategy Brainstorming

**User need:** Generate product ideas based on user feedback themes.

**v1.0: Quality-focused**
```
You're a product strategist helping brainstorm solutions.

Context:
- Product: [Description]
- Users: [Personas]
- Recent feedback themes:
  1. [Theme 1 with examples]
  2. [Theme 2 with examples]
  3. [Theme 3 with examples]

For each theme, suggest 2-3 potential solutions that:
- Address the core user problem
- Are feasible for our team
- Align with product vision
- Differentiate from competitors

Format:
**Theme:** [Name]
**Problem:** [Core user pain]
**Solutions:**
1. [Solution] - [How it solves the problem] - [Why it's differentiated]
2. [Solution] - [How it solves the problem] - [Why it's differentiated]

Be creative but practical. Focus on solutions we could prototype
and test within 2-4 weeks.
```

**This works well for brainstorming sessions with stakeholders.**

## Key Takeaways

1. **Prompt engineering is PM work** - You understand user intent best
2. **Quality first, cost second** - Prove it works, then optimize
3. **Prompts are product strategy** - Every instruction is a product decision
4. **Show, don't just tell** - Examples beat descriptions
5. **Version everything** - Track changes, A/B test, rollback if needed
6. **Test systematically** - Build evals, measure quality
7. **Iterate based on failures** - User corrections reveal prompt opportunities
8. **Start with prompts alone** - Before RAG or fine-tuning
9. **Encode tradeoffs intentionally** - Helpfulness vs accuracy, agency vs control
10. **Monitor continuously** - Prompts drift as usage evolves

## Further Learning

### Essential Resources

**Aakash Gupta:**
- "Prompt Engineering for PMs" - Mental models and frameworks
- Newsletter: [news.aakashg.com](https://www.news.aakashg.com)

**Reforge:**
- "Steal These Prompts" - Practical examples for PMs
- AI Product Development curriculum

**OpenAI:**
- Prompt engineering guide (technical but useful)
- Best practices documentation

**Anthropic:**
- Claude prompt engineering documentation
- Thinking styles and prompt patterns

### Related Frameworks in This Tool

- `/frameworks/ai/ai-evals.md` - Testing prompt quality
- `/frameworks/ai-era-practices/continuous-calibration.md` - Evolving AI behavior
- `/frameworks/ai-era-practices/prototype-first.md` - Using prompts as prototypes
- `/frameworks/discovery/continuous-discovery.md` - User research informing prompts

---

**Remember:** Prompt engineering isn't a technical skill to outsource. It's core PM work in the AI era.

You understand users. You make product tradeoff decisions. You iterate based on feedback. These are exactly the skills prompt engineering requires.

Treat prompts as product strategy, test them systematically, and iterate based on real user behavior.

**Quality first. Cost second. Always be calibrating.**
