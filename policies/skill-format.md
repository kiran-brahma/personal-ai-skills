# Skill format

Each concrete skill is a directory containing its own `SKILL.md` with YAML frontmatter containing at least:

```yaml
---
name: example-skill
description: Explains what the skill does and when it applies.
---
```

Skill names use lowercase letters, numbers, and hyphens.

## Layout

Every concrete skill is a directory directly under `skills/` (installed) or `library/`
(on demand), named for the skill: `skills/code-review/SKILL.md`,
`library/content-fence/SKILL.md`. The layout is flat, one level, with no exceptions. A name
is unique across both tiers.

A skill that always needs another skill declares an install-time dependency, so `bin/skills-sync select` installs both:

```yaml
metadata:
  requires: grilling domain-modeling
```

For a skill needed only in one branch, declare a lazy dependency. Ask-kb loads it from the
catalogue only when that branch runs:

```yaml
metadata:
  lazy-requires: tdd code-review
```

Declare only real dependencies. A mention or a "see also" does not count. `validate`
checks both kinds of dependency against the complete skill catalogue (`R1-requires`), but
only `requires` makes `select` install another skill.

`profiles.json` separates the four primary themes from optional install profiles. Every
skill appears in exactly one theme, which sets its section in Ask-kb's generated catalogue.
Optional profiles only affect what a particular machine installs.

This is not a stylistic preference, and it is worth being exact about which agent
forces it:

- **Claude Code** discovers `skills/<name>/SKILL.md` and ignores anything deeper.
  One level is its whole search.
- **Pi** recurses, but stops at the first `SKILL.md` it finds and does not look
  beneath it, so a skill nested under another skill is invisible to it. A category
  router with its own `SKILL.md` would hide every skill under it.
- **Codex** recurses to any depth and does not stop at a parent `SKILL.md`, so the
  flat layout is not for its benefit. It has a different constraint: it copies
  plugins into a cache and silently drops symlinks, so a symlinked skill directory
  cannot substitute for a real one, and it truncates skill descriptions past a
  fixed budget.

So the flat layout is required by Claude Code and Pi. Codex tolerates nesting but
cannot tolerate symlinks.

Ask-kb stays at `skills/ask-kb/SKILL.md` and is the only general router. Theme names are
catalogue groups, not parent directories or separate router skills. Because every concrete
skill is a sibling, nothing is nested beneath a router and the discovery order in
`AGENTS.md` still holds. Ask-kb lists trigger boundaries and loads selected instructions; it
never duplicates those instructions.

`bin/skills-sync validate` enforces all of this. A change that breaks it is a change
that breaks at least one agent.

## The description rule

The description is a **trigger contract**, not a summary. It answers one question:
should this skill fire for the request in front of the agent? Everything else belongs
in the body, where it costs nothing until the skill is actually invoked.

Budget: **200 bytes per description, 9000 bytes across the installed tier.** Library
descriptions are never loaded at startup, so they are exempt from the total; they still
keep the 200-byte rule because each one becomes a line in the index Ask-kb reads. Codex loads every
description into a fixed skills budget and silently truncates once that is exceeded.
Truncation degrades routing with no error, so the limit is a correctness constraint
rather than a cost optimisation. `disable-model-invocation` does not exempt a skill: Codex
ignores that field and charges the description regardless.

Write it in three parts, in this order:

1. **What it does**: one clause, concrete, naming the artifact or outcome.
2. **When it fires**: the phrasing a user would actually type.
3. **When it does not**: the neighbouring skill that should handle those cases.

Rules:

- Do not restate the skill name, or open with "This skill".
- Do not describe the workflow, phases, or sub-agents. That is body content.
- Include the words that distinguish this skill from its nearest neighbour. If two
  descriptions would both match a request, at least one of them is wrong.
- Prefer concrete triggers to abstract capability claims.

```yaml
# Too long: explains the workflow, which the body already does.
description: A constrained editorial-audit skill for the daily musing, a short one-sitting
  piece intended to carry one atomic idea. Review drafts and finals for atomicity, argument
  structure and fallacies when argumentative, definition quality when observational, prose
  quality using the bundled style notes, and the 300-word cap for finals. Use when...

# Right: 155 bytes, every trigger preserved, boundary explicit.
description: "Review the daily musing (one atomic idea, 300-word cap) for atomicity,
  argument structure, and prose. Not for essays or blog drafts, use cognitive-editor."
```

## Adding a skill

Scaffold it so it starts conformant, then fill in the body:

```bash
bin/skills-sync new my-skill -d "What it does. When it fires. Not for X, use Y."
```

The command refuses an over-budget description and an invalid name. After writing the
body, record the skill in `registry.yaml` and run `bin/skills-sync validate`.

The portable skill may include `references/`, `scripts/`, `assets/`, or `agents/` only when those resources directly support the skill. Keep the entrypoint focused and disclose detailed material progressively.

Portable content should not depend on one agent's private metadata or installation path. Agent-specific integration belongs under `adapters/`.

Before a skill is considered ready:

1. its frontmatter and structure validate;
2. its instructions are reviewed for scope and unintended permissions;
3. its provenance is recorded when it originated elsewhere; and
4. important behaviour is tested with realistic evaluation cases.
