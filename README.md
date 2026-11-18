# expert-preflight-skill

Lightweight expert reasoning skill for refining and executing tasks with deeper analysis, without expanding scope.

## What it does

`expert-preflight` makes the agent approach a task like an experienced practitioner in the relevant domain. Before refining or producing anything, it considers four questions, scaled to the task's complexity and risk:

1. What would an expert check that the request does not mention (blind spots)?
2. What primary evidence (requirements, code, contracts, data) should inform the work?
3. Which concrete professional method fits this problem?
4. What observable evidence would show the result is correct?

It aims for deeper reasoning, not broader scope. It keeps your intent and constraints, challenges assumptions only when justified, prefers the simplest sufficient solution, and says so when no improvement is needed.

## When to use it

Use it when a task is ambiguous, high-stakes, or in a domain where missed considerations are costly. Skip it for trivial requests. It is configured as manual-only (`disable-model-invocation: true`), so it never runs unless you invoke it.

## Refine vs. Apply

| Mode | Does | Does not |
| --- | --- | --- |
| **Refine** | Returns material observations (if any) and an improved, ready-to-use request, or "Proceed unchanged". | Execute the request. |
| **Apply** | Produces or improves the requested artifact directly, validated against requirements and evidence. | Add deliverables beyond what was asked. |

If the intent is ambiguous, Refine is used.

## Installation (Claude Code)

The skill's `name` is `expert-preflight`, and the skill directory name should match it. Clone or link the repository under that name.

Personal (all projects):

```bash
git clone https://github.com/amirbena/expert-preflight-skill ~/.claude/skills/expert-preflight
```

Project-only:

```bash
git clone https://github.com/amirbena/expert-preflight-skill .claude/skills/expert-preflight
```

Or, from an existing local checkout, symlink it:

```bash
ln -s /path/to/expert-preflight-skill ~/.claude/skills/expert-preflight
```

Claude Code watches existing skill directories for changes. If `~/.claude/skills/` (or `.claude/skills/`) did not exist when the session started, run `/reload-skills` or restart. The repository root holds `SKILL.md`; the other files are not part of the skill.

## Invocation

```
/expert-preflight refine Add caching to our API to make it faster
/expert-preflight apply Write an ADR for moving from REST to gRPC between the order and billing services
```

Mode keywords are optional; plain wording such as "improve this prompt" selects Refine, and "write/create/edit ..." selects Apply.

## Example use cases

- **Prompt**: `/expert-preflight refine "Summarize this contract"`: surfaces missing constraints (audience, risk focus, jurisdiction) and returns a tighter prompt.
- **ADR**: `/expert-preflight apply write an ADR for choosing Postgres over DynamoDB`: grounds the ADR in the actual requirements and existing ADR format, states the rejected alternatives and consequences.
- **GitHub Issue**: `/expert-preflight apply create an issue for the login timeout bug`: writes a scoped issue with reproduction evidence and testable acceptance criteria.
- **Technical documentation**: `/expert-preflight apply improve docs/deploy.md`: checks the doc against the real scripts and config, and fixes what diverges.

## Design

Single-agent and lightweight: no subagents, extra model calls, external services, MCP dependencies, scripts, or background processing. It uses only the current agent's reasoning and tools, and reads targeted evidence rather than whole repositories.

## Compatibility

- **Claude Code**: verified against the Claude Code skills documentation. Uses `name`, `description`, `license`, plus Claude Code's `disable-model-invocation` and `argument-hint`. Invoke with `/expert-preflight` at the start of a message; arguments are passed to the skill as text.
- **claude.ai uploads / Skills API**: the Claude Code docs state that only `name`, `description`, `license`, `compatibility`, `metadata`, and `allowed-tools` are accepted there, and other keys are rejected. `argument-hint` and `disable-model-invocation` would need to be removed before uploading.
- **Other Agent Skills-compatible tools**: the layout (a directory with `SKILL.md` and YAML frontmatter) follows the Agent Skills format, but the open specification could not be fetched during verification, and other tools' install paths and field support are unverified. Check your tool's documentation.

## License

MIT
