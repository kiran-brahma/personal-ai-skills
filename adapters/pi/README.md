# Pi adapter

Pi exposes a portable skill as `/skill:name` and accepts arguments after the command. Discovery goes through `.agents/skills`, a committed relative symlink to `../skills`, so a clone works with no setup. `bin/skills-sync refresh` creates it if it is missing.

Pi's discovery differs from the other agents in one way that constrains the whole library: it recurses into subdirectories, but stops at the first `SKILL.md` it finds and does not look beneath it. A skill nested under another skill is therefore invisible to Pi. `bin/skills-sync validate` enforces the flat layout that keeps this from happening.

The canonical skills intentionally use standard `SKILL.md` frontmatter and relative references. Keep Pi-specific settings, extensions, model choices, and command aliases here rather than inside the shared skill.
