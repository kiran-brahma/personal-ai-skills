# Repository agent instructions

This is the canonical control document for work in this repository. Agent-specific entrypoints such as `CLAUDE.md` and `GEMINI.md` must refer back here instead of defining competing rules.

## Repository purpose

Maintain one public, GitHub-hosted, version-controlled library of reusable skills for coding, writing, research, planning, and miscellaneous work.

GitHub is the canonical source. A committed and pushed change is the version agents should consume. Do not maintain local-only skill variants.

## Required discovery order

Before selecting a skill:

1. Read this file.
2. Read [SKILLS.md](SKILLS.md) to identify the tier.
3. Installed work: read the category router (`skills/coding/SKILL.md`) to identify the specific skill. On-demand work: follow `skills/decide-skills/SKILL.md`, which picks one library skill from its generated index.
4. Read the selected skill's own `SKILL.md` and only the supporting references it directs you to use.
5. Read any project-specific rules that are in scope for the work.

Do not load every skill by default. Use the catalogue, the router, and the index to narrow discovery.

A router is a skill beside the skills it routes to, not a directory above them. It names its targets rather than containing them.

## Two tiers

- `skills/<name>/` is the **installed** tier. It is linked into every agent, and its descriptions are charged against the budget. Keep it to daily-use skills, skills an installed skill calls by name, and skills that must fire unprompted.
- `library/<name>/` is the **on-demand** tier. No agent scans it, so it costs nothing at startup. `decide-skills` reaches it through `skills/decide-skills/references/index.md`, which `bin/skills-sync index` generates from each library skill's frontmatter (`metadata.group` sets its group).

Both tiers follow the same flat layout rules, and a name must be unique across both. Move a skill with `bin/skills-sync tier <name> installed|library`, following the `skill-tiers` skill.

## The layout contract

The layout is flat and machine-enforced. Before committing any change to `skills/`, run:

```bash
bin/skills-sync validate
```

The rules exist because an agent breaks without them, and each finding names which one:

- A skill is exactly `skills/<name>/SKILL.md` or `library/<name>/SKILL.md`. Claude Code searches one level and finds nothing deeper.
- No `SKILL.md` may sit beneath another. Pi stops at the first one it finds and never looks below it.
- A skill directory is real, never a symlink. Codex drops symlinks when it copies a plugin into its cache.
- `name:` matches the directory, and names are unique library-wide. A mismatch or a duplicate fails silently at run time.
- The generated library index is current. `decide-skills` finds library skills only through it.
- Installed descriptions stay within the per-skill and library budgets in [policies/skill-format.md](policies/skill-format.md). Codex truncates past a fixed budget with no error, which degrades routing invisibly.

Do not relax a rule to make a change fit. The layout is what allows one copy of a skill to serve every agent, which is the point of the repository.

Git hooks run `validate` before each commit and reconcile the local install after. Do not bypass them with `--no-verify` to land a change that does not validate.

## Project rules

Project-specific `AGENTS.md`, `CLAUDE.md`, or equivalent rules documents may add constraints for the project being worked on. They must not silently rewrite this repository's canonical skill library.

When rules conflict, follow this order unless the user explicitly changes it:

1. direct user request;
2. applicable project-specific rules;
3. this repository control document;
4. the selected skill;
5. general agent defaults.

## New-skill adoption workflow

When a new skill is proposed or discovered, do not immediately install, activate, rewrite, or treat it as authoritative.

First inspect the complete skill package, including `SKILL.md`, scripts, references, assets, metadata, dependencies, external links, and required permissions. Then explain to the owner:

- what problem the skill solves;
- when it should and should not trigger;
- the workflow it asks the agent to follow;
- what output or evidence it produces;
- what implicit assumptions it makes;
- what tools, files, network access, or permissions it requires;
- where it may conflict with this repository, a project, or another skill; and
- which parts should be adjusted for the owner's preferences.

Pause for the owner's discussion and approval before changing the skill into the active library. If adjustments are requested, apply them to the single canonical skill and explain the resulting local behaviour.

After approval, scaffold it with `bin/skills-sync new <name> -d "<description>"` so it starts conformant. Add `--library` unless it meets the installed-tier rule in `skills/skill-tiers/SKILL.md`. Then record it in `registry.yaml`, add relevant evaluation cases under `evals/`, and update the changelog when appropriate.

## Skill changes

When modifying an existing skill, summarize the behavioural change and its likely effect on future agent decisions.

Do not silently replace a locally adapted skill with upstream content. Compare upstream changes, local intent, and evaluations before adopting them:

```bash
bin/skills-sync upstream        # what changed upstream, and where it collides with a local edit
bin/skills-sync adopt --apply   # three-way merge that preserves local adaptations
```

`adopt` leaves conflict markers where upstream and local changed the same lines. Resolving them is a judgment about local intent, not a merge to complete mechanically. `validate` fails while any marker remains, so an unresolved merge cannot reach a commit or a release.

Move the pinned commit with `bin/skills-sync upstream --pin <source>` only after the review, the edits, and the evaluation cases are done. Pinning is a claim that the comparison was made and resolved.

## Releasing

A release is gated, not a push. `bin/skills-sync release` blocks on a dirty tree, a validation failure, an invalid plugin manifest, an existing tag, and a missing changelog entry, then publishes and verifies that the local install actually moved.

The evaluation cases under `evals/` are prose for human judgment, not executable fixtures. `release` names which cases cover the skills that changed, but nothing runs them. Structural checks are not behavioural ones; say so rather than implying a release was verified end to end.

## Scope discipline

Do not add agent-specific copies of a skill merely because Claude, Gemini, Codex, Pi, or another agent has different discovery mechanics. Keep the skill portable and place integration instructions in `adapters/` or the relevant agent entrypoint.

Do not add a new skill when a project rules document is the correct place for project-only information.
