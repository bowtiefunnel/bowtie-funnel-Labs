<div align="center">
  <h1>🔀 llm-switchboard</h1>
  <p><strong>Local LLM prompt router — free-ish for workflow, frontier for thinking.</strong></p>

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](../../LICENSE)
![Works with Claude Code](https://img.shields.io/badge/works%20with-Claude%20Code-6b46c1.svg)
![Zero dependencies](https://img.shields.io/badge/dependencies-0-green.svg)

  <p>
    A ~130-line router that sits <b>before OpenRouter</b>. It classifies a prompt in
    <b>&lt;1ms</b>, picks the model, and hands the ID to your OpenRouter call. No extra
    network hop, no LLM-based classification — just heuristics.
  </p>
</div>

---

## 🌟 Why

Using a frontier model for every request wastes time and money. Traditional routers
burn *another* LLM call to classify the prompt. This one scores prompts locally across
weighted heuristic dimensions, so the frontier model is reserved for the work that
actually needs it.

It's a **tool**, not an agent or a skill: `prompt in → model ID out`. It never calls
the model — you do.

```
prompt ──▶ [ switchboard ]  local, <1ms, no network
                 │  model = "anthropic/claude-opus-4.8"
                 ▼
           [ OpenRouter ]  ── the paid call
                 ▼
            response
```

---

## 📦 Install

No npm, no build. Copy the one file into your project:

```bash
cp tools/llm-switchboard/btf-switchboard.js /path/to/project/lib/
```

Runs in browser and Node (ESM, zero dependencies).

---

## 🚦 Tiers → models

Every prompt lands in one of four tiers. The default table (edit freely) keeps the
cheap workflow miles on Gemini and reserves frontier Claude for thinking.

| Tier | Task shape | Standard model | Agentic model |
| :--- | :--- | :--- | :--- |
| 🟢 **SIMPLE** | narrate, classify, route | `google/gemini-2.5-flash-lite` | `google/gemini-3-flash-preview` |
| 🟡 **MEDIUM** | summaries, standard drafting | `google/gemini-3-flash-preview` | `anthropic/claude-sonnet-5` |
| 🔴 **COMPLEX** | analysis, code, long context | `anthropic/claude-sonnet-5` | `anthropic/claude-opus-4.8` |
| 🧠 **REASONING** | proofs, multi-step logic | `anthropic/claude-opus-4.8` | `anthropic/claude-fable-5` |

The **agentic** table kicks in automatically when the router detects a multi-step
tool prompt (file ops, `deploy`, `step 1… step 2`, `until it passes`), or when you
force it. Tool-loop reliability beats price there — so it climbs to premium Claude.

All slugs verified live on OpenRouter.

---

## 📖 Usage

```js
import { route } from "./btf-switchboard.js";

const { model, tier } = route("Prove that sqrt(2) is irrational, step by step.");
// → { model: "anthropic/claude-opus-4.8", tier: "REASONING", confidence: 0.88, ... }

const res = await fetch("https://openrouter.ai/api/v1/chat/completions", {
  method: "POST",
  headers: { Authorization: `Bearer ${process.env.OPENROUTER_API_KEY}`, "Content-Type": "application/json" },
  body: JSON.stringify({ model, messages: [{ role: "user", content: prompt }] }),
});
```

### Options

```js
route(prompt, {
  agentic: true,          // force the agentic table for this prompt
  tables: MY_OWN_TABLE,   // { std: {...}, ag: {...} } to override the model map
});
```

`route()` returns the classification too: `{ tier, rawTier, confidence, ambiguous, signals, agentic, tokens }`.
Use `classify(prompt)` if you only want the tier.

---

## 📊 How it works

Scores each prompt across weighted dimensions — reasoning markers, code, technical /
business-analysis vocab, creative cues, simple-question cues, agentic signatures,
imperative verbs, output-format demands — then maps the weighted score onto tier
boundaries with a sigmoid confidence. Below the confidence threshold a prompt is
**ambiguous** and falls to a safe default tier (MEDIUM).

> ⚠️ This is a **heuristic port tuned for GTM/agent prompts** — the boundaries and
> keyword lists are ours, not a byte-exact clone of any npm package. Retune
> `DIM`, `BOUND`, and `DEFAULT_TABLES` for your own prompt mix.

### Where it sits

`route()` returns `.model` only — it does **not** call OpenRouter, retry, or fall back.
Your OpenRouter wrapper owns auth, retries, and 429 handling. Keep the switchboard a
pure, local decision.

---

## 📄 License

MIT © Bowtie Funnel
