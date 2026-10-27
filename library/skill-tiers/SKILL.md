---
name: skill-tiers
description: Move a skill between installed and on-demand library tiers, or audit which skills belong in each, keeping the budget and index correct.
disable-model-invocation: true
---

# Skill tiers

The tier is the library's **default**: what a machine installs when it has no `my-skills.txt`, and what the plugin ships. Keep the installed tier small and the library large. **Installed** skills (`skills/`) cost description budget in every session. **Library** skills (`library/`) cost nothing until Ask-kb loads one. To change only what one machine installs, use `setup-skills` instead. Follow [`AGENTS.md`](../../AGENTS.md) for anything beyond tier placement.

## Placement rule

A skill stays **installed** when any of these holds. Otherwise it belongs in the library.

1. **Daily**: the owner uses it most working days.
2. **Called**: an installed skill requires its instructions at every invocation. If it only needs another workflow sometimes, use a lazy dependency so Ask-kb can load it from the catalogue when needed.
3. **Ambient**: it must fire mid-task without being asked, such as `unslop` running as a final pass.

A library skill may freely load installed skills. An installed skill may also load a library skill on demand through Ask-kb; declare that with `metadata.lazy-requires` so validation checks the reference without installing the dependency.

## Move a skill

1. **Confirm with the owner first.** Name the skill, its destination, and the invocation change. An on-demand skill is loaded through Ask-kb; a promoted skill gains its own `/name` and starts costing budget.
2. Run `bin/skills-sync tier <name> library` or `bin/skills-sync tier <name> installed`. This runs `git mv` and regenerates the index.
3. Add the skill to exactly one theme in `profiles.json` and to any optional install bundles that should contain it. If it always needs another skill, declare an install-time dependency so `select` installs both:

   ```yaml
   metadata:
     requires: grilling unslop
   ```

   If it needs another skill only in a particular workflow branch, declare a lazy dependency instead:

   ```yaml
   metadata:
     lazy-requires: tdd code-review
   ```

4. Run `bin/skills-sync validate`. Fix every `I1-refs` finding by rewriting the relative link across tiers (`../x/SKILL.md` becomes `../../skills/x/SKILL.md` or `../../library/x/SKILL.md`). Moving a skill to the installed tier can trip `B2-desc-total`. Tighten a description, or demote something else, rather than raising the limit.
5. If Ask-kb's routing notes mention the skill, update them.
6. Add a changelog entry that states the behavioural change: what now loads on demand, and what fires on its own.

Done when validate passes with zero errors and the owner has approved each move.

## Audit

When asked which skills should move, list every installed skill with its description bytes, sorted by size, and mark which placement rule keeps it installed. A skill no rule keeps is a demotion candidate. Present the candidates, the bytes they would free, and the invocation each would lose. Move nothing until the owner picks.
