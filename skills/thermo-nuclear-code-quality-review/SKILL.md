---
name: thermo-nuclear-code-quality-review
description: Apply a strict maintainability and structural-simplicity review to the changed code in a major change, looking for deep modules, fewer concepts, and deletion opportunities.
disable-model-invocation: true
---

# Thermo-nuclear code-quality review

Review the changed code for structural regressions, not cosmetic preferences. Look for a code-judo move that deletes branches, wrappers, layers, shared state, or special cases while preserving behavior.

Prioritize:

- minimal coupling and narrow, deep interfaces;
- direct, boring code over magical or generic mechanisms;
- logic in its canonical layer;
- explicit type and state boundaries;
- no ad-hoc branching growth or unnecessary sequential orchestration;
- decomposition before a changed file crosses 1,000 lines;
- reuse of existing canonical helpers;
- fewer concepts for a reader to hold in mind.

Report a small set of high-conviction findings with evidence and a remedy. Do not approve merely because tests pass: tests provide safety at the edges, while this review checks whether the design remains understandable and changeable.
