# Litloop × Otari — presentation slides

[Presenterm](https://github.com/mfontanini/presenterm) deck for the
**Mozilla Otari Hackathon — Devs Wilding** submission:
*AI book-metadata enrichment — grounded, judged, reversible*.

## Run it

```sh
cargo install presenterm     # https://mfontanini.github.io/presenterm
presenterm presentation.md
```

Tips:

- Slide breaks use `---` via the frontmatter `options.end_slide_shorthand: true`
  (presenterm's default separator is the `<!-- end_slide -->` comment — without
  that option the whole deck collapses into 2 slides).
- The deck uses the built-in `light` theme (white background).
- The three `mermaid +render` slides render as real diagrams in presenterm
  (mermaid-cli `mmdc` is required: `npm i -g @mermaid-js/mermaid-cli`).
  Viewed on GitHub, those blocks show as plain code — the deck in a real
  terminal (or exported PDF via `presenterm -e`) is where diagrams shine.
- Navigate with `→`/`←` (or `space`), quit with `q`. See `presenterm --help`
  for presenter-remote options.

## What's inside

A 5-minute demo deck (~20–25s per slide):

- Problem → one-gateway architecture → ground & judge → cite-gates
- Cover vision gate (and the 'Into the Wild' story)
- Live before/after results for five books
- Literature DNA via **Otari code execution** (sandbox matplotlib)
- **Budgets** — per-user monthly quota, per-call ledger
- Day 2: the self-hosted **books MCP server** and MCP-grounded enrichment
- Honest tradeoffs, submission checklist

## Links

- Litloop: <https://github.com/nebiyuelias1/litloop> (branch: `feat/club-literature-dna`, PR #137 → `otari-hackthon`)
- Books MCP: <https://github.com/projectahi/books-mcp>
- Otari: <https://otari.ai> · <https://github.com/mozilla-ai/otari>
