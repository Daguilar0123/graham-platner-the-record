# Graham Platner: The Record

Public documentation site for the Graham Platner case as a whole — his own words,
a verification ledger of every allegation and its claimed corroboration, the
FEC-documented outside money, and a catalog of every major negative story from
campaign launch (Aug 2025) to withdrawal (Jul 10, 2026).

**Live site:** https://daguilar0123.github.io/graham-platner-the-record/
**Companion ledger:** https://daguilar0123.github.io/graham-platner-campaign-finance/ —
the standalone FEC independent-expenditure record (kept deliberately separate;
it draws no conclusions).

## The standpoint, declared

This site reads the case from a stated editorial position, printed at the top of
the page: Platner denies the allegations, and until an item of corroborating
evidence is verified by an investigation independent of the outlet that published
it, the site treats the item as unverified and his denial as the operative
account. The site never states that any accuser is lying; allegations are
recorded as allegations, denials as denials. No charge, court finding, or
adjudication exists anywhere in this record.

## Structure

- `index.html` — The Questions: the editorial front door (commentary, clearly labeled), funneling to the documentary pages
- `the-record.html` — the record page: his words, the verification ledger, the money summary, the catalog, the overlay, the mandate
- `fifield-kavanaugh.html` — the Fifield–Kavanaugh documentary file
- `data/attacks.json` — the media catalog (35 primary records + secondary list + outlet ownership)
- `data/verification-ledger.json` — every allegation, every evidence item, provenance in the reporters' own words
- `data/milestones.json` — campaign milestones, monthly stories-vs-spending overlay, official primary results
- `documents/` — vetted public-record documents, each with a provenance note

## Documentation

- **[ARCHITECTURE.md](ARCHITECTURE.md)** — how the whole system is built and *why* (the
  two-repo topology, the content-as-data spine, the render pipeline, the trust pipeline).
- **[docs/adr/](docs/adr/)** — Architecture Decision Records: the "why" behind each major choice.
- **[CLAUDE.md](CLAUDE.md)** — operating rules for AI agents working in this repo.
- **[CONTRIBUTING.md](CONTRIBUTING.md)** — how to submit documents and corrections.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Short version: free GitHub account,
[submit a document](../../issues/new?template=submit-document.yml) with
provenance, maintainer review + automated security checks before anything
publishes. Corrections outrank everything — open an issue with a source.

© 2026 Daniel Ismael Aguilar · https://grownfromconcrete.org
