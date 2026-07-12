# 0001 — Two repositories, one domain

**Status:** Accepted (2026-07)

## Context

The project has two distinct bodies of work: an *editorial* documentation site that reads a
contested case from a declared standpoint, and a *neutral* FEC campaign-finance ledger that
draws no conclusions at all. The money ledger's value depends on being citable on its own,
free of any editorial framing — a reporter or skeptic should be able to point to it without
inheriting the argument of the other site.

## Decision

Keep them as **two separate GitHub repositories** — `graham-platner-the-record` (editorial)
and `graham-platner-campaign-finance` (neutral ledger) — deployed under one GitHub Pages
domain, and stitched together only by a shared, identical **projnav** strip and absolute
cross-links.

## Consequences

- The money ledger stays quarantined and independently citable; its "draws no conclusions"
  claim is structurally credible because it lives apart.
- The cross-links are absolute and hard-coded, so the repo names and URL scheme become a
  public contract — changing either is a coordinated, audited edit across both repos (canonical
  tags, og/twitter, sitemaps, JSON-LD, and the projnav on all four pages), never a simple rename.
- The projnav must be kept byte-identical across all four pages; a restyle happens everywhere
  at once or not at all.
