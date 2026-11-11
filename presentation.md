---
title: "Litloop × Otari"
sub_title: "nebiyu@508.dev · github.com/nebiyuelias1"
author: "Neba · Nebiyu Elias"
event: "Mozilla Otari Hackathon — Devs Wilding (Nov 8–11, 2026)"
theme:
  name: light
options:
  end_slide_shorthand: true
---

## The problem

Litloop — an OS for book clubs (Amharic + English) — had rules-based metadata only:

- *"The Alchemist"* filed under **Business & Economics**
- no country of origin at all
- English descriptions for an Amharic book club
- covers = unsplash placeholders, randomly low-res

Google Books / Open Library are thin for Ethiopian titles.

**Goal:** improve book metadata with AI — grounded, sourced, reversible.

---

## What we built

One Rails pipeline where **every AI call flows through the Otari gateway** —
one virtual key, open-weight models by default:

```
books table ──▶ GROUND ──▶ JUDGE ──▶ SEE ──▶ VALIDATE ──▶ APPLY ──▶ audit
```

- gateway-run **web search**, **code execution**, **MCP servers**
- strict **structured outputs**, **Files API** vision
- Ruby-side gates — **no model output is trusted**
- every write reversible: originals + provenance in an audit JSON

---

## The code behind the pipeline

```mermaid +render
flowchart TD
  A["admin · Enrich button"] --> J["BookEnrichmentJob\nSolidQueue"]
  J --> E["BookMetadataEnricher"]
  E --> G["GROUND · gpt-oss-120b\nbooks MCP + web search"]
  G --> JU["JUDGE · gpt-oss-120b\nstrict json_schema"]
  JU -. "empty / timeout" .-> M["mistral-large"]
  JU --> CV["CoverVisionJudge\ndeepseek-v4.1-flash"]
  CV --> VA["VALIDATE\npure Ruby gates"]
  VA --> AP["APPLY\naudit JSON · reversible"]
```

*open weights first — frontier escalation only when the cheap path stalls*

---

## Cite-gates — confidence is mechanical

```mermaid +render
flowchart LR
  P["update"] --> Q1{"cited?"}
  Q1 -- yes --> H["HIGH"]
  Q1 -- no --> Q2{"quote in facts?"}
  Q2 -- yes --> M["MEDIUM"]
  Q2 -- no --> X["rejected"]
```

- unattributed claims **never reach the database**

---

## Covers — vision gates every swap

```mermaid +render
flowchart TD
  C["judge citation"] --> Q["BookCoverImprover\ncollect candidates\ncited · wiki · OL · page mining"]
  Q --> F["fetch_image_bytes\nfollow redirects"]
  F --> VG{"CoverVisionJudge\nreal cover?\nmatches? high-res?"}
  VG -- "yes" --> SW["swap + audit JSON"]
  VG -- "no / junk" --> Q
```

- bad candidates loop back until the vision budget runs out —
  only **verified** bytes touch the book

---

## Literature DNA — the sandbox draws the charts

```mermaid +render
flowchart LR
  D["club data\nreads · reviews · RSVPs"] --> W["gpt-oss-120b\nwrites matplotlib"]
  W --> S["otari_code_execution\nOtari sandbox"]
  S --> CH["📊 charts attached\n+ code · stdout audited"]
```

- panels: attendance bars · weekday donuts · genre treemap · difficulty curve

---

## Budgets — every call is metered

- `OtariUsage` ledger: **every** chat, search, vision, sandbox call
  attributed to a user + feature
- **per-user monthly quota** (default 5 runs), enforced app-side;
  admins exempt
- usage + cost per model live in the Otari dashboard

```
gpt-oss-120b : 23 calls   $ 0.0042
deepseek-vl  :  9 calls   $ 0.0011
                ───────────────
          total          $ 0.0053
```

---

## Books MCP — exact grounding

A **self-hosted books MCP server** (Cloudflare Worker): Google Books +
Open Library + Project Gutenberg, deduplicated by ISBN, cached 7 days.

- registered once in the Otari dashboard: purpose hint + tool allowlist
- the gateway runs the tool loop — the app just sends:

```ruby
client.chat(..., mcp_server_ids: [ENV["OTARI_MCP_BOOK_SERVER_ID"]])
```

- grounding **prefers MCP lookups** — exact records by ISBN where
  web search returned 646-byte fact piles

---

## Thanks

![image:width:28%](nebiyu.png)

**Neba** — 7+ years full-stack · Ethiopia 🇪🇹 → Taiwan 🇹🇼
ASUS · 508.dev · COSCUP 2026 speaker

- Litloop: `github.com/nebiyuelias1/litloop` — PR #137
- Books MCP: `github.com/projectahi/books-mcp`
- Otari: `otari.ai` · `github.com/mozilla-ai/otari`
- me: `github.com/nebiyuelias1` · `nebiyu@508.dev`
