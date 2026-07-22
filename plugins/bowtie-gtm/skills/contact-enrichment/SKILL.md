---
name: contact-enrichment
description: Use when a list needs verified emails, phones, and profile attributes before it's usable — completing raw rows so contacts are reachable and sends don't bounce (Selection). Runs on the Growth (Verbiflow) MCP.
---

# Contact Enrichment

It fills every row with verified emails, phones, titles, and attributes so contacts are complete and reachable.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_enrich_emails` / `growth_enrich_companies` — verified emails and firmographics.
3. `growth_fetch_person_profiles` / `growth_extract_person_attributes` — titles, seniority, attributes.
4. `growth_lookup_phone_start` → `growth_lookup_phone_status` — phone numbers where available.
5. `growth_resolve_company_domains` — fix missing/ambiguous domains.

## Repurpose (the Bowtie way)

Publish a completeness summary (coverage %, verified counts) alongside the enriched list on labs.

## Notes

- Do not send, sequence, or mutate platform state unless the user explicitly asks.
