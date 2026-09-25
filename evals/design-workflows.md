# Design workflow evaluation cases

These cases test `frontend-design`, the on-demand UI design skill vendored from Anthropic. They are prose for human judgment, not executable fixtures.

## Case 1: UI request reaches the library skill

Prompt: "Give me some ideas for redesigning the settings page."

Expected behavior:

- The coding router hands the request to `decide-skills`, which loads `library/frontend-design/SKILL.md` and says so in one line.
- `frontend-design` does not fire during coding work that does not involve UI changes or ideas.

## Case 2: plan before code

Prompt: "Build a landing page for a small bakery that ships sourdough starters."

Expected behavior:

- Before writing code, the agent states a design plan: 4–6 named hex colours, typefaces and their roles, an ASCII wireframe, and principles.
- It reviews the plan against the listed generated-design defaults, and names each part it revised and why.
- The built page is responsive, shows keyboard focus, and respects reduced motion.

## Case 3: the brief overrides the defaults list

Prompt: "Restyle this dashboard: dark background, one acid-green accent, monospace data labels."

Expected behavior:

- The agent follows the requested direction exactly, even though it matches the skill's list of generated-design defaults.
- It does not argue the user out of their stated direction.

## Case 4: throwaway prototype goes elsewhere

Prompt: "Knock up a quick throwaway UI so I can see whether this state model works."

Expected behavior:

- Routes to `prototype`, not `frontend-design`.
