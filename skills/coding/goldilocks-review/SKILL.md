---
name: goldilocks-review
description: "Compare viable designs after a spec and before tickets, choosing the simplest architecture that preserves required behavior. Mandatory gate before to-tickets."
disable-model-invocation: true
---

# Goldilocks review

This is the design gate between an approved PRD/spec and implementation tickets. It protects the resulting system from solutions that are easy to generate but tangled to change.

## Gate

Do not create GitHub issues or local implementation tickets until this review is complete and the user has approved the chosen design. Trivial, isolated changes may be explicitly marked `skipped: trivial` with a one-sentence reason.

## Inputs

Read, in order:

1. The approved PRD or spec.
2. The project’s `CONTEXT.md`, relevant ADRs, and existing design documents.
3. The current code paths and operational configuration affected by the proposal.
4. Any prototype, research note, or issue discussion named by the PRD/spec.

Do not treat the speed of a previous AI-generated implementation as evidence that its design is simple.

## Review method

1. State the problem in one sentence without prescribing the mechanism.
2. Separate required complexity from incidental complexity. Required complexity comes from the domain or environment; incidental complexity comes from avoidable coupling, hidden state, indirection, or operational machinery.
3. Map the important data, rules, effects, state transitions, and operational dependencies.
4. Compare at least two materially different solution shapes unless the constraints prove only one viable shape exists. Include the smallest plausible solution, even when it seems less familiar.
5. Prefer deep modules: substantial behavior behind a small, stable interface at a clean seam. Count hidden connections and operational moving parts, not files or classes.
6. Give minimal coupling and operational simplicity priority over implementation speed, local convenience, and speculative flexibility.
7. Challenge mutable state. Keep facts immutable where possible, make state transitions explicit, and avoid making unrelated concerns depend on time-varying shared data.
8. Check that data, business rules, presentation, storage, and orchestration can change independently. More modules are acceptable when their interfaces are narrow and their assumptions are visible.
9. Trace the operational path: deploy, configure, observe, retry, recover, migrate, roll back, and support the change. Reject a design whose runtime behavior cannot be explained in a short sequence.
10. Apply the deletion test: identify abstractions, flags, queues, layers, and dependencies that disappear if the design is reframed. Prefer deleting incidental complexity over rearranging it.

Use `architect`, `how`, `why`, or `blast-radius` when the design cannot be evaluated from the current context. Use them as targeted supporting lenses, not as a ritual checklist.

## Output

Write `docs/decisions/<feature-slug>-goldilocks.md`, creating `docs/decisions/` when needed. The document must contain:

- **Status:** `proposed`, `approved`, `rejected`, or `skipped: trivial`.
- **Problem and constraints:** what must be true and what cannot change.
- **Required complexity:** domain and environmental complexity the design cannot remove.
- **Candidates:** at least two distinct shapes, each with coupling, operational, state, and change-cost notes.
- **Decision:** the selected shape and why it is in the Goldilocks zone.
- **Rejected alternatives:** why each was not chosen.
- **Interfaces and seams:** what each module owns and what it is allowed to know.
- **Operational path:** deploy, observe, recover, and rollback considerations.
- **Ticket boundaries:** the vertical slices that may safely become implementation tickets.
- **Open questions:** only questions that block approval or materially change the design.

Keep the document decision-focused. Do not turn it into an implementation plan or duplicate the PRD.

## Approval

Present the decision brief to the user. If the selected design or any open question is consequential, stop with `Status: proposed` and wait. After approval, update the document to `Status: approved`; only then may `to-tickets` publish work.

If the user rejects the design, record the rejection and reason, return to the affected constraint, and produce a revised comparison. Never silently move the rejected shape into tickets.
