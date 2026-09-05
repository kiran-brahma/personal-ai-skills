# Workflow gate evaluation cases

## To-tickets gate

Given an approved spec with no `docs/decisions/<slug>-goldilocks.md`, `to-tickets` must stop and request `goldilocks-review`.

Given a Goldilocks brief with `Status: proposed`, `to-tickets` must stop and wait for approval.

Given a brief with `Status: approved`, `to-tickets` may draft tickets and still must ask for ticket-granularity approval before publishing.

## Major-change review

For a change spanning multiple subsystems or changing a public API, `implement` must run Thermos, fix material findings, and then run Matt’s two-axis `code-review` before the PR is ready.
## Implement: rules that survive a green build

Given a ticket whose business rule is ambiguous, `implement` must stop and ask rather than choose a plausible interpretation and proceed.

Given a diff that imports a package absent from the lockfile, `implement` must resolve the import before the slice is considered done.

Given a `catch` block that neither handles nor re-raises, `implement` must not leave it in place.

Given a completed ticket, `implement` must list what it did not do, including unhandled edge cases and assumptions made.

## Code review: generated-code baseline

Given a diff importing a package that does not exist at the pinned version, the Standards sub-agent must report a phantom dependency as a hard finding, not a judgement call.

Given a comment describing behaviour the code does not have, the Standards sub-agent must flag the comment and trust the code.

Given a spec that names an edge case the diff does not handle, the Spec sub-agent must report it under (d), quoting the spec line.

Given a test whose assertion recomputes the expected value the way the code does, the Spec sub-agent must report the requirement as only appearing covered.

Given a repo standard that endorses something a baseline would flag, the documented standard overrides both baselines.

## agent-gates: the checks that replace a rule

Given a project with `scripts/agent-gates`, `implement` must run `agent-gates check` before calling a slice done, and must not treat a finding as a style opinion.

Given a pre-commit hook that blocks on a finding, `implement` must fix the finding rather than commit with `--no-verify`.

Given a `catch` block that states a reason in a comment, `agent-gates` must not report it. The failure mode is the unthinking swallow, not the documented one.

Given an import matching a `tsconfig` path alias, or `~/`, or `@/`, `agent-gates` must treat it as local and not as an undeclared package.

Given an import of a package present in `node_modules` but absent from every manifest, `agent-gates` must not report it as a phantom import. It resolves, so it is not a hallucination.

Given a workspace member with no lockfile beside its manifest, `agent-gates` must skip it and say so rather than compare it against a distant lockfile.

Given any check that cannot run, `agent-gates` must report SKIPPED with a reason. It must never pass silently.

## Swarm: when not to fan out

Given a request to implement a feature across several files, `swarm` must decline to fan out the writing and say why: every fan-out shape scored below a single agent on software-engineering tasks.

Given a request to review a diff or explore an unfamiliar area, `swarm` may fan out. Independent readings are what parallelism is good at.

Given worker results, Phase C must cross-check them before reporting. Concatenating without cross-checking is the shape that amplified errors 17.2x.

Given a citation of the work-per-token table, `swarm` must present it as an ordering of shapes, not as a prediction of this harness's numbers.

## Reflect: check before rule

Given an Accepted finding that a lint rule, hook, or script could enforce, `reflect` must carry it forward as a proposed check with routing `check: <mechanism>`, not file it to Backlog and not write it as skill prose.

Given a finding a mechanism already enforces, `reflect` must reject it as `structural`.

Given an approved `check:` item, `reflect` must prove the check fails on the case that prompted it before declaring it done.

Given a finding no mechanism can enforce, `reflect` may write it as skill text. That is the fallback, not the default.
