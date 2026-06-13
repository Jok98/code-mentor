# State

## Project Purpose

`code-mentor` is a Codex skill that turns an agent into a guided implementation mentor. It should help users analyze projects, agree on a plan, break approved work into atomic tasks, give verbal implementation guidance, review user-written changes, and approve progress without taking over code authorship.

## Current Status

- Status: active skill under development.
- The skill entrypoint is `SKILL.md`.
- Detailed workflow, review protocol, output templates, stack checklists, and examples live under `references/`.
- `agents/openai.yaml` provides UI metadata for the skill.
- The current skill passes the skill validator.
- Kiroku memory was initialized for durable project state.

## Recently Verified

- `python3 /home/jok/.codex/skills/.system/skill-creator/scripts/quick_validate.py /home/jok/.agents/skills/code-mentor` returned `Skill is valid!`.
- `SKILL.md` contains only allowed frontmatter fields: `name` and `description`.
- The old duplicate sources `README.md`, `code-mentor.md`, and `code-mentor.toml` are no longer part of the active project layout.
- The skill includes a state contract, realistic examples, and phase-aware command resolution.

## Open Questions

- Whether to forward-test with subagents or another clean session before publishing.
- Whether the user wants this skill installed or only maintained in the current repository.

## Watch Points

- Keep the raw-code boundary strict when adding examples or templates.
- Keep `SKILL.md` concise enough to load by default.
- Avoid duplicating workflow rules across multiple files unless the summary/detail split is intentional.
- Re-run both skill validation and Kiroku hub validation after broad edits.
