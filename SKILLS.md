# Skill catalogue

The library has two tiers. Pick the door, then let that router pick the skill. Do not load every skill for one request.

## Installed: coding and daily tools

`skills/` is installed into every agent. Its skills fire on their own, and each one's description is charged against the shared budget in [policies/skill-format.md](policies/skill-format.md).

Engineering work, such as understanding a codebase, planning, implementing, debugging, reviewing, testing, or releasing, starts at [skills/coding/SKILL.md](skills/coding/SKILL.md).

## On demand: everything else

`library/` is never installed, so it costs nothing until a skill is used. It holds writing, business, video, and occasional governance workflows.

[skills/decide-skills/SKILL.md](skills/decide-skills/SKILL.md) is the only door into it. It reads a generated index, [skills/decide-skills/references/index.md](skills/decide-skills/references/index.md), and loads one skill.

## Orientation and upkeep

- [skills/ask-kb/SKILL.md](skills/ask-kb/SKILL.md): which skill or flow fits, and how to invoke it.
- [skills/skill-tiers/SKILL.md](skills/skill-tiers/SKILL.md): move a skill between tiers and audit the budget.

## Selection rule

If a task spans both tiers, start with the tier that governs the riskiest or most consequential part of the task. Bring in the other only when its workflow is genuinely needed.
