---
name: expert-preflight
description: Lightweight expert-level reasoning pass for a task, prompt, or professional artifact. Use only when explicitly invoked. Refine mode improves a request without executing it; Apply mode produces or improves the requested artifact (ADR, issue, LLD, review, docs, message) with the same expert rigor.
license: MIT
argument-hint: "[refine|apply] <request or artifact task>"
disable-model-invocation: true
---

# Expert Preflight

Bring the rigor of an experienced practitioner in the relevant domain to the task: deeper reasoning, not broader scope. Work as a single agent with the tools you already have. No subagents, extra model calls, external services, or scripts.

## Choose the mode

- **Refine**: the user wants a better request, prompt, or plan before running it. Triggered by `refine`, or by asking to improve/sharpen/review a prompt or request.
- **Apply**: the user wants an artifact created, edited, reviewed, or implemented. Triggered by `apply`, or by asking to write/create/edit/implement something.
- Ambiguous intent: use Refine.
- In Refine, never execute the task, even partially.

## Reasoning principles (shared by both modes)

Ask these silently, scaled to the task's complexity and risk. A simple, low-risk task needs a moment's thought, not an analysis.

1. **Blind spots**: what would a leading practitioner in this domain check that the user did not ask about?
2. **Primary evidence**: which original requirements, code, contracts, data, or constraints should inform this, rather than summaries or assumptions? Read only what is targeted and necessary; do not scan whole repositories or re-read large files.
3. **Method**: which concrete technique, tool, or established practice fits this specific problem? Skip generic advice.
4. **Validation**: what observable evidence, acceptance criteria, existing contracts, or checks would show the result is correct?

## Guardrails

- Deepen, do not expand: keep the user's intent, constraints, and scope.
- Challenge assumptions when evidence justifies it; do not agree by reflex.
- Separate verified problems from hypothetical risks; say so when evidence is insufficient instead of inventing facts.
- Respect decisions already validated unless new evidence justifies revisiting them.
- Follow the project's existing conventions, templates, and docs; do not impose your own structure where one exists.
- Prefer the simplest solution that meets the real requirements. No speculative abstractions, infrastructure, or edge cases.
- Do not manufacture findings to look thorough. No repetitive or exhaustive analysis, no mandatory multi-pass review.
- Know when it is good enough and say so.

## Refine

1. Read the request and any directly relevant context.
2. Apply the principles.
3. Respond with:
   - **Observations**: only material blind spots, wrong or unverified assumptions, or missing evidence. Omit if none.
   - **Improved request**: a concise version ready to use, preserving the original intent, constraints, and scope. Include objective validation criteria when they are missing and useful.
   - If the original is already sufficient, say **"Proceed unchanged"** with one line of reason, and do not rewrite it.
4. Stop. Do not run the refined request.

## Apply

1. Understand the task and its constraints.
2. Do focused expert analysis and examine relevant primary evidence.
3. Produce or modify the requested artifact directly, in the project's format if one exists.
4. Check the result against the requirements and observable evidence (e.g. referenced files, existing contracts, existing tests).
5. Deliver only what was requested. Add brief reasoning only where it helps the user understand a non-obvious decision, or to flag material uncertainty. Do not list the four questions, and do not create extra reports or documents.
