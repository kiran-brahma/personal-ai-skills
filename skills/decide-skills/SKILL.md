---
name: decide-skills
description: "Find and run the right skill from this library when no installed one fits, or recommend adding or building one. For writing, business, video, uninstalled skills."
---

# Decide skills

Each machine installs only the skills its user picked. Everything else in the repository stays uninstalled, costing nothing until it is needed. This skill is the door to all of it: it reads a one-line-per-skill index, picks one skill, and runs it. When nothing fits, it says what to add or build.

## 1. Find the repository

The index is beside this file: [`references/index.md`](references/index.md). Skill files live outside the install, so resolve the repository root from this skill's **real** directory. The install is a symlink, and a path built from the symlink points at nothing:

```bash
cd "<this skill's directory>" && cd "$(pwd -P)/../.." && pwd
```

Every path in the index is relative to that root.

## 2. Pick one skill

Read the index. Match the request against each trigger contract and pick the **narrowest** one. When two entries match, the `Not for X` clauses decide. If they still tie, ask the user one question that names both.

- The user named a skill (`decide-skills musings-reviewer`): take it directly, with no matching.
- The match is a skill you can already see in your installed skill list: invoke it normally and stop here.
- Nothing fits: go to [Nothing fits](#nothing-fits). Do not stretch a near miss to fit.

Done when exactly one skill is chosen, or you have established that none fits.

## 3. Load it

1. If the index lists group rules for the chosen skill's section, read that file from `references/groups/` first.
2. An entry marked `[explicit]` is a gate. Run it only when the user asked for that workflow by name or unmistakable intent. Otherwise name it and ask before running.
3. Read `<root>/<path from the index>` and follow it exactly as if the user had invoked it directly. Relative paths inside it resolve from its own directory. Read only the references it directs you to.
4. Tell the user in one line which skill you loaded, so they can redirect you.

When a loaded skill names another skill, an installed one is invoked normally and an uninstalled one goes back through step 2.

If this is the second time this session you have loaded the same uninstalled skill, or the user says they will use it often, offer to install it: `bin/skills-sync select --add <name>`.

## Nothing fits

Work down this list, and stop at the first step that answers the need:

1. **Do it plainly.** Most requests need no skill. If a skill would only restate general competence, say that no skill fits and do the work.
2. **Recommend an upstream skill.** The `sources:` in `<root>/registry.yaml` are the libraries this one draws from, such as Matt Pocock's skills, pstack, and gstack. If one of them plausibly has the workflow, name the source and what to look for. Never install from it directly: `AGENTS.md` requires inspecting and approving a skill before adoption.
3. **Offer to build one.** Offer this only for a workflow the user will repeat, with steps or judgment general knowledge lacks. If they agree:
   - It goes in **their fork**, never upstream. If `origin` is the upstream library (`git remote -v`), say they need to fork first.
   - Scaffold it with `bin/skills-sync new <name> -d "<trigger contract>" --library`, then write the body with the `writing-for-agents` skill.
   - Run `bin/skills-sync index` and `bin/skills-sync validate`, then commit. To install it on this machine, run `bin/skills-sync select --add <name>`. Leave it out of `profiles.json`: that file is shared with upstream, and editing it invites merge conflicts on every sync.
