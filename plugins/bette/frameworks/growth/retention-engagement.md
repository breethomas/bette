# Retention and Engagement

A thinking tool for diagnosing retention problems and designing engagement loops. Retention is the output. Engagement is the input. This framework works backward from the curve shape to the intervention.

## Retention Curve Shapes

The shape of the retention curve tells you what kind of problem you have before you look at anything else.

**Flattening curve.** Healthy. Some users churn early (didn't find value), but a cohort stabilizes and sticks. The flattening point is your "core retained base." The questions are: can you flatten earlier (faster time-to-value) and can you flatten higher (retain more of each cohort)?

**Declining to zero.** The product is a utility, not a habit. Every cohort eventually leaves. Either the use case is episodic (job search, apartment hunting) and retention is the wrong metric, or the product fails to create ongoing value. Before "fixing" retention, decide if the product is meant to retain at all.

**Smile curve.** Users leave and come back. This is resurrection, not retention. Indicates the product has latent value but no habit loop. Common in marketplace and content products. The opportunity is building a trigger that brings users back before they fully churn.

**Staircase.** Retention drops in steps, often at billing cycles or contract renewals. The product delivers value between steps but not enough to survive a re-evaluation moment. Fix the re-evaluation experience or make the value continuous rather than periodic.

**Source:** Brian Balfour (Reforge) -- retention curve taxonomy and the relationship between curve shape and product strategy.

## Engagement Loops

Retention doesn't happen because you ask users to come back. It happens because the product creates a reason to return. Every sustained product has at least one functioning loop.

### Core Action Loop

The simplest loop: user does the core action, gets value, has a reason to do it again.

- What is the core action? (One action, not five. If you can't name one, the product lacks focus.)
- How quickly does the user get value from performing it?
- What naturally triggers the next occurrence?

If the core action doesn't create a reason to repeat, no amount of engagement tactics will fix retention.

### Habit Loop (Nir Eyal / Hooked Model, adapted)

**Trigger** -- what prompts the user to open the product? External triggers (email, notification, calendar) are a crutch. Internal triggers (anxiety, curiosity, routine) are the goal. If the product only gets opened via external triggers, it hasn't built a habit.

**Action** -- the behavior the product wants. Must be low-friction. The harder the action, the stronger the trigger needs to be.

**Reward** -- the value delivered. Variable rewards (different each time) sustain engagement longer than predictable rewards. Social validation, information discovery, and completion are the three reward types that scale.

**Investment** -- user puts something in that makes the product better for next time. Data, preferences, connections, content. Investment raises switching costs and personalizes the next trigger. Without investment, each session starts from zero.

### Network and Social Loops

User activity creates value for other users, which brings them back, which creates more value. These loops compound but are hard to start. Relevant when the product has multi-user dynamics. Irrelevant for single-player products -- don't force social features where they don't belong.

**Source:** Casey Winters -- writing on engagement loops, particularly the distinction between viral loops (growth) and engagement loops (retention).

## Cohort Analysis

### How to Read Cohort Charts

- **Rows** are cohorts (grouped by signup date, activation date, or first purchase).
- **Columns** are time periods since the cohort's start.
- **Read down columns** to see if the product is getting better over time (are newer cohorts retaining better than older ones?).
- **Read across rows** to see the retention curve shape for each cohort.

### What to Look For

**Vintage effects.** Are newer cohorts better or worse? Better = product improvements are working. Worse = growth is attracting lower-quality users or the market is saturating.

**Seasonal patterns.** Do cohorts that start in certain months behave differently? If yes, control for seasonality before drawing conclusions about product changes.

**Feature-driven shifts.** Did a specific launch change the curve? Compare cohorts immediately before and after. If the post-launch cohort flattens higher or earlier, the feature improved retention. If not, it didn't, regardless of what the launch metrics said.

**Segment differences.** Aggregate cohorts hide segment-level stories. Split by acquisition channel, plan tier, company size, or use case. The "average" retention curve often doesn't describe any real user.

## Leading Indicators of Churn

By the time a user churns, the decision happened weeks or months earlier. These signals precede the cancellation:

- **Usage frequency drops.** The most reliable signal. If a daily user becomes weekly, they're disengaging. Define the expected frequency for your product and alert on deviations.
- **Feature breadth narrows.** Users stop exploring and use only one or two features. They've decided the product is a utility, not a platform. Expansion revenue and upsell will fail in this state.
- **Support tickets increase.** Frustrated users file tickets. Silent users just leave. An increase in tickets from a segment is a warning, not a complaint to be managed.
- **Core action stops.** The clearest signal. If the user stops doing the one thing the product is for, they're gone. The gap between last core action and cancellation is your intervention window.
- **Champion leaves.** In B2B, retention is often tied to one person. When that person changes roles or leaves the company, the account is at risk regardless of product usage.

## Resurrection Strategies

Bringing churned users back is harder than retaining them, but some products have natural resurrection opportunities.

**Re-engagement triggers.** Effective when something genuinely changes: new feature that addresses the reason they left, their data updated in a way that creates new value, or a life event that makes the product relevant again. Ineffective when it's "we miss you" with no substance.

**What brings users back (Lenny Rachitsky's research):**
- A change in the user's circumstances (new job, new project, new life stage).
- A change in the product (feature they wanted, price they can afford, platform they now use).
- Social pull (colleague, friend, or community draws them back).

The product can only control the middle one. Design resurrection around product changes that address known churn reasons. The other two are outside your control -- build awareness so when circumstances change, users remember the product exists.

**Dormancy windows.** Define how long a user can be inactive before they're "churned" vs. "dormant." Dormant users with stored data or investment are more likely to return than users who never invested. Treat them differently.

---

*Retention is the single metric that separates products that compound from products that plateau. Everything else -- growth, revenue, expansion -- depends on the denominator not leaking.*
