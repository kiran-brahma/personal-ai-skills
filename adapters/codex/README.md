# Codex adapter

Codex discovers portable skills from its configured skill directories. In Codex CLI and the IDE extension, use `/skills` to open the selector or explicitly mention a skill as `$skill-name`.

The canonical skills in this repository do not depend on `agents/openai.yaml`, private model slugs, or Codex-only tool metadata. Add host-specific presentation or dependency metadata here if it becomes necessary; do not fork the skill instructions.

For a project-local setup, make the repository’s `.agents/skills` directory available to Codex, or link the canonical skill directories through the user-level skills location. Codex reloads or restarts may be needed after installation changes.
