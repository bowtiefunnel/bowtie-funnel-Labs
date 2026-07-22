---
name: data-ops-artifacts
description: Use for the connective work between skills — listing, joining, exporting, and staging the artifacts that move data from one skill to the next. Spans every lifecycle stage. Runs on the Growth (Verbiflow) MCP.
---

# Data Ops & Artifacts

It manages the artifacts, joins, and exports that move data between every other skill, so nothing is lost between steps.

## Requires

The Growth (Verbiflow) MCP. If it isn't connected yet:

```bash
claude mcp add --transport stdio growth -- npx -y growth-mcp
```

Always call `growth_session_init` first (auth + workspace).

## Steps

1. `growth_session_init` — auth + workspace.
2. `growth_list_artifacts` / `growth_get_artifact` — find prior rows, jobs, joins.
3. `growth_join_csv_files` / `growth_join_clay_results_by_domain` — merge sources.
4. `growth_clay_export_csv` / `growth_export_job_csv` — export deliverables.
5. `growth_stage_artifact_to_sequence_source` — stage rows into a sequence for review.

## Repurpose (the Bowtie way)

Turns any artifact into a shareable export or a published labs page — the last mile of every play.

## Notes

- Prefer chaining by `artifact_id`; CSV is for import/export edges, not the default primitive.
- Do not send, sequence, or mutate platform state unless the user explicitly asks.
