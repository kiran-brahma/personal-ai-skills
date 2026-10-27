# Skill routing evaluation cases

These are prose cases for human judgment, not executable tests. They cover Ask-kb's universal router, the four theme catalogue, direct skill requests, and on-demand loading.

## Case 1: plain-language request routes through Writing

Prompt: "Review my musing for today." (Paste a 250-word musing.)

Expected behavior:

- Ask-kb lists every skill in Writing, with short descriptions, recommends `musings-reviewer`, and waits for the user's choice.
- After the user chooses, reads the Writing routing notes and `library/musings-reviewer/SKILL.md`.
- Reads no other skill body.

## Case 2: a cross-theme request combines options

Prompt: "Help me evaluate this business decision, then shape the result into an essay."

Expected behavior:

- Ask-kb combines the relevant Productivity and Writing options in one menu.
- It gives one recommendation and waits for the user's choice before beginning.
- The user can select a first workflow; Ask-kb loads only that skill. The next workflow is selected separately when needed.

## Case 3: a directly named skill skips the menu

Prompt: "Use `cognitive-editor` to audit this draft."

Expected behavior:

- Treats the exact skill name as the user's selection and loads `library/cognitive-editor/SKILL.md` directly.
- Does not show a menu or load another skill body.

## Case 4: nothing fits

Prompt: "Which skill should I use to convert a CSV to JSON?"

Expected behavior:

- Says no listed skill fits and asks whether the user wants a general response.
- Does not stretch a near match to fit.

## Case 5: explicit skill-library request

Prompt: "Find or build a skill for planning my weekly meals."

Expected behavior:

- Loads `library/decide-skills/SKILL.md` without showing it as an ordinary task option.
- Checks whether an existing skill or approved upstream source fits before offering to build one.
- If building is appropriate and approved, scaffolds it in the user's fork and adds it to exactly one theme.

## Case 6: Implement waits for an explicit choice

Prompt: "I have a spec for this feature."

Expected behavior:

- Ask-kb lists every Coding skill, recommends one, and waits for the user's choice.
- If the user chooses Implement, loads `skills/implement/SKILL.md` and its lazy TDD and Code Review dependencies from their indexed paths when needed.
- If Codex activates Implement from its description before the user chooses it, Implement's body asks whether to run and does not begin work.

## Case 7: plugin consumer can load the library

Setup: install from the marketplace as a consumer, with no local author checkout.

Expected behavior:

- The plugin exposes only the three default skills at startup.
- The plugin package contains the complete `library/` tree as data.
- Ask-kb resolves the generated index and a selected library skill from the plugin's repository root.
- Library skill descriptions do not appear in the agent's startup skill list.

## Case 8: one primary theme per skill

Setup: inspect `profiles.json` and the generated catalogue.

Expected behavior:

- Every skill appears exactly once under Coding, Writing, Productivity, or Misc.
- The index is generated from the theme map, not from optional install profiles.
- `bin/skills-sync validate` reports no missing, duplicate, or unknown theme assignments.
