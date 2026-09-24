---
name: ask-kb
description: Ask which skill or flow fits your situation in this library, what is installed versus on demand, and how to invoke each. A guide to the library.
disable-model-invocation: true
---

# Ask KB

A guide for someone who does not remember every skill, including a first-time user of this library. Answer the question the user asked. If they asked nothing specific, give the tour below in under 30 lines.

## How the library is shaped

Two tiers, so a large library stays cheap to carry:

- **Installed** (`skills/`): the daily skills. Every agent loads their one-line descriptions at startup and fires them on its own. This is the whole engineering workflow plus a few cross-cutting tools such as `unslop`, `grilling`, `handoff`, and `research`.
- **On demand** (`library/`): everything used occasionally, such as writing workflows, business decisions, and video. No agent sees these at startup. `decide-skills` reads a short index, loads the one that fits, and runs it.

Adding a hundred library skills adds nothing to startup context. Only the installed tier is charged against the description budget, which `bin/skills-sync validate` enforces.

## Which door to use

| Situation | Use |
| --- | --- |
| Building, fixing, reviewing, or shipping software | Just ask. The coding skills fire on their own. For the engineering flow (idea → spec → tickets → implement → review), invoke `ask-matt`. |
| Anything else: an essay, a musing, a book, a business decision, a video | `decide-skills <what you want>`, or name the skill: `decide-skills musings-reviewer` |
| "What on-demand skills exist?" | Read [`../decide-skills/references/index.md`](../decide-skills/references/index.md) and list its groups and entries. It is generated from the library, so it is always current. |
| Moving a skill between tiers, or checking the budget | `skill-tiers` |

Answer "which skill for X" from the index and the installed skill list you can already see. Do not guess from memory. Name the skill, say which tier it is in, and give the exact invocation.

## Invocation by agent

| Agent | Installed skill | On-demand skill |
| --- | --- | --- |
| Claude Code (symlink install) | `/name` | `/decide-skills name` |
| Claude Code (plugin install) | `/kb:name` | `/kb:decide-skills name` |
| Codex | `$name` | `$decide-skills name` |
| Pi | `/skill:name` | `/skill:decide-skills name` |

Plain language works as well: "review my musing" reaches `decide-skills` through its description.

## For someone adopting this library

These skills encode one person's working style. Four of them name KB directly and assume KB's writing ecosystem: `content-fence`, `cognitive-editor`, `musings-reviewer`, and the writing group rules. Point a new user at the README's install section. If they want the library shaped around their own judgment, suggest forking it and using `skill-tiers` to choose their own daily set.
