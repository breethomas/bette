---
name: competitive-research
description: Systematic competitive intelligence with parallel agent analysis. Analyzes competitors thoroughly and synthesizes into actionable insights.
---

# Competitive Research

Conduct systematic competitive research using the **competitor-researcher** agent. Analyzes each competitor thoroughly and synthesizes findings into actionable insights.

**Inspired by Teresa Torres' workflow for systematic competitive intelligence.**

## Entry Point

When this skill is invoked, start with:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 COMPETITIVE RESEARCH
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Systematic competitive intelligence that compounds over time.

What competitors do you want to analyze?
(Names or URLs)

What's your focus?
  • Pricing
  • AI features
  • UX/product experience
  • Go-to-market
  • All of the above

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Usage

```
/competitive-research
```

Then provide:
- Competitors to analyze (names or URLs)
- Focus areas (pricing, AI features, UX, etc.)

## What Happens

1. **Gathers input** - Which competitors? What focus?
2. **Researches sequentially** - Each competitor analyzed thoroughly (10-15 min each)
3. **Saves individual files** - One markdown file per competitor
4. **Synthesizes findings** - Comparison tables and strategic recommendations
5. **Creates Linear issue** (optional) - Track insights in your workflow

## First-Time Setup

On first run, you'll be asked where to save research:

```
Where should I save competitive research files?

Recommendation: Create a directory OUTSIDE your company codebase, like:
- ~/Documents/pm-work/competitive-research
- ~/pm-research
- ~/competitive-intel

This keeps sensitive competitive analysis separate from your company's git repos.
```

## The Compound Effect

This is your FIRST analysis - thorough and time-consuming.
Next time you update this research? Minutes, not hours.
That's how systems compound.

| Analysis Round | Time | What Happens |
|----------------|------|--------------|
| First | 1 hour | Thorough, structured research |
| Second | 15 min | Update existing files |
| Third | 15 min | Compare to previous versions |

## Output Structure

```
[research-dir]/
└── YYYY-MM-DD-[topic]/
    ├── competitor-1.md      # Individual analysis
    ├── competitor-2.md      # Individual analysis
    ├── competitor-3.md      # Individual analysis
    └── synthesis.md         # Comparison & recommendations
```

## Synthesis Contents

The synthesis file includes:
- **Executive Summary** - What did you learn?
- **Strategic Positioning Comparison** - How competitors position
- **Feature/Capability Comparison** - Side-by-side table
- **Pricing Comparison** - Models and tiers
- **Strategic Gaps & Opportunities** - Where can we win?
- **Recommended Actions** - Now, next, later

## Linear Integration (Optional)

If Linear MCP is configured:
- Creates issue with executive summary
- Links to research files
- Highlights top 3 recommended actions
- Labels with "competitive-intel"

## Related Commands

- `/strategy-session "competitive positioning"` - Discuss findings strategically

---

**Philosophy (Teresa Torres):**
- Sequential reliability - Process one competitor at a time
- Compounding system - First analysis is thorough, updates are fast
- Data ownership - Everything stored locally
- Synthesis matters - Raw research isn't useful without insights
