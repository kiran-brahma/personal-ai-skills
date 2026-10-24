---
name: book-reference-extractor
description: "Build source-faithful book documents from highlights or notes: author reconstruction, durable reference, reader response, Book Memo. Interviews the reader first."
---

# Book Reference Extractor

Create a durable long-form document that brings together:

1. the strongest accurate reconstruction of the supplied book material;
2. the reader's independently stated position; and
3. the tensions, applications, and unanswered questions that survive contact between them.

The default deliverable is continuous, memo-length prose. Call it a `Book Memo` only when the user asks for that form; otherwise call it a long-form book document.

## The interview gate

Do not draft the document until the reader interview is complete and the reader has confirmed a shared-understanding checkpoint. The gate applies even when the supplied material contains no reader notes. Existing notes are hypotheses about the reader's position, to be verified; never turn notes, silence, or a likely reaction into the reader's considered view.

The interview is non-steering. Questions expose the reader's position. They do not defend the author, recommend an application, or suggest an answer, because any of those would contaminate an independent assessment.

## Source and voice contract

The goal is source-faithful language, not AI imitation.

- Preserve the author's important terms, distinctions, and meaningful short phrases exactly as they appear in the supplied material. Use the author's vocabulary when connecting ideas rather than smoother synonyms that shift emphasis.
- Quote only wording present in the supplied material, keep quotations short, and give their source location. Never manufacture an author quotation.
- Preserve the reader's meaningful wording, especially about experience, resistance, uncertainty, and conditions. Use first person only for a position the reader stated or confirmed.
- You supply connective prose and structure, never new beliefs, evidence, certainty, or a synthetic authorial voice. Using the author's concepts and words is fidelity; copying a named author's mannerisms is imitation.

Track the provenance of every substantive sentence: author claim, author observation, reader judgment, extractor inference, or possible application. Label the last two when they appear in the document. Cut any sentence whose provenance you can't defend.

## Workflow

### 1. Build a private source map

Read all supplied highlights, excerpts, notes, metadata, and style guidance. Take the title from the metadata, or use a neutral placeholder. Keep every page, chapter, location, or highlight reference, and note the coverage boundary: a highlight set does not represent the whole book.

Privately reconstruct the governing question and central argument; the strongest propositions and observations; mechanisms and evidence; key vocabulary and exact phrases; boundaries, countercases, costs, and tensions; and what the material does not establish. Then pick the two to four claims or tensions that most need the reader's judgment: those that could change interpretation, action, or the reader's view.

Do not show the user a polished author summary at this stage.

### 2. Interview the reader

Read [`references/reader-position-interrogation.md`](references/reader-position-interrogation.md) and follow it. The first response is the interview round only: four or five numbered questions anchored to the supplied material, with short source phrases or locations where useful.

### 3. Confirm the shared understanding

When every material branch is resolved or deferred, show a compact checkpoint of confirmed material only: what the supplied material establishes about the author's case; what the reader accepts, rejects, doubts, or cannot yet decide; the reader's important words and the conditions attached to them; terms that must survive into the prose; and what remains open.

Ask the reader to confirm or correct it. Repeat after corrections. If the reader pauses, keep the checkpoint as the interim state and wait.

### 4. Draft the document

Read [`references/memo-grade-prose.md`](references/memo-grade-prose.md) first. Write the author's case first, then the reader's response, then comparison or application only where it adds understanding. Default shape, adapted to the material, with empty sections omitted:

```markdown
# [Book Title]

Coverage note: [What the supplied material covers and does not establish.]

## The book's argument

[Long-form prose using the author's vocabulary and meaningful supplied phrases.]

## My response

[The reader's confirmed position in the reader's words and first-person perspective.]

## Where the argument meets experience

[Optional prose on agreement, resistance, application, or tension.]

## What remains unresolved

[Optional prose carrying unanswered questions, boundaries, and revision conditions.]
```

Add a compact source note only when it improves traceability; do not turn the document back into a catalogue of fields.

### 5. Audit before returning

Check every substantive sentence for source, wording, speaker, confidence, and boundary. Remove AI filler, generic praise, transitions that imply causality the source doesn't, and polish that hides uncertainty.

## Author reconstruction standard

The author section is not a conventional summary. Explain the problem the author is trying to solve, the central argument, the mechanisms that make it plausible, the evidence and examples behind it, and the strongest credible countercase. Preserve the author's uncertainty and unresolved tensions. Never use the reader's position to strengthen, soften, omit, or reinterpret the author's case.

Keep an idea only when it is non-obvious or unusually useful, supported by the supplied material, transferable beyond its example, and bounded by conditions or countercases. Merge repetitions; don't pad with every memorable line.

Do not add outside context unless the user asks for it; then label it and keep it separate from the supplied material.

## Optional structured format

Only when the user asks for a reference schema or machine-retrievable record: return the author record followed by a separately dated reader record, using the sections `Argument in View`, `Minimal Glossary`, `Propositions`, `Observations`, `Tensions and Limits`, `Rules`, and `Reader Position`, omitting any that don't earn their place. The interview gate, the author-first separation, and source locations still apply.
