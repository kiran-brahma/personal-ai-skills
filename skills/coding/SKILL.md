---
name: coding
description: Route software-development work to the most relevant focused skill in this category, including planning, implementation, debugging, review, testing, and release work.
---

# Coding skill catalogue

Read this file when `SKILLS.md` identifies coding as the relevant category. Select the narrowest specific skill that matches the task, then read that skill's `SKILL.md` before acting.

## Foundation: Matt Pocock workflow

Use these skills for the default engineering flow. The main path is:

`grill-with-docs → to-spec → goldilocks-review → to-tickets → implement → code-review`

For a major change, run `thermos` after implementation, fix its findings, and then run `code-review`. Every pull request must pass `code-review` before it is considered complete.

The Matt skills are deliberately kept as separate, focused skills. Select the narrowest one rather than loading the whole set.

Engineering skills live under [`matt/engineering`](../../packages/matt-pocock-skills/README.md), including `ask-matt`, `grill-with-docs`, `to-spec`, `to-tickets`, `implement`, `code-review`, `tdd`, `domain-modeling`, `codebase-design`, `diagnosing-bugs`, `triage`, `wayfinder`, `prototype`, `research`, `wizard`, and merge-conflict handling.

The supporting productivity skills live under [`../misc/matt/productivity`](../../packages/matt-pocock-productivity/README.md), including `grilling`, `grill-me`, `handoff`, `teach`, `to-questionnaire`, `wait-what`, and `writing-for-agents`.

## Supporting skills: pstack

Use pstack skills only for the specific task they improve. They supplement the Matt workflow; they do not replace it.

- `architect`: sketch module shapes and interfaces before implementation when the design is uncertain.
- `how`: trace a subsystem or behavior through real code before making a change.
- `why`: recover the rationale and history behind an existing design.
- `blast-radius`: prove what a proposed change can affect before editing.
- `arena`: compare structurally different candidate designs.
- `interrogate`: apply adversarial pressure to a design or implementation before committing to it.
- `show-me-your-work`: maintain an auditable decision trail for long-running or unattended work.
- `create-verification-skill` and `maintain-verification-skill`: create or maintain a project-local, user-path verification skill and feature map.
- `technical-writing`: apply the stricter technical-writing rules to docs, RFCs, issues, and review text.
- `typescript-best-practices`: apply the pstack TypeScript rules when editing TypeScript; use alongside, not instead of, the project’s own standards.
- `recall`: reconstruct recent project context when resuming work.
- `reflect`: turn durable lessons from a completed run into a concrete skill improvement.
- `swarm`: fan out independent exploration or review work and aggregate the results.

Do not import or activate pstack’s Cursor-specific orchestration (`poteto-mode`, `setup-pstack`, `make-bot-ui`, or `automate-me`) as canonical portable skills without a separate adaptation decision.

## Major-change review: Thermos

Use `thermos` when a change crosses system boundaries, changes a data model or migration, alters a public API, touches authentication or authorization, introduces concurrency, or spans multiple subsystems. Thermos runs the deep correctness/security/devex pass and the strict maintainability pass. Fix material findings before running Matt’s `code-review`.

`thermo-nuclear-review` and `thermo-nuclear-code-quality-review` are the two focused passes behind `thermos`. A detailed security audit is a separate workflow and should use the external Codex Security package documented in [`adapters/codex-security/README.md`](../../adapters/codex-security/README.md).

## Portability rule

The canonical `SKILL.md` files use skill names, not a particular harness’s command syntax. Translate explicit invocation through the relevant adapter: Claude Code uses `/skill-name`, Codex uses `$skill-name`, and Pi uses `/skill:name`. A skill may be model-invoked or user-invoked according to its frontmatter; user-invoked gates must not be silently bypassed.
