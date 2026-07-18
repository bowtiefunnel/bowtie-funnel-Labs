# Bowtie Funnel Resources

Reusable skills for AI coding agents. One folder per skill under [`skills/`](skills/).

## Skills

### [`pick-agent-pattern`](skills/pick-agent-pattern/)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Works with Claude Code](https://img.shields.io/badge/works%20with-Claude%20Code-6b46c1.svg)

Pick the right build pattern for an AI agent BEFORE any code is written — and
produce the explicit list of patterns NOT used, so over-engineering dies in
planning instead of in review.

Six gates, worked in order, stopping at the first that holds: buy vs build →
does this need to be an agent at all → the flowchart test (deterministic vs
model-driven control flow) → the neurosymbolic split and the 10-80-10 dial
(neurosymbolic 10-80-10 · guarded judgment ~5-90-5 · deterministic pipeline
0-100-0) → cross-cutting layers and graduated trust → the reliability floor.

Ships with two visual reference pages: the 21 agent build patterns for GTM,
and the 10-80-10 dial. Open `skills/pick-agent-pattern/reference/` in a browser.

### [`agent-anatomy`](skills/agent-anatomy/)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Works with Claude Code](https://img.shields.io/badge/works%20with-Claude%20Code-6b46c1.svg)

Organize any AI agent's project into a clean, filesystem-first layout. One agent
= one folder; every capability is a file in a conventionally-named subfolder.

Most agents start as a pile of loose files: a prompt, a few scripts, a cron job,
some notes, all in one directory. `agent-anatomy` gives them a consistent shape.

**It works two ways:**

- **Scaffold** a new agent — describe what it does, get a real `instructions.md`
  plus only the capability folders it needs.
- **Reorganize** a messy agent — it classifies every file, shows a move plan, and
  only moves things after you approve. It never deletes.

**Before → after:**

```text
support-bot/                     support-bot/
├── prompt.txt                   ├── instructions.md          (the system prompt)
├── refund_tool.py               ├── tools/
├── how_to_escalate.md    ─►     │   └── issue_refund.py      (path = tool name)
├── daily_report.py              ├── skills/
├── slack.py                     │   └── how-to-escalate.md   (on-demand procedure)
├── utils.py                     ├── schedules/
└── notes.txt                    │   └── daily_report.py      (cron job)
                                 ├── channels/
                                 │   └── slack.py             (inbound webhook)
                                 ├── lib/
                                 │   └── utils.py             (shared helper)
                                 └── notes.txt                (dev scratch — left in place)
```

See [`examples/`](examples/) for the full walkthrough.

## Install

Copy the skill folder you want into your Claude Code skills directory:

```bash
# pick-agent-pattern — personal (all projects)
cp -r skills/pick-agent-pattern ~/.claude/skills/

# pick-agent-pattern — project-scoped
cp -r skills/pick-agent-pattern /path/to/project/.claude/skills/

# agent-anatomy — personal (all projects)
cp -r skills/agent-anatomy ~/.claude/skills/

# agent-anatomy — project-scoped
cp -r skills/agent-anatomy /path/to/project/.claude/skills/
```

## Use

Invoke a skill by name (`/pick-agent-pattern`, `/agent-anatomy`), or just
describe the task — the skill triggers itself:

> "should this workflow be an agent?"
> "what pattern should this agent use?"
> "organize this agent folder"
> "scaffold a new agent that answers support tickets"

## Landing page

A standalone page lives at [`docs/index.html`](docs/index.html), served via
GitHub Pages at **[labs.bowtiefunnel.com](https://labs.bowtiefunnel.com)**.

To wire it up: **Settings → Pages → Source: Deploy from a branch → `main` /
`/docs`**, then add the custom domain (the [`docs/CNAME`](docs/CNAME) file already
points at `labs.bowtiefunnel.com`). Add a `CNAME` DNS record for `labs` →
`<user>.github.io` at your DNS host, then enable **Enforce HTTPS**.

## License

[MIT](LICENSE)
