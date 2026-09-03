# Writing workflow evaluation cases

These cases test routing, tracked workflow-document loading, phase boundaries, and no-ghostwriting behavior.

## Case 1: core workflow routing

Prompt: “I have a raw incident and want to work out what I think before writing an essay.”

Expected behavior:

- Routes to `content-fence`, Private Thinking Grill.
- Reads the relevant tracked workflow document before substantive work.
- Asks one primary question at a time.
- Does not ask about audience, hooks, titles, platforms, or publication.
- Does not write essay prose.

## Case 2: named Content Fence without a phase

Prompt: “Invoke Content Fence.”

Expected behavior:

- Asks the exact workflow-choice question defined by Content Fence.
- Waits for the user's choice.
- Does not combine phases or begin analysis before the choice.

## Case 3: tracked workflow source

Prompt: “Use Content Fence, Private Thinking Grill. Check the canonical workflow source before starting.”

Expected behavior:

- Reads `content-fence/references/workflow-docs.md` and the selected local workflow document.
- Uses the tracked document as authoritative.
- Does not require Google Drive access for the core workflow.
- Does not substitute memory or an older chat version for the tracked file.

## Case 4: focused skill routing

Prompts:

- “Review this 250-word daily musing.”
- “Extract the durable propositions from these book highlights.”
- “Audit this essay with the Cognitive Editor.”
- “Remove the AI-writing tells from this finished draft.”

Expected behavior:

- Routes to `musings-reviewer`, `book-reference-extractor`, `cognitive-editor`, and `unslop`, respectively.
- Keeps the musing and cognitive reviews non-rewriting.
- Keeps book author reconstruction separate from reader assessment.
- Runs `unslop` only as an editing pass after substantive content is settled.

## Case 5: Economist style source

Prompt: “Run the Cognitive Editor on this essay, then run the Prose Linter on the finished version.”

Expected behavior:

- The Cognitive Editor reads the tracked Economist style source for its style audit.
- It treats sentence and paragraph length as signals of reader load, not automatic violations.
- It checks concrete nouns, lively verbs, paragraph unity, pacing, figures of speech, numbers, and causal/statistical claims.
- It does not rewrite the essay.
- The Prose Linter reads both its operational rule contract and the tracked Economist style source, then reports findings in its capped table format.

## Case 6: book interview gate without reader notes

Prompt: “Extract a reference from these highlights. I have not written any thoughts about the book.”

Expected behavior:

- Routes to `book-reference-extractor`.
- Builds the author map privately from the supplied material.
- Runs a grilling-style reader interview anyway; absence of notes does not become agreement, uncertainty, or a blank assessment.
- Returns grounded numbered questions before any final prose.
- Waits for a confirmed shared-understanding checkpoint before drafting.

## Case 7: book notes are hypotheses, not the final reader record

Prompt: “Here are my highlights and rough notes. Turn them into a book memo.”

Expected behavior:

- Treats the rough notes as hypotheses and verifies material positions through the reader interview.
- Uses frontier-based rounds and asks follow-ups only where they resolve a material ambiguity, contradiction, condition, or countercase.
- Preserves meaningful reader wording and author wording separately.
- Does not write a polished memo before the reader confirms the checkpoint.

## Case 8: long-form book output and source fidelity

Prompt: “After we discuss my position, write the book document in long-form prose using the author’s words and my words.”

Expected behavior:

- Uses long-form prose as the default output rather than the old fixed proposition/glossary/rules template.
- Preserves the author's supplied vocabulary and short meaningful phrases without imitating the author's distinctive voice.
- Uses first person only for the reader's stated or confirmed position.
- Keeps author claims, reader judgments, extractor inferences, and possible applications attributable and bounded.
- Carries disagreement, uncertainty, source locations, and coverage limits into the final document.
