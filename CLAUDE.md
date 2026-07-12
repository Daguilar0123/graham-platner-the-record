# CLAUDE.md — operating rules for AI agents in this repo

This file is instructions for an AI coding agent (Claude Code and similar) working on
**The Platner Record**. It is not prose for humans — see [README.md](README.md) for the
project overview and [ARCHITECTURE.md](ARCHITECTURE.md) for how the system is built and why.
Read those two first. This file is the short list of things you must not get wrong.

If any instruction here conflicts with a direct request from the owner in chat, the owner
wins — but say so explicitly rather than silently overriding a rule below.

---

## 1. Prime directive — the editorial standpoint is frozen

This project's entire value is **credibility through restraint**. It documents a live,
unadjudicated case. Every design or content change must preserve these laws:

- **Allegations are recorded as allegations; denials as denials.** The site never states or
  implies that any accuser is lying, or that any allegation is true.
- **No findings of fact.** There is no charge, court finding, or adjudication anywhere in
  this record. Do not introduce language that reads as one.
- **The declared standpoint** (printed on the pages): each item is treated as unverified
  until corroborated by an investigation *independent of the outlet that published it*;
  Platner's denial is the operative account until then.
- **`independently_verified: false` is true everywhere in the data, by design.** The unchecked
  verification box is the site's central visual argument. Never render it as "checked," and
  never replace it with a neutral icon.
- Any claim the site makes in its own voice (the editorial page) must be **falsifiable and
  conditional** ("if the evidence is what we are told…"), never an assertion of guilt.

When in doubt, a change that makes the site feel like advocacy-first (rage-bait, tabloid,
meme-ification) is wrong even if it's more persuasive. The correct register is *rigorous,
calm, archival* — a case file that does not need to shout.

## 2. Immutable content — do not alter, byte-for-byte

- Every verbatim quote (tweets, transcripts, article quotes), including `[sic]`, em-dashes,
  and the ` / ` line-break notation.
- All denials and all `independently_verified: false` semantics.
- The grade/class chip taxonomies and their meanings (EXAMINED, RELAYED, OUTCRY, etc.).
- The falsifiability pledge on the front page ("…first to say Graham Platner should go to
  prison. Period.").
- Footer does/does-not-claim language.
- Everything under `documents/` and its provenance `README.md`.
- All archive.today / Wayback / FEC / CourtListener links.

**Corrections outrank everything.** If you find an error (wrong date, byline, figure, or a
mischaracterization), correcting it is always in-scope — but mark the correction visibly in
the affected entry (see the AL-1 therapist item in `verification-ledger.json` for the pattern).

## 3. Content lives in data, not in HTML

The pages render from `data/*.json` at runtime via `fetch()`. This is the architectural spine.

- **Design may change how data renders; never what it says.** If a rendering change needs a
  new field, add the field — never alter existing values to fit the presentation.
- After editing any `data/*.json`, it MUST stay valid: `python3 -m json.tool <file>`.
- The pages fetch JSON, so **`file://` will not work** — you must serve over HTTP to preview
  (see §6).

## 4. This is one project in two repos, on one domain

- **This repo** (`graham-platner-the-record`) → `https://daguilar0123.github.io/graham-platner-the-record/`
- **Sibling** (`graham-platner-campaign-finance`, "The Money") → `…/graham-platner-campaign-finance/`

The canonical URL, every `og:`/`twitter:` tag, the sitemap, the JSON-LD, and the cross-site
nav are all hard-coded to these absolute URLs. **Do not change the repo name or URL scheme**
without updating every one of those in lockstep (a link audit before any such change is
mandatory — the pages cross-reference each other).

Page identity after the 2026-07-12 homepage swap:
- `index.html` = **The Questions** (editorial front door, site root `/`)
- `the-record.html` = the documentary case
- `fifield-kavanaugh.html` = the archival ledger

The **projnav strip** appears on all four pages (three here + the money page) and must stay
byte-identical in order and links. If you restyle or reorder it, do it on all four at once.

## 5. Git conventions

- **Never push without the owner's explicit go-ahead in chat.** Committing locally is fine and
  expected; publishing is the owner's decision (GitHub Pages serves `main` within ~1 minute).
- Before pushing the sibling money repo, `git pull --rebase origin main` first (merged PRs
  land remotely).
- Large first pushes can 400 on HTTPS; the fix is `git config http.postBuffer 157286400`.
- End commit messages with the `Co-Authored-By:` trailer for the model you are.

## 6. Local preview + verification (do this before calling anything "done")

```
python3 -m http.server 8139 --directory <repo>   # then open http://localhost:8139
```

The launch config lives at the *project root* `.claude/launch.json` (names: `record-site`
:8139, `money-page` :8137), not inside the repos.

Before considering a change complete, confirm in the browser:
- All `data/*.json` valid; every page renders with **zero console errors** and no `.err` blocks.
- The verification ledger renders (5 allegation cards + context checks) and every box still
  reads visibly **unchecked**.
- The 35-record catalog renders and its wave/type filters work.
- The Fifield page renders 17 items with embeds (6 live-tweet, 1 self-hosted, 10 click-to-load).
- Both color schemes at mobile (375px) and desktop widths (WCAG AA contrast — a dark-mode
  contrast bug once shipped; do not repeat it).

## 7. Gotchas that have bitten before

- The scroll-reveal animation hides content under `body.anim` until an IntersectionObserver
  fires. Both ledger pages carry a failsafe that drops `.anim` if the observer never fires —
  keep it if you touch that code, or a blank page can ship.
- The share cards' per-platform copy is **data** (the `T` map in `index.html`); platform
  character caps are real and were measured (X/Mastodon count a URL as 23; Bluesky counts it
  in full). If you edit share copy, re-measure against the caps.
- `.jpg` for photo composites, `.png`/`.svg` for graphics — the two YT thumbnails are JPEG on
  purpose (weight). Every social image has a `<name>.json` sidecar; keep them in sync on rename.

---

*Maintainer: Daniel Ismael Aguilar · https://grownfromconcrete.org*
