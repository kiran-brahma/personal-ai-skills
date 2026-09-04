---
name: unslop
description: "Final editorial pass to remove AI-writing patterns from long-form prose while preserving meaning, voice, and quotations. Use when writing sounds AI-generated."
---

# Unslop

Improve readability without changing what the document is trying to say.

Treat this as an editorial pass, not a license to rewrite the argument. Make the smallest change that solves the problem. Rewrite more aggressively only when a local fix cannot repair the sentence or paragraph.

## Governing hierarchy

Apply priorities in this order:

1. Preserve facts, source fidelity, epistemic status, attribution, quotations, defined terms, uncertainty, and task-specific constraints.
2. Preserve the document's intended mode and voice.
3. Reduce cognitive load and remove AI-writing patterns.
4. Add stylistic personality only when the document is supposed to carry a point of view.

When a lower rule conflicts with a higher rule, follow the higher rule.

Do not edit merely because this skill was invoked. If the prose is already clear and natural, leave it alone.

## Workflow

Before returning the document, silently perform this pass:

1. Identify sentences, paragraphs, headings, and formatting that create unnecessary cognitive load or read as machine-produced.
2. Fix them with the smallest useful edit.
3. Re-read for meaning drift, lost qualification, changed attribution, or altered certainty.
4. Audit the result with one question: `What still makes this feel obviously AI-written or harder to read than it needs to be?`
5. Fix only the remaining material problems.
6. Return only the improved document unless the user asks to see the audit or edits.

Read `references/pattern-catalog.md` when conducting the pass.

## Reduce cognitive load

Cut every word that does no work. If five words carry the full meaning, do not use ten.

Prefer short, everyday words unless a longer or technical term is more precise. Keep source-specific terminology, defined concepts, real symbols, quotations, and domain terms when changing them would reduce accuracy.

Use full stops as working-memory breaks. A sentence often reads well around 20 to 30 words, but this is a guide, not a limit. Keep a longer sentence when one thought genuinely requires its conditions or qualification. Split it when the reader must hold several independent ideas at once or backtrack to parse it.

One thought per sentence is a useful default. Do not force clipped prose. Vary sentence length so the writing has rhythm.

Merge or split paragraphs when that reduces effort. Preserve the order of reasoning unless a local reordering clearly improves comprehension without changing meaning.

## Write for one reading

Prefer active voice when the actor matters. Passive voice is fine when the actor is unknown or irrelevant.

Keep modifiers next to what they modify. Make pronouns point to one obvious noun. Repeat the noun when needed.

Break long noun strings into clauses. Keep articles and small structural words when they prevent ambiguity.

Use one name for one thing. Do not cycle through synonyms merely to avoid repetition.

Place conditions before the statement or action they govern when that makes the sentence easier to parse.

## Headings must predict the section

Rewrite vague, generic, jargon-heavy, or decorative headings.

A heading should tell the reader what they are about to read. Prefer a claim, question, action, mechanism, tension, or concrete subject over labels such as `Strategy`, `Key considerations`, `Insights`, `The landscape`, or `Discussion`.

Use sentence case unless another governing format requires something else.

Do not change stable identifiers or headings whose exact wording is part of a required template.

## Preserve the document mode

Reference writing stays dry. Do not add opinion, personality, rhetorical flourishes, or emotional reactions to source-faithful records.

Explanations, analysis, essays, and memos may carry a view when the task calls for one. In those modes, allow natural first person, judgment, uneven rhythm, and restrained personality when they improve the writing.

Do not manufacture personality. Specificity is better than performative informality.

## Added explanations and examples

Avoid adding new examples, analogies, metaphors, or connective claims.

Add one only when a concept would otherwise remain materially hard to understand and the source does not provide a sufficient example. In source-faithful work, place it in the relevant section and label it clearly as `AI-added explanation:`. Never let it appear to come from the source or author.

Prefer a concrete explanation over a decorative analogy. Do not use an analogy as evidence.

## Source-faithful documents

For transcripts, books, research notes, legal or factual references, and other source-grounded work:

- preserve the original claim strength and qualification;
- preserve disagreement, ambiguity, and unresolved tension;
- preserve exact quotations except for corrections explicitly allowed by the governing task;
- preserve defined terminology when wording carries meaning;
- do not add opinion to make the prose feel more human;
- remove stylistic repetition, but preserve repetition when the repetition itself is evidence of emphasis or materially affects interpretation;
- never trade traceability for elegance.

## Final standard

The finished prose should be easier to read, less generic, and less predictably machine-shaped without calling attention to the editing.

The best pass is often small. Clear writing does not need to prove that it has been edited.
