# Repository model

## Purpose

This repository is a general-purpose, public library of skills used by the repository owner across AI agents and types of work.

The broad initial areas are:

- coding;
- writing; and
- miscellaneous work such as research, planning, and organization.

## Canonical version

There is one maintained version of a skill in this repository. A local change is not considered the maintained version until it is committed and pushed to GitHub.

Agents may cache or check out a committed version locally, but local copies are deployment artifacts rather than alternate sources of truth.

## Project-specific rules

Project rules are not skill variants. A project may provide its own rules document containing constraints, conventions, domain facts, or acceptance criteria. The relevant agent should read that document when working in the project.

Reusable skill behaviour belongs in `skills/`. Rules that only apply to one project belong with that project.

## Source and adaptation

An external skill may be adapted into this repository. The adapted skill remains one canonical local skill, while its source, commit, license, and local changes are recorded in `registry.yaml`.

Upstream changes are reviewed and selectively adopted. They do not overwrite the local skill automatically.
