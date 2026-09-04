# Pi adapter

Pi exposes a portable skill as `/skill:name` and accepts arguments after the command. Install with:

```bash
bin/skills-sync refresh
```

Pi loads skills from its agent directory, `~/.pi/agent/skills` unless `PI_AGENT_DIR` overrides it, and from `<cwd>/.pi/skills` for project scope. It follows symlinks, so `refresh` links each skill there exactly as it does for Claude Code.

Pi also reads the user-global `~/.agents/skills`, the cross-harness Agent Skills location that `refresh` populates for Codex, and deduplicates by real path. A skill present in both directories is listed once, so the overlap costs nothing. Pi's own source treats that directory as a trusted user resource; the project-local `.agents/skills` inside a repository is gated behind project trust instead, which is a separate mechanism and is not what this repository relies on.

Pi honours `disable-model-invocation`, so gated skills are installed but do not appear in `available_skills`. Verified: 26 of the 59 are listed, matching the count that is not gated. Codex does not honour it.

Pi's discovery differs from the other agents in one way that constrains the whole library: it recurses into subdirectories, but stops at the first `SKILL.md` it finds and does not look beneath it. A skill nested under another skill is therefore invisible to Pi. `bin/skills-sync validate` enforces the flat layout that keeps this from happening.

The canonical skills intentionally use standard `SKILL.md` frontmatter and relative references. Keep Pi-specific settings, extensions, model choices, and command aliases here rather than inside the shared skill.
