# Skill catalogue

The library has two tiers. Ask-kb is the single default router; its generated catalogue groups every skill into the four themes.

## Default set

`skills/` contains the three skills loaded by default:

- `ask-kb`: the universal router. It lists every skill in relevant themes, recommends one, waits for the user's choice, then loads it.
- `grilling`: the user's frequently used design-interview workflow.
- `implement`: the user's frequently used, explicitly invoked implementation workflow. It loads TDD and Code Review lazily.

## On demand

`library/` holds the rest of the skill collection. Ask-kb reads [`skills/ask-kb/references/index.md`](skills/ask-kb/references/index.md) to find and load the selected skill. The four themes are Coding, Writing, Productivity, and Misc; each skill has exactly one primary theme.

`decide-skills` remains on demand for explicit skill-library requests and for finding or building a skill. Ask-kb omits Ask-kb and `decide-skills` from ordinary task menus.

## Optional install profiles

Profiles in [`profiles.json`](profiles.json) remain optional bundles for `setup-skills`. They do not define theme membership or the default set. A machine can install extra skills with `bin/skills-sync select`; otherwise the remaining library stays available through Ask-kb without loading its descriptions at startup.

## Maintenance

- [`skills/ask-kb/SKILL.md`](skills/ask-kb/SKILL.md): routing behavior and loading rules.
- [`library/skill-tiers/SKILL.md`](library/skill-tiers/SKILL.md): repository-default tier changes.
- [`library/setup-skills/SKILL.md`](library/setup-skills/SKILL.md): per-machine optional installs.
