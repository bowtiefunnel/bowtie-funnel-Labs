---
name: account-market-research
description: Use when you need to understand and prioritize target companies — firmographics, funding, investor portfolio, and recent activity — before outreach (Awareness) or to find whitespace in accounts you already own (Expansion). Runs on the Growth (Verbiflow) MCP.
---

# Account & Market Research

It pulls firmographics, funding, and recent activity on any company, so you spend outreach on the accounts most likely to buy.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_research_company` — pull firmographics, funding, and recent activity.
3. `growth_get_company_research` — retrieve the completed research (returns an `artifact_id`).
4. `growth_find_investor_portfolio` — optional: an investor's other portfolio companies as lookalikes.
5. **Prioritize:** rank accounts by fit and timing, then brief sales.

## Repurpose (the Bowtie way)

Render the ranked accounts to a branded **target-account brief** and publish to `labs.bowtiefunnel.com/<client>/target-accounts/` — a page sales opens, not a spreadsheet.

## Notes

- Do not send, sequence, or mutate platform state unless the user explicitly asks.
