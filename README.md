# Personal Agent Skills

This is my public, version-managed library of AI-agent skills.

The skills are being adopted and adapted from my experience using AI agents to build software. They are not a neutral collection of generic prompts. Each skill reflects how I want an agent to think, plan, implement, review, and learn while working with me.

## Why this repository exists

Using every available skill by default creates two problems:

- The agent spends too much context carrying instructions that do not apply to the current task.
- Skills change over time, so keeping many installed copies updated becomes manual work.

This repository provides one canonical, version-controlled source for the skills I use. A small global instruction file will point Claude, Codex, Pi, or another compatible agent to this repository. The agent can inspect the catalogue and load only the skill needed for the current task.

The global file stays small. It tells the agent where the skills live and how to select them. The detailed workflows, references, scripts, provenance, and evaluations stay in this repository.

## The adoption philosophy

I start with well-written external skills, then adapt them to my own working style. A local change is intentional when it improves the way I work, even when the upstream skill is already strong.

The repository therefore maintains one canonical local version of each adopted skill. It does not maintain separate Claude, Codex, and Pi copies. Harness-specific discovery and invocation details belong in [`adapters/`](adapters/), while the workflow itself remains portable.

Upstream updates are inputs for review. They are not copied over automatically. Before adopting an update, I compare:

1. The new upstream behavior.
2. The local adaptation and the reason it exists.
3. The evaluation cases and observed behavior.
4. The effect on other skills and the overall workflow.

The registry records the upstream repository, commit or version, license, local adaptations, status, and update policy for each source.

## The workflow foundation

The default engineering workflow is based on Matt Pocock’s skills:

`grill-with-docs → to-spec → goldilocks-review → to-tickets → implement → code-review`

The workflow is deliberately gated. After a PRD or spec is complete, `goldilocks-review` checks for a solution that is simple in the resulting system, not merely easy for an AI to generate. It gives minimal coupling and operational simplicity priority, with a preference for deep modules behind limited interfaces.

For a major code change, the sequence is:

`implement → thermos → fix findings → code-review → pull request`

Every pull request must complete `code-review`. Detailed security audits use the separately loaded Codex Security workflow rather than the normal coding workflow.

## Categories

Skills are grouped into focused categories so agents can narrow discovery before loading detailed instructions.

- [`Coding`](skills/coding/SKILL.md): planning, implementation, debugging, testing, architecture, review, and release work.
- [`Business`](skills/business/SKILL.md): business ideas, customer value propositions, strategic decisions, and complex operating problems.
- [`Writing`](skills/writing/SKILL.md): documentation and other writing workflows.
- [`Miscellaneous`](skills/misc/SKILL.md): research, planning, productivity, and other reusable work.
- [`Governance`](skills/governance/SKILL.md): maintaining skills and proposing updates to project agent instructions.

Each category has a router. Each concrete skill has its own `SKILL.md`. Supporting references and scripts live beside the skill that owns them.

## Current skill sources

- **Matt Pocock:** foundation engineering and productivity workflows.
- **pstack:** targeted supporting lenses for architecture, codebase understanding, blast-radius analysis, adversarial review, verification, technical writing, and long-running work.
- **Thermos:** deep review for major changes before Matt’s final code review.
- **Continual learning:** proposal-first updates to `AGENTS.md` and `CLAUDE.md` based on durable lessons.
- **gstack:** selected product-discovery and founder-review methods, adapted into portable business workflows.
- **Codex Security:** external-only workflow for detailed security audits.

The source list and pinned references are in [`registry.yaml`](registry.yaml). Adapted-license notices are in [`THIRD_PARTY.md`](THIRD_PARTY.md).

## How agents use the skills

Agents should read the global entrypoint, identify the relevant category, read the category router, and then load the narrowest skill that matches the task. Full skill instructions are loaded on demand rather than carried in every session.

Explicit invocation uses each agent’s native syntax:

- Claude Code: `/skill-name`
- Codex: `$skill-name` or the `/skills` selector
- Pi: `/skill:name`

The same portable `SKILL.md` remains the source for all three. See the adapter documentation for setup details.

## Repository layout

```text
skills/
├── AGENTS.md        Canonical repository control document
├── CLAUDE.md        Claude entrypoint that refers to AGENTS.md
├── GEMINI.md        Gemini entrypoint that refers to AGENTS.md
├── SKILLS.md        Top-level category catalogue
├── policies/        Repository rules and decision records
├── skills/          Category routers and portable skills
├── adapters/        Agent-specific discovery and installation details
├── evals/           Behavioral evaluation cases
├── registry.yaml    Skill inventory and provenance metadata
├── THIRD_PARTY.md   Notices for adapted external skills
└── CHANGELOG.md     Human-readable repository history
```

The GitHub repository is the canonical source. Local copies are for development and evaluation; agents should consume the committed and pushed version.
