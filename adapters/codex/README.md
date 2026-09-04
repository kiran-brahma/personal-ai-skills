# Codex adapter

Codex discovers portable skills from its configured skill directories. In Codex CLI and the IDE extension, use `/skills` to open the selector or explicitly mention a skill as `$skill-name`.

The canonical skills in this repository do not depend on `agents/openai.yaml`, private model slugs, or Codex-only tool metadata. Add host-specific presentation or dependency metadata here if it becomes necessary; do not fork the skill instructions.

Codex installs skills through a plugin marketplace. From a clone:

```bash
codex plugin marketplace add "$PWD"
codex plugin add kb@kb-skills
```

Afterwards `bin/skills-sync refresh` keeps it current. Codex restarts are needed after installation changes.

Three Codex behaviours shape how this repository is packaged:

- **Symlinks do not survive.** `codex plugin add` copies the plugin into `~/.codex/plugins/cache/`, and symlinked skill directories are dropped from that copy with no error. Skill directories must be real, which `bin/skills-sync validate` enforces.
- **`marketplace upgrade` only refreshes Git marketplaces.** For a local checkout it is a no-op. Updates come from `codex plugin add`, which re-reads the marketplace and installs the version named in `.codex-plugin/plugin.json`, replacing the previous cache entry. This is why the version is derived rather than hand-edited: an unchanged version means an unchanged install.
- **Descriptions share a fixed budget.** Codex loads every skill description and silently shortens them once the budget is exceeded, degrading routing with no error. It ignores `disable-model-invocation`, so gated skills are charged too. `policies/skill-format.md` sets the per-skill and library limits.

The marketplace manifest lives at `.claude-plugin/marketplace.json`. Codex reads that path as well as its own, so one catalogue serves both agents; only the plugin manifests differ.
