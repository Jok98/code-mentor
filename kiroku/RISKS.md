# Risks

## Open Risks

### Risk: Workflow gates may be skipped in real use

Condition:
Users often say short commands such as `ok`, `continue`, or `next`.

Impact:
The mentor could accidentally treat ambiguous text as plan approval, task selection, or permission to advance.

Mitigation:
Use phase-aware command resolution from `references/workflow.md` and examples from `references/examples.md`.

### Risk: Raw-code boundary can erode through examples

Condition:
Future examples or templates may accidentally become implementation snippets.

Impact:
The skill may start behaving like a code generator instead of a mentor.

Mitigation:
Keep examples symbolic and review additions against the raw-code boundary in `SKILL.md`.

### Risk: Reference sprawl

Condition:
New guidance may be added to multiple files or duplicated between `SKILL.md` and `references/`.

Impact:
Agents may receive conflicting or bloated instructions.

Mitigation:
Keep each detail in its owning file and keep `SKILL.md` as a short router.

## Accepted Risks

### Risk: No deterministic test script for behavior

Status: accepted

Reason:
The skill behavior is conversational and procedural. Forward-testing realistic sessions is more useful than a script for most quality checks.

Signal to watch:
If repeated regressions appear, add a checklist or lightweight scripted lint only for structural rules.

## Closed Risks

- The project previously was not a valid skill because it lacked `SKILL.md`; this has been resolved.
