---
kind: "library-hub"
updated: "2026-10-13"
tags: ["career/library"]
---

# Library Rebuild

[[Career Library]] · [[Library Import Ledger]]

## Scope and fidelity

The rebuild inventories 1015 source files, including bounded, selectively chosen project documents and educational code examples. It converts readable text, Word bodies, HTML text, slide text/tables/notes, notebook Markdown/code cells, and both pattern-workbook sheets into Markdown. PDFs and relevant figures are retained intact inside the vault.

Questions and solutions are paired where filenames and context support it. Coding Ninjas contains 74 question notes across seven source topics, plus an algorithm reference. Imported solutions are unverified; no code was executed or submitted.

## Conversion limits

- Word paragraph text, headings, lists, hyperlinks, footnotes, and supported figures are extracted. Native page layout, comments, tracked-change presentation, and embedded objects are not reproduced.
- Slide text and speaker notes are extracted; the original deck remains the reference for non-text visuals and layout.
- Notebook code and Markdown are retained. Large execution outputs and widgets stay outside.
- Full PDF-to-Markdown conversion is deferred. Exercise-PDF extraction dropped mathematical symbols, so the original PDFs are used instead of incomplete text.
- Credential-like literals in two lecture notebooks are redacted in the vault copies; originals remain unchanged.
- Empty Inversion Count and Crossword solution files are recorded rather than replaced with fabricated answers.

- Some original project snapshots referenced missing screenshots or policy/license files. Those absences are labelled explicitly; misbased documentation links were redirected to the available native notes.

## Preservation

Source files are not moved or edited. The earlier library hubs are backed up under `.copilot/library-rebuild/before`. Existing Climb lane contents, Company Tracker, and company task properties are not part of this rewrite. Import inventory and decision data are under `.copilot/library-rebuild`; no dependency environments or repositories were added.

## Completion checks

Final checks cover source-to-destination accounting, attachment hashes, internal links, note metadata, and exclusion of source-code files and forbidden dependency/build folders. UI responsiveness and rendered reading experience also need a user check; a file-count check cannot prove the app feels smooth.

## Verified rebuild snapshot

- 1015 source records accounted for; 70 exact duplicate copies avoided.
- 872 Markdown notes in the finished library, including source notes, reading notes, study guides, and preserved hubs.
- 202 original PDFs and eight raster figures; two native Bases for browsing/practice.
- Approximately 5.8 MB of Markdown and 196.6 MB overall, mostly PDFs.
- Source hashes unchanged, attachments verified, and no missing native links or malformed generated properties in the final scan.
- No raw project/practice code files, repository trees, dependency folders, videos, or build output imported. Educational code is retained inside reference Markdown fences.
- Obsidian's live metadata search matched all 74 Coding Ninjas question notes. The API remained responsive; visual responsiveness still needs the user's judgement.

The source and attachment checks are structural/fidelity checks, not a claim that every source answer, career metric, diagram, or page layout was independently validated.
