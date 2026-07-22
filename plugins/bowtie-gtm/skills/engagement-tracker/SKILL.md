---
name: engagement-tracker
description: Use when you need to see who's engaging across email and LinkedIn — replies, statuses, and full conversation history — to act at the right moment (Education), including watching the deal conversation into close (Mutual commit). Runs on the Growth (Verbiflow) MCP.
---

# Engagement Tracker

It tracks replies, send status, and full LinkedIn conversation history, so you act at the right moment.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_email_get_send_status` / `growth_linkedin_get_send_status` — delivery + reply status.
3. `growth_linkedin_get_chat_history` / `growth_linkedin_get_messages` / `growth_linkedin_list_threads` — full conversation context.
4. `growth_linkedin_get_contact_relationship` — where the relationship stands.
5. **Route** the hottest replies to sales; flag quiet threads for follow-up.

## Repurpose (the Bowtie way)

Publish an engagement digest — who replied, who's warm, what's stalled — as a weekly client-facing page.

## Notes

- Do not send, sequence, or mutate platform state unless the user explicitly asks.
