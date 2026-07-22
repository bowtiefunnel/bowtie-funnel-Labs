---
name: ai-personalization
description: Use when a sequence needs genuine per-prospect openers written from real research — not mail-merge variables (Education). Runs on the Growth (Verbiflow) MCP.
---

# AI Personalization

It writes a genuine per-prospect opener from real research — their post, role, company — not a template variable.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_run_sequence_personalization` — generate openers across the list.
3. `growth_get_sequence_personalization_progress` — watch the job.
4. `growth_get_personalization` — pull the real fact behind a specific opener.
5. `growth_set_personalization_note` — pin a manual note where you want to override.

## Repurpose (the Bowtie way)

Publish a sample of personalized openers (with the evidence each is based on) for client review before send.

## Notes

- Use `growth_get_personalization` for real facts — do not invent profile details from priors.
- Do not send, sequence, or mutate platform state unless the user explicitly asks.
