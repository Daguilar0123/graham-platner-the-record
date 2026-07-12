# 0002 — Case content lives in JSON, rendered at runtime

**Status:** Accepted (2026-07)

## Context

The site's credibility rests on the *evidence* being auditable, and on a hard wall between
what the site *says* (facts, quotes, provenance) and how it *looks* (design). If content were
authored directly in HTML, a design change and a factual change would touch the same code, and
a skeptic auditing the claims would have to read the markup to find them.

## Decision

Store the case content in `data/*.json` (verification ledger, media catalog, milestones,
Fifield ledger) and have each page **`fetch()` and render it at runtime** in vanilla JS. The
governing rule: *design may change how data renders, never what it says.* New rendering needs
get a new field; existing values are never altered to fit presentation.

## Consequences

- The evidence is auditable as structured data — anyone can read or diff the JSON directly.
- Content edits (and corrections) are isolated to data files; design edits are isolated to
  HTML/CSS. The two never collide.
- Pages must be served over HTTP — `fetch` cannot read `file://` — so local preview requires a
  static server, and there is no build step that inlines the data.
- Every data edit must keep the JSON valid (`python3 -m json.tool`), since a parse error blanks
  the section that depends on it.
