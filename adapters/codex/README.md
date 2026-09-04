# Codex adapter

Codex discovers portable skills from its configured skill directories. In Codex CLI and the IDE extension, use `/skills` to open the selector or explicitly mention a skill as `$skill-name`.

The canonical skills under `skills/` must remain portable and must satisfy the common Agent Skills format. Add host-specific presentation or dependency metadata here if it becomes necessary; do not fork the skill instructions.

## Installing

```bash
bin/skills-sync refresh
```

This links each skill into `~/.agents/skills`, the cross-harness Agent Skills location that Codex reads. It is a live path: an edit is visible to the next Codex session with no reinstall, no cache copy, and no version bump. Restart Codex to pick up changes.

Pi reads this directory as well as its own agent directory, and deduplicates by real path, so the overlap is harmless.

For a machine that only consumes the library, `bin/skills-sync bootstrap --role consumer` installs the plugin from the marketplace instead, so it tracks published releases rather than the working tree. **Do not use both routes on one machine**: Codex would carry every skill twice, once namespaced by the plugin and once bare. `bin/skills-sync doctor` warns when both are present.

## Codex behaviours that shape this repository

- **Codex recurses to any depth** and does not stop at a parent `SKILL.md`. The flat layout in `policies/skill-format.md` is required by Claude Code and Pi, not by Codex. Verified against depths one through five, and against a skill nested beneath a directory that carries its own `SKILL.md`.
- **Symlinks do not survive a plugin install.** `codex plugin add` copies the plugin into `~/.codex/plugins/cache/`, and symlinked skill directories are dropped from that copy with no error. This is why the plugin route needs real directories, and why the live route links directly into a skills directory instead.
- **`marketplace upgrade` only refreshes Git marketplaces.** For a local checkout it is a no-op, so the plugin route updates only when the version in `.codex-plugin/plugin.json` changes. The live route has no such constraint.
- **Descriptions share a fixed budget.** Codex loads every skill description and silently shortens them once the budget is exceeded, degrading routing with no error. It ignores `disable-model-invocation`, so gated skills are charged too. `policies/skill-format.md` sets the per-skill and library limits.

The marketplace manifest lives at `.claude-plugin/marketplace.json`. Codex reads that path as well as its own, so one catalogue serves both agents; only the plugin manifests differ.
