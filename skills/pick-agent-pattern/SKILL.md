---
name: pick-agent-pattern
description: Use when planning a new AI agent, turning an existing workflow into an agent, or auditing an agent for over-engineering — before an architecture is settled or a spec is written. Triggers on "plan this agent", "what pattern should this agent use", "make this workflow an agent", "should this be an agent", "rebuild X agent", or "is this over-engineered".
---

# Pick Agent Pattern

Run the gate sequence that picks an agent's build pattern and forces the
"patterns NOT used" list, so over-engineering dies in planning.

**The gates live in ONE place — read them, never reproduce from memory:**
`pick_agent_pattern.md` (in this skill's folder)

The framework the gates encode is explained visually in two reference pages
(open them in a browser):

- `reference/agent-build-patterns.html` — the 21 control-flow patterns
  (chains, routers, ReAct, orchestrator-worker…) and the choosing rule:
  can you draw the flowchart before runtime?
- `reference/the-dial.html` — the 10-80-10 dial: the three build tiers
  (neurosymbolic 10-80-10 · guarded judgment ~5-90-5 · deterministic
  pipeline 0-100-0/0-100-5), the two-question ambiguity test, and the
  pyramid discipline (most agents are pipelines; only a handful reason).

## Steps

1. Read the canonical gates doc above in full (it evolves; memory of it is
   stale). The intake block and gates are inside it.
2. Fill the doc's intake block from the user's request and the codebase — including
   the two reuse lines (shared plumbing to reuse; competitor/parity evidence, i.e. a
   feature-by-feature table against the product being rebuilt). Fields the user
   didn't supply: estimate them and mark `[assumed]` — only stop to ask if the
   description is too vague to pass Gate 2 (the doc's 3-question rule). Include the
   filled intake in your output. If a parity pass hasn't been done for a competitor
   rebuild, recommend doing it BEFORE the gates so scope is settled.
3. Work Gates 0→5 IN ORDER, stopping at the first that holds. Do not skip a gate;
   do not escalate past a gate that holds.
4. Produce the doc's 5-part output format (verdict line with the dial tier,
   NEURAL/SYMBOLIC/HUMAN flowchart, patterns NOT used, v0, top-3 failure
   modes → gates). Under a page.
5. If this feeds a build: fold the verdict into the agent's spec, and record the
   calibration result in the doc's Edge Cases section so the gates keep learning.

## Red flags

- Reciting gates from memory instead of reading the doc → stale gates, missed rules.
- Producing a verdict without the "patterns NOT used" list → the list is the point.
- Orchestrator–worker chosen because "the job is big" → re-check Gate 2; big ≠ unknowable.
- Most verdicts coming out neurosymbolic → gates escalated too easily; a healthy
  fleet is a pyramid (see reference/the-dial.html).
