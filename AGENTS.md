# AGENTS.md

Canonical instructions for working in this repository.

## Project
`expert-preflight` is a single Agent Skill. The repository root is the skill: `SKILL.md` is the canonical definition. Keep the repo minimal: `SKILL.md`, `README.md`, `LICENSE`, `AGENTS.md`, `CLAUDE.md`.

## Skill constraints
- Preserve the Refine/Apply behavior; Refine never executes the task.
- Single-agent and lightweight: no subagents, extra model calls, external services, scripts, or dependencies.
- No nested `.claude/skills/` copies or duplicate skill definitions.
- Do not claim compatibility with a platform without verifying its requirements.
- Keep `SKILL.md` frontmatter valid, and keep README install/usage in sync with it.

## Git workflow
- Branches: `<type>/<short-description>`, with type one of `feat`, `fix`, `docs`, `refactor`, `chore`. No unnecessary branches.
- One focused GitHub Issue per meaningful change, created before the work is committed.
- Conventional Commits (e.g. `feat: add refine mode`).
- Pull requests target `main` and link the issue with `Closes #N`.
- Squash merge only after checks pass and with explicit approval. No force merges.
- Do not push, merge, or change the remote without explicit approval.
