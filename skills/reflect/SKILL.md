---
name: reflect
description: Spawn three parallel review subagents over the active transcript, surface learnings, and route each to a skill edit. Use when the user says reflect.
disable-model-invocation: true
---

# Reflect

**Portability note.** This skill was adapted from pstack. If the text below names Cursor-only paths, tools, transcript locations, or model slugs, translate them to the current harness and project layout. Do not read unrelated workspaces or private transcripts; if an equivalent capability is unavailable, state the limitation and continue with the safest supported alternative.

Mine the current conversation for durable learnings, then route them into skill edits.

Invoke when the user says "reflect" or "/reflect". Skip when the conversation is trivial, off-topic, or already covered by an existing skill the parent followed correctly. One-offs are not learnings.

## 1. Locate the active transcript

Before fanning out, find this conversation's transcript in the `agent-transcripts/` directory the system prompt names. Do not glob across other project transcript directories. That crosses workspace boundaries and reads private chats from unrelated projects.

```bash
ls -t <agent-transcripts>/*.jsonl <agent-transcripts>/*/*.jsonl <agent-transcripts>/*/subagents/*.jsonl 2>/dev/null | head -10
```

That covers the legacy flat (`<id>.jsonl`), current nested (`<id>/<id>.jsonl`), and subagent (`<parent>/subagents/<child>.jsonl`) layouts. For each candidate, read the first JSONL line. Take the file whose `message.content[0].text` contains the conversation's opening user prompt. If none matches, pass a tight digest of the session instead.

## 2. Spawn three reviewers in parallel

One message, three `Task` calls, `subagent_type: generalPurpose`, agent mode (`readonly: false`). Reviewers need MCP access to look up the tickets, chat threads, and observability traces the transcript references, and readonly strips MCPs.

Each reviewer and the synthesizer name a role line in the current harness's model configuration and a default. Set `model` to that line's value, or to the default if the rule or the line is missing. Leave `model` unset when the value is `auto` or `inherit-parent`. If the Task tool rejects a slug, use the default and say so. If it rejects the default, use the closest valid slug of the same family from its error message. Pick each subagent's reasoning level and fast or standard speed for the job: deep reasoning for judgment, a fast tier for search and grunt work.

| Lens | Role line | Default `model` | Prompt template |
|---|---|---|---|
| Judgment | `reflect judgment, divergent, synthesizer` | `a high-reasoning model` | `references/judgment-reviewer.md` |
| Tooling | `reflect tooling` | `a fast model from a second family` | `references/tooling-reviewer.md` |
| Divergent | `reflect judgment, divergent, synthesizer` | `a high-reasoning model` | `references/divergent-reviewer.md` |

Pass each template verbatim, substituting the transcript path or digest where marked. Reviewers return findings in the `Task` response body.

## 3. Synthesize

One `Task` call, `subagent_type: generalPurpose`, `model` from the `reflect judgment, divergent, synthesizer` line (default `a high-reasoning model`), agent mode (`readonly: false`). It spot-verifies citations through MCP, and readonly strips MCPs. Pass `references/synthesizer.md` verbatim, with each reviewer's full output inlined where marked. It returns an Accepted / Rejected / Backlog list.

## 4. Prefer a check over a rule

A rule is text a future agent reads and may or may not follow. A check is code that runs and gives the same answer every time. A lesson worth keeping is worth encoding as the more reliable of the two, so this pass asks of every Accepted item: could this be a check instead?

Walk the list and name what would enforce each item: a lint rule, a test, a git hook, a validation script, a metadata flag, a schema. Where something would, that is the deliverable, and the skill edit shrinks to a pointer at it.

Carry such an item forward as a proposed check, presented to the user in step 5 alongside the edits. Do not drop it into Backlog on the grounds that a script would do it better: a lesson deferred that way is a lesson lost, because the script never gets written and the rule never gets added either.

Only when no check is possible does the lesson stay as skill text.

## 5. Apply

Present the synthesizer's full Accepted / Rejected / Backlog output and wait for explicit approval before applying any Accepted edit. The user picks the subset and may redirect routings. Skill changes affect every future agent in the org. Do not auto-apply.

File each Backlog item to your team's devex or backlog tracker without waiting. Only the Accepted list waits for approval.

Follow each approved row's Routing exactly:

- Trivial existing-skill edit (a one-line bullet, a tightened sentence, a stale fact corrected): the parent does it directly.
- Substantive existing-skill edit (a new section, a new pattern table, more than ~10 lines): hand to Cursor's built-in `create-skill` skill and run its draft / test / iterate loop.
- `tune description: <skill path>` (the skill exists but didn't trigger when it should have): hand to `create-skill` and run its description-optimization loop.
- `new skill via create-skill: <kebab-name>`: hand creation to `create-skill`. Do not invent the shape ad hoc.
- `check: <mechanism>`: write the check, then prove it fails on the case that prompted it before declaring it done. A check that never fires is worse than none, because it manufactures confidence. Where the repo already has a home for such checks (a validation script, a pre-commit hook), add it there rather than starting a new one.

If your environment ships a SKILL.md validator, run it on every touched skill before declaring done.

## 6. Summarize for the user

Short list, no preamble:

- Edits applied: `<skill path>`. What changed, one line each.
- Checks added: `<path>`. What it catches, and the case it was proven against. One line each.
- New skills created: `<skill path>`. One line each (rare).
- Backlog filed to the devex tracker: `<issue title>` (`<tags>`). One line each.
- Dropped: one line per rejected finding + reason from the synthesizer.
