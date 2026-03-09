---
name: bette-health
description: "Audit your Bette context architecture. Checks CLAUDE.md files, reference files, memory system, and session management. Use when user says 'check my setup', 'bette health', 'audit my context', 'is my bette working'."
user-invocable: true
---

# Bette Health Check

Audit the context architecture that powers Bette. Identifies gaps, staleness, and opportunities to level up.

## Procedure

Run each check below in order. Collect all findings, then present a single report at the end. Do NOT present findings incrementally — gather everything first.

### Check 1: Global CLAUDE.md

**File:** `~/.claude/CLAUDE.md`

- Does it exist?
- Does it contain working style preferences (planning protocol, communication style)?
- Does it reference Bette or a project workspace?
- Is it under 200 lines? (Over 200 = likely bloated, suggest trimming)

**Scoring:**
- Missing: FAIL
- Exists but minimal (under 10 lines or no structure): WARN
- Exists with clear structure: PASS

### Check 2: Project CLAUDE.md

**File:** Look for `CLAUDE.md` in the current working directory, then check parent directories (up to 3 levels).

- Does it exist?
- Does it reference context files (BACKLOG.md, GOALS.md, reference/)?
- Does it have a "Context to Load" or equivalent section?
- Does it have a prioritization filter?

**Scoring:**
- Missing: FAIL
- Exists but no context loading instructions: WARN
- Exists with context loading and filter: PASS

### Check 3: Reference Files

**Files:** Look in the project directory (where CLAUDE.md was found) for:
- `reference/people.md`
- `reference/domains.md`
- `reference/company.md`

For each file:
- Does it exist?
- Does it have a "Last updated" date?
- If it has a date, is it within the last 30 days? (Stale = over 30 days)
- Does it contain TODO placeholders that were never filled in?

**Scoring:**
- Missing: FAIL
- Exists but all TODOs / never customized: WARN
- Exists but stale (over 30 days): WARN
- Exists, customized, and current: PASS

### Check 4: SessionStart Hook

**File:** `~/.claude/settings.json`

- Does the file exist?
- Does it contain a `hooks.SessionStart` entry?
- Does the SessionStart hook reference a script that exists?
- Is the referenced script executable?

**Scoring:**
- No settings.json or no hooks: FAIL
- Hook exists but script missing or not executable: WARN
- Hook exists and script is functional: PASS

### Check 5: Memory System

**File:** Look for MEMORY.md in:
- `~/.claude/projects/` (any subdirectory)
- `~/.claude/MEMORY.md`
- Project directory `MEMORY.md`

- Does any memory file exist?
- Is it under 200 lines? (Over 200 = context bloat risk)
- Does it contain session patterns, preferences, or disambiguation notes?

**Scoring:**
- No memory file anywhere: WARN (not FAIL — memory builds over time)
- Exists but over 200 lines: WARN
- Exists and well-maintained: PASS

### Check 6: Session Management

**Directory:** Look for a `sessions/` directory in the project workspace.

- Does the directory exist?
- Are there any session files?
- When was the most recent session file created?
- Are session files following the YYYY-MM-DD naming convention?

**Scoring:**
- No sessions directory: WARN
- Directory exists but empty: WARN
- Has recent session files with proper naming: PASS

### Check 7: Backlog and Goals

**Files:** Look in the project directory for:
- `BACKLOG.md`
- `GOALS.md`

For each:
- Does it exist?
- Is it empty or only contains the template?
- Does GOALS.md have a "Last updated" date within the current quarter?

**Scoring:**
- Missing: FAIL
- Exists but empty/template-only: WARN
- Exists with real content: PASS

### Check 8: Configuration Marker

**File:** `~/.claude/.bette-configured`

- Does it exist?
- What date was it configured?
- What workspace path is recorded?

**Scoring:**
- Missing: WARN (Bette may not have been set up via bette-setup)
- Exists: PASS

---

## Report Format

After running all checks, present the report in this format:

```
Bette Health Check
==================

Maturity Level: [AD HOC / PLANNED / SYSTEMATIC / OPTIMIZED]

[Check results table]

| Check                | Status | Detail                              |
|----------------------|--------|-------------------------------------|
| Global CLAUDE.md     | [status] | [one-line detail]                 |
| Project CLAUDE.md    | [status] | [one-line detail]                 |
| Reference: people    | [status] | [one-line detail]                 |
| Reference: domains   | [status] | [one-line detail]                 |
| Reference: company   | [status] | [one-line detail]                 |
| SessionStart hook    | [status] | [one-line detail]                 |
| Memory system        | [status] | [one-line detail]                 |
| Session management   | [status] | [one-line detail]                 |
| Backlog              | [status] | [one-line detail]                 |
| Goals                | [status] | [one-line detail]                 |
| Config marker        | [status] | [one-line detail]                 |

[Next steps]
```

Use these status indicators:
- PASS — Working as expected
- WARN — Functional but could improve
- FAIL — Missing or broken, needs attention

### Maturity Level Determination

**Ad Hoc** (score 0-3 PASS):
No CLAUDE.md files, no reference files. Claude starts every session cold. Context is entirely in the user's head.

Characteristics:
- No persistent context architecture
- Every session requires re-explaining preferences and context
- No reference files for people, domains, or systems

**Planned** (score 4-6 PASS):
CLAUDE.md exists with basic preferences. Some reference files started. Context is captured but not systematically maintained.

Characteristics:
- Global or project CLAUDE.md exists with working style
- At least one reference file has real content
- Backlog or goals file exists with entries

**Systematic** (score 7-9 PASS):
Layered context architecture in place. Reference files current. Session management active. Claude has reliable context every session.

Characteristics:
- Both global and project CLAUDE.md with clear structure
- Reference files customized and updated within 30 days
- SessionStart hook configured and working
- Session notes being saved

**Optimized** (score 10-11 PASS):
Full context engineering. Memory system captures patterns. Hooks automate context loading. Skills extend capabilities. Claude is a true operating system.

Characteristics:
- Everything in Systematic, plus:
- Memory file with session patterns and disambiguation
- Regular session notes with proper naming
- Configuration marker from guided setup

### Next Steps

Based on the maturity level, suggest **exactly 3 actionable next steps** to level up. Be specific — name the file to create or update, and what to put in it.

**Ad Hoc next steps (examples):**
1. Run `/bette:bette-setup` to generate your full context architecture
2. Create `~/.claude/CLAUDE.md` with your working style preferences
3. Create a project CLAUDE.md with context loading instructions

**Planned next steps (examples):**
1. Fill in TODO placeholders in reference/people.md — add your direct reports and key collaborators
2. Add a SessionStart hook to load context automatically (run bette-setup or configure manually)
3. Update GOALS.md with this quarter's actual goals

**Systematic next steps (examples):**
1. Review MEMORY.md — prune entries over 6 months old, add recent session patterns
2. Update reference/domains.md — last updated [date], consider adding [specific gap noticed]
3. Start using session notes after major work sessions to build persistent context

**Optimized next steps (examples):**
1. Review reference file freshness — [file] was last updated [date]
2. Consider archiving old session notes (over 3 months) to keep the directory scannable
3. Check if any new team members or domain changes need to be added to reference files
