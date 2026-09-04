---
name: writing
description: Route writing work to the most relevant focused skill in this category, including drafting, editing, rewriting, reviewing, and adapting content.
---

# Writing skill catalogue

Read this file when `SKILLS.md` identifies writing as the relevant category. Select the narrowest specific skill that matches the task, then read that skill's `SKILL.md` before acting.

## Available skills

- [`content-fence`](../content-fence/SKILL.md): The core, phase-gated workflow for Kiran's private thinking, Thinking Essay development, Reader Reconstruction, Reader-Response Audit, and final Prose Linter work.
- [`book-reference-extractor`](../book-reference-extractor/SKILL.md): Build source-faithful long-form book documents after a confirmed grilling-style reader interview.
- [`cognitive-editor`](../cognitive-editor/SKILL.md): Audit essays and other writing for foundations, bias, evidence, replicability, style, and series fit without rewriting.
- [`musings-reviewer`](../musings-reviewer/SKILL.md): Audit one short daily musing for atomicity, argument structure, definitions, fallacies, prose, and the final word cap.
- [`unslop`](../unslop/SKILL.md): Perform a final, meaning-preserving pass that removes AI-writing patterns and unnecessary cognitive load.

## Route the workflow

Use `content-fence` as the primary workflow for Kiran's personal essays, The Operator Stack, personal blog posts, book-based essays, observation pieces, and related long-form writing. It owns the phase boundaries and must not be silently combined with another workflow.

Route focused requests as follows:

- Raw idea, incident, reading, experiment, or unresolved observation: `content-fence`, Private Thinking Grill.
- Existing Thinking Essay plus Thinking Documents or references: `content-fence`, Thinking Essay Development.
- Dated Thinking Essay snapshot that needs one reader-centred essay design: `content-fence`, Reader Reconstruction.
- Completed Reader Essay plus its architecture: `content-fence`, Reader-Response Audit.
- Finished prose that needs the canonical style audit: `content-fence`, Prose Linter.
- Book highlights, excerpts, or notes requiring an author reconstruction, long-form book document, reader interview, or Book Memo: `book-reference-extractor`.
- One short daily musing: `musings-reviewer`. Do not use it for essays or other long-form writing.
- General developmental audit or a request to run the Cognitive Editor: `cognitive-editor`.
- A final readability or anti-AI editing pass after the content is settled: `unslop`. It is an editing pass, not a substitute for argument or reader-response review.

When a request could match both `cognitive-editor` and `musings-reviewer`, route a daily musing to `musings-reviewer`; route other writing to `cognitive-editor`. When a request asks for both diagnosis and rewriting, complete the diagnostic workflow first and run `unslop` only as a separate final pass.

## Source-document preflight

Before substantive work, inspect the selected skill for a `references/workflow-docs.md` manifest. If one exists:

1. Read the manifest and each relevant tracked workflow document.
2. Confirm that the document title and selected phase match the manifest.
3. Use the tracked content as authoritative over memory, prior chat versions, and general writing advice.
4. Treat edits to these documents as ordinary Git changes. Do not fetch Google Drive or require a connector for the tracked workflow.

If a future skill instead declares an external live-document manifest, follow that skill's connector instructions. For the current writing package, the canonical workflow documents are tracked locally in [`content-fence/references/workflow-docs.md`](../content-fence/references/workflow-docs.md). Google Drive is optional only when the user supplies an external document, such as an essay ledger, as task context.

When a skill is added, list it here with its path and a concise description of when it applies. Keep this catalogue focused on routing; detailed instructions belong in the specific skill.
