# PM-Friendly Evals Guide: Start Small, Scale Smart

**For PMs who want to test AI quality without overengineering**

**Sources:** Aman Khan, Hamel Husain, Shreya Shankar

**Last Updated:** January 2025

---

## The Problem Evals Have a Bad Reputation

You hear "evals" and think:
- "That sounds like ML engineering work"
- "Don't I need special tools?"
- "Won't this take months to set up?"
- "Isn't this for data scientists, not PMs?"

**The truth:** You can start testing your AI's quality this week with a spreadsheet and 20 test cases.

The comprehensive eval systems you read about? Those come later, after you've learned what matters through manual review of real outputs.

---

## The Core Principle

**"Error analysis is the most important activity in evals."** - Hamel Husain

Translation: Looking at what your AI gets wrong teaches you more than any automated metric.

**For PMs:** You don't need fancy infrastructure. You need systematic attention to what's actually happening in your product.

---

## Good, Better, Best: Choose Your Starting Point

### 🟢 Good: Start This Week

**Time investment:** 2-3 hours setup, 30 min per review

**What you get:** Clear visibility into what works and what doesn't

**How to do it:**

1. **Pick one critical user flow**
   - Example: "User asks for product recommendations"
   - Example: "Customer support query gets answered"
   - Example: "Code generation for a specific task"

2. **Write 20 test cases manually**
   - 15 cases you expect to work (happy path)
   - 5 cases that might be tricky (edge cases)
   - Write them in a spreadsheet: Input | Expected Output | Pass/Fail | Notes

3. **Run your AI against them**
   - Copy/paste inputs into your product
   - Record actual outputs
   - Mark pass or fail based on your judgment

4. **Look for patterns**
   - What types of inputs fail most?
   - Are there specific failure modes?
   - What's working better than expected?

**That's it. You're doing evals.**

**Example spreadsheet:**
```
Input                          | Expected Output      | Pass/Fail | Notes
------------------------------ | -------------------- | --------- | -----
"Recommend a laptop under $800"| Surface mid-range... | Pass      | Good
"Best phone for photography"   | iPhone 15 Pro...     | Pass      | Good
"Cheapest gaming PC"           | Custom build...      | Fail      | Recommended gaming laptop instead
```

**When to use this:**
- ✅ You're just starting with AI features
- ✅ You have one core use case
- ✅ You can manually review 20 outputs
- ✅ You want to validate your AI works before shipping

---

### 🟡 Better: Scale Up (1-2 Months In)

**Time investment:** 30 min/week ongoing

**What you get:** Growing test coverage + ability to catch regressions

**Skills:** `/upgrade-evals` (error analysis), `/build-judge` (automated evaluation), `/generate-test-data` (diverse inputs)

**How to do it:**

1. **Run error analysis on real traces** (`/upgrade-evals`)
   - Read ~100 traces from production or staging
   - Judge each trace pass/fail
   - Let failure categories emerge from what you observe — don't start with pre-defined categories
   - Compute failure rates to prioritize what to fix

2. **Fix obvious problems first**
   - Missing prompt instructions → add them
   - Engineering bugs → fix the code
   - Missing tools → add them
   - Only build evaluators for failures that persist after fixing

3. **Build LLM-as-Judge for subjective failures** (`/build-judge`)
   - One judge per failure mode. Binary pass/fail only.
   - Each judge checks exactly one thing (tone, faithfulness, relevance — not all at once)
   - Prefer code-based checks (regex, schema validation) for anything objective
   - Only use LLM judges when code can't check the failure mode

4. **Generate diverse test data when needed** (`/generate-test-data`)
   - Define dimensions of variation (query type, user persona, complexity)
   - Generate tuples, convert to natural language, filter for quality
   - Use to fill gaps in underrepresented scenarios

5. **Track pass rate over time**
   - Create a simple dashboard (spreadsheet works!)
   - Chart: Pass rate by week
   - Goal: Don't let quality degrade as you iterate

6. **Review failures weekly**
   - Spend 30 minutes looking at what failed
   - Categorize by the failure modes from your error analysis
   - Prioritize fixes based on frequency and business impact

**When to graduate to Better:**
- Your basic test set (20 cases) is consistently passing
- You're making frequent changes to prompts or context
- You have 30 min/week to maintain this
- Manual review is getting tedious

**Tool recommendations:**
- Spreadsheets (Google Sheets, Excel) - Works great
- Braintrust, Confident AI - If you want real tooling
- Custom dashboard (Streamlit, Retool) - If you have eng time

---

### 🔵 Best: Systematic Approach (3+ Months In)

**Time investment:** Ongoing process, integrated into development

**What you get:** Comprehensive quality assurance, production monitoring, regression protection

**When you're ready for this:**
- ✅ You have 100+ test cases
- ✅ Your AI feature is in production with real users
- ✅ You're making frequent changes (weekly/daily)
- ✅ Quality issues are costing you (churn, support tickets, reputation)
- ✅ You have eng resources to build infrastructure

**What it includes:**

1. **Three-level eval system** (Hamel's framework)
   - Level 1: Unit tests (fast assertions, run on every change)
   - Level 2: Human & model eval (comprehensive test sets)
   - Level 3: A/B testing (production validation with real users)

2. **Automated regression testing**
   - Tests run on every deployment
   - CI/CD integration
   - Alerts when quality drops

3. **Production monitoring**
   - Real-time quality tracking
   - User feedback integration
   - Distribution shift detection

4. **Continuous improvement loop**
   - Error analysis → Update test set → Fix issues → Deploy → Monitor

**See the detailed framework:** [ai-evals.md](./ai-evals.md)

**When NOT to jump to Best:**
- ❌ You haven't done Good and Better yet
- ❌ You're not sure what "good quality" means for your use case
- ❌ You don't have production users yet
- ❌ You're still figuring out your product

**Build the foundation first.** Start small.

---

## Key Insights from the Experts

### From Hamel Husain

> "Creating an LLM judge is a hack I use to trick people into carefully looking at their data."

**Translation for PMs:** The real value isn't the automation—it's forcing yourself to systematically examine what your AI is doing.

> "Be wary of optimizing for high eval pass rates. If you're passing 100% of your evals, you're likely not challenging your system enough."

**Translation for PMs:** Your test set should have some failures. That's how you learn where the limits are.

> "Don't buy fancy LLM tools. Use what you have first."

**Translation for PMs:** Start with spreadsheets. Upgrade only when manual process becomes painful.

### From Aman Khan

> "The difference between a demo and a product is a comprehensive eval system."

**Translation for PMs:** You can't ship responsibly without knowing what your AI gets wrong.

> "Every production incident should become an eval case."

**Translation for PMs:** When users report bugs, add them to your test set. Never make the same mistake twice.

### From Shreya Shankar

> "Evals get a bad name because people try to build infrastructure before understanding what they're testing."

**Translation for PMs:** Figure out what "good" means first. Build tools second.

---

## When to Graduate to More Depth

### Signs you've outgrown "Good"
- ✅ Manual review of 20 cases takes 5 minutes
- ✅ You're changing your AI frequently (daily/weekly)
- ✅ You have obvious failure patterns you want to track
- ✅ You're worried about breaking things

**→ Move to "Better"**

### Signs you've outgrown "Better"
- ✅ You have 100+ test cases
- ✅ Manual weekly review is taking >1 hour
- ✅ You have production users experiencing issues
- ✅ You're making multiple changes per week
- ✅ Quality issues are costing you money/reputation

**→ Move to "Best"** and read [ai-evals.md](./ai-evals.md)

---

## Common PM Mistakes to Avoid

### ❌ Mistake 1: "I'll build the perfect eval system first"
**Problem:** You spend months building infrastructure without knowing what matters.

**Fix:** Start with 20 manual test cases this week. Learn what's important. Build tools later.

### ❌ Mistake 2: "I'll use an off-the-shelf metric like BLEU or ROUGE"
**Problem:** Generic metrics don't capture what your users actually care about.

**Fix:** Define "good" based on your product's requirements. Use your judgment.

### ❌ Mistake 3: "This is the ML team's job"
**Problem:** PMs understand user expectations better than anyone. You should define quality.

**Fix:** You own the quality bar. Partner with eng on implementation, but you define success.

### ❌ Mistake 4: "I need 1000 test cases to start"
**Problem:** You never start because the bar is too high.

**Fix:** 20 cases covering your core use case is infinitely better than 0 cases covering everything.

### ❌ Mistake 5: "100% pass rate means we're good"
**Problem:** Your test set isn't challenging enough. You'll miss real issues.

**Fix:** Include hard cases. Aim for 80-90% pass rate on a challenging test set.

---

## Practical Checklist: Get Started Today

### ☐ Step 1: Define one critical user flow (15 min)
What's the most important thing your AI does?
- Customer support response
- Content generation
- Recommendations
- Search/retrieval
- Code generation

Write it down: "For [user type], the AI should [expected behavior]"

### ☐ Step 2: Create 20 test cases (1 hour)
Open a spreadsheet. Create these columns:
- Input (what the user provides)
- Expected Output (what should happen)
- Actual Output (leave blank for now)
- Pass/Fail (leave blank for now)
- Notes (why it passed or failed)

Write 15 happy path cases + 5 edge cases.

### ☐ Step 3: Run tests manually (30 min)
- Go to your product
- Input each test case
- Copy actual output into spreadsheet
- Mark pass or fail based on your judgment
- Add notes on why things failed

### ☐ Step 4: Look for patterns (15 min)
- What percentage passed?
- What types of inputs failed most?
- Are failures related (prompt issue? data issue?)?
- What surprised you?

### ☐ Step 5: Pick one thing to improve (10 min)
Based on failures, what's the highest-impact fix?
- Update prompt
- Add more context
- Change retrieval strategy
- Set better expectations with users

### ☐ Step 6: Rerun tests after fix (15 min)
Did it improve? By how much?

**Congratulations, you just did your first eval cycle. 🎉**

**Next week:** Add 5 more test cases based on what you learned.

---

## Real-World Example: E-commerce Recommendations

### Week 1: Good (Start Small)

**PM Sarah's situation:**
- Building AI product recommendations
- Feature is in beta
- Not sure if it's working well

**What she did:**

Created 20 test cases in Google Sheets:
```
Input: "Laptop under $800 for college"
Expected: Mid-range laptops, student-friendly features
Actual: [Ran test]
Pass/Fail: Pass
Notes: Good recommendations, mentioned student discounts

Input: "Best phone for photos"
Expected: High-end phones with good cameras
Actual: [Ran test]
Pass/Fail: Fail
Notes: Recommended mid-range phones, missed flagship cameras
```

**Result:** Found that price-sensitive queries work great, but quality-focused queries need work.

**Time spent:** 2 hours

### Week 5: Better (Scaled Up)

**Progress:**
- Now has 60 test cases
- Added every bug report as a test
- Using Claude as LLM-judge for consistency

**What changed:**
- Weekly 30-min review meeting
- Dashboard tracking pass rate (currently 85%)
- Prompt iterations happen faster

**Judge prompt:**
```
Evaluate this product recommendation as PASS or FAIL.

Criteria:
- Matches user's stated budget
- Addresses user's primary need (photography, gaming, etc.)
- Recommends appropriate tier (budget/mid/premium)

User query: {query}
Recommendation: {output}

Verdict: PASS or FAIL
Reason: [explain]
```

**Result:** Pass rate improved from 75% to 85% over 4 weeks. Customer complaints down 40%.

### Month 4: Best (Systematic)

**Expansion:**
- 200+ test cases organized by category
- Automated regression tests run on every deploy
- Production monitoring shows real user satisfaction
- A/B tests validate changes before full rollout

**Infrastructure:**
- Custom dashboard built in Streamlit
- Slack alerts when pass rate drops below 80%
- Weekly review with eng team
- Monthly review of production patterns

**Result:** Recommendation quality is a competitive advantage. Customer retention up 15%.

**The key:** Sarah started with 20 test cases in a spreadsheet. She didn't wait for perfect infrastructure.

---

## Tools by Level

### Good: Start Small
- **Google Sheets or Excel** - All you need
- **Your product** - For running tests
- **Your brain** - For pass/fail judgment

Cost: $0

### Better: Scale Up
- **Spreadsheets still work**
- **LLM APIs** (OpenAI, Anthropic) - For LLM-as-judge
- **Simple dashboard** (Google Sheets charts, Notion)
- **Optional:** Braintrust, Confident AI, Langfuse

Cost: $10-50/month

### Best: Systematic
- **Eval platforms** - Braintrust, Weights & Biases, custom
- **Production monitoring** - Datadog, Grafana, custom
- **CI/CD integration** - GitHub Actions, CircleCI
- **A/B testing platform** - LaunchDarkly, Statsig

Cost: Varies (can build custom or buy platform)

---

## FAQ

### "How many test cases do I really need?"

**Start:** 20 cases covering your core use case
**Scale:** Add 5-10 per week as you find issues
**Target:** 50-100 cases = solid coverage for most products

More cases ≠ better. Coverage of important scenarios > raw volume.

### "Should I use human review or LLM-as-judge?"

**Start with human:** You need to develop intuition for what "good" means

**Add LLM-as-judge when:**
- You have 50+ test cases (manual review is tedious)
- You understand what "good" looks like (you can write a clear rubric)
- You want to run tests frequently (daily/multiple times per day)

**Keep human review:** Even with LLM-as-judge, review results weekly yourself.

### "What if my product does multiple things?"

Start with ONE use case. The most critical one.

Once you have evals working for that, add another use case.

**Don't try to eval everything at once.** You'll never start.

### "How do I know if I'm testing the right things?"

**Ask yourself:**
- What user complaints have we gotten?
- What would make me nervous to demo to a customer?
- What failure would be most embarrassing?

Test those scenarios first.

### "Can't I just use production metrics?"

**Yes AND no:**

Production metrics (user satisfaction, retention, etc.) tell you if you have a problem.

Evals tell you WHAT the problem is and if your fix worked.

You need both:
- **Evals** = Dev/staging testing, fast feedback
- **Production metrics** = Real-world validation

### "When should I invest in eval tooling?"

**Signals you're ready:**
- ✅ Manual review takes >1 hour per week
- ✅ You're making changes multiple times per week
- ✅ You have 100+ test cases
- ✅ Quality issues are costing you (support tickets, churn)

**Not ready yet:**
- ❌ You have <50 test cases
- ❌ You're not sure what "good" means
- ❌ You change your AI infrequently (monthly)

---

## Summary: Your Path Forward

```
Week 1: Good (/start-evals)
├─ 20 test cases in spreadsheet
├─ Manual pass/fail review
└─ Identify top failure pattern

Week 5: Better (/upgrade-evals → /build-judge)
├─ Error analysis on ~100 real traces
├─ Failure categories emerge from data (not brainstormed)
├─ LLM-as-Judge per failure mode (binary pass/fail)
├─ /generate-test-data for diverse inputs
└─ Track pass rate over time

Month 4+: Best
├─ 200+ test cases
├─ Automated regression testing
├─ /eval-rag for retrieval-specific evaluation
├─ /calibrate for continuous monitoring
└─ Continuous improvement loop
```

**The key:** Start where you are. Improve from there.

---

## Related Frameworks

**When you're ready for more depth:**
- [AI Evals & Testing (Comprehensive)](./ai-evals.md) - Full framework from Aman Khan
- [Production AI Systems](./production-ai-systems.md) - Chip Huyen on monitoring and quality
- [Continuous Calibration](../ai-era-practices/continuous-calibration.md) - How AI products evolve differently

**Strategy context:**
- [Four Risks](../discovery/four-risks.md) - Marty Cagan's framework includes feasibility risk (can we build quality AI?)
- [AI Unit Economics](../ai-era-practices/ai-unit-economics.md) - Cost of poor quality vs cost of evals

---

## The Eval Skills Chain

```
/start-evals              → 20 test cases (start here)
  ↓ "ready to scale"
/upgrade-evals             → Error analysis on real traces
  ↓ "need more diverse inputs"
/generate-test-data        → Dimension-based synthetic data
  ↓ "need automated evaluation"
/build-judge               → LLM-as-Judge per failure mode
  ↓ "RAG-specific issues"
/eval-rag                  → Retrieval + generation eval
  ↓ "ongoing maintenance"
/calibrate                 → Continuous calibration
```

## Key Takeaways

1. **Start small** - 20 test cases this week > perfect eval system never
2. **Error analysis > automation** - Looking at failures teaches you what matters
3. **Categories emerge from traces, never brainstormed** - Pre-defined lists cause confirmation bias
4. **Binary pass/fail only** - No Likert scales, no letter grades. Forces clear decision boundaries.
5. **PMs own quality** - You define "good," eng implements the testing
6. **Graduate when ready** - Don't jump to "Best" before mastering "Good"
7. **Tools come last** - Understand the problem before building infrastructure

**Remember:** The best eval system is the one you actually use. Start simple. Improve continuously.

---

**Next step:** Open a spreadsheet and write your first 20 test cases. Right now. Go.
