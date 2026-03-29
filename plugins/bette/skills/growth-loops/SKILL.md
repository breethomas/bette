---
name: growth-loops
description: Find your growth loop or stay stuck in linear acquisition hell. Identify viral, content, network, and paid loop opportunities using Elena Verna's framework.
---

# Growth Loops

**If you're buying all your growth, you're doing it wrong.**

Most PMs think about growth as a funnel: spend money → acquire users → hope they stick. That's expensive and doesn't compound.

Growth loops are different: users create value → that value attracts more users → they create more value. It compounds.

**Philosophy:** "Growth isn't a funnel that leaks. It's a loop that compounds." - Elena Verna

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 GROWTH LOOPS ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Growth that compounds beats growth you pay for every time.

What do you want to do?

  1. Identify loop opportunities
     → Analyze your product for potential loops

  2. Design a specific loop
     → Deep dive on viral, content, or network loop

  3. Optimize loop velocity
     → Make existing loops cycle faster

  4. Map current growth mechanics
     → Understand what's driving growth today

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## What This Does

Identifies if your product has (or could have) compounding growth:
- **Viral loops** - Users invite users
- **Content loops** - User-generated content attracts organic traffic
- **Network effects** - More users = more value
- **Paid loops** - Revenue funds acquisition (only if efficient)

Then tells you which loop fits your product and how to build it.

## Usage

```
/growth-loops [product/feature]
```

**Examples:**
- `/growth-loops` - Analyze current product for loop opportunities
- `/growth-loops "referral program"` - Design loop for specific feature
- `/growth-loops --map` - Map existing user flows to loop types
- `/growth-loops --velocity` - Focus on loop speed optimization

## What Happens

1. **Understands your product:**
   - What's the core value proposition?
   - Who are the users?
   - What's the typical user journey?
   - Where does viral potential exist?

2. **Identifies loop opportunities** across 4 types:
   - **Viral loops** (users invite users)
   - **Content loops** (UGC attracts organic traffic)
   - **Network effects** (more users = more value)
   - **Paid loops** (revenue funds acquisition)

3. **Maps the loop structure:**
   - Input → Action → Output → New Input
   - Where does the cycle reinforce?
   - What makes the loop sustainable?

4. **Analyzes loop velocity:**
   - How long does one loop cycle take?
   - Faster loops compound faster
   - Optimization opportunities

5. **Returns growth loop design** with implementation suggestions

## Growth Loop Types

### 1. Viral Loops
Users invite users directly.

**Examples:**
- Dropbox referral (both get storage)
- Slack (team invites)
- Figma (share designs)

**When it fits:**
- Product has multi-player value
- Users naturally want to invite others
- Network size increases value

**Velocity:** Fast (hours to days)

---

### 2. Content Loops
User-generated content attracts organic traffic.

**Examples:**
- Yelp reviews (rank in Google)
- Pinterest pins (visual search)
- Stack Overflow answers (SEO)

**When it fits:**
- Users create public content
- Content is searchable/shareable
- Long-tail SEO opportunity

**Velocity:** Slow (weeks to months)

---

### 3. Network Effect Loops
More users = more value for everyone.

**Examples:**
- Marketplaces (more buyers → more sellers → more buyers)
- Social networks (more friends = more value)
- OpenTable (more diners → more restaurants)

**When it fits:**
- Multi-sided platform
- Value scales with total users
- Critical mass required

**Velocity:** Medium (weeks)

---

### 4. Paid Loops
Revenue funds acquisition.

**Examples:**
- SaaS with positive CAC/LTV
- E-commerce with repeat purchases
- Subscription products

**When it fits:**
- LTV > CAC (healthy unit economics)
- Reliable conversion rates
- Scalable acquisition channels

**Velocity:** Medium to slow (30+ days)

---

## Loop Velocity Analysis

```
/growth-loops --velocity
```

Focuses on **how fast** loops cycle:

**Why velocity matters:**
- Faster loops compound faster
- More cycles per year = more growth
- Small velocity improvements = big compounding gains

**Example:**
- Loop A: 7-day cycle (52 cycles/year)
- Loop B: 2-day cycle (182 cycles/year)
- Loop B compounds 3.5x faster

**Optimization strategies:**
- Reduce friction in invite flow
- Automate parts of the loop
- Incentivize faster action
- Remove approval/review delays

---

## Integration Options

### With Linear
- Analyzes product/feature issues for loop potential
- Tags issues with loop type (viral, content, network, paid)
- Creates loop optimization backlog

### Manual
- Describes your product and gets loop analysis
- Outputs loop diagrams in markdown
- Provides implementation checklist

## Common Use Cases

### Product Strategy Review
```
/growth-loops
```
Identify which loops your product should build

### Feature Prioritization
```
/growth-loops "referral program"
```
Validate growth impact before building

### Growth Audit
```
/growth-loops --map
```
Map all existing user flows to loop types, find gaps

### Velocity Optimization
```
/growth-loops --velocity
```
Speed up existing loops for more compounding

## Learn More

**Full frameworks:**
- `frameworks/growth/growth-loops.md` - Elena Verna's complete framework
- `frameworks/growth/four-fits.md` - Brian Balfour's validation (complements loops)
- `frameworks/growth/product-led-sales.md` - Elena Verna on PLG + loops

**Related commands:**
- `/four-fits` - Validate product-channel fit for viral loops
- `/lno-prioritize` - Leverage tasks often = building loops
- `/now-next-later` - Roadmap loop implementations

---

**Framework:** Growth Loops (Elena Verna)
**Best for:** Designing sustainable, compounding growth
**Key insight:** "Growth isn't a funnel that leaks. It's a loop that compounds."
**Remember:** Retention is the foundation. Without retention, loops won't compound. Fix retention first.
