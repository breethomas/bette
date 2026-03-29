# Pricing Strategy

A thinking tool for pricing decisions. Not a textbook -- a framework for when a specific pricing question is on the table.

## Pricing Models

Each model encodes a different relationship between value and payment. Pick the one that matches how customers experience value.

| Model | When It Fits | Watch Out For |
|-------|-------------|---------------|
| **Per-seat** | Value scales with people using it. Collaboration tools, CRMs. | Discourages adoption. Users share logins. Penalizes the behavior (more users) you want to encourage. |
| **Usage-based** | Value correlates directly with consumption. APIs, infrastructure, messaging. | Revenue is unpredictable for both sides. Customers fear runaway bills. Requires metering infrastructure. |
| **Tiered** | Distinct customer segments with different needs and willingness to pay. Most B2B SaaS. | Too many tiers create confusion. Too few leave money on the table. The middle tier should be the target, not the default. |
| **Freemium** | Product has a natural free use case that leads to paid. Network effects help. | Free users cost money. If conversion is below 2-5%, the free tier is a charity, not a funnel. Must gate on value, not annoyance. |
| **Reverse trial** | Full product experience creates switching costs. Users who try everything convert better than users who start limited. | Requires a clear "aha" within the trial window. If the product takes months to show value, reverse trial just delays churn. |
| **Flat-rate** | Simplicity is a competitive advantage. Buyer hates complexity. One clear promise. | Leaves money on the table from heavy users. Hard to expand revenue without new products. |

The right model often combines elements. Per-seat with usage caps. Tiered with add-ons. The question is always: does the pricing structure align with how the customer gets value?

## Willingness-to-Pay Research

You cannot set prices from a spreadsheet. You need data on what customers will actually pay. Three approaches, from rigorous to fast.

### Van Westendorp Price Sensitivity Meter

Four questions, asked to a representative sample:

1. At what price would this be **so cheap** you'd question the quality?
2. At what price is this a **bargain** -- a great deal for what you get?
3. At what price is this **getting expensive** -- you'd still consider it but would think hard?
4. At what price is this **too expensive** -- you'd never buy it?

Plot the cumulative distributions. The intersections reveal the acceptable price range, the optimal price point (where "too cheap" meets "too expensive"), and the indifference price (where "bargain" meets "getting expensive"). The range between optimal and indifference is your pricing sweet spot.

Works best with 100+ responses. Below that, use it directionally, not precisely.

### Gabor-Granger

Show a specific price point. Ask: would you buy at this price? If yes, increase. If no, decrease. Repeat across respondents at different starting points. Produces a demand curve -- what percentage of customers convert at each price.

Simpler than Van Westendorp. Better for validating a specific price than exploring the full range.

### Customer Interviews

When you don't have survey scale, direct conversation works. Key questions:

- "What are you paying now for [alternative/competitor/workaround]?"
- "What would you stop using if you had to cut budget by 20%?"
- "If this cost $X, what would need to be true for that to feel worth it?"

Listen for anchoring to current spend, not to value delivered. Customers anchor to what they pay today, not what the product is worth to them. Push past the anchor.

**Source:** Madhavan Ramanujam, *Monetizing Innovation* -- the definitive work on pricing research in product development. Core argument: pricing conversations belong before building, not after.

## Packaging

### Good/Better/Best

The most common B2B SaaS structure. Design principles:

- **Good** should be a real product, not a crippled demo. It either serves a genuine segment or acts as the entry point to a land-and-expand motion.
- **Better** is the target tier. Most customers should land here. Design it first, then derive Good (subtract) and Best (add).
- **Best** is for customers who self-select on budget or need. Premium features should be things that are expensive to deliver or valuable only at scale, not things you artificially gate.

### When Bundling Helps vs. Hurts

**Bundle when:** features are complementary (using one makes the other more valuable), discovery is a problem (customers don't know they need it), or simplicity drives conversion.

**Unbundle when:** customer segments have sharply different needs, some features have high marginal cost, or customers perceive they're paying for things they don't use.

**Source:** Patrick Campbell (ProfitWell/Paddle) -- extensive research on packaging and its impact on SaaS retention and expansion.

## When to Change Pricing

### Signals

- **High conversion rate, low expansion.** Price is too low. Customers aren't stretching.
- **High churn at first renewal.** Value gap -- the price exceeded the realized value. Fix the product or lower the price.
- **Feature gating frustration.** Customers hitting walls on the wrong features. The packaging is wrong, not the price.
- **Sales cycle lengthening.** May indicate price is above the "no-brainer" threshold for the buyer's authority level.
- **Competitor pricing shift.** Only relevant if customers actually comparison-shop. Many don't.

### Process

1. Segment the change. Don't reprice everyone at once.
2. Grandfather existing customers (or give extended notice). Trust is more expensive to rebuild than the revenue from forcing a price increase.
3. Tie the increase to new value. "We added X, Y, Z -- the new price reflects that."
4. Test with new customers first. Existing customer pricing changes are a separate, harder conversation.

### Communication

Direct. Specific. Lead with value, not apology. "We're increasing prices" is worse than "We're launching a new tier that includes [specific things] at [price]."

Never: surprise customers, hide the change in ToS updates, or raise prices without adding value. The trust cost exceeds the revenue gain.

## Growth vs. Monetization

The core tension: optimizing for users (growth) and optimizing for revenue (monetization) eventually conflict.

**Optimize for growth when:**
- Network effects are present (more users = more value for all users).
- Market share matters more than revenue in the current phase.
- The product hasn't found PMF yet -- don't optimize revenue on a product people don't love.
- Land-and-expand is the strategy -- get in cheap, prove value, expand.

**Optimize for monetization when:**
- PMF is established and retention is strong.
- The growth rate has plateaued and the business needs margin.
- Investors or the market expect a path to profitability.
- Free/cheap users are consuming resources without converting.

**The Elena Verna test:** "Would this pricing change make our best customers happier or unhappier?" If the answer is unhappier, the change is extracting value, not creating it. Extraction works once. Creation compounds.

**Source:** Elena Verna -- extensive writing on pricing within PLG motions, particularly the tension between growth metrics and revenue metrics.

---

*Frameworks are thinking tools. They clarify the question, they don't answer it. The answer comes from your customers, your data, and your judgment about what to optimize for right now.*
