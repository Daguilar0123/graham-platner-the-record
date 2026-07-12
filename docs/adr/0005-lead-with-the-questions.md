# 0005 — Lead the site with The Questions (homepage swap)

**Status:** Accepted (2026-07-12)

## Context

The site originally opened on *The Record* (the documentary case) at the root URL, with the
editorial (*The Questions*) as an inner page. As the editorial matured it became the clearest
statement of the project's purpose — the "why" — and the natural entry point that should funnel
readers to the documentary pages. The catch: the record repo had never been pushed, so the URL
layout was still free to change with zero link rot. After first publish it would cost redirects
and re-shared links permanently.

## Decision

Swap the homepage: **`the-questions.html` → `index.html`** (site root), and the former
homepage → **`the-record.html`**. Add a funnel strip on the new front door pointing to The
Record / Fifield–Kavanaugh / The Money. Do it *before* first publish.

## Consequences

- Visitors land on the argument and are routed to the receipts; the front door carries the
  project's purpose.
- One-time cost: every canonical, `og:url`, JSON-LD url, sitemap entry, the projnav order on all
  four pages (both repos), the README, and social-sidecar `source_page` fields had to be updated
  together. A full link audit was run before the swap; five in-body `./` links that meant "The
  Record" (not "self") were the sharpest hazard and were rewritten to `the-record.html`.
- The tension with [ADR-0004](0004-declared-standpoint-constraint.md) — leading with commentary
  risks reading advocacy-first — is mitigated by keeping the "this is commentary" box prominent
  and the funnel to the documentary pages high on the page.
