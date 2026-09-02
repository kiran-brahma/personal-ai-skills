# Personal Agent Skills

A public, version-controlled library of reusable skills for AI agents used for coding, writing, research, and miscellaneous work.

## Repository model

This repository is the canonical source for the skills it contains. Agents should use the committed version from GitHub rather than a manually copied local variant.

The repository contains one maintained version of each skill. Project-specific rules are supplied separately by the project that is being worked on; they are not duplicated as skill variants.

The root instruction files use the conventional uppercase names `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md`. `AGENTS.md` is canonical; the other two are entrypoints that refer to it. Lowercase duplicates are deliberately avoided because they can conflict with uppercase filenames on case-insensitive filesystems.

## Layout

```text
skills/
├── AGENTS.md       Canonical control document for this repository
├── CLAUDE.md       Claude entrypoint; refers to AGENTS.md
├── GEMINI.md       Gemini entrypoint; refers to AGENTS.md
├── SKILLS.md       Top-level category catalogue and routing guide
├── policies/       Repository rules and decision records
├── skills/         Category routers and portable skills
│   ├── coding/
│   │   ├── SKILL.md  Category router
│   │   └── <skill-name>/SKILL.md
│   ├── writing/
│   ├── misc/
│   └── governance/
├── adapters/       Agent-specific discovery and installation details
│   ├── claude/
│   ├── codex/
│   ├── pi/
│   └── codex-security/
├── evals/          Behavioural test cases for skills
├── registry.yaml   Skill inventory and provenance metadata
├── THIRD_PARTY.md   Notices for adapted external skills
└── CHANGELOG.md    Human-readable repository history
```

## Guiding principles

1. Keep the portable skill itself compatible with the common Agent Skills format.
2. Keep agent-specific setup in `adapters/`, not inside the portable skill instructions.
3. Add a skill only when it provides reusable guidance that changes agent behaviour.
4. Treat upstream updates as inputs for review, not automatic replacements.
5. Prefer one canonical skill with configurable project context over multiple near-duplicates.
6. Validate important skills with realistic behaviour-based evaluations.
7. Before activating a new skill, understand its workflow and discuss required adaptations with the repository owner.

## Status

The first trial set contains Matt Pocock’s engineering/productivity workflow, selected pstack supporting skills, the Goldilocks design gate, and the Thermos major-change review. Provenance and local adaptations are recorded in [`registry.yaml`](registry.yaml); trial skills become active after their evaluations and behavior have been checked.
