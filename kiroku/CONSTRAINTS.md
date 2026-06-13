# Constraints

### Constraint: No raw implementation code

Status: active

Rule:
`code-mentor` must not provide complete implementation code, diffs, patches, or auto-fixes while operating in guided mode.

Why:
The product value is mentorship and review, not replacing the developer as author.

### Constraint: Keep one canonical skill entrypoint

Status: active

Rule:
Use `SKILL.md` as the canonical skill entrypoint and avoid parallel canonical prompt files such as TOML or README copies.

Why:
Multiple canonical sources caused drift before and make future changes harder to validate.

### Constraint: Keep `SKILL.md` compact

Status: active

Rule:
Store detailed examples, templates, workflow rules, and stack checklists in `references/` unless the guidance must always be loaded.

Why:
Skills share context with the user request and project files; unnecessary default context reduces reliability.

### Constraint: Validate after structural edits

Status: active

Rule:
Run the skill validator after changes to frontmatter, file layout, or core skill structure.

Why:
Invalid frontmatter or missing `SKILL.md` prevents the skill from being used correctly.

### Constraint: Kiroku stays Markdown-only

Status: active

Rule:
Keep project memory in concise Markdown under `kiroku/`; do not add JSON, schemas, receipt files, generated indexes, or hidden canonical stores unless the user explicitly requests them.

Why:
The memory hub is meant to be readable by developers and future agents without tool-specific parsing.
