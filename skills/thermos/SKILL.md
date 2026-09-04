---
name: thermos
description: Run the deep correctness/security/devex and maintainability reviews for a major code change, then synthesize prioritized findings before the normal code review.
disable-model-invocation: true
---

# Thermos

Use this gate for major changes: cross-system or cross-module work, data-model or migration changes, public API changes, authentication or authorization, concurrency, or changes spanning multiple subsystems.

1. Pin the review scope to the branch, PR, or changed files. Read the diff and the relevant spec without guessing beyond the change.
2. Run the `thermo-nuclear-review` and `thermo-nuclear-code-quality-review` passes in parallel when the harness supports parallel workers. Otherwise run them separately with the same fixed scope.
3. Synthesize findings by priority, keeping correctness/security/devex findings distinct from maintainability findings.
4. Fix all material findings and rerun the affected verification. Do not proceed to Matt’s `code-review` with unresolved material Thermos findings.

Thermos is a major-change review gate, not a substitute for the final two-axis spec-and-standards review. Detailed security audits use the external Codex Security workflow.
