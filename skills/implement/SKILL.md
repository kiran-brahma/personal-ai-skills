---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

Use /tdd where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, if this is a major change, use `thermos` first. Fix its material findings and repeat the relevant verification. Then use `code-review` to review the work. Every pull request must complete `code-review` before it is ready.

Commit your work to the current branch.
