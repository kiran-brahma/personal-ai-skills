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

## Case 9: first-run setup for a new user

Setup: a fresh fork after `bin/skills-sync setup`, with only `core` installed.

Prompt: "/setup-skills"

Expected behavior:

- Asks one question at a time, and no more than about four.
- Recommends a small set of profiles with reasons and the startup bytes from `select --dry-run`. Does not recommend `writing` unless the user asks for KB's essay workflow.
- Installs only after approval, then says to restart the agent and how to reach uninstalled skills.

## Case 10: uninstalled skill reached, then promoted

Setup: `coding` installed, `business` not.

Prompt: "decide-skills should I take this client at a 30% discount?" Then, later in the same session, another decision question.

Expected behavior:

- Loads `library/decision-navigator/SKILL.md` from the index both times.
- On the second load, offers `bin/skills-sync select --add decision-navigator`.

## Case 11: nothing fits, build one

Prompt: "decide-skills plan my week's meals from what's in my fridge. I do this every Sunday."

Expected behavior:

- No skill fits. The need repeats, so it offers to build one rather than stretching a near miss.
- Checks `git remote -v`. If `origin` is the upstream library, says to fork first.
- Scaffolds with `new ... --library`, writes the body with `writing-for-agents`, and installs by name. Leaves `profiles.json` alone.

## Case 12: sync

Prompt: "/setup-skills update"

Expected behavior:

- Runs `bin/skills-sync sync`. Merges only the latest release tag, not upstream `main`.
- Lists new upstream skills as uninstalled and offers `select --add`.
- On a real conflict, stops and uses `resolving-merge-conflicts`. A conflict only in the generated index is rebuilt without asking.
