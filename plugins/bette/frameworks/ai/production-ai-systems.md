# Production AI Systems

**Source:** Chip Huyen (huyenchip.com, "Designing Machine Learning Systems", Lenny's Newsletter appearances)

**Last Updated:** January 2025

---

## Overview

Building production AI systems is fundamentally different from ML research or demos. This framework helps PMs think about what it takes to deploy reliable AI at scale.

**Core insight:** The gap between a demo and a product is production engineering—monitoring, cost management, data quality, UX, and reliability.

---

## The Demo-to-Product Gap

### What Works in a Demo
- Latest frontier model (expensive)
- Hand-picked test cases
- Happy path only
- No cost constraints
- Manual fixes when it breaks
- "It works on my machine"

### What Production Requires
- Cost-optimized model selection
- Comprehensive testing (happy path + edge cases + adversarial)
- Graceful failure handling
- Cost per user at scale
- Automated monitoring and alerting
- Reliable infrastructure

**For PMs:** Always ask "What's our path from demo to production?" Don't celebrate working prototypes as shipping.

---

## Key Framework: The AI Engineering Stack

### 1. Model Selection & Optimization

**The hierarchy (cheapest to most expensive):**

1. **Prompt Engineering**
   - Start here always
   - Iterate on prompts and instructions
   - Test different phrasings
   - Cost: Minimal (just API calls)

2. **Context Engineering**
   - Better data retrieval (RAG)
   - Improved chunking strategies
   - Metadata enrichment
   - Cost: Low to medium

3. **Tool Use / Function Calling**
   - Let AI call external systems
   - Augment with real-time data
   - Structured outputs
   - Cost: Medium

4. **Fine-tuning**
   - Custom model adaptation
   - Only when above approaches fail
   - Cost: High (training + serving)

**PM decision framework:**
```
Problem → Try prompting → Still not working?
→ Try better data/context → Still not working?
→ Try tool use → Still not working?
→ THEN consider fine-tuning
```

**Common mistake:** Jumping to fine-tuning without exhausting simpler approaches.

**See also:** For the strategic product decision of when to use RAG vs fine-tuning based on your use case characteristics (data changeability, query volume, style needs), see `frameworks/ai/fine-tuning-vs-rag.md`.

---

### 2. Data Quality > Tool Selection

**What matters most:**

**Data preparation:**
- Thoughtful chunking (how you split documents)
- Formatting (Q&A pairs vs raw text)
- Metadata enrichment (tags, categories, dates)
- Deduplication and cleaning
- Relevance filtering

**What matters less:**
- Which vector database you use
- Latest embedding model
- Fancy similarity algorithms

**For PMs:**
- Spend 80% of time on data quality
- Spend 20% on tool selection
- Most teams do the opposite

**Questions to ask:**
- "How are we chunking our data?"
- "What metadata are we including?"
- "How do we handle duplicates or outdated content?"
- "What's our data refresh strategy?"

---

### 3. System-Level Optimization

**AI is one component of a larger system.**

**Optimize for:**
- End-to-end latency (not just model inference time)
- Total cost per user interaction
- Reliability (what % of requests succeed?)
- User experience (including when AI fails)

**Example:**
- Model takes 2 seconds to respond
- But data retrieval takes 5 seconds
- And formatting response takes 1 second
- Total: 8 seconds user experience

**Where to optimize?** Not just the model.

**For PMs:** Map the entire user journey. Find bottlenecks. Optimize system-wide.

---

### 4. Production Monitoring

**What to monitor:**

**Quality metrics:**
- Response accuracy/relevance
- Hallucination rate
- User satisfaction (thumbs up/down)
- Task completion rate

**Performance metrics:**
- Latency (p50, p90, p99)
- Throughput (requests/second)
- Error rate
- Availability/uptime

**Cost metrics:**
- Cost per request
- Cost per user per month
- Total inference costs
- Data storage/retrieval costs

**Data health:**
- Distribution shift (is prod data different from training data?)
- Feature drift
- Data freshness

**For PMs:**
- Define acceptable ranges for each metric
- Set up alerts when metrics degrade
- Review dashboards weekly
- Every incident becomes an eval case (see `ai-evals.md`)

---

## Real-Time vs Batch vs Near-Real-Time

**Real-time ML:** Predictions made instantly when requested

**Batch ML:** Predictions made in bulk, stored, retrieved later

**Near-real-time:** Predictions made frequently (hourly, every 15 min) and cached

**Complexity comparison:**

| Aspect | Batch | Near-Real-Time | Real-Time |
|--------|-------|----------------|-----------|
| Infrastructure | Simple | Medium | Complex |
| Latency | Hours to days | Minutes to hours | Milliseconds |
| Cost | Low | Medium | High |
| Feature freshness | Stale | Somewhat fresh | Very fresh |
| Use cases | Recommendations, reports | Feeds, dashboards | Fraud detection, pricing |

**PM decision framework:**
- Do users need instant results? → Real-time
- Can we refresh every hour? → Near-real-time (much cheaper!)
- Can we pre-compute? → Batch (cheapest)

**Common mistake:** Building real-time when near-real-time works fine. Real-time is 10x harder and more expensive.

---

## Cost Optimization Strategies

**AI products have marginal costs.** Unlike traditional SaaS, each user interaction costs money (inference).

### Model Selection
- Don't always use GPT-4 / Claude Opus
- Use cheaper models (GPT-3.5, Claude Haiku) where quality suffices
- Route requests: simple queries → cheap model, complex → expensive model

### Caching
- Cache frequent queries/responses
- Reuse computations when possible
- Store embeddings, don't recompute

### Batching
- Process multiple requests together (cheaper)
- Trade latency for cost when acceptable

### Prompt Optimization
- Shorter prompts cost less
- Remove unnecessary context
- Don't include full documents when summaries work

**For PMs:**
- Model cost at 10x scale, 100x scale
- What's cost per user per month?
- What % of revenue is inference cost?
- Can we sustain this at scale?

See `frameworks/ai-era-practices/ai-unit-economics.md` for monetization strategies.

---

## Handling AI Failures Gracefully

**AI will fail.** Models hallucinate, give wrong answers, or refuse to respond.

### UX Strategies

**Confidence indicators:**
- "I'm not sure, but..." (when model is uncertain)
- Show sources (let users verify)
- Offer fallback options

**Human-in-the-loop:**
- AI suggests, human approves (low agency)
- Human can override AI decisions
- Escalate to human when AI is uncertain

**Graceful degradation:**
- If AI fails, what's the fallback?
- Can the feature work without AI?
- Don't make AI a single point of failure

**Error messages:**
- "I couldn't find an answer" (not "An error occurred")
- Offer alternative paths forward
- Maintain user trust

**For PMs:** Design the failure experience as carefully as the success experience.

**See also:** `frameworks/ai-era-practices/continuous-calibration.md` (start low agency, earn autonomy)

---

## Data Distribution Shift

**The problem:** Production data differs from training data. Model quality degrades over time.

**Causes:**
- User behavior changes
- New edge cases emerge
- Seasonal patterns
- Product changes
- Adversarial users

**Detection:**
- Monitor input distributions
- Track output quality metrics
- Watch for performance degradation
- User feedback trends

**Solutions:**
- Continuous model retraining
- Update evals with new cases (see `ai-evals.md`)
- Calibrate prompts and context
- Collect production data for improvement

**For PMs:**
- Expect quality to degrade
- Plan for continuous improvement
- Budget for monitoring and retraining
- This is ongoing work, not one-time

---

## Pre-training vs Post-training (Decision Framework)

**Pre-training:** What the model learned during foundational training (GPT-4, Claude, etc.)

**Post-training:** Adaptation for specific tasks (fine-tuning, RLHF, prompt engineering)

### When to Use Each Approach

**Prompt Engineering (Start Here):**
- ✅ Fastest iteration
- ✅ No training required
- ✅ Works for most cases
- ❌ Limited by base model capabilities

**Context Engineering (RAG, Better Data):**
- ✅ Inject domain knowledge
- ✅ Keep data fresh
- ✅ No model training
- ❌ Adds retrieval complexity

**Tool Use / Function Calling:**
- ✅ Access external systems
- ✅ Get real-time data
- ✅ Structured outputs
- ❌ Requires API integration

**Fine-tuning (Last Resort):**
- ✅ Adapts model behavior deeply
- ✅ Can improve on narrow tasks
- ❌ Expensive (training + serving)
- ❌ Slow iteration
- ❌ Hard to maintain multiple versions
- ❌ May degrade on other tasks

**Chip's guidance:** "Fine-tuning should be your last resort. Exhaust simpler optimization approaches first."

---

## Platform Reliability Over Flashy Tools

**Build infrastructure that enables experimentation.**

**Good platform:**
- Easy to swap models (OpenAI → Anthropic → local)
- Easy to test prompt variations
- Easy to A/B test approaches
- Version control for prompts and configs
- Reproducible experiments
- Fast deployment cycles

**Bad platform:**
- Locked into specific vendor
- Hard to change anything
- No experimentation framework
- Manual deployments
- Can't reproduce results

**For PMs:**
- Invest in abstraction layers
- Don't hard-code vendor specifics
- Build for iteration speed
- Make experimentation easy

**Chip's insight:** "A solid platform should facilitate easy tool swapping as requirements evolve."

---

## When to Apply This Framework

Use this framework when:

✅ **Planning AI features**
- What's our path from demo to production?
- What infrastructure do we need?

✅ **Evaluating AI vendors**
- How do we avoid lock-in?
- What's the total cost at scale?

✅ **Deciding build vs buy**
- Should we fine-tune or use off-the-shelf?
- Can we solve this with better prompts?

✅ **Monitoring AI quality**
- What metrics matter?
- How do we detect degradation?

✅ **Optimizing costs**
- Where are we spending most?
- What can we cache, batch, or simplify?

✅ **Handling failures**
- How should our UX handle AI errors?
- What's our fallback experience?

---

## Related Frameworks

**Complements:**
- `frameworks/ai/ai-evals.md` - How to test AI quality systematically
- `frameworks/ai/fine-tuning-vs-rag.md` - Strategic decision framework for choosing RAG vs fine-tuning based on product needs
- `frameworks/ai-era-practices/ai-unit-economics.md` - Cost and monetization
- `frameworks/ai-era-practices/continuous-calibration.md` - Ongoing AI improvement

**Aligns with:**
- **Marty Cagan's Four Risks** - Feasibility and viability risks for AI
- **Teresa Torres' Discovery** - User feedback informs what to optimize

---

## Practical Checklist for PMs

### Before Building
- [ ] Can we solve this with prompting alone?
- [ ] What's our data quality strategy?
- [ ] What's the cost per user at 10x scale?
- [ ] How will we monitor quality in production?
- [ ] What's our failure UX?

### During Development
- [ ] Are we testing on realistic data (not just happy path)?
- [ ] Have we tried simpler approaches before fine-tuning?
- [ ] Can we swap vendors/models easily?
- [ ] What's our deployment and rollback plan?

### After Launch
- [ ] What metrics are we tracking?
- [ ] How are we collecting failure cases?
- [ ] What's our retraining/calibration schedule?
- [ ] Are we seeing distribution shift?
- [ ] What's our actual cost per user?

---

## Common PM Mistakes

❌ **"Let's fine-tune immediately"**
→ ✅ Start with prompting, exhaust simpler approaches first

❌ **"We need the best model"**
→ ✅ Use the cheapest model that meets quality bar

❌ **"The demo works, ship it"**
→ ✅ Plan for monitoring, cost, failures, scale

❌ **"AI engineers handle this"**
→ ✅ PMs own quality bar, cost model, UX, success criteria

❌ **"We'll figure out monitoring later"**
→ ✅ Monitoring is critical from day 1

❌ **"Vector database choice is critical"**
→ ✅ Data quality matters 10x more than tool selection

---

## Key Questions for PMs

**On approach:**
- "Have we tried prompt engineering before fine-tuning?"
- "What's our data quality strategy?"
- "Are we optimizing the system or just the model?"

**On costs:**
- "What's our cost per user per month at 10x scale?"
- "Can we use a cheaper model for some requests?"
- "What can we cache or batch?"

**On reliability:**
- "What happens when the AI fails?"
- "How do we monitor quality degradation?"
- "What's our fallback experience?"

**On infrastructure:**
- "Can we swap vendors/models easily?"
- "How fast can we iterate on prompts?"
- "Are we locked into specific tools?"

---

## Further Reading

**Chip Huyen's blog:**
- "Designing Machine Learning Systems" (O'Reilly book)
- "Real-Time Machine Learning: Challenges and Solutions"
- "Common Pitfalls When Building Generative AI Applications"
- "Data Distribution Shifts in Production ML"

**Lenny's Newsletter:**
- "AI Engineering 101 with Chip Huyen"
- "Why AI Evals Are the Hottest New Skill"

---

## Bottom Line

**Production AI is about reliable systems, not just accurate models.**

Start with prompting. Focus on data quality. Optimize the whole system. Monitor continuously. Handle failures gracefully. Build platforms that enable iteration.

Fine-tuning is the last resort. Most AI failures are UX problems. Talk to users, look at data, and ship reliable products.
