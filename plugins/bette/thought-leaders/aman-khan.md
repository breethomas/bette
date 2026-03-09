# Aman Khan

**Focus:** AI Evals, AI Product Management, Building Reliable AI Systems

**Why He Matters:** Aman is at the forefront of how to build and ship reliable AI products. He writes extensively about the challenges PMs face with AI systems and how to address them through comprehensive evaluation strategies.

---

## Core Philosophy

**"You can't ship AI products without evals. Even simple evals are better than no evals."**

AI systems are probabilistic, not deterministic. Traditional software testing doesn't work. You need comprehensive evaluation systems to catch failures before production.

## Key Frameworks

### AI Evals (Evaluations)
Systematic testing of AI systems across diverse inputs and scenarios.

**Types:**
- Unit evals (single component)
- Integration evals (end-to-end)
- Regression evals (don't break existing)
- Human evals (subjective quality)

**See:** `frameworks/ai/ai-evals.md`

### Failure Mode Cataloging
Identify and test for AI-specific failures:
- Hallucinations (making up facts)
- Prompt injection (users bypassing instructions)
- Off-topic responses
- Inconsistent behavior
- Degraded performance over time

### Continuous Calibration
AI products need ongoing tuning, not just deployment.
- Monitor quality in production
- Collect failures
- Add to eval dataset
- Improve prompts/models
- Redeploy

## What Makes Him Different

**Traditional software:** Write tests → Code → Deploy → Done

**Aman's AI approach:** Build evals → Build feature → Test against evals → Deploy → Monitor → Calibrate → Repeat

**Key insight:** AI products are never "done" - they need continuous calibration based on real-world usage.

## Best For

- Building AI features with confidence
- Testing AI quality systematically
- Catching failures before users do
- Monitoring AI systems in production
- Ensuring reliable AI experiences

## AI-Era Necessity

This isn't "nice to have" - it's essential for AI products:
- Without evals, you're shipping blind
- Users will find your failure modes (embarrassingly)
- Quality degrades over time without monitoring
- Can't improve what you don't measure

## Key Insights from Aman

### "Our AI still couldn't do basic math"
Story about discovering their AI failed at arithmetic despite seeming sophisticated.
**Lesson:** Test the basics, not just the advanced cases.

### LLM-as-Judge
Use another LLM to evaluate responses at scale.
Faster than human review, better than rule-based checks.

### Start with Small Eval Sets
Don't need 10,000 test cases on day 1.
Start with 20-50 critical cases. Expand over time.

### Eval Before Building
Define success criteria and test cases BEFORE implementing.
Forces clarity on what "good" means.

## Quotes

> "The difference between a demo and a product is a comprehensive eval system."

> "Every production incident should become an eval case."

> "Evals are to AI products what unit tests are to software - but even more critical."

> "If you can't measure it, you can't ship it responsibly."

## Further Learning

**Start here:**
- Substack: [amankhan1.substack.com](https://amankhan1.substack.com)
- Posts on building AI products, evals, and PM lessons

**Deep dives:**
- "How we discovered our AI still couldn't do basic math"
- "Building evals for AI products"
- "LLM-as-Judge: Using AI to evaluate AI"

**Follow for updates:**
- Substack (primary platform)
- LinkedIn: [linkedin.com/in/aman-khan](https://www.linkedin.com/in/aman-khan)
- Twitter/X: @amankhan1

## When to Apply His Thinking

- ✅ Building any AI-powered feature
- ✅ Deploying LLMs in production
- ✅ Testing AI quality
- ✅ Ensuring reliable AI experiences
- ✅ Monitoring AI systems

## Practical Tips from Aman

1. **Evals before building**: Define success criteria first
2. **Test failure modes**: Happy path + edge cases + adversarial
3. **Start small**: 20-50 cases better than perfect dataset later
4. **Automate**: Run on every change, before every deploy
5. **Monitor production**: Every failure becomes an eval case
6. **Human review matters**: Automated evals miss subtle issues

## Related Thinkers

Works well with:
- **Marty Cagan** (Four Risks) - Evals address feasibility and value risk for AI
- **Teresa Torres** (Discovery) - User feedback informs eval cases
- **Modern PM practices** - Evals are the "quality assurance" for AI era

## Common Misunderstandings

❌ "Evals take too long" - Start small, automate, expand over time

❌ "GPT-4 is perfect" - All models have failure modes, test them

❌ "We'll test in production" - Users will find embarrassing failures

❌ "Evals are just for ML engineers" - PMs need to own quality criteria

## Aman's Focus Areas

**AI Product Management:**
- How PMs should think differently about AI features
- Balancing speed with quality
- Defining success for probabilistic systems

**Evals & Testing:**
- Building comprehensive test datasets
- Automated evaluation strategies
- LLM-as-judge techniques

**Production AI:**
- Monitoring and alerting
- Continuous calibration
- Handling failures gracefully

**On AI Tools:** Acknowledges tools evolve rapidly - principles matter more than specific tools

## Why This Matters for PMs

**Traditional PM skills don't cover:**
- How to test probabilistic systems
- How to define "good" for subjective outputs
- How to catch hallucinations
- How to calibrate continuously

**Aman provides:**
- Frameworks for AI quality
- Eval strategies that work
- Production monitoring approaches
- Real-world lessons from shipping AI

## Key Concepts

### Golden Dataset
Collection of "known good" test cases.
Run before each deployment.
Alert if quality regresses.

### Eval Coverage
Not just happy path - need:
- Edge cases (unusual but valid)
- Adversarial (trying to break it)
- Boundary (out of scope)
- Regression (don't break existing)

### Continuous Calibration (CC/CD)
Like CI/CD but for AI:
- Continuous monitoring
- Continuous calibration
- Deploy improvements regularly

---

**Bottom line:** Aman teaches you how to build AI products that actually work reliably in production.

Build evals first. Test comprehensively. Monitor continuously. Calibrate regularly.
