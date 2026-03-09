# 2026-03-08 — Bette Rebrand + Unified Plugin Build

## Done

### Phase 1: Rebrand
- Restructured pm-coding-guardrails → bette-work (maturity model, test-first, patterns library)
- Created bette-architect repo (5 guides, 4 annotated examples)
- Renamed pm-thought-partner → bette-think (plugin + repo, v3.0.0)
- Renamed pm-ai-playbook → bette-work
- Updated GitHub profile: Bette Davis framing, four-repo narrative
- Updated all repo descriptions, topics, local directories, remotes
- Updated global CLAUDE.md references
- Reviewed Anthropic code modernization ebook — pulled maturity model, test-first, pattern capture
- Researched obra/superpowers — SessionStart hook bootstrap, plugin architecture

### Phase 2: Plan
- Drafted unified Bette product plan (PLAN.md in bette-architect)
- Researched Claude Code plugin system — official docs + known bugs
- Resolved: hybrid bootstrap (setup generates hook in settings.json, not plugin)
- Resolved: two-path onboarding (guided + self-service)
- Resolved: modular architecture, flat routing, think active by default

### Phase 3: Build
- Created unified `bette` repo (github.com/breethomas/bette)
- 142 files: 54 skills, 7 agents, 22 frameworks, 15 thought leaders, 4 templates, 9 docs
- bette-setup skill (two-path onboarding)
- bette-health skill (context architecture audit)
- SessionStart hook script (hybrid bootstrap)
- Work skills converted to SKILL.md format
- All supporting content ported from bette-think, bette-os, bette-work, bette-architect
- Profile README updated — unified plugin as hero

## Key Decisions
- Four repos stay as educational/documentation layer
- Unified `bette` plugin is the product
- Hybrid bootstrap: setup generates SessionStart hook externally (plugin hooks broken #12151)
- Think active by default, operate and work opt-in
- No custom meta-skill router — Claude Code native discovery handles routing
- MIT license for unified plugin (CC BY-NC-SA for individual repos)

## Next
- Test install on clean machine (Balance machine ideal)
- Test bette-setup onboarding end-to-end
- Update four companion repo READMEs to point to unified bette
- Iterate on skill YAML descriptions for better routing
- Draft Slack migration message for PM team
- Clean up .makemd files that got committed accidentally

## Resume Prompt
Unified bette plugin is live at github.com/breethomas/bette. PLAN.md in bette-architect has full architecture. Four companion repos are renamed and published. Profile README leads with the unified plugin install commands.
