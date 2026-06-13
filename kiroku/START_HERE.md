# Start Here

## Mission

- Maintain `code-mentor` as a Codex skill for guided implementation mentorship.
- The skill helps agents analyze, plan, guide, and review software work while keeping the developer as code author.

## Current State

- `SKILL.md` is the active skill entrypoint and validates successfully.
- The skill uses progressive disclosure through `references/`.
- Current core behavior: no raw implementation code, no patches, gated planning, one task at a time, review before progress.
- State persistence, realistic examples, and anti-ambiguity command rules are already added.
- The Kiroku memory hub now exists in `kiroku/`.

## Next Action

- Run forward-testing on realistic prompts before treating the skill as mature.
- If forward-testing is deferred, commit the current valid skill and memory hub.

## Hard Constraints

- Preserve developer authorship: do not make `code-mentor` generate copy-paste implementation code.
- Keep `SKILL.md` compact; move detailed procedures and examples into `references/`.
- Do not reintroduce duplicate canonical sources such as `code-mentor.toml`.
- Keep memory as concise Markdown under `kiroku/`; do not add JSON or generated indexes.

## Read Only If Needed

- `STATE.md` for current project status.
- `WORK.md` for TODO, DONE, and continuation tasks.
- `ARCHITECTURE.md` before changing skill structure.
- `DECISIONS.md` and `CONSTRAINTS.md` before changing workflow rules.
- `IDEAS.md` for deferred or rejected directions.
- `RISKS.md` for fragile areas and mitigations.
