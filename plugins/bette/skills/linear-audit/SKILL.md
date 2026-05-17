---
name: linear-audit
description: Audit Linear at any altitude — workspace, project, or team. Use for "audit my Linear", "Linear workspace health", "pre-flight check", "before starting backlog work", "is this project on track", "project health", "stalled", "at risk", "how does this team write issues", "issue audit", "onboarding to a new team", or any request to inspect Linear structure, conventions, or execution health.
---

# Linear Audit

One entry point for Linear inspection. Dispatch to the right backing agent based on what the user is asking about.

## Prerequisites

Linear MCP must be configured. If it's not, tell Bree and stop.

## Routing

Pick the agent that matches user intent. If intent is ambiguous, ask one question and proceed.

- **Workspace altitude** — "audit my Linear", "workspace health", "pre-flight", "where do I start", "how is this org using Linear", or no specific target named.
  Dispatch the **linear-workspace-analyzer** agent. No input needed.

- **Project altitude** — "is [project] on track", "health of [project]", "project health", "stalled", "at risk", named project.
  Dispatch the **project-health-checker** agent. Pass the project name.

- **Team altitude** — "how does [team] write issues", "issue audit on [team]", "onboarding to [team]", "team conventions", named team.
  Dispatch the **team-organization-analyzer** agent. Pass the team name.

The agents own the analysis logic — thresholds, sampling, report format. Don't reimplement here.

## After the Report

Offer concrete next steps from the agent output (red flags, follow-up prompts, or a related altitude — e.g., a workspace audit naturally suggests project-health on flagged projects).
