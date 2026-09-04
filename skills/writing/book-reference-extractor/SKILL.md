---
name: book-reference-extractor
description: "Build source-faithful book documents from supplied highlights or notes: author reconstruction, durable reference, reader response, Book Memo. Interviews the reader first."
---

# Book Reference Extractor

Create a durable long-form document that brings together:

1. the strongest accurate reconstruction of the supplied book material;
2. the reader's independently stated position; and
3. the tensions, applications, and unanswered questions that survive contact between them.

The default deliverable is continuous, memo-length prose. Call it a `Book Memo` only when the user requests that form; otherwise call it a long-form book document. The old proposition/glossary/observations/rules template is an optional extraction format, used only when the user asks for a reference schema or machine-retrievable record.

## The interview gate

Do not draft the final document until the reader interview is complete and the reader has confirmed a shared-understanding checkpoint.

This gate applies even when the supplied documents contain no reader notes. When notes exist, treat them as hypotheses about the reader's position and verify them in the interview. Never silently turn notes, silence, or likely reactions into the reader's considered view.

Before the interview, work privately from the supplied material to identify the author's governing question, claims, evidence, mechanisms, terms, boundaries, and tensions. Use that private map to ask precise questions. Do not return a polished author summary as the final document before the interview.

For the interview stage, apply the `grill-with-docs` workflow in-line and follow its `grilling` and `domain-modeling` disciplines:

- map the reader's position as a decision tree;
- ask the current frontier in rounds, so later questions do not smuggle in unsettled assumptions;
- sharpen overloaded terms and test concrete counterexamples;
- continue until every material branch is resolved or explicitly deferred; and
- do not draft on the reader's behalf before the reader confirms the shared understanding.

The book-specific interview remains non-steering. Questions expose the reader's position; they do not defend the author, recommend an application, or supply a preferred answer. The general grilling workflow may use recommended answers for design decisions; omit recommendations here because they would contaminate an independent reader assessment.

## Source and voice contract

The goal is source-faithful language, not AI imitation.

- Preserve the author's important terms, distinctions, and meaningful short phrases exactly as they appear in the supplied material whenever they carry conceptual weight.
- Draft substantive author sentences from the source phrase bank first. Use minimal paraphrase when exact wording is unavailable, and omit or label anything that would require invented nuance.
- Use the author's vocabulary when connecting ideas. Do not replace it with smoother AI synonyms that change emphasis or erase a distinction.
- Quote only wording present in the supplied material, keep quotations short, and preserve their source location. Never manufacture an author quotation.
- Preserve the reader's meaningful wording, especially descriptions of experience, resistance, uncertainty, and conditions. Use first person only for a position the reader stated or confirmed.
- Let the AI supply connective prose and structure, not new beliefs, evidence, certainty, or a synthetic authorial voice.
- Do not imitate a named author's verbal fingerprints. Using the author's concepts and supplied words is source fidelity; copying a distinctive mannerism is imitation.

Maintain an internal provenance map for every substantive sentence: author-derived, reader-derived, source-grounded connective prose, extractor inference, or possible application. Label the last two when they appear in the document. Remove any sentence whose provenance cannot be defended.

## Workflow

### Stage 1: Intake and private source map

1. Read all supplied highlights, excerpts, notes, metadata, and style guidance.
2. Establish the title from supplied metadata. If it is unavailable, use a neutral placeholder.
3. State the coverage boundary internally. Do not imply that a highlight set represents the whole book.
4. Preserve page, chapter, location, section, or highlight references.
5. Reconstruct privately:
   - the governing question and central argument;
   - the strongest propositions and observations;
   - mechanisms and supporting evidence;
   - the author's key vocabulary and exact phrases;
   - boundaries, countercases, costs, and unresolved tensions; and
   - the parts the supplied material does not establish.
6. Select the two to four claims or tensions that most require the reader's judgment. Prefer material that could change interpretation, action, or the reader's view.

Completion criterion: a private source map exists, every selected interview question is anchored to supplied material, and every available source location is attached.

### Stage 2: Reader interview

Read `references/reader-position-interrogation.md`, then run the grilling-style interview.

Ask about the exact component that needs the reader's judgment: observation, mechanism, scope, conclusion, implication, cost, or revision evidence. Ask rather than teach. Accept uncertainty and deferral as real outcomes.

When the reader has supplied notes, test whether the notes are still the reader's position, what experience supports them, and where the wording needs correction. When the reader supplied no notes, begin from the selected claims and tensions rather than inferring an empty or agreeable position.

Completion criterion: each material branch of the reader's position is resolved or marked unanswered, and the reader has not been led toward agreement.

### Stage 3: Shared-understanding checkpoint

Before drafting, show a compact checkpoint containing only confirmed material:

- what the supplied material establishes about the author's case;
- what the reader accepts, rejects, doubts, or cannot yet decide;
- the reader's important words and the conditions attached to them;
- the terms and distinctions that must survive into the prose; and
- the disagreements and questions that remain open.

Ask the reader to confirm or correct it. If the reader corrects it, update the map and repeat the checkpoint. Do not draft the final document until the reader confirms it. If the reader pauses, preserve the checkpoint as an interim state and wait.

Completion criterion: the reader explicitly confirms that the checkpoint is accurate, with any remaining uncertainties identified for the document.

### Stage 4: Draft the long-form document

Read `references/memo-grade-prose.md` before drafting. Use it as the long-form prose standard; its filename is retained for compatibility with existing references.

Write the author's case first, then the reader's response, then comparison or application only where it adds understanding. Braid the voices only with clear attribution. Do not make a sentence sound like the author's claim when it is the reader's judgment or the extractor's inference.

Use a small number of descriptive headings only when they improve navigation. The default shape is:

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

Adapt the headings to the material. Omit empty sections. Add a compact source note only when it improves traceability; do not turn the document back into a catalogue of fields.

### Stage 5: Final source-and-voice audit

Before returning the document, inspect it sentence by sentence. Check the source, wording, speaker, confidence, and boundary of every substantive claim. Remove AI filler, generic praise, invented transitions that imply causality, and polished language that conceals uncertainty.

Completion criterion: the document reads as a coherent long-form account in the author's and reader's established language, while every claim remains attributable, bounded, and traceable.

## Author reconstruction standard

The author section is not a conventional summary. It should explain the problem the author is trying to solve, the central argument, the mechanisms that make it plausible, the evidence and examples that support it, and the strongest credible countercase. Preserve the author's uncertainty and unresolved tension. Do not use the reader's position to strengthen, soften, omit, or reinterpret the author's case.

Use the alpha standard. Keep an idea only when it is non-obvious or unusually useful, consequential, supported by the supplied material, transferable beyond its example, and bounded by conditions or countercases. Merge repetitions. Do not pad the prose with every memorable line.

Distinguish these statuses internally and label the last three when visible:

- Author claim: a general argument the author explicitly advances.
- Author observation: a concrete pattern, event, example, or behaviour the author reports.
- Extractor inference: a conclusion reasonably derived from the supplied material but not explicitly stated.
- Possible application: a decision use suggested by the material but not claimed by the author.
- Reader judgment: the reader's independently stated assessment.

Do not invent context, evidence, causality, or certainty. Use external context only when the user explicitly requests it, label it, and keep it separate from the supplied material.

## Reader position record

Keep a structured record privately so the long-form prose remains honest. Record only what the reader supplied or confirmed:

- assessment date;
- current stance toward each material claim or tension;
- meaningful reader wording;
- experience that supports or weakens the position;
- failure conditions and neglected variables;
- problem examined and potential benefit;
- risk or cost of over-application;
- evidence or experience that could change the view; and
- open or deferred questions.

Do not force an assessment for every claim. Do not convert absence into agreement. If the structured record is requested, expose it as a separate appendix or use the optional extraction format; otherwise let the long-form prose carry it naturally.

## Optional reference format

Use the old structured format only when explicitly requested for retrieval or extraction. In that mode, preserve the author-first/reader-second separation and the source locations. The available sections are `Argument in View`, `Minimal Glossary`, `Propositions`, `Observations`, `Tensions and Limits`, `Rules`, and `Reader Position`; omit any section that does not earn its place. Read the two reference documents before using it.

## Quality gate

Before returning a completed final document, verify:

1. The private source map was completed before the interview.
2. The interview happened even when reader notes were absent.
3. The interview followed a frontier-and-rounds design tree and reached a confirmed checkpoint.
4. The reader's view did not alter the author reconstruction.
5. Author terms and meaningful supplied phrases were preserved where they carry meaning.
6. Reader wording was preserved where it carries judgment or experience.
7. No quotation, belief, evidence, causality, or certainty was invented.
8. Every inference, application, and reader judgment is attributable or labelled.
9. The default output is long-form prose rather than the old fixed template.
10. Disagreement, uncertainty, boundaries, and unanswered questions remain visible.
11. Source locations and coverage limits are preserved.
12. Every paragraph advances the argument, explains a mechanism, preserves evidence, establishes a boundary, changes a judgment, or carries a real uncertainty.
13. The final voice contains no generic AI padding or imitation of a named author.

## Response contracts

### Before reader answers

Return the interview round only: four or five numbered questions grounded in the supplied material, with short source phrases or locations where useful. Do not return the final document, a polished author summary, recommendations, or suggested answers.

### During the interview

Ask the current frontier in numbered rounds. Ask follow-ups only when they resolve a material ambiguity, contradiction, unstated condition, unsupported confidence, or missing countercase. Recompute the frontier after each answer. Do not draft prose on the reader's behalf.

### At the checkpoint

Return the compact shared-understanding checkpoint and ask for confirmation or correction. Wait for that response before drafting.

### After confirmation

Return the complete long-form document. Include the coverage note, author argument, reader response, and only the comparison, application, source notes, or unresolved questions that the material and confirmed interview support.

### If the user explicitly requests the old structured record

Return the complete author record followed by the separately dated reader record, using the optional reference format. The interview and confirmation gate still apply.
