# Contributing — adding a skill or tool

This repo ships **reusable skills and tools for AI coding agents**. Everything follows
one convention so an agent (or a human) can add the next one without re-deciding layout.

**When asked to "add a skill/tool per CONTRIBUTING.md," follow the matching checklist below.**

---

## First: is it a skill or a tool?

- **Skill** — instructions *for the agent* (a workflow, checklist, or reference the model
  reads and follows). No runtime code runs on its own. → goes in [`skills/`](skills/).
- **Tool** — reusable *runtime code* the agent imports/runs (`prompt in → result out`).
  → goes in [`tools/`](tools/).

If it does work at runtime, it's a tool. If it changes how the agent thinks or acts, it's a skill.

---

## Add a SKILL

1. **Create** `skills/<name>/SKILL.md` (kebab-case name). Front-matter + body:
   ```markdown
   ---
   name: <name>
   description: Use when <triggering conditions> — <what it helps do>.
   ---
   # <Name>
   ## Overview … ## When to use … ## Steps … ## Common mistakes
   ```
   Put any heavy reference or scripts in `skills/<name>/reference/`.
2. **Register** it in [`README.md`](README.md) under `## Skills` — copy an existing entry's
   shape (heading link, badges, 2–3 line description, install block).
3. **Add a landing-page card** to the **Skill directory** `<section aria-label="Skills">`
   in [`docs/index.html`](docs/index.html) — reuse the `.skill-card` markup. A skill/tool
   that isn't on the landing page is invisible from the front door of labs.bowtiefunnel.com.
4. **Verify** the description's trigger is specific and third-person ("Use when…").
5. Commit + push (see **Ship** below).

## Add a TOOL

1. **Create** `tools/<name>/` with:
   - `btf-<name>.js` (or the code file) — ESM, **zero dependencies**, browser + Node where possible.
     Export a small, obvious API. Leave a runnable self-check.
   - `README.md` — package-style, mirroring the layout of
     [`tools/llm-switchboard/README.md`](tools/llm-switchboard/README.md):
     **what it is → install (copy the file) → tier/usage table → usage snippet → how it works → license.**
2. **Register** it in [`README.md`](README.md) under `## Tools` (2–3 line blurb + install/use snippet).
3. **Add two web cards** so it's discoverable on both surfaces of labs.bowtiefunnel.com:
   - **Landing page** — a `.skill-card` in the **Tool directory** `<section aria-label="Tools">`
     of [`docs/index.html`](docs/index.html).
   - **Tools page** — a `.toolcard` block in the **"Our own tools"** `<section class="own">`
     of [`docs/tools/index.html`](docs/tools/index.html).

   Both link to the GitHub folder (tools aren't under `docs/`, so they aren't web-served).
   Reuse existing markup + theme tokens; don't invent new styles.
4. **Verify — required for tools.** Run the self-check before committing:
   ```bash
   node --input-type=module -e 'import { <fn> } from "./tools/<name>/btf-<name>.js"; /* assert expected outputs */'
   ```
   Never ship model/slug/endpoint values you didn't verify live (e.g. OpenRouter model
   slugs rotate — confirm against the live API, don't trust memory).

---

## Ship (both)

```bash
git pull --rebase origin main          # sync first
git add <paths>
git commit -m "<Type>: <what changed>

Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>"
git push origin main
```

Then **confirm it's live**: the repo deploys via GitHub Pages from `main` `/docs` at
**[labs.bowtiefunnel.com](https://labs.bowtiefunnel.com)**. For a page change, curl the URL
and grep for your addition (Pages rebuilds in ~1 min).

## House rules

- **One folder per skill/tool.** Name in kebab-case. Don't scatter files.
- **Reuse before adding** — check `skills/` and `tools/` for something close first.
- **Keep it portable** — no secrets, no hard-coded local paths, MIT-compatible.
- **Update the index** — a new folder that isn't linked from `README.md` doesn't exist.
- **Verify, then claim done** — if a check failed or was skipped, say so.
