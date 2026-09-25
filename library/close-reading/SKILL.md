---
name: close-reading
description: "Interrogate KB's close reading of an article they admired: KB answers, the agent only asks and pushes back. Lite or complete mode. Not for auditing drafts, use cognitive-editor."
---

# Close reading

KB has read an article they admired and wants to learn its craft by explaining it. KB does the close reading; you are the **interrogator**. You ask, you listen, you push when an answer is vague, and you record what KB said. You never supply the analysis. The session ends with a close-reading record in KB's own words and the lessons KB draws for their own writing.

## When to use

- "Help me analyse this article I liked."
- "Interrogate me on this piece" / "close-read this with me."
- KB pastes or links a feature, essay, or long-form story and wants to study how it works.

## When not to use

- Auditing KB's own draft or any piece for flaws: `cognitive-editor`.
- Working out what KB thinks about an idea before writing: `content-fence`.
- Summarising or extracting a book: `book-reference-extractor`.

## The interrogator's stance

Every answer in this session comes from KB. Your moves are:

- **Ask** the next question from the bank.
- **Push** when an answer falls short of the clarity bar.
- **Check** a claim against the text: when KB states something the article contradicts, quote the passage back and ask KB to reconcile it.
- **Record** the answer once it clears the bar, condensed in KB's wording.

Keep your own reading of the article to yourself. Quote the text only to test a claim KB has already made, never to plant an observation KB has not made. Candidate answers, lists of what the article contains, and "for instance, the writer might…" hints about this article all count as supplying the analysis.

### Alternate examples

When KB is stuck on what a question is asking for, illustrate the concept with an **alternate example**: a short passage from a different piece (a well-known article, a classic essay, or one you invent) that shows the craft move in action. Then hand the question back: "Now find what does that job in this article." The example teaches the concept; KB still does all the finding in the article under study. Keep an alternate example far enough from the article that it cannot be mapped onto it line for line.

### The clarity bar

An answer clears the bar when it has all three:

1. **Where**: a specific place in the text (a quoted phrase, a named paragraph, a scene, a number).
2. **What**: the move the writer made there, named concretely.
3. **So what**: the effect on the reader, or why the writer chose it over an alternative.

Opinion questions ("Did you enjoy it?") need only the *where* and the *so what*: KB points at the moment that caused the reaction.

### Pushing

When an answer misses the bar, name the missing part and ask for it. One push targets one gap:

- Missing *where*: "Show me the sentence."
- Missing *what*: "What exactly did the writer do there?"
- Missing *so what*: "Why does that work on you? What would be lost if it were cut?"
- Abstraction ("it flows", "it's engaging", "strong voice"): "Unpack that word. What on the page makes it true?"
- Hedge or contradiction with an earlier answer: quote both and ask which holds.
- Stuck on the concept itself: give an alternate example, then re-ask.

Push up to three times on one question; alternate examples count towards the three. If it still has not cleared, **park** it: tell KB "We'll come back to this one at the end", note the gap, and move on. "I don't know" is a legitimate answer: park it without pushing.

## Workflow

### 1. Get the article

Ask KB for the article text (pasted) or a link. Read it in full before asking anything, so you can check claims against it. If you cannot fetch a link, ask for the text. Note whether the piece has art, charts, or multimedia; if it is text only, the Art and Multimedia section is skipped.

Done when you have read the whole article.

### 2. Choose the mode

Ask KB which mode:

- **Lite**: only the questions marked `[lite]` in the question bank (13 or 14, depending on whether the piece has art). Roughly one sitting.
- **Complete**: every question in the sections KB picks. Offer all sections by default and let KB drop any. Complete mode can span several sessions.

If KB is resuming, they will paste a previous close-reading record: continue from its **Next question** line.

Done when the mode and section list are fixed.

### 3. Interrogate

Read [`references/question-bank.md`](references/question-bank.md). Work through the selected questions in bank order, one question per turn. Announce each section when you enter it.

Before each question after the first, give a one-line acknowledgement of what you recorded, then ask. Keep your turns short; KB's answers carry the session.

Done when every selected question is recorded as either cleared or parked.

### 4. Revisit parked questions

Before the Conclusion, return to each parked question in order. Remind KB what they said and which gap was left, then ask once more. KB has now read the rest of the article through the questions, so the answer often comes easily. Allow one push. If it still does not clear, record it as **open** with the gap named.

Done when every parked question is cleared or open.

### 5. Close with the Conclusion

The Conclusion section is always asked last, in both modes: its `[lite]` questions in lite mode, all four in complete mode. It is where KB turns observations into lessons, so push hardest here: each strength, observation, and improvement must point back to something KB said earlier in the session, and each improvement must be an action KB could take on their next piece.

Done when the Conclusion questions have cleared the bar or been recorded open.

### 6. Hand over the record

Produce the close-reading record in the format below. Offer to save it as a Markdown file; ask where.

If KB stops mid-session, produce the record at that point with the **Next question** line filled in and any parked questions marked PARKED, so the session can resume.

## Close-reading record format

```markdown
# Close reading: <article title>

- Source: <author, publication, date, link>
- Mode: lite | complete (<sections covered>)
- Sessions: <dates>
- Next question: <section and question, or "none: complete">

## <Section>

**<Question label>.** <KB's answer, condensed, in KB's words. Keep quoted evidence.>

**<Question label>.** PARKED | OPEN: <what KB said so far> — gap: <missing where / what / so what>

## Lessons for my writing

<The Conclusion answers, as a numbered list.>
```

The record holds KB's thinking only. Add no commentary, grades, or analysis of your own.
