---
name: quality-gates
description: >
  Pre-commit checklist and coding quality standards for PMs who code. Pattern
  matching, CI/CD readiness, testing, code review. Use when user says 'quality
  gates', 'pre-commit check', 'before I push', 'check my code', 'am I ready
  to commit'.
user-invocable: true
---

# Quality Gates

Walk the user through the pre-commit checklist interactively — one gate at a time. Do not dump the full checklist. Check each gate, identify issues, and help fix them before moving on.

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 QUALITY GATES — Pre-Commit Check
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Let me walk through the gates before you commit.

First — what project are you working in? (I need to check
the codebase conventions and run the right tools.)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Context

The user is a product manager who codes, not a software engineer. The goal is to ship features quickly while respecting engineering quality. Quality gates prevent creating cleanup work for the team.

Reference: `docs/coding/quality-gates.md` for the full checklist. `docs/core-principles.md` for underlying principles.

## Workflow

Work through five gates sequentially. At each gate, Claude does the actual checking — run commands, read files, verify. Do not just ask the user "did you do X?" — verify it directly.

### Gate 1: Pattern Matching

**What Claude does:**
1. Ask what files were changed: `git diff --name-only` (staged and unstaged)
2. For each changed file, find similar existing code in the project
3. Compare the user's code against established patterns
4. Flag deviations: naming, spacing, structure, conventions

**Pass criteria:**
- Changed code follows existing patterns in the codebase
- No new patterns introduced where existing ones apply
- Naming conventions match

**If issues found:**
- Show the existing pattern and the user's deviation side by side
- Offer to fix automatically
- Do NOT proceed to Gate 2 until resolved or user explicitly accepts the deviation

### Gate 2: Code Quality

**What Claude does:**
1. Identify the project's formatter and linter (package.json, Makefile, config files)
2. Run formatters: e.g., `prettier --check`, `black --check`, `mix format --check-formatted`
3. Run linters: e.g., `eslint`, `flake8`, `credo`
4. Run type checking if applicable: e.g., `tsc --noEmit`, `mypy`

**Pass criteria:**
- Formatter reports no changes needed
- Linter reports zero errors (warnings are acceptable but flag them)
- Type checker passes clean

**If issues found:**
- Run the auto-fix commands (formatter, linter --fix)
- Show what was fixed
- Re-run checks to confirm clean

### Gate 3: Testing

**What Claude does:**
1. Check if automated tests exist for the changed code
2. Run the test suite: identify the correct test command from project config
3. Verify all tests pass
4. Ask the user: "Have you manually tested this in the actual environment?"

**Pass criteria:**
- Test suite passes (zero failures)
- Tests exist for changed functionality (flag if missing)
- User confirms manual testing

**If issues found:**
- If tests fail, show the failures and help debug
- If no tests exist for changed code, ask: "Should we generate tests before committing?" (invoke test-first pattern if yes)
- Do NOT skip — testing is non-negotiable

### Gate 4: CI/CD Readiness

**What Claude does:**
1. Identify what CI runs (look for `.github/workflows/`, `Makefile`, CI config)
2. Run everything CI will run, locally
3. Confirm all checks pass

**Pass criteria:**
- Every check CI will run has been run locally and passes
- No "I'll fix it after pushing" situations

**If issues found:**
- Fix them. Do not proceed.
- Show the user exactly what CI would have caught

### Gate 5: Code Review Readiness

**What Claude does:**
1. Run `git diff --cached` (or `git diff` if nothing staged) to see what will be committed
2. Check for accidental files (config changes, unrelated modifications, debug code)
3. Check commit is focused — does one thing
4. Assess: would a senior engineer have concerns reviewing this?

**Pass criteria:**
- Only relevant files staged
- No debug code, console.logs, commented-out code
- Changes are focused (single purpose)
- Working directory is clean of experimental code

**If issues found:**
- Help the user unstage accidental files
- Flag debug code or commented-out code for removal
- If the commit does too many things, suggest splitting

## Completion

After all five gates pass:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ALL GATES PASSED

 Gate 1: Pattern Matching    [PASS]
 Gate 2: Code Quality        [PASS]
 Gate 3: Testing             [PASS]
 Gate 4: CI/CD Readiness     [PASS]
 Gate 5: Code Review Ready   [PASS]

 Ready to commit. Go ahead.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

If any gate has warnings (not blockers):

```
 Gate X: [item]              [PASS with warnings]
   - [Warning description]
```

## Prompt Engineering Sub-Check

If `git diff` shows changes to AI prompt files (system prompts, agent prompts, prompt templates), add an additional check after Gate 2:

**Prompt Engineering Gate:**
1. Identify the failure mode being addressed
2. Check for hard constraints (NEVER) vs soft guidance
3. Check for specific BAD/GOOD examples
4. Check for dependent operation conflicts
5. Ask: "How will you verify this prompt change works?"

Reference: `docs/coding/prompt-engineering.md` for the full framework.

## Rules

- Never skip a gate. If the user asks to skip, explain why that gate matters.
- Do the checking yourself — run commands, read code, verify. Do not just ask the user to self-report.
- Fix issues at the gate where they're found. Do not accumulate a list for later.
- If working in a team codebase, be extra strict on pattern matching (Gate 1).
- If working in a solo project, testing standards can be lighter but still present (see `docs/coding/solo-projects.md`).
