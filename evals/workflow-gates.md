# Workflow gate evaluation cases

## To-tickets gate

Given an approved spec with no `docs/decisions/<slug>-goldilocks.md`, `to-tickets` must stop and request `goldilocks-review`.

Given a Goldilocks brief with `Status: proposed`, `to-tickets` must stop and wait for approval.

Given a brief with `Status: approved`, `to-tickets` may draft tickets and still must ask for ticket-granularity approval before publishing.

## Major-change review

For a change spanning multiple subsystems or changing a public API, `implement` must run Thermos, fix material findings, and then run Matt’s two-axis `code-review` before the PR is ready.
