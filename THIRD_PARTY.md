# Third-party skill notices

This repository contains adapted skill instructions from several third-party projects. The local copies are tracked in `registry.yaml` with their upstream commit, version, license, and adaptations.

## Matt Pocock skills

Source: [mattpocock/skills](https://github.com/mattpocock/skills), commit `24fe0ef7737efae15c87225755e9f6f5965e4888`, version `1.3.1`. The `pr` skill adapts the Summary visuals of Dex Horthy's `show-me` skill (HumanLayer); see `skills/pr/CREDITS.md`.

Copyright (c) 2026 Matt Pocock

## pstack and Thermos

Source: [cursor/plugins](https://github.com/cursor/plugins), commit `efa2a531985e0a8084d36ff3cf87233be8a9f34b`, pstack version `0.14.7`, Thermos version `1.0.0`. `correct` and `principle-test-behavior-not-implementation` come from commit `2cbf58508f40de470d7490b55c51d71241928fa2`, pstack version `0.15.13`.

Copyright (c) 2026 Lauren Tan (pstack)

Copyright (c) 2026 Cursor (Thermos)

## Fallow

Source: [fallow-rs/fallow-skills](https://github.com/fallow-rs/fallow-skills), commit `1dd4ea25f2db5bd7e73f21883fc3ec8fd7833a63`, version `1.2.57`.

Copyright (c) 2026 Bart Waardenburg

The adapted skills (`fallow`, `fallow-review`) are distributed under the MIT License. The upstream package's Claude plugin marketplace scaffolding (`.claude-plugin/`, `commands/`, `bin/`) and its `agents/openai.yaml` interface descriptors were not vendored — the latter is Codex-specific policy metadata, which `policies/skill-format.md` places under `adapters/`, not the portable skill. Only the two `SKILL.md` files and their `references/` were kept. `fallow-review`'s Claude-Code-only feedback hooks were removed when upstream dropped them in 1.4.41.

## Anthropic skills

Source: [anthropics/skills](https://github.com/anthropics/skills), commit `33375500bcea98d610eb30ce10ac4e59b89c390d`.

Copyright (c) Anthropic, PBC

The `frontend-design` skill is distributed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0); the full terms are in `library/frontend-design/LICENSE.txt`. The body is vendored verbatim. Only the description was shortened to fit this repository's trigger budget, and the skill sits in the on-demand library tier.

## MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## gstack business methods

Source: [garrytan/gstack](https://github.com/garrytan/gstack), commit `0d1bd5616c0ef096bb7ccee336f63c60ee408618`, version `1.79.0`.

Copyright (c) 2026 Garry Tan

The repository contains selected and substantially adapted business methods, not a wholesale copy of gstack. gstack-specific runtime paths, telemetry, private memory, host integrations, promotional material, and engineering-only orchestration were not adopted.

Codex Security is not included in this repository. It is tracked as an external, proprietary workflow only; see [`adapters/codex-security/README.md`](adapters/codex-security/README.md).
