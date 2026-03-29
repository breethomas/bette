---
name: four-fits
description: Find which fit is broken before you burn cash scaling. Brian Balfour's framework for validating sustainable growth readiness.
---

# Four Fits

**Before you scale, all four fits must work. If one is broken, scaling fails.**

Most companies scale too early. They have product-market fit and think they're ready. They're not. You need all four:

1. **Market ↔ Product** - Do customers want this?
2. **Product ↔ Channel** - Can you reach customers efficiently?
3. **Channel ↔ Model** - Can your business model support acquisition costs?
4. **Model ↔ Market** - Can you monetize this market profitably?

**One broken fit = don't scale yet.** Fix it first.

**Philosophy:** "All four fits must align for $100M+ growth. Scaling with misaligned fits burns cash." - Brian Balfour

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 FOUR FITS ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Before you scale, all four fits must work.

What do you want to do?

  1. Full assessment
     → Evaluate all four fits

  2. Diagnose growth blocker
     → Find which fit is broken

  3. Pre-scale validation
     → Checklist before spending

  4. Specific market segment
     → Analyze fit for new segment

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/four-fits
```

**Examples:**
- `/four-fits` - Full assessment of current state
- `/four-fits --validate` - Pre-scale validation checklist
- `/four-fits --diagnose` - Identify which fit is blocking growth
- `/four-fits --market "SMB SaaS"` - Specify market explicitly

## What Happens

1. **Gathers context** about your product:
   - What's your market? (SMB, enterprise, consumer)
   - What's your product? (feature set, positioning)
   - What's your primary channel? (paid, viral, content, sales)
   - What's your business model? (SaaS, marketplace, freemium, transaction)

2. **Assesses each fit** independently:
   - Questions to validate fit strength
   - Evidence required
   - Common anti-patterns
   - Confidence level (Validated / Needs Work / Misaligned)

3. **Identifies misalignments:**
   - Which fits are blocking scale?
   - Where are the gaps?
   - What validation is needed?

4. **Returns** detailed assessment with:
   - Fit-by-fit analysis
   - Overall readiness score
   - Recommended fixes
   - When to scale (or not)

5. **Provides validation activities** to de-risk each fit

## Four Fits Deep Dive

### Fit #1: Market ↔ Product

**The question:** Do customers want this?

**Validation signals:**
- High retention (>80% for SaaS)
- Strong NPS (>40)
- PMF survey >40% "very disappointed"
- Organic word-of-mouth
- Customers choose you over alternatives

**Anti-patterns:**
- Low retention (<60%)
- Building features customers don't use
- Winning on price, not value

**See:** `/pmf-survey` for validation

---

### Fit #2: Product ↔ Channel

**The question:** Can we reach customers efficiently through this channel?

**Validation signals:**
- Customers discover you naturally
- CAC is sustainable (<1/3 of LTV)
- Acquisition is repeatable and scalable
- Product is suited to channel (e.g., viral product + viral channel)

**Anti-patterns:**
- CAC > LTV (unsustainable)
- Channel is saturated (CPCs rising)
- Product onboarding too slow for channel
- Can't scale channel 10x

**Channel types:**
- Paid (Google Ads, Facebook, etc.)
- Viral (referrals, word-of-mouth)
- Content (SEO, owned media)
- Sales (outbound, inside sales)

---

### Fit #3: Channel ↔ Model

**The question:** Does our business model support acquisition costs?

**Validation signals:**
- LTV/CAC > 3 (healthy)
- Payback period acceptable (< 12 months)
- Gross margins support channel costs
- Can profitably acquire at scale

**Anti-patterns:**
- LTV/CAC < 2 (unprofitable)
- Payback > 18 months (too long)
- Thin margins can't support CAC
- Model doesn't scale with volume

**See:** `/ai-cost-check` for cost modeling

---

### Fit #4: Model ↔ Market

**The question:** Can we monetize this market profitably?

**Validation signals:**
- Market can afford your pricing
- TAM is large enough for ambitions
- Can expand within accounts
- Model aligns with market buying behavior

**Anti-patterns:**
- Market can't afford pricing (too expensive for segment)
- TAM too small for goals
- No expansion revenue (one-and-done)
- Mismatch in sales cycle vs model

---

## Diagnostic Mode

```
/four-fits --diagnose
```

Helps identify WHICH fit is blocking growth:

**Symptoms → Diagnosis:**

**Low retention, high churn**
→ Market-Product fit issue
→ Run: `/pmf-survey`

**High CAC, can't scale acquisition**
→ Product-Channel fit issue
→ Consider: Different channel or improve activation

**Unprofitable customer acquisition**
→ Channel-Model fit issue
→ Run: `/ai-cost-check` or raise prices

**Can't expand, limited TAM**
→ Model-Market fit issue
→ Consider: Different market segment or business model

---

## Related Commands

- `/pmf-survey` - Validate Market-Product fit specifically
- `/growth-loops` - Design Product-Channel fit via loops
- `/lno-prioritize` - Prioritize work to fix misaligned fits
- `/ai-cost-check` - Validate Channel-Model economics

## Learn More

**Full frameworks:**
- `frameworks/growth/four-fits.md` - Brian Balfour's complete framework
- `frameworks/growth/growth-loops.md` - Elena Verna on sustainable growth
- `frameworks/measurement/pmf-survey.md` - Validate Market-Product fit

---

**Framework:** Four Fits (Brian Balfour)
**Best for:** Validating sustainable scaling readiness
**Key insight:** "All four fits must align for $100M+ growth. Scaling with misaligned fits burns cash."
**Remember:** Fix fits in order - Market-Product first, then Product-Channel, then Channel-Model, then Model-Market. Don't skip ahead.
