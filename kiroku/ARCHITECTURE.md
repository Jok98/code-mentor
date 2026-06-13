# Architecture

## Skill Layout

- `SKILL.md` is the only skill entrypoint.
- `agents/openai.yaml` contains UI metadata.
- `references/` contains detailed guidance loaded only when needed.
- `kiroku/` contains project memory and is not part of runtime skill behavior.

## Progressive Disclosure

`SKILL.md` keeps always-needed instructions: identity, raw-code boundary, workflow phases, state contract, reference routing, command interpretation, response discipline, and approval bar.

Detailed material is split by owner:

- `references/workflow.md`: phase machine, state contract details, command matrix, scope changes, uncertainty handling.
- `references/inspection-and-review.md`: repository inspection and review protocol.
- `references/output-templates.md`: optional structured response templates.
- `references/stack-checklists.md`: framework and domain checklists.
- `references/examples.md`: realistic calibration scenarios.

## Runtime Flow

The intended `code-mentor` flow is:

1. Analyze repository and request.
2. Propose a high-level plan.
3. Wait for explicit plan approval.
4. Break the approved plan into atomic tasks.
5. Guide one task verbally.
6. Wait for the user implementation.
7. Inspect and review changed code.
8. Approve, request rework, or block on missing context.
9. Propose the next task without starting it automatically.

## Validation Pattern

Use the skill validator after structural edits:

```bash
python3 /home/jok/.codex/skills/.system/skill-creator/scripts/quick_validate.py /home/jok/.agents/skills/code-mentor
```

Use the Kiroku checker after memory updates:

```bash
python3 /home/jok/.agents/skills/kiroku-forge/scripts/check_hub.py /home/jok/.agents/skills/code-mentor
```

## Design Pattern

The project intentionally uses Markdown instructions rather than scripts. The behavior is procedural and judgment-based, not a deterministic transformation that benefits from executable tooling.
