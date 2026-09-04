# Claude adapter

Claude-specific discovery and installation details belong here.

The canonical skills under `skills/` must remain portable and must satisfy the common Agent Skills format. This adapter may describe how Claude discovers or links the selected skills, but it must not create a second maintained copy of their instructions.

Claude Code exposes user-invoked skills as `/skill-name`. Install with:

```bash
bin/skills-sync refresh
```

This links each `skills/<name>` into `~/.claude/skills` (or `$CLAUDE_CONFIG_DIR/skills`), creating what is missing, removing links whose skill left the repository, and repairing links whose target moved. It only ever touches links that point into this repository: a real directory, or a link into another library, is reported as a conflict and left alone. Re-run it after any pull that adds, renames, or removes a skill. Do not maintain a second instruction copy here.

Claude Code reads skills at startup, so restart or run `/reload-plugins` afterwards.

The canonical skills may contain `disable-model-invocation: true` for explicit gates such as `goldilocks-review`, `thermos`, and `continual-learning`. Keep those gates explicit when using `/skill-name`.
