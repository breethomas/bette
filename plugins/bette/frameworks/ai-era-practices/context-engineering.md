# Context Engineering: Building Systems That Make AI Work

**Source:** Anthropic Engineering, Phil Schmid
**Category:** AI-Era Practices
**Best for:** Building reliable AI products, understanding AI failure modes, systematic validation

---

## Core Principle

**Context matters more than prompts.**

The future of AI product development isn't about collecting perfect prompts—it's about building systems that give AI the right context, tools, and feedback loops to solve problems iteratively.

## Why This Matters

**The old mental model:**
- Craft the perfect prompt
- Get perfect output
- Ship it

**The reality:**
- Prompts are just instructions
- **Context** is the data, tools, memory, and constraints AI has access to
- Systems that manage context beat perfect prompts every time

## What Is Context Engineering?

Context engineering is designing the **environment** in which AI operates:

1. **Data & Knowledge** - What information does the AI have access to?
2. **Tools & Actions** - What can the AI do?
3. **Memory & State** - What does the AI remember across interactions?
4. **Constraints & Guardrails** - What boundaries exist?
5. **Feedback Loops** - How does the AI learn and improve?

**Example:** A customer support AI doesn't need a "perfect prompt" for answering questions. It needs:
- Access to current product docs (data)
- Ability to search order history (tools)
- Memory of this conversation (state)
- Rules about refunds (constraints)
- User feedback on helpfulness (feedback)

## Why Context Matters More Than Prompts

**Common pattern:** AI works great in testing, fails mysteriously in production.

**First instinct:** "We need better prompts!"

**Actual root causes:**
- Conversation history gets polluted over time
- AI has access to bad/outdated data
- No systematic testing infrastructure
- Validation is "vibes" not evals
- Context changes between test and production

**The fix is systemic:**
- Clean and validate data sources
- Monitor context quality
- Test with real scenarios (not just happy paths)
- Measure quality systematically

**Key insight:** When AI fails, check the context first, prompts second.

## The Framework

### 1. Audit Your Context

**Ask:**
- What data does my AI have access to?
- Is that data clean, current, complete?
- What happens when data is stale or wrong?
- Does the AI have too much context (overwhelming) or too little (guessing)?

**Common issues:**
- Conversation history poisoning
- Outdated documentation
- Conflicting information sources
- Too much irrelevant context

### 2. Design Your Tool Access

**Ask:**
- What actions can the AI take?
- What tools does it need to solve problems?
- What should it NOT be able to do?

**Examples:**
- Customer support AI: Can search orders, can't issue refunds > $100 without human
- Code assistant AI: Can read code, can run tests, can't deploy to production
- Research AI: Can search web, can analyze data, can't make conclusions without sources

**Key principle:** Start with low agency, increase as you validate.

### 3. Build Feedback Loops

**The goal:** AI improves through real usage, not just prompts.

**Three types of feedback:**
1. **Immediate validation** - Does this output pass basic checks? (code runs, JSON is valid, etc.)
2. **User feedback** - Thumbs up/down, edit rate, retry rate
3. **Systematic evals** - Regular testing against known scenarios

**Anti-pattern:** One-shot prompting with no feedback loop.

**Better:** AI tries → validates → gets feedback → iterates.

### 4. Start Simple, Add Sophistication

**Don't:**
- Build elaborate context systems before validating the concept
- Over-engineer before you understand what matters
- Optimize for edge cases you haven't encountered

**Do:**
- Start with minimal viable context
- Ship and observe failure modes
- Add context/tools/constraints based on real needs

**Example progression:**

**Week 1:** Basic prompt + current page context
- Learn: AI hallucinates product names

**Week 2:** Add product catalog to context
- Learn: AI can't handle multi-step requests

**Week 3:** Add tool to break requests into steps
- Learn: Some requests need order history

**Week 4:** Add order history access with constraints
- Learn: Works well, but slow for power users

**Week 5:** Add memory of frequent requests per user
- Ship it

## Context Engineering vs. Prompt Engineering

| Prompt Engineering | Context Engineering |
|-------------------|---------------------|
| "How do I phrase this perfectly?" | "What information/tools does AI need?" |
| One-shot optimization | Iterative system design |
| Prompt library | Context architecture |
| Static instructions | Dynamic environment |
| Craft perfect prompt | Build feedback loops |

**Both matter**, but context matters more.

**Good prompt with bad context:** Fails
**Okay prompt with good context:** Works

## Common Mistakes

### Mistake 1: Treating Prompts as the Solution

**Problem:** "Our AI is bad, we need better prompts!"

**Reality:** Often the prompt is fine, but:
- The data is wrong/stale
- The AI lacks necessary tools
- There's no validation of outputs
- Context is overwhelming or insufficient

**Fix:** Audit context first, prompts second.

### Mistake 2: Not Testing Context Quality

**Problem:** "We gave the AI access to our docs, why isn't it working?"

**Reality:**
- Docs might be outdated
- Docs might contradict each other
- Docs might be too technical/vague
- AI might be retrieving irrelevant sections

**Fix:** Test what the AI actually receives. Print the context. Validate it's useful.

### Mistake 3: Static Context

**Problem:** Same context for all users, all queries.

**Reality:** Context should adapt:
- Power users vs. beginners need different context depth
- Simple queries need less context than complex ones
- Context should update as product evolves

**Fix:** Design adaptive context systems.

### Mistake 4: No Feedback Loop

**Problem:** Ship AI → hope it works → don't measure.

**Reality:** You're flying blind.

**Fix:**
- Measure basic quality (accuracy, relevance, safety)
- Collect user feedback (thumbs, edits, retries)
- Build systematic testing (evals on known scenarios)
- Iterate based on data, not vibes

## Practical Applications

### For Customer Support AI

**Context design:**
- Recent conversation history (last 10 messages)
- Customer's order history (last 6 months)
- Current product catalog and docs
- Known issues and outages

**Tools:**
- Search knowledge base
- Look up order details
- Create support ticket (if can't resolve)

**Constraints:**
- Can't promise refunds > policy limit
- Can't access other customers' data
- Must cite sources for policy answers

**Feedback:**
- Thumbs up/down from customer
- "Was this helpful?" after resolution
- Ticket escalation rate (if AI fails)

### For Code Assistant AI

**Context design:**
- Current file being edited
- Related files (imports, dependencies)
- Recent edit history
- Project conventions (linting rules, style guide)

**Tools:**
- Read files in project
- Run tests
- Search documentation

**Constraints:**
- Can't write to files without approval
- Can't access secrets/credentials
- Must explain reasoning for suggestions

**Feedback:**
- Acceptance rate of suggestions
- Edit rate (how much dev changes output)
- Time saved vs. manual coding

### For Research/Analysis AI

**Context design:**
- User's research question
- Previously gathered sources
- Domain-specific knowledge base
- Constraints (date range, source types)

**Tools:**
- Web search
- Paper database search
- Data analysis functions

**Constraints:**
- Must cite sources
- Can't make claims without evidence
- Flag low-confidence answers

**Feedback:**
- User marks sources as relevant/not
- User refines question based on findings
- Follow-up questions indicate quality

## The Validation Stack

Good context engineering includes validation at multiple levels:

**Level 1: Basic Sanity Checks**
- Does output match expected format?
- Does code compile?
- Is JSON valid?
- Are required fields present?

**Level 2: Context Quality Checks**
- Is the retrieved context relevant?
- Is the context up to date?
- Is there contradictory information?

**Level 3: Output Quality Checks**
- Is this factually correct?
- Is this helpful to the user?
- Does this match brand voice/policy?

**Level 4: System Performance**
- Latency acceptable?
- Cost per request sustainable?
- Error rate within bounds?

**Key principle:** Start simple (Level 1), add sophistication as you learn (Levels 2-4).

## When Context Engineering Matters Most

**High-stakes decisions:**
- Medical advice AI needs verified, current medical knowledge
- Financial AI needs real-time market data and regulatory constraints
- Legal AI needs case law access and jurisdictional context

**Complex multi-step tasks:**
- Travel planning AI needs flights, hotels, activities, user preferences
- Code refactoring AI needs full codebase context and test coverage
- Research AI needs multiple sources, citations, and synthesis tools

**Personalized experiences:**
- E-commerce AI needs purchase history, browsing behavior, preferences
- Learning AI needs student progress, misconceptions, learning style
- Fitness AI needs goals, capabilities, past workout history

## AI-Era Best Practices

**1. Context is a first-class design concern**
- Design your context architecture early
- Document what AI has access to
- Version your context like you version code

**2. Test your context, not just your prompts**
- Print what AI actually receives
- Validate data quality
- Test with real edge cases

**3. Build feedback loops from day one**
- Measure what matters
- Collect user feedback
- Iterate based on data

**4. Start simple, evolve based on real usage**
- Don't over-engineer upfront
- Ship to learn what context matters
- Add sophistication as needs emerge

**5. Context > prompts, but both matter**
- A great prompt with bad context fails
- An okay prompt with good context works
- Perfect is both, but prioritize context

---

## Key Takeaways

✅ **Context (data, tools, memory, constraints) matters more than prompts**
✅ **Design the environment AI operates in, not just the instructions**
✅ **Build feedback loops—AI improves through iteration, not perfect prompts**
✅ **Start simple, ship to learn, add sophistication based on real needs**
✅ **Validate context quality, not just output quality**

**Bottom line:** The future of AI products isn't prompt libraries. It's systems that give AI the right context to solve problems iteratively and improve through real usage.

---

## Related Frameworks

- **[Prompt Engineering for PMs](prompt-engineering-for-pms.md)** - How prompts fit into the bigger picture
- **[AI Evals](../ai/ai-evals.md)** - Systematic validation of AI outputs
- **[Continuous Calibration](continuous-calibration.md)** - Building feedback loops into products
- **[AI Unit Economics](ai-unit-economics.md)** - Cost implications of context design

## Further Reading

- **Anthropic:** [Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- **Phil Schmid:** [Context Engineering](https://www.philschmid.de/context-engineering)
