# Skill mechanics

The skill-specific branch of [`writing-for-agents`](SKILL.md): what changes when the document is a skill (frontmatter, the invocation choice, and router skills). Everything else about writing it is the universal reference in `SKILL.md`.

## Invocation

Invocation controls whether an agent may select a skill on its own. Supported agents differ: some honor `disable-model-invocation`, while others use agent-specific policy or only treat descriptions as discovery metadata. Keep the portable trigger and authorization rules in the skill body; adapters may document extra frontmatter where needed.

Two common choices, trading the two loads:

- In agents that support this distinction, a **model-invoked** skill keeps a `description` so the agent can discover and select it. A **user-invoked** skill suppresses autonomous selection while remaining available to the human. For example, Claude Code supports `disable-model-invocation: true`; other agents may use different controls or treat the field as ordinary metadata. Check the relevant adapter before relying on frontmatter for invocation policy.

Descriptions may remain part of startup context even when the skill body is loaded only after selection. Keep descriptions concise and use them as routing pointers. Put portable authorization rules in the skill body, where they can be followed across agents.

Choose the invocation setting based on the behavior of the target agent. If startup cost matters, reduce the installed set and let a router load on-demand skills from a catalogue instead of assuming metadata alone will prevent context loading.

Shared reference needed by multiple skills can live in a plain file outside the skill system, with each skill pointing to it. For cross-agent libraries, a router can read a generated catalogue and load the selected skill's complete instructions only when needed.

## Splitting by invocation

The invocation cut of splitting (the sequence cut lives in `SKILL.md`): split off a model-invoked skill when you have a distinct leading word that should trigger it on its own (a trigger word you actually use in your prompts), or another skill must reach it. You pay context load for the new always-loaded description, so that independent reach has to be worth it.

## Router skills

When the skill library grows, a **router skill** can keep the startup set small while making the rest discoverable. The router reads a catalogue, presents matching options, recommends one, and follows the user's selection by reading that skill's full instructions. Keep this behavior in the skill body because agents differ in how they handle implicit invocation and metadata. A direct user request for a named workflow can bypass the menu.
