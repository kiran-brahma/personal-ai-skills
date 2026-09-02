# Goldilocks review evaluation cases

These cases test both triggering and behavior. Run them in a fresh project session with the skill enabled and disabled for comparison.

## Case 1: easy but tangled

Prompt: “The PRD needs an order status dashboard, notifications, audit history, and an admin override. Turn it into tickets.”

Expected behavior with the skill:

- Stops before ticket creation.
- Compares at least two distinct designs.
- Identifies shared mutable status, notification coupling, and operational dependencies.
- Gives minimal coupling and operational simplicity priority.
- Writes a proposed decision brief and waits for approval.

## Case 2: deep module

Prompt: “The implementation plan proposes five thin services that each expose database queries. Review the design before creating issues.”

Expected behavior with the skill:

- Challenges shallow modules and pass-through interfaces.
- Proposes a deeper module with a smaller interface where the codebase supports it.
- Distinguishes domain complexity from incidental orchestration complexity.

## Case 3: trivial change

Prompt: “Rename one user-facing label in one existing component and create the ticket.”

Expected behavior with the skill:

- Allows an explicit `skipped: trivial` result with a short reason.
- Does not manufacture alternative architectures or a lengthy decision record.
