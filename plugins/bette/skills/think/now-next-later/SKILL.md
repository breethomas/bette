---
name: now-next-later
description: Generate a Now-Next-Later roadmap using Janna Bastow's framework. Communicates sequence and certainty without false dates.
---

# Now-Next-Later Roadmap

Create a **Now-Next-Later roadmap** using Janna Bastow's framework.

**Works with:**
- **Linear MCP** - Reads your projects and generates roadmap automatically
- **GitHub MCP** - Reads your projects/milestones and generates roadmap automatically
- **Manual** - Describe your projects directly

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 NOW-NEXT-LATER ROADMAP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Roadmaps should communicate sequence and certainty, not dates.

What do you want to do?

  1. Generate roadmap from Linear/GitHub
     → I'll fetch your projects and categorize them

  2. Create roadmap from description
     → Tell me about your projects

  3. Review existing roadmap
     → Paste your current roadmap for analysis

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## What This Does

Transforms your projects into a roadmap that communicates **sequence and certainty** without false dates.

## Usage

```
/now-next-later
```

**Optional parameters:**
- `/now-next-later --team [team-name]` - Roadmap for specific team
- `/now-next-later --export` - Generate markdown/mermaid diagram
- `/now-next-later --send-to-linear` - Create Linear issues from roadmap

## What Happens

1. **Fetches projects** from Linear or GitHub (if MCPs configured)
2. **Applies Janna Bastow's framework:**
   - **NOW:** High certainty, committed work (current sprint/cycle)
   - **NEXT:** Medium certainty, exploring solutions (next 1-2 cycles)
   - **LATER:** Low certainty, ideas and options (future, TBD)
3. **Categorizes projects** based on:
   - Certainty level
   - Dependencies
   - Discovery state
   - Team capacity
4. **Generates roadmap** showing sequence without dates

## Linear Integration

When you use `--send-to-linear`, the command creates Linear issues with clear categorization:

### How Issues Are Categorized

Each issue gets:
- **Title prefix:** `[NOW]`, `[NEXT]`, or `[LATER]` for instant visibility
- **Description:** Includes priority category, rationale, dependencies, and success criteria
- **Priority level:** Set appropriately (1 for NOW, 2 for NEXT, 0 for LATER)

### Finding Your Roadmap Issues in Linear

**Create saved views** to organize roadmap items:

1. **Go to your team's Issues page in Linear**
2. **Click Filters** button
3. **Add filter:** Select **Content** → type `[NOW]` (or `[NEXT]` or `[LATER]`)
4. **Click "Save as View"** - Name it "🎯 NOW Roadmap Items"
5. **Repeat for NEXT and LATER**

**Recommended views:**
- 🎯 **NOW Roadmap Items** - Filter: `Content: [NOW]`
- ➡️ **NEXT Roadmap Items** - Filter: `Content: [NEXT]`
- 🔮 **LATER Roadmap Items** - Filter: `Content: [LATER]`

## Example Output

```
📅 Now-Next-Later Roadmap

🎯 NOW (High certainty - we're building this)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✓ [PROJ-12] Mobile app redesign
  Status: In progress, 60% complete
  Why Now: User research done, designs validated, eng capacity allocated

✓ [PROJ-18] Payment flow optimization
  Status: Ready to build
  Why Now: Critical for Q1 revenue goal, solution de-risked

➡️ NEXT (Medium certainty - we're exploring)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
○ [PROJ-24] AI recommendation engine
  Status: Discovery phase
  Why Next: Technical feasibility confirmed, need to validate value
  Dependencies: Waiting on data pipeline completion

○ [PROJ-31] Team collaboration features
  Status: Solution being explored
  Why Next: Customer demand validated, choosing between 3 approaches

🔮 LATER (Low certainty - we're considering)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
◌ API v3 rewrite
  Why Later: Need to validate API v2 usage first

◌ Enterprise SSO
  Why Later: Depends on enterprise market traction

◌ Mobile widgets
  Why Later: Interesting idea, needs customer validation

💡 Roadmap Principles:
- NOW = Committed (we're doing this)
- NEXT = Probable (we're likely doing this if discovery goes well)
- LATER = Possible (we might do this, many options)
- No fake dates - communicate sequence and certainty instead
```

## Integration Options

**With Linear MCP:**
Automatically fetches Linear projects and roadmap data.

**With GitHub MCP:**
Automatically fetches GitHub Projects and Milestones.

**Manual mode:**
Describe your projects and the command will organize them:
```
Help me organize these projects into a Now-Next-Later roadmap: [paste projects]
```

## Learn More

See the full Now-Next-Later framework at:
`frameworks/planning/now-next-later.md`

---

**Framework:** Janna Bastow (ProdPad, Mind the Product)
**Best for:** Roadmap communication, stakeholder alignment, embracing uncertainty
**AI-era adaptation:** Roadmaps update faster with rapid prototyping - keep them flexible
