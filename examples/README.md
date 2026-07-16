# Example: reorganizing a support bot

A real run of the [`agent-anatomy`](../skills/agent-anatomy/) skill on a messy
agent folder.

## Before

A support agent's files, all dumped in the root — no structure, unclear what's
what:

```text
support-bot/
├── prompt.txt          # the system prompt
├── refund_tool.py      # def issue_refund(order_id)
├── lookup-order.py     # def lookup_order(order_id)
├── how_to_escalate.md  # a procedure the agent follows
├── daily_report.py     # "runs every morning at 9am"
├── slack.py            # receives messages from a slack webhook
├── utils.py            # def format_currency(cents)
└── notes.txt           # dev scratch: "todo: fix the refund bug"
```

## The skill's move plan

It classifies each file and shows this **before touching anything** — moves only
happen after you approve:

```text
current path        →  new path                    reason
prompt.txt          →  instructions.md             system prompt (the required file)
refund_tool.py      →  tools/issue_refund.py       discrete action; path = tool name
lookup-order.py     →  tools/lookup_order.py       discrete action
how_to_escalate.md  →  skills/how-to-escalate.md   on-demand procedure
daily_report.py     →  schedules/daily_report.py   cron job
slack.py            →  channels/slack.py           inbound message channel
utils.py            →  lib/utils.py                shared helper, not a capability
notes.txt           →  (leave in place)            dev scratch — flagged, not moved
```

## After

```text
support-bot/
├── instructions.md
├── notes.txt                    # left in place
├── tools/
│   ├── issue_refund.py
│   └── lookup_order.py
├── skills/
│   └── how-to-escalate.md
├── schedules/
│   └── daily_report.py
├── channels/
│   └── slack.py
└── lib/
    └── utils.py
```

Nothing deleted — 8 files before, 8 after, same contents, just relocated and
renamed. No empty folders are created (`connections/`, `subagents/`, `memory/`
don't appear because no file warranted them).
