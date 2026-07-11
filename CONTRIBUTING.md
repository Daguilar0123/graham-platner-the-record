# Contributing to The Record

This project documents the public record of the Graham Platner case. Contributions
are welcome — and every contribution passes through review before anything is
published. You need a free GitHub account; you do not need to know how to code.

## How to submit a document

**Easiest path (no code):** open a
[document submission](https://github.com/Daguilar0123/graham-platner-the-record/issues/new?template=submit-document.yml)
— attach the file, answer the provenance questions, submit. The maintainer vets it
and commits it to `documents/` if it qualifies.

**Pull-request path:** use GitHub's *Add file → Upload files* button in the
`documents/` folder. GitHub forks the repo for you and opens a pull request.
Automated checks and maintainer review run before anything merges.

## Submission rules (enforced in review)

1. **Public-record material only.** Court/agency filings, FEC documents, archived
   published articles, dated screenshots of public posts, official results.
   Nothing hacked, leaked in violation of law, or private.
2. **Provenance required.** What the document is, where it came from, when it was
   created, and how you obtained it. Submissions without provenance are declined.
3. **No personal information about private individuals.** Addresses, phone
   numbers, employers of non-public figures, etc. get redacted before merge — or
   the submission is declined if redaction can't cure it.
4. **The editorial rules bind every contribution.** Allegations are recorded as
   allegations, denials as denials. No findings of fact, no accusations against
   accusers, journalists, or donors. Material arguing a conclusion belongs
   somewhere else; material documenting the record belongs here.
5. **File constraints.** Accepted types: pdf, png, jpg, webp, txt, md, json, csv.
   Max 25 MB per file. Video/audio stay external — link YouTube or archive.org
   instead.

## What happens to your submission

Every file is treated as untrusted until vetted: automated checks (file-type
allowlist, size, antivirus) run on every pull request, the maintainer reviews in a
sandboxed viewer, and `main` is protected — nothing merges without maintainer
approval. Accepted documents get a provenance note in `documents/README.md` and
appear in the site's record.

## Corrections

Found an error — a wrong date, byline, figure, or a mischaracterized summary?
Open an issue with a source. Corrections outrank everything else in the queue.
