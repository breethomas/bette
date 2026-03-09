# Fine-tuning vs RAG: A PM Decision Framework

**Category:** AI Product Strategy
**Last Updated:** January 2025

## Overview

When building AI features, PMs face a critical technical decision: should you customize a model through fine-tuning, or should you provide better context through RAG (Retrieval-Augmented Generation)?

**This isn't an engineering decision—it's a product strategy decision** that affects:
- Unit economics (cost per interaction)
- Time to market
- Maintenance burden
- Feature quality and accuracy
- Competitive moats

---

## What PMs Need to Know

### Fine-tuning
**What it is:** Training a pre-existing model on your specific data to change how it behaves.

**What it's good for:**
- Teaching a model your **style, tone, or format**
- Making models smaller/cheaper while maintaining quality
- Encoding specialized knowledge into model parameters
- Reducing tokens needed per request (lower costs at scale)

**What it's NOT good for:**
- Frequently changing information (you'd need to retrain constantly)
- Large knowledge bases that change often
- Situations requiring source citations
- Getting started quickly (requires training time and data prep)

### RAG (Retrieval-Augmented Generation)
**What it is:** Giving a model relevant context from your documents/data at query time, rather than training it.

**What it's good for:**
- **Dynamic, frequently-updated information** (docs, product catalogs, support tickets)
- Large knowledge bases (thousands+ of documents)
- Providing citations/sources for answers
- Quick iteration (no retraining needed)
- Situations where you need to explain "why" the AI said something

**What it's NOT good for:**
- Teaching consistent brand voice or writing style
- High-frequency, repeated queries (you pay for retrieval every time)
- When you need the fastest possible response times
- Learning complex reasoning patterns

---

## The Decision Framework

### Use RAG When:

✅ **Your data changes frequently**
- Support documentation
- Product catalogs
- News/current events
- Regulatory/compliance docs
- Example: Customer support chatbot accessing latest help articles

✅ **You need to cite sources**
- Legal/compliance requirements
- Building trust through transparency
- Audit trails for AI decisions
- Example: Research assistant citing specific papers

✅ **You have large, growing knowledge bases**
- 1000s+ of documents
- Regularly adding new content
- Multiple data sources
- Example: Enterprise search across company wikis

✅ **You want to iterate fast**
- MVP/testing phase
- Frequently changing requirements
- Learning what information matters
- Example: New AI feature, still figuring out what users need

**When to worry:** RAG costs scale with query volume (retrieval + larger prompts). At massive scale, this can be expensive.

---

### Use Fine-tuning When:

✅ **You need consistent style/tone/format**
- Brand voice that doesn't sound "AI-ish"
- Specific output formatting (JSON, markdown, etc.)
- Domain-specific language patterns
- Example: AI writing product descriptions in your brand's voice

✅ **You're making the same type of request repeatedly at scale**
- High query volume (100K+ per day)
- Similar prompts over and over
- Predictable use cases
- Example: Automated email response generation

✅ **You want to use smaller/cheaper models**
- Fine-tuned GPT-4o-mini can outperform vanilla GPT-4
- Significantly lower per-query costs
- Faster response times
- Example: High-volume classification tasks

✅ **Your knowledge is relatively static**
- Domain expertise that doesn't change often
- Historical data analysis
- Specialized reasoning patterns
- Example: Medical diagnosis assistant (medical knowledge is stable)

**When to worry:** Fine-tuning requires upfront investment (data prep, training time, evaluation). Updates require retraining. Not ideal for rapidly changing domains.

---

### Use BOTH When:

🎯 **The Optimal Pattern (for many production systems):**

**Fine-tune for:** Style, tone, formatting, reasoning patterns
**RAG for:** Facts, current information, specific details

**Example: Customer support AI**
- Fine-tuned to respond in your brand voice, maintain conversation flow, handle edge cases gracefully
- RAG to access latest product docs, recent ticket history, current promotions

**Example: Content generation tool**
- Fine-tuned to write in your brand's style and follow your editorial guidelines
- RAG to incorporate latest product features, current campaigns, recent news

**Why this works:** You get the best of both—consistent quality from fine-tuning + fresh, accurate information from RAG.

---

## Cost Considerations

### RAG Costs Scale With:
- Number of queries (every query requires retrieval)
- Amount of context retrieved (more tokens = more cost)
- Complexity of retrieval (vector search, reranking)

**Rule of thumb:** Better for low-to-medium query volumes, especially if information changes frequently.

### Fine-tuning Costs:
- Upfront: Data preparation, training compute, evaluation
- Ongoing: Cheaper per-query (smaller model, fewer tokens)
- Updates: Must retrain periodically (time + compute)

**Rule of thumb:** Better for high query volumes with relatively stable patterns.

### Break-even Example:
If you're making 1M requests/month:
- RAG might cost $5-10K/month (GPT-4 + retrieval overhead)
- Fine-tuned GPT-4o-mini might cost $1-2K/month + $500 retraining quarterly
- **Fine-tuning wins on economics at scale**

---

## Common Mistakes PMs Make

❌ **"We need fine-tuning because RAG isn't accurate enough"**
→ Usually the problem is bad retrieval (wrong chunks, poor search), not RAG itself. Fix retrieval first.

❌ **"Fine-tuning will teach the model our company knowledge"**
→ Fine-tuning is better for *how* to respond, not *what* to know. Use RAG for knowledge.

❌ **"We should fine-tune first since it's more advanced"**
→ Start with RAG. It's faster to test, easier to debug, and you can iterate quickly. Fine-tune later if needed.

❌ **"We need to choose one approach"**
→ The best production systems use both. They're complementary, not mutually exclusive.

---

## Decision Tree

```
Question: Does your AI feature need to access frequently changing information?
├─ YES → Start with RAG
│  └─ High query volume (100K+/day) + consistent style needed?
│     └─ YES → Add fine-tuning for style/efficiency
│     └─ NO → RAG alone is fine
│
└─ NO → Is there a consistent pattern/style/format you need?
   ├─ YES → Consider fine-tuning
   │  └─ Need to cite sources or explain reasoning?
   │     └─ YES → Add RAG for transparency
   │     └─ NO → Fine-tuning alone works
   │
   └─ NO → Start with base model + prompt engineering
      └─ Still not good enough?
         └─ Try RAG first, fine-tuning second
```

---

## Examples from Real Products

### GitHub Copilot
- **Fine-tuned:** On code patterns, syntax, common programming practices
- **No RAG needed:** Code patterns are stable; they're teaching "how to write code"

### Notion AI
- **RAG:** Accesses your specific workspace documents
- **Fine-tuned:** For Notion's writing style and output formatting
- **Why both:** Needs your current docs (RAG) but consistent quality (fine-tuning)

### ChatGPT with Web Search
- **Base model:** Pre-trained on internet-scale data
- **RAG (web search):** For current events and recent information
- **Why RAG:** Web changes constantly; can't fine-tune fast enough

### Customer Support Chatbot (typical implementation)
- **RAG:** Latest product docs, recent tickets, current policies
- **Fine-tuned:** Company voice, handling difficult customers, edge cases
- **Why both:** Docs change weekly (RAG) but tone should be consistent (fine-tuning)

---

## Questions to Ask Your Engineering Team

1. **"What's our expected query volume at scale?"** (affects cost equation)
2. **"How often does our source data change?"** (affects RAG vs fine-tuning choice)
3. **"What's our latency budget?"** (fine-tuning usually faster)
4. **"Do we need to explain AI decisions?"** (RAG better for citations)
5. **"How much training data do we have?"** (need 50-500+ examples for good fine-tuning)

---

## When to Revisit This Decision

🔄 **Revisit quarterly or when:**
- Query volume increases 10x
- Data update frequency changes significantly
- User feedback indicates quality/accuracy issues
- Cost becomes a major concern
- Latency requirements change

---

## Integration with Other Frameworks

**See also:**
- `/frameworks/ai/production-ai-systems.md` - Chip Huyen's hierarchy: Always try prompt engineering before RAG, RAG before fine-tuning
- `/frameworks/ai/ai-evals.md` - How to evaluate which approach is working better
- `/frameworks/discovery/four-risks.md` - Feasibility Risk includes cost modeling and technical constraints

**Related to:**
- **Value Risk:** Does fine-tuning actually improve user outcomes? Or just engineering complexity?
- **Feasibility Risk:** Do we have the data/expertise for fine-tuning? Can our team maintain RAG infrastructure?
- **Business Viability Risk:** What are unit economics at scale? Can we afford our approach?

---

## Bottom Line for PMs

**Default path for most products:**
1. Start with prompt engineering (cheapest, fastest)
2. Add RAG if you need external knowledge (still relatively fast)
3. Add fine-tuning if you need consistent style at scale (more investment)

**The trap:** Jumping to fine-tuning because it sounds more "advanced." RAG is often the right answer.

**The opportunity:** Using both fine-tuning + RAG gives you the best product—but only if your scale justifies the complexity.

**Remember:** This is a product decision about user experience and unit economics, not just a technical choice.
