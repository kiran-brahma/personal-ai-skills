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
