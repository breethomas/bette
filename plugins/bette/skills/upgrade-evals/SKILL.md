---
name: upgrade-evals
description: >
  Systematic error analysis on real AI traces. Read traces, judge pass/fail,
  let failure categories emerge from data, compute failure rates, decide what
  to fix. Use when you have 50+ test cases or are seeing production failures.
  Do NOT use when you have fewer than 20 test cases (use /start-evals first).
---

# Upgrade Evals

Guide the PM through reading real LLM pipeline traces and building a catalog of how the system fails. Categories emerge from traces, never brainstormed.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 UPGRADE EVALS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Error analysis on real traces. Categories emerge from data.

What AI feature are we analyzing?
How are you collecting traces today?

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Prerequisites

- The PM has an AI feature in production (or staging with real-ish data).
- At least some traces are available: inputs, outputs, and ideally intermediate steps (tool calls, retrieved docs, reasoning).
- The PM has run `/start-evals` or equivalent (has basic familiarity with pass/fail judgment on outputs).

## Core Process

### Step 1: Collect Traces

Ask the PM where traces live. Help them pull ~100 representative traces.

**Target: ~100 traces.** New failure types stop appearing around this number. Adjust for system complexity.

**From real user data (preferred):**
- Small volume: random sample.
- Large volume: sample across key dimensions (query type, user segment, feature area).
- Use embedding clustering (K-means) to ensure diversity if volume is high.

**From synthetic data (when real data is sparse):**
- Use `/generate-test-data` to create diverse inputs.
- Run synthetic queries through the full pipeline and capture complete traces.

**What to capture per trace:** Input, all intermediate LLM calls, tool uses, retrieved documents, reasoning steps, and final output. The more of the pipeline visible, the better the root cause analysis.

Claude Code executes: Write Python scripts to pull traces from the PM's logging system, API, or database. Format them for review.

### Step 2: Read Traces and Judge Pass/Fail

Present each trace to the PM. For each one, ask: **did the system produce a good result?** Pass or Fail.

For failures, the PM notes what went wrong. Focus on the **first thing that went wrong** in the trace — errors cascade, so downstream symptoms disappear when the root cause is fixed.

Write observations, not explanations. "SQL missed the budget constraint" not "The model probably didn't understand the budget."

**Template for tracking:**

```
| Trace ID | Pass/Fail | What went wrong |
|----------|-----------|-----------------|
| 001      | Fail      | Missing filter: pet-friendly requirement ignored in SQL |
| 002      | Fail      | Proposed unavailable times despite calendar conflicts |
| 003      | Fail      | Used casual tone for luxury client; wrong property type |
| 004      | Pass      | - |
```

**If the PM is stuck articulating what feels wrong:** prompt with common failure types — made-up facts, malformed output, ignored user requirements, wrong tone, tool misuse. These are conversation starters, not a category list.

**Do NOT start with a pre-defined failure list.** Let categories emerge from what the PM actually sees.

Claude Code executes: Build the tracking spreadsheet/table. Pull and format individual traces for review. Compute running statistics.

### Step 3: Group Failures into Categories

After reviewing 30-50 traces, start grouping similar notes into categories. Don't wait until all 100 are done — grouping early sharpens what to look for in remaining traces.

1. Read through all failure notes.
2. Group similar ones together.
3. Split notes that look alike but have different root causes.
4. Give each category a clear name and one-sentence definition.

**When to split vs. group:**

Split these (different root causes):
- "Made up property features (solar panels)" vs. "Made up client activity (scheduled a tour never requested)" — one fabricates external facts, the other fabricates user intent.

Group these (same root cause):
- "Missing bedroom count filter" + "Missing pet-friendly filter" + "Missing price range filter" = **Missing Query Constraints**

**LLM-assisted clustering** (use only after the PM has reviewed 30-50 traces):

Claude Code executes: Run clustering on failure annotations. Present suggested groupings to PM for review. LLMs cluster by surface similarity (e.g., grouping "app crashes" and "login is slow" because both mention login). The PM validates whether groupings reflect actual root causes.

**Aim for 5-10 categories** that are:
- Distinct (each failure belongs to one category)
- Clear enough that someone else could apply them consistently
- Actionable (each points toward a specific fix)

### Step 4: Label Every Trace

Go back through all traces and apply binary labels (pass/fail) for each failure category. Each trace gets a column per category.

Claude Code executes: Build the labeling spreadsheet or script. Automate where possible — some categories may be detectable with simple code checks.

### Step 5: Compute Failure Rates

Claude Code executes:

```python
failure_rates = labeled_df[failure_columns].sum() / len(labeled_df)
failure_rates.sort_values(ascending=False)
```

Present the ranked list to the PM. The most frequent failure category is where to focus first.

### Step 6: Decide What to Do About Each Failure

Work through each category with the PM in this order:

**Can we just fix it?** Many failures have obvious fixes that don't need an evaluator:
- The prompt never mentioned the requirement → add the instruction.
- A tool is missing or misconfigured → add/fix the tool.
- An engineering bug in retrieval, parsing, or integration → fix the code.

If a clear fix resolves the failure, do that first. Only consider an evaluator for failures that persist after fixing.

**Is an evaluator worth the effort?** Not every remaining failure needs one. Ask the PM:
- Does this failure happen frequently enough to matter?
- What's the business impact when it does happen?
- Will this evaluator actually get used to iterate on the system?

Reserve evaluators for failures the PM will iterate on repeatedly.

**For failures that warrant an evaluator:** prefer code-based checks (regex, parsing, schema validation) for anything objective. Use `/build-judge` only for failures that require judgment. Critical requirements (safety, compliance) may warrant an evaluator even after fixing the prompt, as a guardrail.

**What to tell your engineer:** For each category, produce a one-line summary: category name, frequency, recommended action (fix prompt / fix code / build evaluator / skip).

### Step 7: Iterate

Expect 2-3 rounds of reviewing and refining categories. After each round:
- Merge categories that overlap.
- Split categories that are too broad.
- Clarify definitions where the PM would hesitate.
- Re-label traces with the refined categories.

## Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ERROR ANALYSIS RESULTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature: [name]
Traces reviewed: [count]
Overall pass rate: [%]

FAILURE CATEGORIES (ranked by frequency):

| Category | Rate | Action |
|----------|------|--------|
| [name] | [%] | Fix prompt |
| [name] | [%] | Build evaluator → /build-judge |
| [name] | [%] | Fix code |
| [name] | [%] | Skip (low impact) |

NEXT STEPS:
1. Fix [top category] — [specific action]
2. Build judge for [category] — run /build-judge
3. Re-run analysis after fixes

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Stopping Criteria

Stop reviewing when new traces aren't revealing new kinds of failures. Roughly: ~100 traces reviewed with no new failure types in the last 20.

## Trace Sampling Strategies

When production volume is high, use a mix:

| Strategy | When to Use | Method |
|----------|------------|--------|
| **Random** | Default starting point | Sample uniformly from recent traces |
| **Outlier** | Surface unusual behavior | Sort by response length, latency, tool call count; review extremes |
| **Failure-driven** | After guardrail violations or user complaints | Prioritize flagged traces |
| **Uncertainty** | When automated judges exist | Focus on traces where judges disagree or have low confidence |
| **Stratified** | Ensure coverage across user segments | Sample within each dimension |

## Routing

**Next steps after error analysis:**
- Need more diverse test inputs? → `/generate-test-data`
- Need automated evaluation for a subjective failure mode? → `/build-judge`
- RAG-specific issues (retrieval vs generation)? → `/eval-rag`
- Ongoing monitoring and calibration? → `/calibrate`

## Anti-Patterns

- Brainstorming failure categories before reading traces.
- Starting with pre-defined categories. A fixed list causes confirmation bias.
- Skipping the PM for initial review. The PM must review the first 30-50 traces.
- Using generic scores as categories ("hallucination score," "helpfulness score").
- Building evaluators before fixing obvious problems.
- Treating this as a one-time activity. Re-run after significant changes.

---

**Methodology:** Adapted from Hamel Husain's error-analysis skill (evals-skills, MIT license)
**PM adaptation:** Claude Code pulls/reads traces, PM provides pass/fail judgment and domain expertise
