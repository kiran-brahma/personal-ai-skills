# Contributions and updates

## Adding a skill

Before adding a skill, document the reusable problem it solves and why an existing skill or project rules document is insufficient.

New skills begin as `trial` entries in `registry.yaml` when they need evaluation. They become `active` only after their intended behaviour and scope have been checked.

## Updating a skill

Update the canonical skill in the repository, record the change in the changelog, and commit it before expecting agents to consume it as the latest version.

For adapted external skills, compare upstream changes with the local skill and local intent. Adopt only changes that remain appropriate for this repository.

### Taking a raincheck on upstream

```bash
bin/skills-sync upstream
```

This compares every vendored skill against the commit `registry.yaml` pins for its source, and reports four things:

- **changed upstream** — what the original author has altered since the pin.
- **CONFLICT** — an upstream change to a file you have also edited locally. These are the ones that need a decision rather than a copy: adopting upstream wholesale would discard a local adaptation.
- **locally edited** / **not vendored by choice** — your existing divergence, separating deliberate edits from files never taken (an agent-specific manifest, say). Knowing which is which is what makes the conflict list readable.
- **upstream has N not vendored** — skills the author has added that this library does not carry. Selective adoption is a recorded adaptation for some packages, so a long list here is expected, not a backlog.

A skill derived from an upstream *method* rather than copied from an upstream directory has nothing to diff, and is reported as such. Those need a human read of the source.

The command never edits a skill. Adoption is the sequence this repository already requires: read the upstream change, decide what survives contact with the local adaptation, edit the canonical skill, re-run the relevant evaluation cases, and record the behavioural change in the changelog. Only then record the new commit:

```bash
bin/skills-sync upstream --pin <source-id>
```

Pinning is a claim that the comparison was made and resolved. Moving the pin without doing the work silently converts an unreviewed upstream change into an adopted one.

## Avoiding variants

Do not create separate copies for Claude, Codex, Pi, or individual projects merely because their setup differs. Keep one portable skill and add a thin adapter or project rules document when integration or context differs.

Create a separate skill only when the task, trigger conditions, or required behaviour is genuinely different.
