---
name: youtube-transcript-to-prose
description: "Turn a YouTube, podcast, lecture, or interview transcript into faithful essay prose, ads and clutter removed. Not a summary or a new essay."
---

# YouTube Transcript to Prose

Produce a faithful essay edition of what was said. Make it read as connected prose, not a cleaned transcript. Preserve the creator's language and thinking without claiming to know what they would have published.

Use these self-contained editorial rules. Do not invoke `content-fence`, `cognitive-editor`, or `unslop`, and do not import their style rules; those skills shape the user's own writing, while this one preserves someone else's. Follow explicit user instructions over these defaults.

Run `unslop` afterwards only when the user asks for it, and only on prose that is already faithful. It is an editing pass, not a licence to reshape the source.

## Preserve the source

- Follow the video's order. Rebuild sentences and paragraphs locally, but do not regroup scattered passages by theme or move the ending to the beginning.
- Preserve every distinct idea, example, anecdote, digression, qualification, disagreement, and step in the reasoning. Do not impose a word count or compression target.
- Keep the creator's vocabulary, distinctive phrases, technical terms, numbers, formulas, and concrete details. Prefer their words over polished synonyms.
- Preserve ownership and claim strength. Do not turn an uncertain recollection into a fact, a preference into a rule, or one person's view into another's.
- Add only the small grammatical and connective wording needed to express relationships already explicit in the source. Do not supply new facts, explanations, analogies, causal links, arguments, or conclusions.

## Make it an essay

- Build paragraphs around complete thoughts. Repair grammar, punctuation, sentence boundaries, and false starts. Vary sentence length naturally; avoid both rambling speech and mechanically clipped prose.
- Replace spoken scaffolding with direct exposition. Instead of announcing that the speaker will discuss a belief, explain that belief using the source's words.
- Make the subject central. Remove empty narration such as “let me get back into this,” but retain first-person experience, judgment, and meaningful uncertainty. Keep an anecdote about finding an article even if its spoken introduction needs repair.
- Integrate selected direct quotations into explanatory paragraphs. Use quotations for distinctive language; let surrounding prose carry the explanation. Avoid an endless sequence of “he said” and “the book says.”
- Preserve expressive reactions when they carry the narrator's judgment or voice. Do not sanitize enthusiasm, bluntness, humor, or disagreement into neutral textbook prose.
- Remove verbal stutters and genuinely redundant local restatements. Retain recurring ideas when they carry emphasis, a new example, a qualification, or a later return to the subject. Do not deduplicate the whole video into a summary.
- Use a plain title and restrained section headings drawn from the source's vocabulary where useful. Do not force the material into three ideas, a new framework, or a manufactured thesis and conclusion. A sequence of reflections may remain a sequence of reflections.

## Handle interviews and quotations

For an interview, present the question and the context the interviewer actually supplied, followed by the respondent's answer in essay prose. Use names or neutral speaker labels. Preserve each follow-up exchange in order. Do not merge speakers into one voice or infer what a question “really meant.”

Keep the narrator, quoted authors, and people quoted within those sources distinct. Attribute source-derived passages where needed without repetitive attribution on every sentence. Do not turn a book author's “I” into the narrator's personal experience.

Quote only wording supported by the transcript. Preserve the wording of direct quotations apart from punctuation and clear transcription repairs. Do not put newly composed connective prose inside quotation marks. When quotation boundaries are unclear, use attributed prose or flag the uncertainty instead of inventing a verbatim quotation. Keep interruptions outside the quoted passage and in their original position.

## Remove non-editorial material

Remove all advertisements, sponsorship reads, affiliate pitches, discount codes, and promotional calls to action. Remove quotations and anecdotes used solely to introduce a sponsor, even when they resemble editorial content. Retain genuine editorial discussion of a product or business; a brand mention alone is not an advertisement.

Remove greetings, sign-offs, requests to like or subscribe, break announcements, timestamps, caption line breaks, thumbnail links, and duplicated pull quotes or display headings. Preserve substantive content embedded in an introduction or closing. Do not let misplaced transcript headings determine the essay's structure.

## Handle imperfect input

Read the full supplied transcript before editing. For long inputs, work through consecutive sections and assemble them without shortening later sections to fit. Do not claim a partial source or output is complete.

Correct clear transcription errors when the supplied context supports the repair. Do not guess unfamiliar names, missing words, or visual information. Preserve unresolved factual discrepancies; do not silently fact-check or reconcile conflicting figures. Put a brief editorial note outside the essay only when unresolved source damage materially affects understanding.

If only a link is supplied, obtain the actual transcript through available permitted tools. If it cannot be accessed, request the transcript rather than reconstructing the video from its title, description, or summaries.

## Final pass and delivery

Compare the draft against the transcript in sequence. Check that:

- all substantive passages survive, including digressions and the ending;
- ads and transcript clutter are gone;
- numbers, uncertainty, speaker ownership, and quotation boundaries are intact;
- each new connective sentence is supported by the source;
- the result reads as an essay without replacing the creator's voice.

Deliver the prose, with known source title, creator, and URL in a short source line outside the essay when available. Do not invent metadata or imply the creator authored or approved the edited edition. Do not add summaries, takeaways, exercises, RAG chunks, or analysis unless requested; the user handles RAG separately. For a full transcript, provide a document in the requested format, defaulting to Markdown. For a requested sample, return only that section with a brief scope label.
