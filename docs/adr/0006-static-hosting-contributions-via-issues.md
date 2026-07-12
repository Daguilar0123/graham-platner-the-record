# 0006 — Static hosting; contributions via issues + CI

**Status:** Accepted (2026-07)

## Context

The site needs to accept public contributions (documents, corrections) from non-technical
people, treat every submission as untrusted until vetted, and never let anything reach the live
site without maintainer review — all with no server to run and no budget for infrastructure.

## Decision

Host statically on **GitHub Pages** (serving `main`), and route all contribution through
**GitHub Issues + CI**:

- A structured issue form (`.github/ISSUE_TEMPLATE/submit-document.yml`) collects the file and
  its provenance; a file upload can alternatively open an auto-PR.
- `.github/workflows/submission-checks.yml` runs automated checks (file-type allowlist, size,
  antivirus) on submissions.
- `main` is branch-protected: no direct pushes; outside changes require review + approval.
- Accepted files land in `documents/` with a mandatory entry in the `documents/README.md`
  provenance ledger.

## Consequences

- Zero backend, zero hosting cost, and a fully public, auditable contribution trail.
- The maintainer is the sole reviewer; branch protection is configured so the owner can still
  push directly while every *outside* contribution is forced through PR + review + checks.
- The `documents/README.md` provenance ledger can't silently degrade — adding a file requires
  adding its provenance entry.
- Publishing is owner-gated by convention (never push without explicit go-ahead), since a push
  to `main` is live within ~1 minute.
