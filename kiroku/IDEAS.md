# Ideas

## Open

### Idea: Add more domain-specific mentor scenarios

Status: open

Notes:
- Possible additions: database migration, frontend workflow, security review, CI failure review.
- Add only if they improve behavior calibration without bloating default context.

### Idea: Forward-test with independent agents

Status: open

Notes:
- Use raw tasks from `references/examples.md`.
- Do not leak expected answers or prior conclusions into the test prompt.

## Rejected

### Rejected: Keep the old TOML as canonical source

Reason:
The old TOML duplicated the skill content and previously contained a naming typo. Keeping it would create drift from `SKILL.md`.

Keep in mind:
Only recreate an agent-specific config if a tool explicitly requires it, and make clear it is generated or secondary.

### Rejected: Store project memory as JSON

Reason:
The active memory approach is Markdown-first Kiroku. JSON would add a parallel canonical store without a current need.

Keep in mind:
Reconsider only if the user explicitly asks for machine-readable memory.

## Forbidden

### Forbidden: Turn `code-mentor` into an implementation agent by default

Reason:
That violates the core product boundary and would erase the distinction between this skill and a normal coding agent.

Keep in mind:
The user can explicitly stop using `code-mentor`, but the skill itself should not silently change behavior.
