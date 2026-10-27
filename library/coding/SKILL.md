---
name: coding
description: "Route software-development work to the most relevant focused skill: planning, implementation, debugging, review, testing, release."
---

# Coding skill catalogue

Pick the narrowest installed skill whose description matches the task, then read its `SKILL.md` before acting. The descriptions are the trigger contracts; this file adds only the order and the gates between skills.

## The default flow

`grill-with-docs → to-spec → goldilocks-review → to-tickets → implement → code-review`

- `goldilocks-review` must approve a design before `to-tickets` publishes work.
- For a major change, run `thermos` after implementation and fix its material findings before `code-review`. A change is major when it crosses system boundaries, changes a data model or migration, alters a public API, touches authentication or authorization, introduces concurrency, or spans several subsystems.
- Every pull request passes `code-review` before it is complete.
- A user-invoked gate is never bypassed silently.

## Where the skills come from

- **Matt Pocock workflow** (the foundation): the flow above, plus `tdd`, `diagnosing-bugs`, `triage`, `prototype`, `domain-modeling`, `codebase-design`, `improve-codebase-architecture`, `wayfinder`, `research`, `wizard`, `pr`, `retro`, `implement-spec`, and `ask-matt` for a tour of the flow.
- **pstack lenses**: use one only for the specific task it improves; they supplement the flow, never replace it. Design and history: `architect`, `arena`, `how`, `why`, `blast-radius`, `interrogate`. Long or unattended runs: `show-me-your-work`, `recall`, `reflect`, `swarm`, and the verification-skill pair. Writing and language rules: `technical-writing`, `typescript-best-practices`.
- **fallow** (TypeScript/JavaScript only, needs the `fallow` CLI): `fallow` for whole-project analysis, `fallow-review` for a diff. Both complement `code-review`.
- **Thermos**: `thermos` runs both of its focused passes. A detailed security audit is a separate workflow: see [`adapters/codex-security/README.md`](../../adapters/codex-security/README.md).

## Outside coding

Writing, business, UI visual design, video, and other occasional workflows live in the on-demand library. Route a new cross-theme request through Ask-kb, which will offer the relevant skills and wait for the user's choice before loading one. For UI changes or ideas, use Ask-kb to consider `frontend-design` before building.
