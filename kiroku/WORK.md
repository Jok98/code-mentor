# Work

## Ongoing

- No implementation task is currently in progress.

## TODO

### Task: Forward-test the skill

Status: todo
Completion:
Run at least one realistic clean-session or subagent scenario that uses `$code-mentor` for a feature, bugfix, or refactor flow and verify that it preserves phase discipline, avoids raw code, and requests review before advancing.

Notes:
- Good scenarios are documented in `references/examples.md`.
- Treat failures as evidence to tighten `SKILL.md` or the relevant reference.

### Task: Commit current project state

Status: todo
Completion:
Commit the valid skill structure and Kiroku memory hub after the user approves the final diff.

Notes:
- Suggested scopes so far include `feat`, `docs`, and `fix` depending on the exact staged changes.

## Blocked

- None.

## Done

- Converted the project from a long prompt/config draft into a valid Codex skill.
- Added `agents/openai.yaml` metadata.
- Split long guidance into focused `references/` files.
- Added state persistence rules to `SKILL.md` and `references/workflow.md`.
- Added realistic behavior examples in `references/examples.md`.
- Added phase-aware command resolution and ambiguous command handling.
- Initialized Kiroku memory for the project.

## Cancelled

- None.
