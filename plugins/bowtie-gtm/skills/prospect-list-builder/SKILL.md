---
name: prospect-list-builder
description: Use when you need a targeted contact list — people at known companies, a persona search, or LinkedIn — as the audience for an outbound play (Awareness) or net-new buyers inside existing accounts (Expansion). Runs on the Growth (Verbiflow) MCP.
---

# Prospect List Builder

Give it companies, titles, or a persona; it returns named contacts with the fields you need to reach them.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_find_people_at_companies` — people at a known company list (or `growth_targeted_search_people` for a persona).
3. `growth_get_people_at_companies_page` — page the results.
4. Hand the `artifact_id` to **Contact Enrichment** and **Lead Qualification**.

## Repurpose (the Bowtie way)

Publish the built list to a branded page at `labs.bowtiefunnel.com/<client>/target-list/` instead of exporting a CSV.

## Notes

- Bounded: `max_per_company` defaults to 5; `max_items` server ceiling 2000.
- Do not send, sequence, or mutate platform state unless the user explicitly asks.
