# Agentic engineering adoption

**Status:** in progress
**Scope:** coding skills only
**Started:** 2026-09-05

This is the working record for a multi-session effort. Read it before continuing the work. It holds the reasoning, the decisions, and the state, so a fresh session does not need the originating conversation.

## Why this exists

Four documents were reviewed for ideas worth adopting into the coding skills:

1. *The New SDLC With Vibe Coding* (Osmani, Saboo, Kartakis; Google, May 2026)
2. *Towards a Science of Scaling Agent Systems* (Kim et al.; Google Research / DeepMind / MIT, arXiv 2512.08296v3)
3. [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) (Anthropic)
4. [Agentic Engineering: A Practitioner's Playbook](https://domino.ai/blog/agentic-engineering-practitioners-playbook) (Domino)

## Owner context that drove every decision

These constraints are not visible from the code. They decide which suggestions apply.

- The owner is a business owner, not a developer. He cannot read a diff and recognise a bad pattern. Every source document assumes a human reviewer who can. That reviewer does not exist here.
- He runs top-tier models for grilling, spec, and design; mid-tier models for implementation. This yields 3-4x more work inside a provider's 5-hour window. The allocation works and is not to be changed.
- Stated ethos: AI is probabilistic, so the system around it must be made deterministic.
- He is not a vibe coder. He will spend one to two hours to avoid repeating work, and prefers simple long-term solutions over quick fixes.
- Current setup is the Matt Pocock chain plus `thermos` for major changes. It resolves about 90% of issues. The remaining 10% have so far been minor bugs he fixed himself. He accepts that residual risk knowingly.

## Vocabulary

Used consistently in this document and in the skills it changes.

- **Check** — code that runs and either passes or fails. Deterministic.
- **Rule** — text an agent reads and may or may not follow. Probabilistic.
- **Gate** — a point where a check must pass before work continues.

The organising principle for the whole effort: **move work from rules to checks wherever a check is possible.**

## The gap this effort targets

The chain is `grill-with-docs → to-spec → goldilocks-review → to-tickets → implement → code-review`.

Four of those skills are long and specific. `implement` was fifteen lines. Three facts meet at that point:

1. `implement` gave the least instruction of any skill in the chain.
2. A mid-tier model runs that step.
3. The owner cannot audit its output.

The unresolved 10% is most likely produced there. The fix is not a larger model at implementation; the allocation is sound. The fix is a more specific `implement` skill and harder checks after it.

## Design decision (Goldilocks)

`Status: approved`. Recorded here rather than in a separate brief because the design question was small and was settled during analysis.

**Problem:** the chain has no defence against the class of error that survives a clean typecheck and a passing test run, and no human who can catch it by reading.

**Shapes considered:**

1. *A new skill for AI-error review.* Rejected. The library has 70 skills. A 71st competes for routing attention with `code-review`, which already owns this job and already has the machinery (labelled heuristics, repo-overrides-baseline, skip-what-tooling-enforces).
2. *One long prose checklist in `code-review`.* Rejected as the sole shape. Detection alone leaves the error already written, and a prose list read by a model is a rule, not a check.
3. *Split by where the error is cheapest to stop.* **Chosen.** Prevention rules go into `implement`, where the error would be written. Detection rules go into `code-review`, split across the axis that owns each question. The mechanical half becomes a real check later (ticket 3).

**Why:** each rule lands where it costs least and where an existing skill already owns the surrounding job. No new routing surface.

**Rejected additions (scope discipline):** "no invented interface" (hallucinated API calls) was drafted into `implement` and removed. It is a real failure mode and a good candidate for a later ticket, but it was not in the approved plan. Adding it silently would be the scope creep `code-review`'s Spec axis exists to catch.

## Tickets

| # | Ticket | Phase | Status |
|---|--------|-------|--------|
| 1 | Make `implement` specific | 1 | done |
| 2 | Add generated-code baseline to `code-review` | 1 | done |
| 3 | Check script and pre-commit gate for the owner's projects | 2 | done |
| 4 | Link tests to user story numbers | 2 | **pending** — start it on the next spec |
| 5 | Add fan-out cost rule to `swarm` | 3 | done |
| 6 | Make `reflect` prefer checks over rules | 3 | done |
| 7 | Add graduation rule to `prototype` | 3 | closed, already covered |
| 8 | Fix the `encode-lessons-in-structure` dangling reference in two remaining files | — | not started |

### Ticket 1 — Make `implement` specific

Six rules, approved. State the ticket and its user stories before coding. Work one vertical slice at a time. Every import resolves against the lockfile. Every `catch` handles or re-raises. Stop and ask on an unclear business rule rather than guessing. List what was not done at the end.

### Ticket 2 — Add generated-code baseline to `code-review`

Five rules, approved, split across the two axes. Standards gets phantom dependency, silent catch, lying comment. Spec gets unhandled named edge case, and tautological test.

### Ticket 3 — Check script and pre-commit gate

Delivered as [`bin/agent-gates`](../../bin/agent-gates): one self-contained stdlib-only Python file with three subcommands, `check`, `install`, and `self-test`.

**Why a script and not a skill.** The description budget was the forcing constraint: the library sits at 8989 of 9000 bytes, so a new skill could not be added without trimming others. That constraint pointed at the right answer anyway. A skill is text a model reads, which makes it a rule. This ticket exists to produce a check. A script also removes the model from the generation step, so the artifact is the same every time.

**Three checks, not five.** The plan named five. Typecheck and tests were dropped from the gate: both are slow, and a slow hook gets bypassed, which costs more than it catches. They stay in `implement` as steps to run, not as hook gates. The three that remain are static, and a full-tree scan of a large project takes about one second.

- `phantom-import` — a bare import that no manifest declares and that does not resolve in `node_modules`.
- `lockfile-drift` — a declared dependency absent from the lockfile beside its manifest.
- `silent-catch` — a `catch` or `except` that neither handles, re-raises, nor states a reason.

**Deliberate narrowings, each one made after a false positive on real code.** A catch whose body is a comment is a documented decision, not an unthinking swallow, so it is allowed. An import that resolves in `node_modules` but is undeclared is a real fragility but a different finding, so it is not reported here. A workspace member with no lockfile beside it is skipped rather than compared against a distant one.

**`install` copies the script into the project** rather than referencing this repo, so a project keeps working after the library moves. It writes `scripts/agent-gates` and `.githooks/pre-commit` and sets `core.hooksPath`, matching the pattern already proven in this repository.

**`self-test` is the part that matters.** A check that never fires is worse than no check, because it manufactures confidence. `self-test` builds known-bad fixtures, proves each check fires, then builds a clean fixture and proves none fires. Every construct in the clean fixture once produced a false positive against a real project, so it doubles as a regression suite. Run it after any edit to the script.

**Measured against the owner's own repositories** during the build. Findings fell from 2305 to 6 on one project and 849 to 11 on another as false-positive classes were fixed: tsconfig path aliases, runtime schemes such as `cloudflare:` and `npm:`, generated build output, workspace manifests outside `packages/`, and a comment stripper that was not string-aware and silently ate whole files. The findings that remain were checked by hand and are true positives.

### Ticket 4 — Link tests to user story numbers

**Status: pending. Deliberately deferred, not forgotten.**

`to-spec` writes numbered user stories. Each test names the story number it covers, in a comment, not in the test name, so `tdd`'s rule that a test reads as a specification on its own terms still holds. Coverage then becomes a set difference the owner can read without reading code, which answers the question he is least equipped to answer alone: did the implementation cover what the spec asked for?

Touches `tdd` and `to-tickets`.

**Why it waits.** The convention only pays once several specs carry it, and retrofitting numbers onto existing tests would produce references that drift immediately. Starting it on real work costs nothing extra.

**Trigger:** the next time `to-spec` writes a spec. Do it then, before `to-tickets` runs, so the first set of tickets already carries story numbers.

**Known risk to handle when building it:** story numbers change when a spec is edited, and a stale number is worse than none. Decide at build time whether the reference points at a number or at a stable story slug.

### Ticket 5 — Fan-out cost rule for `swarm`

The scaling paper measured work per 1000 tokens by topology: one agent 67.7, fan-out without cross-check 42.4, orchestrator 21.5, orchestrator plus peer messaging 13.6. Do not fan out to write code. Do fan out to review code, where model diversity partly substitutes for the human reviewer this owner does not have.

Caveat to record in the skill: the paper matched total token budget across topologies, so some of the penalty is budget fragmentation that does not apply identically here. The ordering of the shapes holds; the exact numbers do not transfer.

### Ticket 6 — Make `reflect` prefer checks

`reflect` step 4 currently moves a finding to Backlog when a script would enforce it better. Invert the emphasis: a check is the first choice, a rule is the fallback when no check is possible.

### Ticket 7 — Graduation rule for `prototype`

**Closed without a change: `prototype` already says this.** Rule 1 is "throwaway from day one, and clearly marked as such." Rule 6 folds the validated *decision* into real code, commits the prototype itself to a throwaway branch off main, and states that "the main branch keeps only the validated decision." That is the graduation rule the Day 1 warning asks for, already written and better placed than a new rule would be.

Adding a second rule saying the same thing would have made the skill longer without making it clearer, which is the noise that degrades a skill. Recorded here so the ticket is not re-opened.

### Ticket 8 — Dangling `encode-lessons-in-structure` reference

`skills/reflect/SKILL.md` pointed at a principle skill named `encode-lessons-in-structure` that does not exist in this library. An agent following that pointer finds nothing. Fixed in `reflect` as part of ticket 6, because the reference sat in the exact sentence being rewritten, and leaving a known-dangling pointer in a rewritten line would be negligent.

Two files still carry it: `skills/show-me-your-work/SKILL.md` and `skills/architect/references/runner-prompt.md`. Both are outside Phase 3's scope, so they are logged rather than fixed. The fix is the same in each: state the principle inline instead of pointing at a skill that was never vendored. Do not create the skill; the description budget is full at 8989 of 9000 bytes.

## Declined, with reasons

Recorded so a later session does not re-propose them.

- **A separate evals discipline** (trajectory evaluation, LM judges, rubrics). Only earns its keep when the artifact being built is non-deterministic. The owner does not build LLM-in-the-loop products. `evals/` in this repo already means something else, so the word would collide.
- **A full verification skill.** Offered and not taken. Ticket 3 is its cheap half. The full version drives the app like a user.
- **Tool and ACI design guidance.** The owner does not build MCP servers or tool surfaces. He consumes one MCP that stores observations.
- **The Ralph loop.** Seven of its eight steps already exist in the chain. Its distinctive contribution, "5-10 critique iterations", is repetition standing in for confidence. `goldilocks-review` terminates on a structural test instead, which is the better shape.
- **A stakes gate at the front of the coding router.** Proposed, then withdrawn. It was designed as a sanctioned way to skip ceremony. The owner does not want the cheap lane and cannot safely use it. Only the graduation half survived, as ticket 7.
- **Conductor and orchestrator framing.** Vocabulary for a human reading a whitepaper. It changes no agent behaviour.
- **CapEx/OpEx economics.** A leadership argument. The actionable part is model routing, which the owner already does better than the source describes.

## Notes on the sources

State these when citing the material, so later work does not overclaim.

- The scaling paper's cross-validated R² is 0.373. Most individual coordination predictors were not significant. What is significant is the baseline paradox (β = −0.236, p = 0.004) and the tool-coordination trade-off (β = −0.096, p = 0.002). The 87% figure is architecture *ranking* accuracy on held-out configurations, which the authors distinguish from absolute prediction.
- Its multi-agent runs were matched for total token budget (mean 4,800 tokens per trial), so part of the measured penalty is budget fragmentation.
- *The New SDLC* is a Google whitepaper with a product path running through it. Its framework material is sound. Its generalisation from "building agents" to "all software engineering" should be held loosely.

## Session log

- **2026-09-05.** Read all four sources. Produced the analysis, then revised it against the owner context above. Agreed the plan. Completed tickets 1 and 2. Created this record.
  - One change outside the approved plan: `implement` said `/tdd`, which breaks the portability rule in `skills/coding/SKILL.md` (canonical files name skills, they do not use one harness's command syntax). Corrected to `tdd` in a line already being rewritten. Disclosed rather than folded in silently.
  - Evaluation cases for both tickets added to `evals/workflow-gates.md`.
- **2026-09-05, later.** Built ticket 3 as `bin/agent-gates`. Wired `implement` to it. Added its evaluation cases. Not yet installed into any of the owner's projects; that is a per-project command he runs.
  - Open question for a later session: `implement` still carries "every import resolves" and "no silent catch" as prose rules, and `agent-gates` now checks both. The prose is the fallback for projects without the script. Revisit whether it should be trimmed once the script is installed everywhere.
- **2026-09-05, Phase 3.** Tickets 5 and 6 done. Ticket 7 closed as already covered. Ticket 8 opened from a dangling reference found while doing 6.
  - Ticket 6 needed a second edit that was not in the plan. `references/synthesizer.md` ran *before* step 4 and routed script-enforceable findings to Backlog, so inverting step 4 alone would have had no effect: the items were already gone by the time step 4 saw the list. The reference file, its routing table, step 5's routing list, and step 6's summary all had to move together, or the new `check:` route would have dead-ended.
  - Phase 2's ticket 4 (link tests to user story numbers) is still open. It was left because it only pays once several specs use it.
  - Candidate for a later ticket: a `no-invented-interface` check, for calls to functions or options that do not exist in the installed library. It is the same failure class as `phantom-import` and probably more common, but it needs resolution against installed type definitions rather than a manifest lookup, so it is a larger job than the three checks built here.
