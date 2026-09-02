# Contributions and updates

## Adding a skill

Before adding a skill, document the reusable problem it solves and why an existing skill or project rules document is insufficient.

New skills begin as `trial` entries in `registry.yaml` when they need evaluation. They become `active` only after their intended behaviour and scope have been checked.

## Updating a skill

Update the canonical skill in the repository, record the change in the changelog, and commit it before expecting agents to consume it as the latest version.

For adapted external skills, compare upstream changes with the local skill and local intent. Adopt only changes that remain appropriate for this repository.

## Avoiding variants

Do not create separate copies for Claude, Codex, Pi, or individual projects merely because their setup differs. Keep one portable skill and add a thin adapter or project rules document when integration or context differs.

Create a separate skill only when the task, trigger conditions, or required behaviour is genuinely different.
