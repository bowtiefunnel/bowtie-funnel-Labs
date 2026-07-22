---
name: multichannel-sender
description: Use when a sequence is ready to send across email and LinkedIn with deliverability and sender-match checks first (Education), or to run welcome flows (Onboarding). Runs on the Growth (Verbiflow) MCP.
---

# Multichannel Sender

It sends and tracks email and LinkedIn touches, with deliverability and sender-match checks before anything goes out.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_test_sender_matching` — confirm the right sender is matched.
3. `growth_sandbox_send_test_email` — a safe test before the real send.
4. `growth_email_send` / `growth_linkedin_send_connect` / `growth_linkedin_send_message` — send **only when the user explicitly asks**.
5. `growth_email_get_send_status` — track delivery.

## Repurpose (the Bowtie way)

Publish a send/deliverability summary (sender, warmup, results) per campaign for the client record.

## Notes

- Never send or connect without explicit user approval.
- Do not send, sequence, or mutate platform state unless the user explicitly asks.
