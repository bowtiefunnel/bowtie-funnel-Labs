---
name: lead-qualification-scoring
description: Use when a list needs AI fit-scoring against your ICP before you spend sends on it (Selection), or to score existing accounts for upsell fit (Expansion). Runs on the Growth (Verbiflow) MCP.
---

# Lead Qualification & Scoring

It scores every row against your ICP with AI, so effort and sends only go to right-fit accounts.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_run_ai_filter_preview` / `growth_update_ai_filter_prompt` — tune the ICP prompt on a sample.
3. `growth_qualify_rows` — score the full list (caps at 500 rows/call).
4. Keep A/B-fit rows; drop the rest before sequencing.

## Repurpose (the Bowtie way)

Publish the scored list with reasons per row, so the client sees *why* each account made the cut.

## Notes

- Bounded: `growth_qualify_rows` caps at 500 rows per call — page for larger lists.
- Do not send, sequence, or mutate platform state unless the user explicitly asks.
