---
name: sequence-builder
description: Use when a qualified list needs a multi-step, multichannel (email + LinkedIn) outreach sequence drafted and wired to its audience source (Education). Runs on the Growth (Verbiflow) MCP.
---

# Sequence Builder

It drafts and publishes multi-step email + LinkedIn sequences, wired to your audience source.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_create_sequence_draft` — start the sequence.
3. `growth_update_sequence_steps` — define the steps and channels.
4. `growth_update_source_config` → `growth_run_source_preview` — wire and preview the audience.
5. `growth_publish_sequence` — publish **only when the user explicitly asks**.

## Repurpose (the Bowtie way)

Publish the sequence plan (steps, timing, channels) as a shareable page for client sign-off before it goes live.

## Notes

- Never publish or send without explicit user approval.
- Do not send, sequence, or mutate platform state unless the user explicitly asks.
