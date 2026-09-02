---
name: continual-learning
description: Review completed work for durable user preferences and workspace facts, then propose a small evidence-backed update to AGENTS.md or CLAUDE.md. Use for governance maintenance or when the user asks what the agents should learn from recent work.
disable-model-invocation: true
---

# Continual learning

Turn repeated, high-signal lessons into proposed updates to the project’s agent instructions. This is proposal-first governance, not automatic memory mutation.

## Scope

Read only the current project’s available work history: the current conversation, explicit user corrections, committed decisions, review findings, and project artifacts. If the harness exposes session transcripts, use only the active project’s transcript directory. Never scan unrelated projects or personal history.

Look for durable patterns in two buckets:

- **Learned user preferences:** stable preferences about communication, implementation trade-offs, review standards, or workflow.
- **Learned workspace facts:** stable facts about the repository, commands, architecture, release process, or operational constraints.

Ignore secrets, credentials, personal data, transient task details, one-off frustrations, unverified assumptions, and facts that belong in a normal project document rather than agent instructions.

## Process

1. Collect candidate lessons and cite the exact conversation, review, commit, or file evidence for each.
2. Deduplicate against the current `AGENTS.md`, `CLAUDE.md`, and relevant project rules.
3. Test each candidate: is it durable, actionable, specific, and likely to improve future agent decisions? If not, discard it.
4. Keep the proposal small. Prefer a few high-signal bullets over a history dump. Do not exceed 12 learned-preference bullets or 12 learned-fact bullets in the target document.
5. Propose the smallest patch and explain why the target file is the correct home. Project-specific facts belong in the project’s rules; reusable workflow instructions belong in a skill; domain facts belong in project documentation.
6. Show the proposed diff and evidence to the user. Do not edit `AGENTS.md`, `CLAUDE.md`, or any other instruction file until the user approves the proposal.
7. After approval, apply only the approved patch, re-read the result, and report what changed and what evidence supports it.

## Output

Return:

- `No high-signal memory updates.` when nothing durable was found; or
- a proposal containing the target file, proposed bullets, evidence, rejected candidates, and the exact approval needed before editing.

Automatic stop hooks, transcript indexes, and harness-specific updater agents are adapters, not part of this portable skill. Add them only after a separate privacy and permissions review.
