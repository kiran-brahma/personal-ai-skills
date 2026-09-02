# Claude adapter

Claude-specific discovery and installation details belong here.

The canonical skills under `skills/` must remain portable and must satisfy the common Agent Skills format. This adapter may describe how Claude discovers or links the selected skills, but it must not create a second maintained copy of their instructions.

Claude Code exposes user-invoked skills as `/skill-name`. Point Claude at the canonical skill directories or install a project-local copy according to your normal Claude Code setup. Do not maintain a second instruction copy here.

The canonical skills may contain `disable-model-invocation: true` for explicit gates such as `goldilocks-review`, `thermos`, and `continual-learning`. Keep those gates explicit when using `/skill-name`.
