# Architecture Decision Records

An **ADR** captures one significant decision: the *context* that forced a choice, the
*decision* made, and the *consequences* accepted. The point is to preserve the **why** so it
isn't relitigated from memory months later — and so a new contributor (human or AI) can
understand not just what the system is, but why it isn't something else.

ADRs are immutable once accepted. If a decision is reversed, you don't edit the old record —
you write a new ADR that supersedes it, and mark the old one `Superseded by NNNN`. The trail
of *changed minds* is itself valuable history.

Format used here: **Title · Status · Context · Decision · Consequences.** Short on purpose.

| # | Decision | Status |
|---|---|---|
| [0001](0001-two-repos-one-domain.md) | Two repositories, one domain | Accepted |
| [0002](0002-content-as-data.md) | Case content lives in JSON, rendered at runtime | Accepted |
| [0003](0003-no-framework-vanilla-static.md) | No framework — vanilla, single-file, static | Accepted |
| [0004](0004-declared-standpoint-constraint.md) | The declared standpoint is a hard constraint | Accepted |
| [0005](0005-lead-with-the-questions.md) | Lead the site with The Questions (homepage swap) | Accepted |
| [0006](0006-static-hosting-contributions-via-issues.md) | Static hosting; contributions via issues + CI | Accepted |
