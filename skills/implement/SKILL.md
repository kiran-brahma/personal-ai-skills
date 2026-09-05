---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

# Implement

Implement the work described by the user in the spec or tickets.

## Before you write code

State which ticket you are implementing and which user stories it covers. If the ticket leaves a business rule ambiguous, stop and ask. A guessed business rule produces code that compiles, passes review, and is wrong, which is the most expensive failure to find later.

## The loop

Work in vertical slices, one at a time. Use `tdd` where possible, at pre-agreed seams. Do not write all the code first and the tests after: bulk implementation commits you to a shape before any of it has been exercised.

Run typechecking regularly and single test files regularly. Run the full test suite once at the end.

## Rules that hold on every slice

These failure modes survive a clean typecheck and a passing test run, so nothing earlier in the chain catches them:

- **Every import resolves.** The package exists, and at the version the lockfile pins. Check it. A plausible package name is not evidence that the package is real.
- **No silent catch.** Every `catch` either handles the failure, re-raises it, or states in a comment why the failure is ignored. A block that silently swallows an error hides the cause and moves the symptom somewhere unrelated.

If the project has `scripts/agent-gates`, run `scripts/agent-gates check` before you call a slice done. It checks both rules above, plus lockfile drift, and it is not a judgement call: a finding is a fact about the code. Where the project has no such script, the rules still hold and you verify them yourself.

A pre-commit hook may run the same checks. If it blocks a commit, fix the finding. Never reach for `--no-verify`.

## When you finish

List what you did not do: parts of the ticket left undone, edge cases not handled, and any assumption you made. An unstated assumption is the part a reviewer cannot check.

Once done, if this is a major change, use `thermos` first. Fix its material findings and repeat the relevant verification. Then use `code-review` to review the work. Every pull request must complete `code-review` before it is ready.

Commit your work to the current branch.
