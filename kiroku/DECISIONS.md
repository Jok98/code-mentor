# Decisions

### Decision: Use a Codex skill layout

Status: active
Area: project structure

Decision:
Represent `code-mentor` as a standard Codex skill with `SKILL.md`, `agents/openai.yaml`, and optional `references/`.

Rationale:
This makes the project discoverable and valid through the skill validator, while avoiding drift between prompt formats.

Consequences:
- `SKILL.md` is the canonical runtime entrypoint.
- Old prompt/config sources should not be reintroduced as competing canonical files.

### Decision: Preserve developer authorship

Status: active
Area: mentor behavior

Decision:
`code-mentor` must guide implementation verbally and must not generate raw implementation code, patches, or diffs by default.

Rationale:
The skill exists to help developers keep ownership and understanding of their code while still receiving senior-level analysis, planning, and review.

Consequences:
- Examples and templates must not include copy-paste-ready implementation blocks.
- Requests for code are handled by restating guided mode and giving verbal implementation direction.

### Decision: Use progressive disclosure

Status: active
Area: skill content

Decision:
Keep only always-needed behavior in `SKILL.md`; route detailed workflow, templates, checklists, and examples to `references/`.

Rationale:
This keeps activation cost low and lets agents load extra context only when relevant.

Consequences:
- New detailed guidance should usually go into a reference file.
- `SKILL.md` should stay compact and routing-focused.

### Decision: Make command handling phase-aware

Status: active
Area: workflow safety

Decision:
Interpret commands such as `ok`, `continue`, `next`, and `done` using current phase first, explicit user intent second, and keyword meaning third.

Rationale:
The same word can mean approval, continuation, task selection, or review depending on workflow state. Phase-aware interpretation prevents accidental task creation, skipped reviews, or unintended raw-code work.

Consequences:
- Ambiguous commands should trigger one narrow clarification.
- Review cannot proceed blindly when no current task or changed code is available.

### Decision: Maintain compact conversation state

Status: active
Area: workflow continuity

Decision:
Track current phase, objective, approved plan, task list, current task, completed tasks, rework, decisions, assumptions, blockers, and next action.

Rationale:
Guided implementation workflows are multi-step. Durable state prevents the mentor from skipping gates or losing context after interruptions.

Consequences:
- State snapshots are shown at phase changes, approvals, rework, scope changes, resumes, or when requested.
- Missing state must be reconstructed from visible evidence and labeled when uncertain.
