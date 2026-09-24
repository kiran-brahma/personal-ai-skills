# Skill routing evaluation cases

These cases test the two-tier library: `decide-skills` routing into `library/`, the `ask-kb` guide, and `skill-tiers` placement. They are prose for human judgment, not executable fixtures.

## Case 1: plain-language request reaches a library skill

Prompt: "Review my musing for today." (Paste a 250-word musing.)

Expected behavior:

- `decide-skills` fires from its description, not an installed writing skill.
- Reads the index, then `references/groups/writing.md`, then `library/musings-reviewer/SKILL.md`.
- States in one line that it loaded `musings-reviewer`.
- Reads no other library skill.

## Case 2: named skill skips matching

Prompt: "decide-skills content-fence"

Expected behavior:

- Loads `library/content-fence/SKILL.md` directly, with no matching step.
- Runs the Source-document preflight from the writing group rules before substantive work.

## Case 3: coding stays on the installed path

Prompt: "This test is flaky, help me find out why."

Expected behavior:

- `diagnosing-bugs` (installed) handles it. `decide-skills` does not fire, or it hands over to the installed skill without reading any library skill.

## Case 4: no fit

Prompt: "decide-skills convert this CSV to JSON."

Expected behavior:

- Reports in one line that no library skill fits, then does the task directly.
- Does not stretch `youtube-transcript-to-prose` or another near miss to fit.

## Case 5: explicit gate

Prompt: "decide-skills, anything from this session worth remembering?"

Expected behavior:

- Identifies `continual-learning`, which is marked `[explicit]`.
- Names it and asks before running, unless the user named it.

## Case 6: symlink install

Setup: installed through `bin/skills-sync refresh`, so `~/.claude/skills/decide-skills` is a symlink.

Expected behavior:

- Resolves the repository root from the real path (`pwd -P`) and reads `library/...` successfully.
- Never looks for `~/.claude/library`.

## Case 7: orientation for a new user

Prompt: "/ask-kb I just installed this. What can it do?"

Expected behavior:

- Explains the two tiers in a few lines, lists the index groups from the live index, and gives the exact invocation for the user's agent.
- Points engineering-flow questions to `ask-matt` rather than restating it.

## Case 8: demotion blocked by a caller

Prompt: "/skill-tiers move unslop to the library."

Expected behavior:

- Finds that `technical-writing` and `blast-radius` (installed) call `unslop`, and cites placement rule 2.
- Recommends keeping it installed, or updating the callers first. Moves nothing without approval.
