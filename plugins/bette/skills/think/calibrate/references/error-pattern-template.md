# Error Pattern Documentation Template

Use this template to systematically document AI feature errors for calibration.

---

## Error Pattern Table

| Error Pattern | Category | Frequency | Impact | Likely Reason | Potential Fix | Priority |
|---------------|----------|-----------|--------|---------------|---------------|----------|
| [description] | [type] | [rare/occ/freq] | [low/med/high] | [why] | [how] | P1/P2/P3 |

---

## Error Categories

### Hallucination
AI makes up information that doesn't exist.

**Examples:**
- Citing nonexistent documents
- Inventing user data
- Creating fake statistics

**Common fixes:**
- Tighter context constraints
- Explicit grounding requirements
- Fact-checking layer

### Wrong Context
AI misreads the situation or applies wrong context.

**Examples:**
- Using data from wrong user
- Applying wrong domain rules
- Misunderstanding timeframe

**Common fixes:**
- Better context retrieval
- Clearer context boundaries
- Validation of context relevance

### Tone Mismatch
Output style doesn't match expected tone.

**Examples:**
- Too formal for casual context
- Too casual for professional context
- Wrong emotional register

**Common fixes:**
- Tone examples in prompt
- Audience-aware instructions
- Tone validation layer

### Scope Creep
AI goes beyond defined boundaries.

**Examples:**
- Answering questions outside domain
- Providing unrequested advice
- Acting beyond authorization

**Common fixes:**
- Explicit scope boundaries
- Hard guardrails for off-topic
- Scope validation checks

### Missing Information
AI lacks context needed for good output.

**Examples:**
- Asking for info already provided
- Generic answers due to missing context
- Incomplete responses

**Common fixes:**
- Better context gathering
- Context availability checks
- Graceful degradation when missing

### Confidence Miscalibration
AI is too certain or uncertain.

**Examples:**
- High confidence on wrong answers
- Low confidence on correct answers
- No confidence indication

**Common fixes:**
- Calibrated confidence scoring
- Confidence training examples
- Confidence display to users

### Edge Case
Scenario not covered by current implementation.

**Examples:**
- Unusual input format
- Rare but valid scenario
- Combination of factors

**Common fixes:**
- Add to test cases
- Handle explicitly in prompt
- Consider if worth supporting

### Adversarial
Intentional misuse or attack.

**Examples:**
- Prompt injection
- Jailbreak attempts
- Data extraction attempts

**Common fixes:**
- Input sanitization
- Output filtering
- Attack detection

---

## Priority Framework

**P1 - Critical:** Fix immediately
- User safety at risk
- Data integrity compromised
- Legal/compliance exposure
- Trust-destroying errors

**P2 - Important:** Fix this cycle
- Significant user frustration
- Quality degradation visible
- Blocking higher agency
- Recurring frequently

**P3 - Nice to Fix:** Backlog
- Minor user inconvenience
- Rare occurrence
- Workaround exists
- Low impact

---

## Example Error Pattern Documentation

### Feature: AI Email Subject Line Generator

| Error Pattern | Category | Frequency | Impact | Likely Reason | Potential Fix | Priority |
|---------------|----------|-----------|--------|---------------|---------------|----------|
| Subject mentions wrong company | Hallucination | Occasional | High | No company context in prompt | Add company name to context | P1 |
| Subject too long for mobile | Edge case | Frequent | Medium | No length constraint | Add character limit | P2 |
| Overly casual tone for B2B | Tone mismatch | Occasional | Medium | Missing audience context | Add B2B/B2C flag | P2 |
| Generates 1 option instead of 3 | Scope creep | Rare | Low | Prompt parsing issue | Enforce output structure | P3 |

**Pattern Analysis:**
- Most common: Length issues (need output constraints)
- Emerging: Tone mismatches (need better audience signal)
- Regression: None observed

**Actions:**
1. P1: Add company name injection to context (this week)
2. P2: Add character limit validation (next sprint)
3. P2: Implement audience flag (next sprint)

**Evals to Add:**
- [ ] Test case: Company name preservation
- [ ] Test case: Subject length <60 chars
- [ ] Test case: Tone matches B2B context

---

## Error Tracking Over Time

Track patterns across calibration cycles:

| Error Pattern | Week 1 | Week 2 | Week 3 | Week 4 | Trend |
|---------------|--------|--------|--------|--------|-------|
| Hallucination | 5 | 4 | 2 | 1 | ↓ Improving |
| Tone mismatch | 3 | 3 | 4 | 5 | ↑ Degrading |
| Edge cases | 2 | 1 | 1 | 1 | → Stable |

**Interpretation:**
- Hallucinations: Fixes working, continue monitoring
- Tone mismatch: New issue emerging, investigate
- Edge cases: Expected baseline, acceptable

---

## Root Cause Analysis Questions

When documenting an error pattern:

1. **What:** What exactly happened?
2. **When:** Under what conditions?
3. **How often:** Rare, occasional, frequent?
4. **Impact:** What's the consequence?
5. **Why:** What's the likely root cause?
6. **Fix:** How could we prevent this?
7. **Test:** How would we catch this in evals?

---

## Using This Template

1. **When errors occur:** Add to the table immediately
2. **Weekly:** Review and prioritize
3. **Monthly:** Analyze patterns and trends
4. **Per cycle:** Turn top patterns into fixes
5. **Always:** Add new test cases for fixed patterns
