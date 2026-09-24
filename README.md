# Personal Agent Skills

This is my public, version-managed library of AI-agent skills.

The skills are being adopted and adapted from my experience using AI agents to build software. They are not a neutral collection of generic prompts. Each skill reflects how I want an agent to think, plan, implement, review, and learn while working with me.

## Why this repository exists

Using every available skill by default creates two problems:

- The agent spends too much context carrying instructions that do not apply to the current task.
- Skills change over time, so keeping many installed copies updated becomes manual work.

This repository is one canonical, version-controlled source for the skills I use, shared across Claude Code, Codex, and Pi. Each agent reads the same `SKILL.md` files from the same directories on disk, so there is one copy to edit and one copy to update.

The second problem is handled by [`bin/skills-sync`](bin/skills-sync), which installs the library into every agent, keeps those installs reconciled with the repository, and gates releases. Git hooks run it, so a skill added in a commit reaches every agent without anyone remembering a step.

## Install

```bash
git clone https://github.com/kiran-brahma/personal-ai-skills.git
cd personal-ai-skills
bin/skills-sync bootstrap --role author --apply
```

`bootstrap` asks what kind of machine this is. An **author** machine installs from its own working tree and wires the git hooks, so an edit is live in the next session. A **consumer** machine installs the published plugin from the marketplace and tracks releases instead, so a local edit never moves its install.

Setting `core.hooksPath` is the only manual step in the whole setup. Everything after it is automatic.

Agents read skills at startup, so restart them after installing.

| Agent | Reads from | Invocation |
| --- | --- | --- |
| Claude Code | `~/.claude/skills` | `/skill-name` |
| Codex | `~/.agents/skills` | `$skill-name`, or the `/skills` selector |
| Pi | `~/.pi/agent/skills` | `/skill:name` |

Codex and Pi both read `~/.agents/skills`, the cross-harness Agent Skills location. Pi deduplicates by real path, so the overlap costs nothing.

## Installing this library yourself

The sections above are for my own machines. To use these skills yourself, **fork** the repository and install only what you need. Everything you don't install stays in your fork, and `decide-skills` can still find and run it.

1. Fork `kiran-brahma/personal-ai-skills` on GitHub, then:

   ```bash
   git clone https://github.com/<you>/personal-ai-skills.git ~/.kb-skills
   ~/.kb-skills/bin/skills-sync setup
   ```

   `setup` adds this repository as the `upstream` remote, installs three entry-point skills into every agent it finds (Claude Code, Codex, Pi), and wires the git hooks.

2. Restart your agent and run `/setup-skills` (`$setup-skills` in Codex). It asks what you work on, recommends a few **profiles** (`coding`, `typescript`, `deep-review`, `business`, `video`, and others in [`profiles.json`](profiles.json)), and installs them with their dependencies. Your choice lives in `my-skills.txt`, per machine and git-ignored. Change it any time with `/setup-skills` or `bin/skills-sync select --add profile:video`.

3. Pull my releases with `bin/skills-sync sync`. It merges the latest release tag, never unreleased work, and reinstalls. New skills arrive uninstalled but reachable.

Your own skills belong in your fork. When `decide-skills` finds that nothing fits a repeated need, it offers to build one: `bin/skills-sync new <name> --library`, then `select --add <name>` to install it.

**Install everything instead.** The plugin installs the default set (everything in `skills/`) with no selection:

```bash
claude plugin marketplace add kiran-brahma/personal-ai-skills && claude plugin install kb@kb-skills
codex plugin marketplace add kiran-brahma/personal-ai-skills && codex plugin add kb@kb-skills
```

Invoke plugin skills as `/kb:skill-name` in Claude Code. Use one route or the other on a machine, never both, or every skill loads twice.

### Using it

You do not need to memorise anything:

- **Coding**: just work. The engineering skills fire on their own. Run `/ask-matt` for the idea-to-ship flow.
- **Everything else**: `/decide-skills review my musing`, `/decide-skills should I take this client`, or name a skill: `/decide-skills content-fence`. Plain language reaches it too.
- **Lost?** `/ask-kb` explains what exists and how to invoke it. In Codex, use `$` instead of `/`. With the plugin, add the `kb:` prefix.

### Two things worth knowing first

**These are personal skills, not a neutral toolkit.** They encode how I want an agent to work with me. Four of them name me directly and are tuned to my writing and my blogs: `cognitive-editor`, `content-fence`, `musings-reviewer`, and the `writing` router. Most of the engineering skills are portable, but if you want a library shaped around your own judgment, fork this and adapt it rather than installing it as-is. That is what I did with the sources below.

**Much of the value is not mine.** The engineering and productivity workflows are adapted from [Matt Pocock's skills](https://github.com/mattpocock/skills), the supporting lenses from [pstack and thermos](https://github.com/cursor/plugins), and the business methods from [gstack](https://github.com/garrytan/gstack). Those authors distribute their own work, kept current by them, and you may prefer to take it from the source. Licences and attribution are in [`THIRD_PARTY.md`](THIRD_PARTY.md); local adaptations and pinned upstream commits are recorded in [`registry.yaml`](registry.yaml).

## Keeping it current

```bash
bin/skills-sync doctor      # what is out of sync, changing nothing
bin/skills-sync refresh     # reconcile every agent with the repository
bin/skills-sync validate    # check the library against the layout contract
```

`refresh` only manages symlinks that point into this repository. A real directory, or a link into another skill library, is reported as a conflict and never touched, so it cannot delete skills it did not install.

The git hooks make this automatic: `pre-commit` validates, and `post-commit`, `post-merge`, and `post-checkout` reconcile the install.

## The adoption philosophy

I start with well-written external skills, then adapt them to my own working style. A local change is intentional when it improves the way I work, even when the upstream skill is already strong.

The repository maintains one canonical local version of each adopted skill. It does not maintain separate Claude, Codex, Pi, or Antigravity copies. Harness-specific discovery and installation details belong in [`adapters/`](adapters/), while the workflow itself remains portable.

Upstream updates are inputs for review, never applied automatically:

```bash
bin/skills-sync upstream        # what the original authors changed since the pinned commit
bin/skills-sync adopt --apply   # three-way merge, preserving local adaptations
```

`upstream` reports what moved and, more usefully, where an upstream change touches a file I have also edited. `adopt` merges the rest and leaves conflict markers where both changed the same lines, because that is a judgment no tool should make. An unresolved merge fails `validate`, so it cannot reach a commit or a release.

Before adopting an update I compare:

1. The new upstream behavior.
2. The local adaptation and the reason it exists.
3. The evaluation cases and observed behavior.
4. The effect on other skills and the overall workflow.

The registry records the upstream repository, commit, license, local adaptations, status, and update policy for each source. `upstream --pin` moves that commit only after the review is done.

## The workflow foundation

The default engineering workflow is based on Matt Pocock's skills:

`grill-with-docs → to-spec → goldilocks-review → to-tickets → implement → code-review`

The workflow is deliberately gated. After a PRD or spec is complete, `goldilocks-review` checks for a solution that is simple in the resulting system, not merely easy for an AI to generate. It gives minimal coupling and operational simplicity priority, with a preference for deep modules behind limited interfaces.

For a major code change, the sequence is:

`implement → thermos → fix findings → code-review → pull request`

Every pull request must complete `code-review`. Detailed security audits use the separately loaded Codex Security workflow rather than the normal coding workflow.

## Two tiers

A library that keeps growing cannot load every skill into every session. Each installed skill's description sits in the agent's context from startup, and Codex silently truncates once the combined descriptions pass a fixed budget. So the library is split:

- **Installed** ([`skills/`](skills/)): the daily set. This is the full coding workflow, the [`coding`](skills/coding/SKILL.md) router, cross-cutting tools such as `unslop`, `grilling`, `handoff`, and `research`, and three entry points: `decide-skills`, `ask-kb`, and `skill-tiers`. These fire on their own.
- **On demand** ([`library/`](library/)): writing, business, video, and occasional governance workflows. No agent scans this folder. [`decide-skills`](skills/decide-skills/SKILL.md) reads a generated [index](skills/decide-skills/references/index.md), one line per skill, then loads only the skill that fits.

The startup cost is the installed descriptions plus one line for `decide-skills`, whether the library holds 20 skills or 200. Both tiers use the same flat, one-level layout. Claude Code searches only one level, and Pi stops at the first `SKILL.md` it finds. [`bin/skills-sync validate`](bin/skills-sync) enforces the layout, checks that the index is current, and charges only the installed tier against the budget. [`policies/skill-format.md`](policies/skill-format.md) records which agent imposes which constraint.

Move a skill between tiers with `bin/skills-sync tier <name> library` or `bin/skills-sync tier <name> installed`. The [`skill-tiers`](skills/skill-tiers/SKILL.md) skill decides which tier a skill belongs in.

## Current skill sources

- **Matt Pocock:** foundation engineering and productivity workflows.
- **pstack:** targeted supporting lenses for architecture, codebase understanding, blast-radius analysis, adversarial review, verification, technical writing, and long-running work.
- **Thermos:** deep review for major changes before Matt's final code review.
- **Continual learning:** proposal-first updates to `AGENTS.md` and `CLAUDE.md` based on durable lessons.
- **gstack:** selected product-discovery and founder-review methods, adapted into portable business workflows.
- **HyperFrames:** selected open-source video-authoring workflows for approved writing explainers and product-launch videos, adapted for the repository's canonical layout and provider boundaries.
- **Codex Security:** external-only workflow for detailed security audits.

The source list and pinned references are in [`registry.yaml`](registry.yaml). Adapted-license notices are in [`THIRD_PARTY.md`](THIRD_PARTY.md). Upstream provenance documents that are not skills live in [`packages/`](packages/).

## Adding a skill

```bash
bin/skills-sync new my-skill -d "What it does. When it fires. Not for X, use Y."            # installed
bin/skills-sync new my-skill -d "..." --library   # on demand; add it to a profile, then `index`
```

The scaffold refuses an over-budget description and a name that will not resolve. A description is a trigger contract, not a summary: it answers whether the skill should fire, and the detail belongs in the body where it costs nothing until the skill is invoked. The rule is in [`policies/skill-format.md`](policies/skill-format.md).

After writing the body, record the skill in [`registry.yaml`](registry.yaml) and run `bin/skills-sync validate`.

## Releasing

```bash
bin/skills-sync release            # preflight only
bin/skills-sync release --apply    # publish, then verify the install moved
```

Preflight blocks on a dirty tree, a detached HEAD, a validation failure, an invalid plugin manifest, a tag that already exists, and a missing changelog entry. Only then does it write the version, commit, tag, push, refresh the local install, and re-check that the install actually moved.

`VERSION` holds the major and minor version. The patch is derived from the commits touching `skills/` or `library/` since the last tag, so it cannot fail to move when the library does. Claude Code and Codex ship an update only when the manifest version changes, which makes a forgotten bump a silent failure rather than a loud one.

## Repository layout

```text
personal-ai-skills/
├── AGENTS.md            Canonical repository control document
├── CLAUDE.md            Claude entrypoint that refers to AGENTS.md
├── GEMINI.md            Gemini entrypoint that refers to AGENTS.md
├── SKILLS.md            Top-level catalogue: which tier, which router
├── VERSION              Major and minor version; the patch is derived
├── bin/skills-sync      Validation, install, release, and upstream tooling
├── .githooks/           Hooks that validate and reconcile on every commit
├── .claude-plugin/      Claude Code plugin and marketplace manifests
├── .codex-plugin/       Codex plugin manifest
├── skills/              Installed tier: daily skills and routers, one level deep
├── library/             On-demand tier, reached only through decide-skills
├── adapters/            Agent-specific discovery and installation details
├── packages/            Provenance documents for vendored upstream packages
├── policies/            Repository rules and decision records
├── evals/               Behavioral evaluation cases
├── registry.yaml        Skill inventory and provenance metadata
├── profiles.json        Install bundles for `select`; sections of the decide-skills index
├── THIRD_PARTY.md       Notices for adapted external skills
├── CHANGELOG.md         Release index
└── changelog/           Release notes, one file per month
```

The GitHub repository is the canonical source. Local copies are for development and evaluation; agents should consume the committed and pushed version.
