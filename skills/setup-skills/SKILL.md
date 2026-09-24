---
name: setup-skills
description: "Choose which skills this machine installs: first-run interview, add or drop profiles, sync a fork with upstream. Not for changing repo defaults, use skill-tiers."
---

# Setup skills

Install only what this user will reach for most weeks. Everything else stays in their fork of the repository, where `decide-skills` can still find and run it, so a lean install loses nothing.

All commands run from the repository root. The install is a symlink, so find the root from this skill's real path:

```bash
cd "<this skill's directory>" && cd "$(pwd -P)/../.." && pwd
```

## Pick the branch

- **First run.** `my-skills.txt` does not exist, or it lists nothing beyond `core`: start at step 1.
- **"Add the video skills" / "drop business."** Run `bin/skills-sync select --add profile:video` (or `--remove`, or a skill name instead of a profile). Report its output, then go to step 5.
- **"Update" / "get the latest."** Go to [Sync](#sync).

## 1. Check the machine

Run `bin/skills-sync select --profiles`. If it fails, or no `upstream` remote exists (`git remote`), run `bin/skills-sync setup` first. `setup` adds the remote, installs `core` only, and wires the git hooks.

Note which agents are present: Claude Code (`~/.claude`), Codex (`codex` on PATH), Pi (`~/.pi/agent`).

## 2. Interview

Ask one question at a time. Stop once the profiles are clear. Four questions is usually enough.

1. What do you use coding agents for? (software, writing, business thinking, video, or other)
2. Software only: which languages? Do you ship large or risky changes, or run agents unattended for long stretches?
3. Will you write or adapt skills of your own?

Map the answers to profiles using the summaries from `select --profiles`:

| Answer | Profile |
| --- | --- |
| Builds software | `coding` |
| TypeScript or JavaScript | `typescript` |
| Big, cross-cutting, or security-sensitive changes | `deep-review` |
| Long or unattended agent runs | `agent-ops` |
| Learning, or editing plain prose | `productivity` |
| Business ideas, decisions, company blog | `business` |
| Explainer or product videos | `video` |
| Writes own skills | `maintainer` |

The `writing` profile is KB's personal essay system, tuned to one person's voice and blogs. Recommend it only if the user asks for that workflow by name.

## 3. Recommend

Show the proposed profiles, one line each on why, the startup bytes that `select --add ... --dry-run` reports, and what stays uninstalled but reachable. Prefer fewer: a profile used monthly belongs in the repo, not in the install. Keep the total well under the budget the command prints.

Done when the user has approved a list.

## 4. Install

Run `bin/skills-sync select --add profile:<a> profile:<b> ...`. It writes `my-skills.txt` (git-ignored, one per machine), pulls in each skill's requirements, and relinks every agent. Report what it added and any conflicts it printed.

## 5. Hand over

Tell the user, in a few lines:

- Restart the agent so it loads the new skills.
- Anything not installed: ask in plain language, or use `decide-skills <name or need>`. `ask-kb` explains the library.
- A need no skill covers: `decide-skills` can recommend an upstream skill or help build a new one in their fork.
- Updates: `bin/skills-sync sync`, or ask this skill to update.

## Sync

Run `bin/skills-sync sync`. It merges the latest upstream release tag (never unreleased `main`), rebuilds the generated index, and relinks. New upstream skills arrive uninstalled; list them and offer `select --add`.

If it stops on conflicts, the user changed a file that upstream also changed. Resolve with the `resolving-merge-conflicts` skill, keeping the user's intent, then run `bin/skills-sync index`, commit, and `bin/skills-sync refresh`.
