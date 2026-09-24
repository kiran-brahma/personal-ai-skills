# Skill installation and freshness

Read this reference when installing or updating skills, diagnosing unexpected workflow behavior, or running HyperFrames setup in CI.

The upstream HyperFrames CLI installs the core set eagerly and workflow skills lazily. In
Kiran's canonical skill library, the selected package is already vendored and reviewed; do not
use the upstream updater to overwrite it.

- **Core set:** `/hyperframes`, the `hyperframes-*` domain skills, and `/media-use`.
- **Workflow skills:** installed by this repository's normal skill sync after review.

## What `init` does

`npx hyperframes init` checks GitHub and refreshes the core set plus other skills already installed. It does not install workflows that have never been used. A current install is a no-op. Offline or rate-limited checks degrade gracefully and do not fail project scaffolding.

The `--skip-skills` CLI flag is temporarily ignored. CI and tests may opt out with `HYPERFRAMES_SKIP_SKILLS=1`.

## Diagnose an upstream project install

```bash
npx hyperframes skills check
npx hyperframes skills check --json
npx hyperframes skills
```

- `skills check` exits non-zero when an installed skill is stale or the core set is incomplete. Workflows available on demand but not installed are not failures.
- The `skills update` commands describe the upstream HyperFrames project only; they are not an
  instruction to update this canonical library in place.
- Bare `skills` installs the full published set explicitly.

If the HyperFrames CLI is unavailable, use `npx skills add heygen-com/hyperframes --skill <workflow-name>` for one workflow or `npx skills add heygen-com/hyperframes --all` for the full published set.

The CLI may print a one-line stale-skill reminder during `render`, `lint`, or `check`. Treat a failed update as a visible tool failure; do not continue from a remembered workflow contract.
