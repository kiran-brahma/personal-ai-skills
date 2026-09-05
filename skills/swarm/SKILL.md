---
name: swarm
description: "Fan out N parallel workers, drain them, and return one report. Use for /swarm, 'swarm this', or parallel coverage, races, gauntlets, and exploration."
disable-model-invocation: true
---

# Swarm

**Portability note.** This skill was adapted from pstack. If the text below names Cursor-only paths, tools, transcript locations, or model slugs, translate them to the current harness and project layout. Do not read unrelated workspaces or private transcripts; if an equivalent capability is unavailable, state the limitation and continue with the safest supported alternative.

Fan out N parallel cloud workers. They may cover separate slices, race the same brief, or mix both. The parent waits, aggregates, and returns one report.

## Before you fan out

Fanning out is not free, and it is paid for in the budget a rate-limited window makes scarce. Measured across 260 controlled configurations (Kim et al., *Towards a Science of Scaling Agent Systems*, arXiv 2512.08296):

| Shape | Work per 1K tokens | Error amplification |
|---|---|---|
| One agent | 67.7 | 1.0x |
| Fan out, results concatenated | 42.4 | 17.2x |
| Fan out, peer cross-check | 23.9 | 7.8x |
| Fan out, orchestrator cross-check | 21.5 | 4.4x |
| Orchestrator plus peer messaging | 13.6 | 5.1x |

Two rules follow:

- **Do not fan out to write code.** On software-engineering tasks every fan-out shape scored below a single agent. Coordination fragments the token budget, and tool-heavy sequential work is where that costs most. Use one agent.
- **Do fan out to review, explore, or race.** Independent readings of one thing are what parallelism is genuinely good at, and different models find different faults. That is this skill's real use.

**Aggregation is what earns the cost.** Concatenating worker output without cross-checking it amplified errors 17.2x, the worst of every shape measured, because nothing intercepts a mistake before it reaches the result. Phase C is not a formatting step; it is the check that makes the fan-out worth running.

**Read the table as an ordering, not a prediction.** That study matched total token budget across shapes, so each worker in a fan-out held a fraction of what the single agent had. Workers here get their own budget, so the real penalty is smaller. The ranking holds; the figures do not transfer.

## Start

Open a todolist with one entry per phase before launching anything.

1. Frame
2. Fan out
3. Aggregate
4. Report

## Phase A: Frame

1. State the done predicate and the artifact or report the swarm must return.
2. Choose the shape. Partition into slices, race N workers on identical briefs, or mix both. For a race or mixed shape, declare `first pass`, `rank all`, or `best-of` before spawning.
3. Set N from the user or derive it from the shape. N is total workers, not the cloud concurrency limit.
4. Pick the worker model from `swarm workers` in `the current harness's model configuration` when present. Otherwise use `a fast exploration model`. For a model race, name each arm's model up front.
5. Give each worker its own writable output when it writes. Use a worktree, branch, or `/tmp/swarm-<slug>/worker-<n>/`.

## Phase B: Fan out

Spawn all N workers in one message with `subagent_type: generalPurpose`, `environment: "cloud"`, `run_in_background: true`, and the configured model. Use `environment: "local"` only when the worker needs access to something on the user's computer.

When a worker must start from a non-default pushed branch, pass `cloud_base_branch`.

Every brief stands alone. Include the goal, scope, exact slice or race arm, how to verify, and what to report. Reports use `PASS`, `ISSUES`, or `BLOCKED` with evidence.

If a worker drops out, proceed with N-1 and note it.

## Phase C: Aggregate

Read the terminal results. For coverage, every required slice needs a result. For a race, apply the selection rule declared up front. Use first pass, rank all, or best-of. Do not paste raw worker dumps.

Keep a compact result table, one-line evidenced issues, and explicit gaps or dropouts.

## Phase D: Report

Return one consolidated in-chat report with the table, issue one-liners, gaps or dropouts, and the race rule when used.
