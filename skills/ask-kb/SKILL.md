---
name: ask-kb
description: Ask which skill or flow fits your situation in this library, what is installed versus on demand, and how to invoke each. A guide to the library.
disable-model-invocation: true
---

# Ask KB

A guide for someone who does not remember every skill, including a first-time user of this library. Answer the question the user asked. If they asked nothing specific, give the tour below in under 30 lines.

## How the library is shaped

Each machine installs only what its user picked. The rest stays in the repository, uninstalled and free until needed.

- **Installed**: the chosen profiles from `profiles.json` (`coding`, `typescript`, `business`, `video`, and others), plus `core`: `decide-skills`, `ask-kb`, and `setup-skills`. Agents load their one-line descriptions at startup and fire them on their own. `my-skills.txt` at the repository root records the choice; without it, the default is everything in `skills/`.
- **Everything else**: `decide-skills` reads a short index of every skill in the repository, loads the one that fits, and runs it.

Adding a hundred skills to the repository adds nothing to startup context. Only what is installed costs anything.

## Which door to use

| Situation | Use |
| --- | --- |
| Building, fixing, reviewing, or shipping software | Just ask. Installed coding skills fire on their own. For the engineering flow (idea → spec → tickets → implement → review), invoke `ask-matt`. |
| Anything else, or a skill you did not install | `decide-skills <what you want>`, or name the skill: `decide-skills musings-reviewer` |
| "What skills exist?" | Read [`../decide-skills/references/index.md`](../decide-skills/references/index.md) and list its sections. It is generated from the repository, so it is always current. |
| First install, adding or dropping a profile, updating | `setup-skills` |
| A need nothing covers | `decide-skills` recommends an upstream skill or helps build one in the user's fork |
| Changing the library's defaults (maintainer) | `skill-tiers` |

Answer "which skill for X" from the index and the installed skill list you can already see. Do not guess from memory. Name the skill, say whether it is installed here, and give the exact invocation.

## Invocation by agent

| Agent | Installed skill | On-demand skill |
| --- | --- | --- |
| Claude Code (fork install) | `/name` | `/decide-skills name` |
| Claude Code (plugin install) | `/kb:name` | `/kb:decide-skills name` |
| Codex | `$name` | `$decide-skills name` |
| Pi | `/skill:name` | `/skill:decide-skills name` |

Plain language works as well: "review my musing" reaches `decide-skills` through its description.

## For someone adopting this library

These skills encode one person's working style. Four of them name KB directly and assume KB's writing ecosystem: `content-fence`, `cognitive-editor`, `musings-reviewer`, and the writing group rules. A new user forks the repository and runs `bin/skills-sync setup`, then `setup-skills` (see the README's install section). Their own skills live in their fork. Upstream releases arrive through `bin/skills-sync sync`.
