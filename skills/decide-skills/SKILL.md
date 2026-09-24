---
name: decide-skills
description: "Pick and run the one on-demand library skill that fits: writing, essays, business decisions, video, skill upkeep. Not for coding, use coding."
---

# Decide skills

This library has two tiers. Daily skills are installed and fire on their own. Everything else lives in `library/`, uninstalled, so it costs nothing until needed. This skill is the only door into `library/`: it reads a one-line-per-skill index, picks one skill, and runs it.

## 1. Find the library

The index is beside this file: [`references/index.md`](references/index.md). Library skills live outside the installed tree, so resolve the repository root from this skill's **real** directory. The install is a symlink, and a path built from the symlink points at nothing:

```bash
cd "<this skill's directory>" && cd "$(pwd -P)/../.." && pwd
```

Every path in the index is relative to that root.

## 2. Pick one skill

Read the index. Match the request against each trigger contract and pick the **narrowest** one. When two entries match, the `Not for X` clauses decide. If they still tie, ask the user one question that names both.

- The user named a skill (`decide-skills musings-reviewer`): take it directly, with no matching.
- The request fits an installed skill better (coding, `unslop`, `grilling`, `research`, and others the agent already sees): hand over to that skill and stop here.
- Nothing fits: say so in one line and do the work without a skill. Do not stretch a near miss to fit.

Done when exactly one library skill is chosen, or you have stated that none fits.

## 3. Load it

1. If the index lists group rules for the chosen skill's group, read that file from `references/groups/` first. It carries routing and style rules shared across the group.
2. An entry marked `[explicit]` is a gate. Run it only when the user asked for that workflow by name or unmistakable intent. Otherwise name it and ask before running.
3. Read `<root>/library/<name>/SKILL.md` and follow it exactly as if the user had invoked it directly. Relative paths inside it resolve from its own directory. Read only the references it directs you to.
4. Tell the user in one line which skill you loaded, so they can redirect you.

When a library skill names another skill, an installed one is invoked normally and a library one goes back through step 2.
