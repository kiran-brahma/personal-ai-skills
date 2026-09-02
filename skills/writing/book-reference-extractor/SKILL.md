---
name: book-reference-extractor
description: Create layered, source-faithful book reference documents and memo-ready reader records from supplied highlights, excerpts, notes, or metadata. Use when the user asks for high-alpha propositions, durable book references, author arguments, observations, tensions, decision rules, reader interrogation, an independent reader assessment, or preparation for an AI-drafted Book Memo. Reconstruct the author first; then question the reader without steering; preserve the reader's dated position separately. Distinguish author claims, extractor inferences, possible applications, and reader judgments; preserve source locations. Do not use for conventional summaries, reviews, or quote collections.
---

# Book Reference Extractor

Create a durable dual-record document from supplied book material:

1. Preserve the strongest accurate reconstruction of the book and author's arguments.
2. Preserve the reader's independent, dated assessment without merging it into the author record.

Use memo-grade classic prose while retaining reference-grade traceability. Do not imitate the verbal fingerprints of any named writer.

## Non-negotiable separation

Keep these records distinct:

- Author record: What the author claims, observes, argues, qualifies, or leaves unresolved.
- Extractor layer: Inferences or possible applications derived from the supplied material. Label each explicitly.
- Reader record: What the reader accepts, rejects, doubts, finds useful, or leaves unanswered.

Never use the reader's view to rewrite, soften, strengthen, omit, or reinterpret the author's case. Never attribute the extractor's synthesis or the reader's position to the author.

Apply this order:

Author first. Reader second. Comparison third, only when useful.

Do not manufacture agreement. Shared understanding means a clear map of the author's case and the reader's independent position, including disagreement and uncertainty.

## Workflow

Determine the current stage and continue from it.

### Stage 1: Build the author record

1. Read all supplied highlights, excerpts, notes, metadata, and style guidance.
2. Reconstruct the book's governing question, central argument, strongest propositions, evidence, mechanisms, boundaries, and unresolved tensions.
3. Draft the complete author record without using the reader's personal views.
4. Preserve all available source locations.
5. If the reader has not yet been interrogated, continue to Stage 2 after the author record.

### Stage 2: Conduct the Reader Position Interrogation

Read `references/reader-position-interrogation.md` before questioning the reader.

1. Select only the propositions or tensions that materially require the reader's judgment.
2. Ask four or five initial questions.
3. Ask no more than three tailored follow-ups after receiving answers, and only when they expose a material ambiguity, contradiction, unstated condition, or missing boundary.
4. Ask rather than teach. Do not recommend, persuade, defend the author, solve the reader's problem, praise an answer, or complete the reader's reasoning.
5. Treat "I do not know" and non-response as valid unresolved states.
6. Allow the reader to stop and return later with the document.

### Stage 3: Record the independent reader assessment

1. Date the reader record.
2. Preserve the reader's own wording when it carries meaning.
3. Label any AI paraphrase as `AI summary`.
4. Record stance, reasoning, failure conditions, relevant problem, potential benefit, risk or cost, revision evidence, and open questions when supplied.
5. Do not force an assessment for every proposition.
6. Mark unanswered items explicitly rather than inventing a position.
7. Return the full document with the unchanged author record followed by the reader record.

### Stage 4: Draft a Book Memo only when explicitly requested

1. Use the completed author record as the source foundation.
2. Use the reader record only as a separate independent assessment.
3. Present the author's case before the reader's assessment.
4. Preserve unresolved disagreement between author and reader.
5. Do not delay the memo merely because some reader questions remain unanswered; carry them into `What Remains Unresolved`.
6. Read `references/memo-grade-prose.md` before drafting.

## Source intake

1. Use supplied highlights, excerpts, notes, metadata, and style guidance as the primary source.
2. Read attached or linked source material before extracting. Use available file or connector tools when needed.
3. Do not use external context unless the user explicitly requests it. Label external context separately and never use it to silently complete missing source material.
4. Establish the book title from supplied metadata when possible. Otherwise use a neutral placeholder.
5. State incomplete coverage plainly. Do not imply that a highlight set represents the whole book.
6. Preserve page, chapter, location, section, or highlight references whenever available.

## Alpha standard

Include an idea only when it is all of the following:

1. Non-obvious or framed in an unusually useful way.
2. Consequential enough to change interpretation, judgment, or action.
3. Supported by the supplied material.
4. Transferable beyond the original example.
5. Bounded by conditions, limits, or countercases.

Reject material that is merely memorable, fashionable, repeated, well-phrased, or generally accepted. Treat repetition as evidence of emphasis, not as a separate insight. Do not mistake novelty for importance.

## Source discipline

Distinguish these epistemic statuses:

- Author claim: A general argument the author explicitly advances.
- Author observation: A concrete pattern, event, experience, example, or behaviour the author reports.
- Extractor inference: A conclusion reasonably derived from the supplied material but not explicitly stated by the author.
- Possible application: A decision use suggested by the material but not claimed by the author.
- Reader judgment: The reader's independent assessment after interrogation.

Label extractor inferences, possible applications, and reader judgments. Never present them as the author's position.

Paraphrase by default. Preserve exact wording only when the wording itself carries unusual meaning. Do not invent context, evidence, causality, or certainty. Do not resolve contradictions unless the supplied material supports the resolution.

Merge duplicates and closely related claims. Do not repeat the same insight across sections. Allow an observation to support a proposition, but require the Observations section to add concrete evidence rather than restate the claim.

## Internal selection workflow

Complete this privately before drafting the author record:

1. Generate plausible candidate ideas.
2. Merge duplicates and closely related claims.
3. Separate claims, observations, examples, inferences, and applications.
4. Assess novelty, consequence, explanatory power, evidential support, transferability, durability, and boundary clarity.
5. Remove generic advice, unsupported claims, decorative anecdotes, weak repetitions, and ideas that cannot survive a countercase.
6. Select the propositions first.
7. Select only the glossary terms needed to understand those propositions.
8. Draft narrowly from the strongest surviving material.

Do not reveal candidate lists, scores, or hidden deliberation.

## Author record

### The highlight set in one sentence

State the central tension or governing claim emerging from the supplied material. Do not claim that it represents the whole book unless the source supports that conclusion.

### Argument in view

Write a compact synthesis, usually 400 to 700 words when the material supports it. Explain:

- the problem the author is trying to solve;
- the central argument;
- how the selected propositions depend on, qualify, or challenge one another;
- the most important unresolved tension; and
- what the supplied material does not establish.

Label this section `Extractor synthesis`. Do not merely repeat the proposition summaries.

### Minimal glossary

Include a term only when misunderstanding it would materially distort a selected proposition. Order terms by conceptual dependency. Use the minimum sufficient set.

Use this format when useful:

- TERM: Define the term in one or two precise sentences.
  - Analogy: Include only when it clarifies the mechanism without distorting it.
  - Why it matters: Explain the term's role in the selected propositions.
  - Common confusion: State a likely misunderstanding or boundary.

Do not create entries merely because a term sounds technical.

### Propositions

Include only the highest-alpha propositions. Do not pad to a fixed count.

Give each proposition a stable identifier such as P1 or P2. Use a complete claim as the title, not a topic label.

Write a compact mini-essay. Most propositions should require 180 to 320 words. Use the shortest length that completes the reasoning. Exceed the range only when compression would remove a necessary distinction, example, or countercase.

Let each proposition move naturally through:

1. The claim or puzzle.
2. The mechanism and supporting evidence.
3. The strongest credible boundary, countercase, cost, or failure mode.
4. The judgment or behaviour the proposition could change.

Do not expose this sequence as a mechanical set of subheadings unless the material is unusually technical. Mark extractor inference explicitly.

End every proposition with:

Recall when: State a specific situation in which the idea should come to mind.

Memory line: Include only when the proposition can be compressed without losing its governing condition or qualification. Otherwise omit it.

Source: Give page, chapter, location, section, or highlight references when available.

### Observations

Include only concrete patterns, events, experiences, examples, or behaviours reported by the author. Keep each observation to one or two sentences. Do not restate a proposition. Add a source reference when available.

### Tensions and limits

Include only genuine contradictions, trade-offs, scope conditions, or unresolved tensions.

For each:

1. State both sides fairly.
2. Explain why both may be credible.
3. Identify the conditions under which each side is more likely to hold.
4. Leave the tension unresolved when the source does not resolve it.

Omit the section when no meaningful tension exists.

### Rules

Extract up to ten decision rules, operating principles, practices, experiments, or prohibitions. Fewer is better.

Preserve four logical elements: condition, action, mechanism, and exception. Express them in one to three natural sentences. Do not force every rule through identical syntax.

Do not mechanically convert every proposition into a rule. Do not claim universal applicability unless the source supports it.

## Reader position

Keep this section independent from the author record. Do not insert reader judgments into `Argument in View`, propositions, observations, tensions, or rules.

For each material proposition or tension discussed with the reader, record only fields supported by the reader's answers:

### [Proposition or tension reference]

Assessment date: [date]

Current stance: Agree / lean agree / uncertain / lean disagree / disagree / unanswered

Reader's own words: [Preserve meaningful wording when available.]

AI summary: [Optional concise paraphrase. Label it.]

Where it may fail: [Reader-identified conditions or countercases.]

Problem it helps examine: [The practical or intellectual problem it clarifies.]

Potential benefit: [What may become possible or easier if the idea holds.]

Risk or cost: [What may go wrong through acceptance or over-application.]

What could change the view: [Evidence, experience, or conditions that could cause revision.]

Open questions: [Unanswered issues.]

Do not force all fields. Do not convert absence into agreement.

## Memo-preparation questions

After recording the reader position, retain only unanswered questions that remain material to a later Book Memo. Questions must diagnose a condition, test a proposition, search for disconfirming evidence, expose a trade-off, or clarify what could revise the reader's view.

Do not answer personal questions on the reader's behalf.

## Prose standard

Read `references/memo-grade-prose.md` when drafting `Argument in View`, propositions, or a Book Memo.

Apply the supplied style guide. When none is supplied:

- Use concrete nouns and active verbs.
- Prefer ordinary words to technical or inflated language.
- Use short, complete sentences and classic prose.
- Build cumulative reasoning rather than a sequence of disconnected summaries.
- Let examples carry evidential weight; do not use anecdotes merely for colour.
- Give the strongest credible countercase rather than attaching a token limitation.
- Preserve accurate unresolved tension instead of forcing a satisfying synthesis.
- Remove stock phrases, praise, throat-clearing, and repetition.
- Make no claim stronger than the source permits.
- Use analogies only to explain, never as evidence.
- Preserve uncertainty when uncertainty matters.
- Use valid Markdown without bold or italic formatting in the completed document.
- Use headings only when they improve retrieval.
- Ensure every paragraph explains a mechanism, preserves evidence, establishes a boundary, advances the argument, or changes a decision.

## Quality gate

Before returning any completed document, verify:

1. The author record is complete before the reader record begins.
2. The reader's view has not altered the author reconstruction.
3. Every proposition satisfies the alpha standard.
4. Every extractor inference, application, AI paraphrase, and reader judgment is labelled.
5. Every available source location is preserved.
6. No idea is needlessly repeated across sections.
7. Tensions are not falsely reconciled.
8. Rules remain conditional and bounded.
9. Unanswered reader questions remain visible rather than being resolved by the AI.
10. Every sentence adds information.
11. A reader can understand the document later without reopening the highlights.
12. The document remains useful even if the reader later changes position or rejects the author's conclusion.

## Response contracts

### Initial extraction with no reader answers yet

Return:

# [Book Title] - Reference Document

Coverage note: [Supplied material and limitations.]

## Author Record

### The Highlight Set in One Sentence

### Argument in View

Label: Extractor synthesis

### Minimal Glossary

### Propositions

### Observations

### Tensions and Limits

Omit when no meaningful tension exists.

### Rules

## Reader Position Interrogation - Round 1

Ask four or five numbered questions only. Do not add recommendations, interpretations, suggested answers, or encouragement after the questions.

### After partial reader answers

Ask up to three tailored follow-up questions only when materially necessary. Otherwise proceed to the updated document. Allow the reader to defer any question.

### Updated reference document

Return the complete author record unchanged, followed by:

## Reader Position

[Independent dated assessments.]

## Open Questions for the Book Memo

[Only unresolved material questions.]

### Book Memo, only when explicitly requested

Use this default structure:

# [Book Title] - Book Memo

## The Author's Case

[Source-faithful memo-grade reconstruction.]

## My Independent Assessment

[Dated reader position, clearly separate from the author record. Use `AI summary` labels for paraphrase.]

## What Remains Unresolved

[Material disagreement, uncertainty, and unanswered questions.]

Do not blend these sections into a single consensus argument.
