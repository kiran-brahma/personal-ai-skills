# Skill format

Each category has a routing `SKILL.md`. Each concrete skill is a directory containing its own `SKILL.md` with YAML frontmatter containing at least:

```yaml
---
name: example-skill
description: Explains what the skill does and when it applies.
---
```

Skill names use lowercase letters, numbers, and hyphens. The description must be specific enough to support accurate discovery and must state the intended scope.

The category routing file may list concrete skills and their trigger boundaries, but it should not duplicate their detailed instructions. A concrete skill should live below its category, for example `skills/coding/code-review/SKILL.md`.

The portable skill may include `references/`, `scripts/`, `assets/`, or `agents/` only when those resources directly support the skill. Keep the entrypoint focused and disclose detailed material progressively.

Portable content should not depend on one agent's private metadata or installation path. Agent-specific integration belongs under `adapters/`.

Before a skill is considered ready:

1. its frontmatter and structure validate;
2. its instructions are reviewed for scope and unintended permissions;
3. its provenance is recorded when it originated elsewhere; and
4. important behaviour is tested with realistic evaluation cases.
