---
name: skill-tiers
description: Move a skill between installed and on-demand library tiers, or audit which skills belong in each, keeping the budget and index correct.
disable-model-invocation: true
---

# Skill tiers

The tier is the library's **default**: what a machine installs when it has no `my-skills.txt`, and what the plugin ships. Keep the installed tier small and the library large. **Installed** skills (`skills/`) cost description budget in every session. **Library** skills (`library/`) cost nothing until `decide-skills` loads one. To change only what one machine installs, use `setup-skills` instead. Follow [`AGENTS.md`](../../AGENTS.md) for anything beyond tier placement.

## Placement rule

A skill stays **installed** when any of these holds. Otherwise it belongs in the library.

1. **Daily**: the owner uses it most working days.
2. **Called**: an installed skill names it (`` `name` `` or a link). Find callers with `grep -rn "\`<name>\`\|/<name>/" skills/`. A library skill would leave that caller pointing at nothing it can see.
3. **Ambient**: it must fire mid-task without being asked, such as `unslop` running as a final pass.

A library skill may freely call installed skills. The reverse needs rule 2.

## Move a skill

1. **Confirm with the owner first.** Name the skill, its destination, and the invocation change. `/musings-reviewer` becomes `/decide-skills musings-reviewer`; a promoted skill gains its own `/name` and starts costing budget.
2. Run `bin/skills-sync tier <name> library` or `bin/skills-sync tier <name> installed`. This runs `git mv` and regenerates the index.
3. Make sure the skill is listed in a profile in `profiles.json`. The first profile listing it sets its section in the index. If it calls another skill, declare that in its frontmatter so `select` installs both:

   ```yaml
   metadata:
     requires: grilling unslop
   ```

4. Run `bin/skills-sync validate`. Fix every `I1-refs` finding by rewriting the relative link across tiers (`../x/SKILL.md` becomes `../../skills/x/SKILL.md` or `../../library/x/SKILL.md`). Moving a skill to the installed tier can trip `B2-desc-total`. Tighten a description, or demote something else, rather than raising the limit.
5. If a profile's group rules in `../decide-skills/references/groups/` mention the skill, update them.
6. Add a changelog entry that states the behavioural change: what now loads on demand, and what fires on its own.

Done when validate passes with zero errors and the owner has approved each move.

## Audit

When asked which skills should move, list every installed skill with its description bytes, sorted by size, and mark which placement rule keeps it installed. A skill no rule keeps is a demotion candidate. Present the candidates, the bytes they would free, and the invocation each would lose. Move nothing until the owner picks.
