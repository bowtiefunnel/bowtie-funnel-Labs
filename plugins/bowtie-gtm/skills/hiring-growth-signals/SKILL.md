---
name: hiring-growth-signals
description: Use when you want companies showing a buying trigger — actively hiring for a role or in a growth cohort — plus the buyers behind them, so you reach out at the moment of intent (Awareness). Runs on the Growth (Verbiflow) MCP.
---

# Hiring & Growth Signals

It surfaces companies posting relevant jobs (and the buyers behind them), so you time outreach to intent instead of guessing.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_job_posting_contacts` — companies hiring for a role, plus contacts.
3. `growth_incubator_batch` / `growth_list_incubator_options` — optional cohort/accelerator signal.
4. **Sequence with a hook** tied to the trigger ("saw you're hiring an SDR…").

## Repurpose (the Bowtie way)

Publish the signal set as a dated feed — `labs.bowtiefunnel.com/<client>/hiring-signals-<week>/` — a recurring inbound-worthy asset.

## Notes

- Do not send, sequence, or mutate platform state unless the user explicitly asks.
