---
name: test-first
description: >
  Generate test suites from existing code before modifying it. AI-generated
  safety nets. Use when user says 'test first', 'generate tests', 'safety net',
  'before I change this code', 'create tests for existing code'.
user-invocable: true
---

# Test First

Generate a test suite from existing code before making changes. Tests capture current behavior so modifications are safe.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 TEST FIRST — Safety Net Before Changes
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Before changing code, let me generate tests that capture how
it works today.

What code do you want to modify? Give me:
- A file path, or
- A module/function name, or
- A description of what you're about to change

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Context

The user is a PM who codes. Before AI, generating a comprehensive test suite for unfamiliar code was a multi-day effort. Now Claude can read the code, understand its behavior, and produce tests in minutes. This is one of the highest-leverage uses of AI in coding: not writing new code, but making existing code safe to change.

Reference: `docs/coding/test-first.md` for the pattern. `docs/coding/solo-projects.md` for testing standards.

## Skip Check

Before proceeding, evaluate whether test-first is appropriate. Ask the user if unclear.

**Always use test-first when:**
- Modifying code the user did not write
- Changing code the user wrote but does not fully remember
- Refactoring (behavior should be identical before and after)
- Touching anything with complex business logic

**OK to skip when:**
- Writing brand new code (nothing to capture yet — write tests alongside instead)
- Trivial changes (fixing a typo, updating a string literal)
- Throwaway prototypes that will be discarded

If the situation calls for skipping, tell the user:

```
This looks like [new code / trivial change / prototype]. Test-first
is for capturing existing behavior before changing it. For this case,
[write tests alongside / skip tests / keep it simple].

Want to proceed with test-first anyway, or move on?
```

## Workflow

### Step 1: Understand the Code

1. Read the file(s) the user identified
2. Identify the project's test framework and conventions:
   - Look for existing test files, test directories, test config
   - Check package.json / Makefile / project config for test commands
   - Note the test file naming convention (e.g., `*.test.ts`, `*_test.go`, `test_*.py`)
3. Identify the public interface of the code to test:
   - Exported functions / methods
   - API endpoints
   - Component behavior (for UI code)
4. Summarize back to the user:

```
Here's what I see:

- File: [path]
- Test framework: [jest/pytest/ExUnit/etc.]
- Existing tests: [yes, at path / no]
- Functions to cover:
  1. [function_name] — [one-line description]
  2. [function_name] — [one-line description]
  ...

I'll generate tests covering:
- Happy path (standard inputs, expected outputs)
- Edge cases (empty inputs, missing data, boundary values)
- Error handling (what happens when things fail)
- Side effects (external calls, state changes)

Ready to generate?
```

### Step 2: Generate the Test Suite

Write tests that cover:

**Happy path (required):**
- Standard inputs produce expected outputs
- Core functionality works as documented/intended

**Edge cases (required):**
- Empty or null inputs
- Missing optional data
- Boundary values (zero, max, empty arrays)
- Unexpected types (if the language allows)

**Error handling (required):**
- Invalid inputs produce appropriate errors
- External dependency failures are handled
- Error messages are meaningful

**Side effects (when applicable):**
- External API calls are made with correct parameters
- State is modified as expected
- Events/callbacks fire correctly

**Test writing rules:**
- Match the project's existing test conventions exactly (file location, naming, style)
- Use the project's existing test utilities and helpers
- Each test should be independent — no shared mutable state between tests
- Test names describe the behavior, not the implementation
- Mock external dependencies, not internal logic

### Step 3: Verify the Baseline

1. Run the generated tests against the existing (unmodified) code
2. ALL tests must pass. This is the green baseline.

**If tests fail:**
- The test is wrong, not the code. The code is the source of truth for current behavior.
- Fix the failing tests. Do not modify the source code.
- Re-run until all tests pass.

Report the baseline:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 BASELINE ESTABLISHED

 Tests generated: [N]
 Tests passing:   [N] / [N]
 Coverage:        [happy path, edge cases, error handling, side effects]

 Green baseline confirmed. Safe to make changes.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Step 4: Proceed with Changes

Once baseline is green, ask:

```
Safety net is in place. What changes do you want to make?

After each change, I'll run the test suite:
- Tests pass  ->  Change is safe
- Tests fail  ->  We decide: intentional behavior change
                   (update the test) or bug (fix the change)
```

Then work through the user's changes iteratively:
1. Make a change
2. Run the test suite
3. If tests fail, show which tests failed and why
4. Ask: "Is this intentional (the behavior should change) or a bug?"
   - Intentional: update the failing tests to reflect new behavior
   - Bug: revert or fix the change
5. Repeat until all changes are complete

### Step 5: Add Tests for New Behavior

After the user's changes are stable and all existing tests pass (or are intentionally updated):

```
Existing behavior is covered. Now let me add tests for the new
behavior you introduced.
```

Generate additional tests for any new functionality, following the same coverage pattern (happy path, edge cases, error handling, side effects).

Run the full suite one final time to confirm everything passes.

## Completion

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 TEST FIRST — Complete

 Original tests:    [N] (baseline behavior)
 Updated tests:     [N] (intentional changes)
 New tests:         [N] (new behavior)
 Total passing:     [N] / [N]

 Code is safe. Ready for quality gates (/quality-gates).
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Rules

- Never modify the source code during Steps 1-3. Only tests are written/fixed during baseline establishment.
- The existing code is the source of truth. If a test fails against existing code, the test is wrong.
- Match the project's test conventions exactly. Do not introduce a different test style.
- Run tests after every change, not just at the end.
- If the user wants to skip baseline verification (Step 3), push back: "Running the baseline is what makes the safety net trustworthy. It takes seconds."
