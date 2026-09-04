# Pi adapter

Pi exposes a portable skill as `/skill:name` and accepts arguments after the command. Install with:

```bash
bin/skills-sync refresh
```

Pi loads skills from its agent directory, `~/.pi/agent/skills` unless `PI_AGENT_DIR` overrides it, and from `<cwd>/.pi/skills` for project scope. It follows symlinks, so `refresh` links each skill there exactly as it does for Claude Code.

`.agents/skills` is **not** a Pi load path, despite appearing in Pi's source: it occurs only in the trust logic, as a project resource that requires trust before it is honoured. The committed `.agents/skills` symlink in this repository is a generic integration point for agents that use that convention, as `.agents/README.md` describes. It does not make skills visible to Pi.

Pi honours `disable-model-invocation`, so gated skills are installed but do not appear in `available_skills` — verified: 26 of the 59 are listed, matching the count that is not gated. Codex does not honour it.

Pi's discovery differs from the other agents in one way that constrains the whole library: it recurses into subdirectories, but stops at the first `SKILL.md` it finds and does not look beneath it. A skill nested under another skill is therefore invisible to Pi. `bin/skills-sync validate` enforces the flat layout that keeps this from happening.

The canonical skills intentionally use standard `SKILL.md` frontmatter and relative references. Keep Pi-specific settings, extensions, model choices, and command aliases here rather than inside the shared skill.
