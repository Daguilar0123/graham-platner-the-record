# Architecture

How **The Platner Record** is built, and *why* it is built that way. This is an
explanation document — read it to understand the system; read [README.md](README.md)
to get oriented, [CLAUDE.md](CLAUDE.md) for the rules, and the JSON files themselves
for exact field-level reference. Major decisions have their own short records under
[`docs/adr/`](docs/adr/).

---

## 1. What constrains everything: the standpoint

Most sites are built to a *functional* spec. This one is built to an **editorial** spec,
and that spec is the strongest architectural constraint in the system — stronger than any
technical choice below.

The site documents a live, unadjudicated case from a *declared* position: allegations are
recorded as allegations and denials as denials; each item is treated as unverified until an
investigation independent of the publishing outlet corroborates it; no finding of fact is
made anywhere. See [ADR-0004](docs/adr/0004-declared-standpoint-constraint.md).

This is not a disclaimer bolted on at the end — it is *load-bearing*, and it shows up in the
data model (`independently_verified: false` everywhere), in the UI (the unchecked box is the
central visual argument), in the copy (the editorial voice is conditional, never accusatory),
and in the contribution rules. When you understand that the credibility *is* the product, the
rest of the architecture — the restraint, the sourcing, the falsifiability — follows.

## 2. Topology: one project, two repositories, one domain

```
                    daguilar0123.github.io   (GitHub Pages, static)
                              │
        ┌─────────────────────┴──────────────────────┐
        ▼                                             ▼
  /graham-platner-the-record/              /graham-platner-campaign-finance/
  ── "The Record" (THIS repo) ──           ── "The Money" (sibling repo) ──
  index.html         The Questions         index.html   the FEC IE ledger
  the-record.html    the case              (draws no conclusions — kept
  fifield-kavanaugh  the archive            deliberately separate)
  data/*.json        the content
        └──────────────── projnav strip ─────────────┘
              (identical on all 4 pages — the continuity spine)
```

The two repos are separate on purpose ([ADR-0001](docs/adr/0001-two-repos-one-domain.md)):
the money ledger draws no conclusions and must stay quarantined from the editorial site so it
can be cited independently. They are stitched into one experience only by a shared **projnav**
strip and absolute cross-links. Because the links are absolute and hard-coded, the repo names
and URL scheme are effectively a public contract — changing them is a coordinated, audited
operation, not a rename.

## 3. The spine: content is data, not markup

The single most important technical decision ([ADR-0002](docs/adr/0002-content-as-data.md)):
**the case content lives in `data/*.json`, and the HTML pages render it at runtime.**

```
  data/verification-ledger.json ─┐
  data/attacks.json ─────────────┼──► fetch() ──► vanilla JS renders ──► DOM
  data/milestones.json ──────────┤     (in <script> at the bottom of each page)
  data/fifield-kavanaugh.json ───┘
```

Why this matters:

- **The evidence is auditable as data.** Anyone can read `verification-ledger.json` and check
  the site against it. A skeptic can diff the data, not reverse-engineer the HTML.
- **Design and content are cleanly separated.** A visual change touches HTML/CSS; a factual
  correction touches JSON. The rule (in CLAUDE.md) is absolute: *design may change how data
  renders, never what it says.* If a new rendering needs a field, add the field.
- **Consequence:** pages must be served over HTTP (`fetch` can't read `file://`). There is no
  build step that inlines the data — the separation is preserved all the way to the browser.

The data files:

| File | Role |
|---|---|
| `verification-ledger.json` | Every allegation + every claimed corroboration, graded by class (EXAMINED, RELAYED, OUTCRY, ABSENT, NOT-CORROBORATED…), with provenance in the reporters' own words. `independently_verified` is `false` throughout, by design. |
| `attacks.json` | The media catalog: 35 primary story records (+ secondary list + outlet-ownership map), organized into three "waves," filterable by wave and type. |
| `milestones.json` | Campaign timeline, the monthly stories-vs-spending overlay series, and the official mandate figures (156,084 votes, etc.). |
| `fifield-kavanaugh.json` | The Fifield–Kavanaugh documentary ledger: 17 verbatim items with grades, live/deleted status, evidence links, analysis blocks, and the 2018-vs-2026 comparison. |

## 4. The rendering layer: deliberately boring

Each page is a **single self-contained HTML file** — inline `<style>`, inline `<script>`,
no framework, no bundler, no npm, no build ([ADR-0003](docs/adr/0003-no-framework-vanilla-static.md)).
The only external runtime dependencies are a few embeds: YouTube iframes, the Buy-Me-a-Coffee
widget, and (on the Fifield page only) Twitter's `widgets.js` for live-tweet embeds.

This is a choice, not a limitation. A static case file should be legible, forkable, and
archivable for years with zero toolchain. Anyone can open one file and read the whole page —
structure, styling, and logic — top to bottom.

**Design system.** All pages share one palette expressed as CSS custom properties
(`--ground`, `--surface`, `--ink`, `--accent`, `--good/--warn/--bad`, etc.), with a full
dark-mode set under `@media (prefers-color-scheme: dark)`. Fonts are system stacks (Georgia
serif for display/quotes, system sans for body, monospace for kickers/tags) — zero webfont
load. Reusable components, each ported consistently across pages:

- **projnav** — the sticky cross-site strip (the continuity spine).
- **secnav** — the fixed scroll navigator (top / prev section / next section / bottom).
- **share hub** — the click-to-preview lightbox + per-image download grid.
- **per-question share cards** — platform-aware share copy authored as *data* (the `T` map);
  X/Bluesky/Mastodon/Facebook/Email/Text each get text tuned to that platform's limits and
  link-handling. Ported from an external SharePanel spec into vanilla JS.
- **verification boxes / grade chips** — the editorial UI primitives; the unchecked box is
  the argument, the chips are the sourcing taxonomy.

## 5. The trust pipeline: how outside material gets in

Contributions are public but gated ([ADR-0006](docs/adr/0006-static-hosting-contributions-via-issues.md)):

```
  contributor
     │  opens issue via .github/ISSUE_TEMPLATE/submit-document.yml  (provenance form)
     │           — or —  uploads a file → auto-PR
     ▼
  .github/workflows/submission-checks.yml   (file-type allowlist, size, AV — advisory→required)
     ▼
  maintainer review in a sandbox        (main is branch-protected: no direct pushes)
     ▼
  merge → documents/  +  a provenance entry in documents/README.md   (what / where / when / who)
     ▼
  GitHub Pages publishes main within ~1 minute
```

The `documents/README.md` provenance ledger is itself an architectural feature: adding a file
*forces* a provenance entry, so the trust chain can't silently degrade.

## 6. Distribution & discoverability

Every page carries a self-referencing `canonical`, full `og:`/`twitter:` tags, and a JSON-LD
block typed to its content (`OpinionNewsArticle` for the front door, `Article`+`Dataset` for
the record page, `Article` for the archive). Supporting cast: `sitemap.xml`, `robots.txt`, a
custom `404.html` (branded, links back into all four pages), a Google Search Console
verification file, and the `social/` kit — 16 share images, each with a JSON metadata sidecar
and embedded EXIF/XMP attribution. The per-question share cards turn readers into distributors
with platform-tuned copy. This layer is why the site can carry its own argument into feeds
without a marketing budget.

## 7. Build & deploy

There is no build. `main` **is** the deployable artifact; GitHub Pages serves it statically
over HTTP/2 with compression and a forced HTTPS upgrade. Deploy = push to `main` (owner-gated).
Local development is a plain static file server (`python3 -m http.server`, config in the
project-root `.claude/launch.json`). Rollback = `git revert`. This is the entire ops story,
and that simplicity is a feature for something meant to persist.

## 8. Cross-cutting concerns

- **Accessibility:** WCAG AA contrast in both themes (a dark-mode contrast regression once
  shipped on the sibling repo and had to be fixed — the bar is now explicit), ARIA on the
  interactive components, `prefers-reduced-motion` respected with a reveal failsafe so content
  never hides behind a non-firing observer.
- **Performance:** no webfonts, no framework, lazy-loaded images/iframes, compressed static
  delivery, sub-200ms warm TTFB. Photo composites are JPEG, graphics are PNG/SVG.
- **Longevity:** minimal external deps, self-hosted preservation copies of key evidence,
  everything plain-text and forkable. The system is designed to still work, and still be
  auditable, years from now.

## 9. Directory map

```
graham-platner-the-record/
├── README.md              orientation (humans)
├── ARCHITECTURE.md        this file (the system, explained)
├── CLAUDE.md              rules for AI agents
├── CONTRIBUTING.md        how to submit documents / corrections
├── docs/adr/              architecture decision records (the "why" archive)
├── index.html             The Questions — editorial front door (site root)
├── the-record.html        the documentary case
├── fifield-kavanaugh.html the archival ledger
├── 404.html               branded not-found
├── data/*.json            THE CONTENT (rendered at runtime)
├── documents/             vetted public-record files + provenance ledger
├── social/                share kit (images + sidecars + svg masters + manifest)
├── .github/               issue template + CI checks (the intake pipeline)
└── sitemap.xml · robots.txt · google…html   discoverability
```

## 10. Where the "why" lives

Point-in-time decisions are recorded as ADRs so they aren't relitigated from memory:

- [0001 — Two repos, one domain](docs/adr/0001-two-repos-one-domain.md)
- [0002 — Content as data](docs/adr/0002-content-as-data.md)
- [0003 — No framework; vanilla static](docs/adr/0003-no-framework-vanilla-static.md)
- [0004 — The declared standpoint as a hard constraint](docs/adr/0004-declared-standpoint-constraint.md)
- [0005 — Lead with The Questions](docs/adr/0005-lead-with-the-questions.md)
- [0006 — Static hosting; contributions via issues](docs/adr/0006-static-hosting-contributions-via-issues.md)

---

*Maintainer: Daniel Ismael Aguilar · https://grownfromconcrete.org*
