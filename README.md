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

A tight demo deck (10 slides):

- Problem → one-gateway pipeline → **code-level architecture** (Ruby classes
  × which LLM does what)
- Cite-gates (HIGH / MEDIUM / rejected), cover vision-gate flow,
  Literature DNA via **Otari code execution**
- **Budgets** — per-user monthly quota, per-call ledger
- The self-hosted **books MCP server**
- Closing: bio, photo and all the links

## Links

- Litloop: <https://github.com/nebiyuelias1/litloop> (branch: `feat/club-literature-dna`, PR #137 → `otari-hackthon`)
- Books MCP: <https://github.com/projectahi/books-mcp>
- Otari: <https://otari.ai> · <https://github.com/mozilla-ai/otari>
- Neba: <https://github.com/nebiyuelias1> · nebiyu@508.dev
