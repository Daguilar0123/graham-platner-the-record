# 0003 — No framework; vanilla, single-file, static

**Status:** Accepted (2026-07)

## Context

The site must remain legible, forkable, and archivable for years — potentially long after any
particular toolchain is maintained. It is a small number of pages with modest interactivity
(filters, a lightbox, tab panels, scroll nav). A React/Next build would add a bundler, a
dependency tree, and a compile step, all of which are liabilities for something meant to
persist and be independently verifiable.

## Decision

Build each page as a **single self-contained HTML file** — inline `<style>`, inline
`<script>`, no framework, no bundler, no npm, no build. Accept only a few external *runtime*
embeds (YouTube, Buy-Me-a-Coffee, and Twitter `widgets.js` on the Fifield page for live tweets).

## Consequences

- Zero build/deploy tooling: `main` is the artifact; any static host serves it.
- Anyone can open one file and read the entire page — structure, style, and logic — and fork
  it without installing anything. Maximum longevity and auditability.
- Shared patterns (design tokens, projnav, secnav, share components) are duplicated across
  files by hand rather than imported from a shared module, so cross-page changes must be applied
  to each page deliberately. This is the accepted cost of the no-build simplicity.
