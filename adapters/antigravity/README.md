# Antigravity adapter

Antigravity-specific discovery and installation details belong here.

The canonical skills under `skills/` must remain portable and must satisfy the common Agent Skills format. This adapter may describe how Google Antigravity discovers or links the selected skills, but it must not create a second maintained copy of their instructions.

## Discovery and Surfaces

Antigravity (Antigravity 2.0 desktop application, Antigravity IDE, and Antigravity CLI `agy`) discovers skills from two scopes:

1. **Workspace scope (Project-Specific):**
   - `<workspace-root>/.agents/skills/<skill-folder>/`
   - Scoped to a specific project. Antigravity walks up from the current working directory to the repository root.

2. **Global scope (Machine-Local):**
   - `~/.gemini/config/skills/<skill-folder>/` (honours `$GEMINI_CONFIG_DIR`)
   - Available across all projects and workspaces on the workstation.
   - For Antigravity CLI: `~/.gemini/antigravity-cli/skills/`.
   - Legacy Antigravity IDE path: `~/.gemini/antigravity/skills/`.
   - Additional explicit paths can be registered via `~/.gemini/config/skills.json`.

## Installing

```bash
bin/skills-sync refresh
```

This links each selected skill into `~/.gemini/config/skills/`, creating missing links, removing links whose skill left the repository, and repairing links whose target moved. It also maintains `~/.gemini/config/skills.json` and synchronizes CLI and IDE symlinks.

Because links are live symlinks, an edit in this repository is immediately visible to the next Antigravity session with no manual reinstall or version bump.

## Invocation

- **Autonomous Model Invocation**: During conversation initialization, Antigravity scans available skills and injects their names and descriptions. The agent activates and reads a skill's full instructions when relevant to the user request.
- **Explicit Slash Command**: Type `/<skill-name>` in the chat canvas or CLI prompt to invoke a skill directly.
- **Gated Skills**: Antigravity honours `disable-model-invocation: true`. Gated skills remain installed and accessible for explicit invocation (`/<skill-name>`), but are omitted from autonomous model prompt injection to protect context and enforce intentional gates.
