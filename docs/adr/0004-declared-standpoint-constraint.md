# 0004 — The declared standpoint is a hard constraint

**Status:** Accepted (2026-07) · the project's defining decision

## Context

The site documents a live, unadjudicated case involving grave allegations, denials, and no
legal finding of any kind. It also has a *declared bias* (it supported the candidate's
politics). Either fact alone makes the work easy to dismiss as advocacy. The only durable
answer is to make the method more rigorous than a neutral outlet's, and to state the position
openly rather than hide it.

## Decision

Treat the editorial standpoint as a **hard architectural constraint**, not a disclaimer:

- Allegations are recorded as allegations, denials as denials. The site never states or implies
  that any accuser is lying or that any allegation is true.
- No findings of fact. Each item is unverified until an investigation *independent of the
  publishing outlet* corroborates it; the denial is the operative account until then.
- The site's own editorial voice is falsifiable and conditional, never accusatory.
- Certain content is **immutable** (verbatim quotes, denials, grade taxonomies, the pledge,
  provenance) and changes byte-for-byte only to *correct* an error — with the correction marked.

## Consequences

- The constraint is enforced structurally: `independently_verified: false` throughout the data;
  the unchecked verification box as the central visual; conditional copy; contribution rules
  that bind every submission to the same standard.
- Design choices that read as advocacy-first (rage-bait, tabloid, meme-ification) are rejected
  even when more persuasive. The register is rigorous/calm/archival.
- Corrections are privileged above all other work ("corrections outrank everything"), because a
  visible, honored correction channel is what makes the standpoint credible rather than defensive.
