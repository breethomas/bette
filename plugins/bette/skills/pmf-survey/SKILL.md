---
name: pmf-survey
description: Create and analyze a PMF survey using Rahul Vohra's Superhuman framework. The magic 40% benchmark for product-market fit.
---

# PMF Survey

Create and analyze a **Product-Market Fit survey** using Rahul Vohra's Superhuman framework.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 PMF SURVEY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

The magic number: >40% "very disappointed" = PMF

What do you want to do?

  1. Create a PMF survey
     → Generate the four questions + implementation guide

  2. Analyze existing results
     → Paste your data, get PMF score + action plan

  3. Understand the framework
     → Learn when and how to use this

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## What This Does

Guides you through running Sean Ellis's PMF survey with Rahul Vohra's systematic approach:
- The magic "very disappointed" >40% benchmark
- Four-question survey structure
- Segment analysis by high-expectation customers
- Actionable improvement plan

## Usage

```
/pmf-survey
```

**Optional parameters:**
- `/pmf-survey --create` - Generate survey questions
- `/pmf-survey --analyze [data]` - Analyze existing survey results
- `/pmf-survey --export` - Export survey to Typeform/Google Forms format

## What Happens

### Mode 1: Create Survey

1. **Validates readiness:**
   - Do you have users who experienced the core product?
   - Have they used it at least twice in last 2 weeks?

2. **Generates four-question survey:**
   - Q1: How disappointed if you could no longer use [product]?
   - Q2: What type of people would most benefit?
   - Q3: What is the main benefit you receive?
   - Q4: What can be improved?

3. **Provides implementation guidance:**
   - Who to survey (active users, not everyone)
   - Survey tool recommendations
   - Sample size calculations

### Mode 2: Analyze Results

1. **Calculates PMF score:**
   - % who answered "very disappointed"
   - Benchmark: >40% = PMF, <40% = not yet

2. **Segments users:**
   - Very disappointed (supporters)
   - Somewhat disappointed (neutrals)
   - Not disappointed (detractors)

3. **Identifies high-expectation customers:**
   - From "what type of people" answers
   - Your most discerning potential users

4. **Generates improvement plan:**
   - What to double down on (from supporters)
   - What to ignore (from detractors)
   - How to convert neutrals

## Example Output (Analysis Mode)

```
📊 PMF Survey Analysis

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 PMF SCORE: 58%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ STRONG PMF (>40% very disappointed)

Responses: 250 total
- 145 (58%) - Very disappointed 🟢
- 72 (29%) - Somewhat disappointed 🟡
- 33 (13%) - Not disappointed 🔴

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
👥 HIGH-EXPECTATION CUSTOMERS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

From "What type of people benefit most?":
1. Technical founders at early-stage startups (mentioned 89 times)
2. Solo developers building side projects (mentioned 67 times)
3. Remote engineering teams (mentioned 54 times)

Focus: Technical founders at early-stage startups
Why: Most discerning, strongest advocates, willing to pay

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💡 MAIN BENEFITS (from supporters)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Top themes:
1. "Saves me 10+ hours/week on documentation" (92 mentions)
2. "Makes code review actually enjoyable" (78 mentions)
3. "Onboards new devs 3x faster" (65 mentions)

🎯 Your core value prop: Time-saving documentation + code review

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔧 IMPROVEMENTS NEEDED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

From supporters (PRIORITIZE):
1. "Better GitHub integration" (45 mentions) → Build this
2. "Slack notifications" (38 mentions) → Build this
3. "Team analytics dashboard" (31 mentions) → Build this

From neutrals (CONSIDER):
1. "More customization options" (22 mentions) → Maybe
2. "Mobile app" (18 mentions) → Later

From detractors (IGNORE):
1. "Should be totally free" (12 mentions) → Wrong segment
2. "Too focused on documentation" (8 mentions) → Not our market

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 ACTION PLAN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ DOUBLE DOWN (you have PMF, now optimize):

1. Focus on high-expectation customer:
   "Technical founders at early-stage startups"

2. Amplify core benefits:
   - Time-saving documentation
   - Code review improvements
   - Faster onboarding

3. Build supporter requests:
   Priority 1: Better GitHub integration
   Priority 2: Slack notifications
   Priority 3: Team analytics

4. Ignore detractor feedback:
   - Wrong pricing expectations = wrong segment
   - "Too focused" = they're not your market

🎯 GROWTH STRATEGY

Now that you have PMF (58% > 40%):
- Segment marketing to "technical founders at early-stage startups"
- Lead with "Save 10+ hours/week on documentation"
- Build supporter-requested features
- Survey again in 3 months to measure improvement
```

## Learn More

See the full PMF Survey framework at:
`frameworks/measurement/pmf-survey.md`

---

**Framework:** Rahul Vohra (Superhuman) based on Sean Ellis
**Best for:** Measuring PMF, prioritizing improvements, identifying target market
**Magic number:** >40% "very disappointed" = PMF
