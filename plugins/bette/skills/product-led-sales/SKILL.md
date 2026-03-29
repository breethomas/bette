---
name: product-led-sales
description: "Analyze when to layer sales onto a product-led motion. Say 'when should we add sales?', 'analyze our PLG motion', 'product-led sales analysis'."
user-invocable: true
---

# Product-Led Sales

Framework for deciding when and how to layer sales onto a product-led motion. Wraps the detailed framework at `frameworks/growth/product-led-sales.md`.

## When This Skill Fires

The user is asking whether (or how) to add a sales motion on top of self-serve product usage. This is not about replacing PLG with sales -- it is about identifying the segment boundary where product alone stops converting.

## Inputs to Gather

1. **Current motion.** Pure PLG, hybrid, or enterprise with PLG aspirations?
2. **Deal characteristics.** Average deal size, buyer count per deal, implementation complexity.
3. **Product data signals.** What usage data exists? Activation metrics, feature adoption, team/org expansion.
4. **Current conversion blockers.** Where do self-serve users stall or churn?

## Analysis

Load `frameworks/growth/product-led-sales.md` for the full framework. Apply it to the user's context:

**Segment the user base.** Not all users need sales. The question is which segment does. Signals that a segment needs sales assist:
- Deal size crosses a threshold where buyers expect a conversation (typically >$10K ACV).
- Multiple stakeholders involved in the purchase decision.
- Implementation requires configuration, migration, or integration work.
- Security/compliance review is part of the procurement process.
- Free-to-paid conversion is low despite strong activation and engagement.

**Define the handoff.** Product-qualified leads (PQLs) replace marketing-qualified leads. A PQL is a usage pattern that predicts conversion. The PQL definition must come from product data, not from sales intuition.

**Structure the sales layer.** Sales in PLS is reactive to product signals, not proactive outreach. The rep's job is to accelerate deals the product has already started, not to generate demand.

## Output

- **Segment recommendation.** Which user segments should get sales assist vs. remain self-serve.
- **PQL definition.** Specific usage signals that trigger sales engagement.
- **Handoff triggers.** When and how a product-qualified user becomes a sales opportunity.
- **Sales role design.** What the rep actually does (demo, negotiate, implement) vs. what the product handles.

## Quality Bar

Every recommendation must tie to a specific signal in the user's product data. "You should add sales when deal sizes are large" is generic advice. "Your data shows 40% of teams with 5+ active users never convert -- that's your PQL trigger for sales assist" is a recommendation.
