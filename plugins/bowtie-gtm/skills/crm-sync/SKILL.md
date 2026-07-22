---
name: crm-sync
description: Use whenever a play needs live account truth — reading and reconciling CRM objects, properties, and associations. Spans every lifecycle stage. Runs on the Growth (Verbiflow) MCP.
---

# CRM Sync

It reads and reconciles CRM objects, properties, and associations, so awareness through expansion all run off live truth.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_crm_list_properties` / `growth_crm_list_association_types` — learn the CRM's shape.
3. `growth_crm_fetch_objects` — pull contacts, companies, deals.
4. `growth_crm_fetch_associations` — resolve who's linked to what.

## Repurpose (the Bowtie way)

Feeds live account context into every other skill; publish reconciled account views where the client needs them.

## Notes

- Do not send, sequence, or mutate platform state unless the user explicitly asks.
