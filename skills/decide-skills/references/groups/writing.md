# Writing group rules

Read after the index points to a skill in the `writing` group.

Use `content-fence` as the primary workflow for Kiran's personal essays, The Operator Stack, personal blog posts, book-based essays, observation pieces, and related long-form writing. It owns the phase boundaries and must not be silently combined with another workflow.

- Raw idea, incident, reading, experiment, or unresolved observation: `content-fence`, Private Thinking Grill.
- Existing Thinking Essay plus Thinking Documents or references: `content-fence`, Thinking Essay Development.
- Dated Thinking Essay snapshot that needs one reader-centred essay design: `content-fence`, Reader Reconstruction.
- Completed Reader Essay plus its architecture: `content-fence`, Reader-Response Audit.
- Finished prose that needs the canonical style audit: `content-fence`, Prose Linter.
- Book highlights, excerpts, or notes requiring an author reconstruction, book document, reader interview, or Book Memo: `book-reference-extractor`.
- One short daily musing: `musings-reviewer`. Never for essays or other long-form writing.
- General developmental audit, or a request to run the Cognitive Editor: `cognitive-editor`.
- A transcript of someone else's video, podcast, lecture, or interview that should become readable prose: `youtube-transcript-to-prose`. A request to reshape, summarize, or argue from a transcript goes to `content-fence` instead.

`unslop` is an installed skill, not a library one. Run it only as a separate final pass after the diagnostic workflow, never in place of argument or reader-response review.

## Source-document preflight

Before substantive work, check the selected skill for a `references/workflow-docs.md` manifest. If one exists, read it and each relevant tracked document, confirm the title and phase match, and treat the tracked content as authoritative over memory and general writing advice. Do not fetch Google Drive for tracked workflows.
