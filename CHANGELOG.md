# Changelog

This file is an index. Detailed release notes live in one file per ISO month so agents can read the relevant month without loading the full project history.

## Latest release

[0.7.6 — 2026-10-22](changelog/2026-10.md#076--2026-10-22--upstream-refresh-hyperframes-on-demand-codex-duplicate-check)

## Monthly index

- [2026-10](changelog/2026-10.md): version `0.7.6`: upstream refresh (Matt Pocock `main`, fallow 1.4.41, pstack 0.15.30), HyperFrames removed in favour of on-demand use from GitHub, `doctor` stale-Codex-copy check; Matt Pocock skills 1.3.1 update (`GLOSSARY.md` rename, `implement-spec`, `pr`, `retro`, `resolving-merge-conflicts` removed) and pstack `correct` and `principle-test-behavior-not-implementation`.
- [2026-09](changelog/2026-09.md): versions `0.1.0`, `0.2.0`, `0.2.1`, `0.2.2`, `0.3.0`, `0.3.1`, `0.4.0`, `0.5.0`, `0.6.1`, `0.6.2`, `0.7.0`, `0.7.1`, `0.7.2`, `0.7.3`, `0.7.4`, and `0.7.5`, including the business blog post generator, the flat cross-agent layout, the decision gates and bias controls in `decision-navigator`, the transcript-to-prose writing skill, the two-tier library with per-machine setup, Google Antigravity support, the `close-reading` interrogator, and Anthropic's `frontend-design` skill. `0.6.0` was tagged without a changelog section; its contents are the two entries still marked Unreleased above it.

## Changelog format

Each release entry includes:

- the ISO date and semantic version;
- links to every added or changed skill;
- the local behavior change and its effect on future agent decisions;
- provenance, license, and upstream reference when the skill is adapted;
- related adapters, registry changes, and evaluation cases.

Create a new `changelog/YYYY-MM.md` file for the first release in each ISO month. Add the month to this index. Keep later releases in the same month in that month’s file.
