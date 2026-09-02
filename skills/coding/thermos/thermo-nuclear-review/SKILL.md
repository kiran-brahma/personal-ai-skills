---
name: thermo-nuclear-review
description: Audit added or modified code for correctness, breakage, security, developer-experience regressions, and feature-gate leaks during a major-change review.
disable-model-invocation: true
---

# Thermo-nuclear review

Audit only code added or modified in the scoped diff. Trace callers and dependent behavior thoroughly enough to finish the research before reporting a finding.

Check for:

- incorrect behavior and regressions in existing flows;
- secrets, configuration, environment, networking, build, or migration changes that break developer experience;
- feature flags or internal-only behavior leaking to the wrong users;
- failure, retry, timeout, concurrency, and rollback behavior;
- mismatch with the originating PRD/spec.

Report only evidence-backed findings with priority, file/line references, impact, and a concrete fix. Do not report untouched existing vulnerabilities unless the change exposes or worsens them. If a PR discussion exists, inspect it only after completing the independent audit.
