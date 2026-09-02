# Pi adapter

Pi exposes a portable skill as `/skill:name` and accepts arguments after the command. Configure the canonical skill directories in Pi settings, or place a project-level link under `.pi/skills` or `.agents/skills`.

The canonical skills intentionally use standard `SKILL.md` frontmatter and relative references. Keep Pi-specific settings, extensions, model choices, and command aliases here rather than inside the shared skill.
