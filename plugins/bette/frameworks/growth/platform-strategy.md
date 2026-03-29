# Platform Strategy

Frameworks for when platform decisions arise. Not everything should be a platform.

---

## Platform vs Product

A **product** solves a user's problem directly. A **platform** enables others to solve problems using your capabilities.

The distinction matters because platforms have fundamentally different economics, support costs, and failure modes. A product that works for 10 customers can be a terrible platform for 100 developers.

**Platform transition costs are real:**
- API contracts are promises. Breaking changes break trust.
- External developers have different needs than your internal team.
- Support burden shifts from "fix it" to "explain it."
- You lose control of the user experience.

Not every successful product should become a platform. The question is whether the value created by others building on top of you exceeds the cost of enabling and supporting them.

---

## Network Effects

**Direct:** More users make the product more valuable for each user. Messaging apps, social networks. Rare and powerful. Hard to manufacture.

**Indirect (cross-side):** More users on one side attract more participants on the other. App stores, marketplaces. More buyers attract more sellers attract more buyers.

**Data:** More usage produces better product quality. Recommendation engines, search, AI models. Every interaction improves the system for everyone. This is the most common network effect in modern software and the easiest to build deliberately.

Not all growth loops are network effects. Viral sharing and word-of-mouth are distribution advantages, not network effects. The test: does the product get structurally better as more people use it, or just more popular?

---

## Chicken-and-Egg Strategies

Two-sided platforms face a cold start problem. Neither side shows up without the other.

**Single-player mode.** Make the product useful to one side before the other side exists. Yelp was useful for reading reviews before restaurants cared about it. OpenTable was useful as a reservation book before diners knew about it.

**Subsidize one side.** Usually the harder-to-acquire side. Make it free or pay them to participate. The other side pays because value exists.

**Seed supply.** Create the initial supply yourself. Reddit seeded its own content. PayPal manufactured transactions. This is a bootstrapping strategy, not a long-term model.

**Piggyback on existing networks.** Go where the participants already are. Integrate with platforms they use. Reduce the effort to join to near zero.

The goal in all cases: get to the minimum viable liquidity where the network sustains itself.

---

## Platform Governance

What you allow and restrict defines your platform more than what you build.

**The trust spectrum:**
- **Fully open:** Anyone can build anything. Maximum innovation, maximum risk. Hard to quality-control.
- **Curated:** Approval process, guidelines, review. Balances openness with quality. Most successful platforms land here.
- **Closed:** Internal only or invite-only. Maximum control, minimum ecosystem.

**Governance decisions that matter:**
- What data do third parties access? (Minimum viable access, not everything.)
- Who can build? (Open registration vs approval vs partnership.)
- What happens when someone breaks the rules? (Clear enforcement, applied consistently.)
- How do you handle competing with your own ecosystem? (This will happen. Have a policy before it does.)

---

## API Strategy

Opening an API is a strategic decision, not a technical one.

**When to open:**
- Third parties are building on top of you anyway (scraping, workarounds)
- Repeated requests for the same integrations
- Your data is more valuable in others' workflows than locked in yours
- Ecosystem value exceeds the cost of support and loss of control

**When NOT to open:**
- Your core product is unstable
- You have not found product-market fit
- You cannot support external developers
- Opening the API commoditizes your differentiation

**What to expose:** Assembled intelligence is more defensible than raw data. If you expose raw data, you become a pipe. If you expose intelligence, you remain the brain. The difference: raw client events vs "this client is likely to refinance in the next 90 days."

**API as moat vs API as leak:** Every endpoint you expose is a potential bypass of your core experience. Design APIs that make your platform more valuable, not ones that let partners replace you.

---

## When to Platformize

**Signals it is time:**
- Partners are building integrations without your help
- Multiple customers ask for the same extensibility
- Your data creates more value in other systems than in yours alone
- Internal teams are duplicating platform-like patterns

**Signals it is too early:**
- The core product is not stable or proven
- You have fewer than a handful of potential ecosystem partners
- The team cannot support the existing product, let alone external developers
- "Platform" is a strategy to avoid choosing a market

The most common mistake: declaring a platform strategy before having a product that people want to build on. Platforms are earned, not declared.
