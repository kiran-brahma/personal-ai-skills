---
name: ask-kb
description: "Route requests that may fit this skill library: show theme options, recommend a skill, and wait for the user's choice."
---

# Ask KB

Route the user to one focused skill while keeping only this router, Grilling, and Implement installed by default. The complete catalogue is in [`references/index.md`](references/index.md).

## Find the catalogue and skill files

Read the generated index beside this file. It lists all skills by their primary theme, with a short trigger description and a repository-relative path to each full `SKILL.md`.

Resolve the repository root from this skill's physical directory: this file is at `<root>/skills/ask-kb/SKILL.md`. Global author installs symlink the skill into the agent's skills folder, so follow the link to its real path. Consumer plugin installs include the complete repository, including `library/`.

## Choose the route

1. If the user explicitly names or unmistakably requests a skill's workflow, or selects one from a menu, treat that as the choice. Load that skill's full `SKILL.md` and follow it.
2. If the user asks to find, select, or build a skill, load `decide-skills` from its indexed path and follow its workflow.
3. Otherwise, compare the request with the theme descriptions and skill trigger descriptions in the index. Select every theme that materially fits the request.
4. If nothing fits, say that no listed skill fits and ask whether the user wants a general response.
5. For each relevant theme, list **every skill in that theme**, not just the closest candidates. For a cross-theme request, combine all skills from the relevant themes into one list. Omit Ask-kb and `decide-skills` from ordinary task menus; include them for skill-library requests. Each option has its name and index description.
6. Mark one recommended skill and give a brief reason. Ask the user to choose, then wait. Do not begin the task before the choice.
7. After the user chooses, read the complete skill file. If the index links routing notes for its theme, read those notes too. For `business-blog-post-generator`, `business-idea-review`, or `decision-navigator`, also read `skills/ask-kb/references/groups/business.md`.
8. Load every `metadata.requires` dependency from its indexed path before starting the selected workflow. Load `metadata.lazy-requires` only when its relevant branch runs. These fields are checked by validation; only `requires` affects optional installation bundles.
9. Tell the user which skill you loaded, then continue its workflow.

## Direct requests

An exact skill name, explicit invocation, or unmistakable request for a named workflow is already the user's choice; load it without presenting a menu. This includes Grilling requests such as "grill me on this" and the user-invoked Implement skill. Implement remains gated: run it only after the user invokes it or selects it from Ask-kb's menu.

When Implement runs, load its lazy dependencies from the indexed library paths: TDD when its workflow applies, and Code Review for its required final review. These dependencies are not installed by default.

## Skill-library requests

For questions about the catalogue, summarize the relevant theme sections. For setup or changing this machine's optional installation, load `setup-skills`. For changing the repository's default tiers or theme assignments, load `skill-tiers`. For a direct request to find or build a skill, load `decide-skills`.

Ask-kb and `decide-skills` are both classified under Misc for catalogue completeness, but neither belongs in ordinary task menus.
