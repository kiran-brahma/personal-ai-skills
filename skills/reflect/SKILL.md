---
name: reflect
description: Spawn three parallel review subagents over the active transcript, surface learnings, and route each to a concrete edit on an existing skill. Use when the user says reflect.
disable-model-invocation: true
---

# Reflect

**Portability note.** This skill was adapted from pstack. If the text below names Cursor-only paths, tools, transcript locations, or model slugs, translate them to the current harness and project layout. Do not read unrelated workspaces or private transcripts; if an equivalent capability is unavailable, state the limitation and continue with the safest supported alternative.

Mine the current conversation for durable learnings, then route them into skill edits.

## When to invoke

- The user said "reflect" or "/reflect".
- A complex task (5+ tool calls) just landed cleanly and the recipe is worth keeping.
- The agent hit dead ends, found the working path, and the path generalizes.
- The user corrected the agent's approach mid-task.
- A non-trivial workflow emerged that isn't captured anywhere.

Skip when the conversation is trivial, off-topic, or already covered by an existing skill the parent followed correctly. One-offs are not learnings.

## Process

### 1. Locate the active transcript

The parent finds its own transcript file before fanning out. The system prompt names the active workspace's `agent-transcripts/` directory; use that path. Do not glob across `other project transcript directories`. That crosses workspace boundaries and reads private chats from unrelated projects.

```bash
ls -t <agent-transcripts>/*.jsonl <agent-transcripts>/*/*.jsonl <agent-transcripts>/*/subagents/*.jsonl 2>/dev/null | head -10
```

Three transcript layouts: legacy flat (`<id>.jsonl`), current nested (`<id>/<id>.jsonl`), and subagent (`<parent>/subagents/<child>.jsonl`).

For each candidate, read the first JSONL line and check that `message.content[0].text` contains the conversation's opening user prompt. Take the matching path. If no path resolves, write a tight digest of the session and pass that instead.

### 2. Spawn three reviewers in parallel

One message, three `Task` calls, `subagent_type: generalPurpose`, explicit `model:` on each, agent mode (`readonly: false`). Reviewers need MCP access for context lookups (tickets, chat threads, observability traces referenced in the transcript); readonly strips MCPs. The prompt forbids file writes; the parent applies edits.

| Lens | `model` | Prompt template |
|---|---|---|
| Judgment | your configured reflect-judgment model (default `a high-reasoning model`) | `references/judgment-reviewer.md` |
| Tooling | your configured reflect-tooling model (default `a second model family`) | `references/tooling-reviewer.md` |
| Divergent | your configured reflect-judgment model (default `a high-reasoning model`) | `references/divergent-reviewer.md` |

Pass each template verbatim, substituting the transcript path or digest where marked. Reviewers return findings in the `Task` response body.

### 3. Synthesize

One `Task` call, `subagent_type: generalPurpose`, using your configured reflect-judgment model (default `a high-reasoning model`), agent mode (`readonly: false`). The synthesizer's quality check includes spot-verifying citations, which can require MCP access; readonly strips MCPs. Use `references/synthesizer.md` verbatim, with each reviewer's full output inlined where marked. The synthesizer returns a structured Accepted / Rejected / Backlog list.

### 4. Prefer a check over a rule

A rule is text a future agent reads and may or may not follow. A check is code that runs and gives the same answer every time. A lesson worth keeping is worth encoding as the more reliable of the two, so this pass asks of every Accepted item: could this be a check instead?

Walk the list and name what would enforce each item: a lint rule, a test, a git hook, a validation script, a metadata flag, a schema. Where something would, that is the deliverable, and the skill edit shrinks to a pointer at it.

Carry such an item forward as a proposed check, presented to the user in step 5 alongside the edits. Do not drop it into Backlog on the grounds that a script would do it better: a lesson deferred that way is a lesson lost, because the script never gets written and the rule never gets added either.

Only when no check is possible does the lesson stay as skill text.

### 5. Apply

Before applying any Accepted edit, present the synthesizer's full Accepted/Rejected/Backlog output to the user and wait for explicit approval. The user picks which subset to apply and may redirect routings. Skill changes affect every future agent in the org; do not auto-apply.

Backlog items file to whatever devex / backlog tracker your team uses automatically. Those are tracker submissions, not skill edits. Only the Accepted list waits for approval.

For each approved Accepted item, follow the Routing field exactly:

- Trivial existing-skill edit (a one-line bullet, a tightened sentence, a stale fact corrected): parent does directly.
- Substantive existing-skill edit (a new section, a new pattern table, more than ~10 lines): hand to Cursor's built-in `create-skill` skill and run its draft / test / iterate loop.
- `tune description: <skill path>` (the skill exists but didn't trigger when it should have): hand to `create-skill` and run its description-optimization loop.
- `new skill via create-skill: <kebab-name>`: hand creation to `create-skill`. Do not invent the shape ad hoc.
- `check: <mechanism>`: write the check, then prove it fails on the case that prompted it before declaring it done. A check that never fires is worse than none, because it manufactures confidence. Where the repo already has a home for such checks (a validation script, a pre-commit hook), add it there rather than starting a new one.

If your environment ships a SKILL.md validator, run it on every touched skill before declaring done. Skip this step if it doesn't.

### 6. Summarize for the user

Short list, no preamble:

- Edits applied: `<skill path>`. What changed, one line each.
- Checks added: `<path>`. What it catches, and the case it was proven against. One line each.
- New skills created: `<skill path>`. One line each (rare).
- Backlog filed to the devex tracker: `<issue title>` (`<tags>`). One line each.
- Dropped: one line per rejected finding + reason from the synthesizer.
