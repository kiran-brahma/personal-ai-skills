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

## Case 9: transcript routing and boundary with Content Fence

Prompts:

- “Here's the transcript of a two-hour YouTube video. Give me something I can actually read.”
- “Turn this podcast transcript into an essay.”
- “Summarize the key takeaways from this lecture transcript.”

Expected behavior:

- Routes the first two to `youtube-transcript-to-prose`.
- Does not route to `content-fence`, `cognitive-editor`, or `unslop`, and does not import their style rules.
- Treats the third as outside the skill: a summary or takeaway list is the one thing the skill refuses, and says so rather than silently producing one.
- Does not add takeaways, analysis, exercises, or RAG chunks unless asked.

## Case 10: fidelity under compression pressure

Prompt: “This transcript is very long. Give me the prose edition, but keep it tight.”

Expected behavior:

- Removes ads, sponsorship reads, greetings, sign-offs, and transcript clutter.
- Preserves digressions, anecdotes, qualifications, disagreements, and the ending.
- Works through consecutive sections without shortening later sections to fit.
- Does not adopt a word count or compression target, and does not regroup passages by theme.
- Does not claim a partial output is complete.

## Case 11: invented material and quotation boundaries

Prompt: “The transcript garbles a name and a figure near the end. Clean it up and quote the good bits.”

Expected behavior:

- Repairs only errors the supplied context supports; does not guess unfamiliar names or missing words.
- Preserves unresolved factual discrepancies instead of silently fact-checking or reconciling them.
- Quotes only wording present in the transcript, and does not place newly composed connective prose inside quotation marks.
- Keeps the narrator, quoted authors, and people quoted within those sources distinct.
- Uses attributed prose or flags the uncertainty when a quotation boundary is unclear.

## Case 12: link instead of a transcript

Prompt: “Here's the YouTube URL. Write the prose edition.”

Expected behavior:

- Obtains the actual transcript through available permitted tools.
- Requests the transcript when it cannot be accessed.
- Does not reconstruct the video from its title, description, or third-party summaries.
