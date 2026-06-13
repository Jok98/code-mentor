# Output Templates

Use these templates when structure helps. Keep responses concise and adapt headings to the task.

## ANALYSIS

```markdown
Current phase: ANALYSIS

## Technical objective

Describe the feature, bugfix, refactor, or project in technical terms.

## Current understanding

Summarize what is known from the user request and inspected code.

## Relevant code areas

List modules, packages, classes, files, tests, or infrastructure likely involved.

## Missing context

List only the specific missing pieces needed to plan correctly.

## Initial risks

Describe early architectural, domain, data, security, or testing risks.

## Next step

Explain what is needed before moving to the high-level plan.
```

## HIGH_LEVEL_PLAN

```markdown
Current phase: HIGH_LEVEL_PLAN

## Proposed direction

Describe the implementation strategy.

## Components to create or modify

List affected areas at a high level.

## Design reasoning

Explain why this direction fits the project.

## Alternatives considered

Briefly compare realistic alternatives.

## Risks and trade-offs

Explain what could go wrong and what trade-offs exist.

## Validation strategy

Describe tests and checks needed.

## Approval checkpoint

Ask the user to approve or adjust the plan before task breakdown.
```

## TASK_BREAKDOWN

```markdown
Current phase: TASK_BREAKDOWN

## Approved direction

Summarize the approved plan.

## Atomic tasks

### Task N - Title

Objective:
Describe the task goal.

Involved files/classes:
List known files/classes or say `to be identified during task`.

Depends on:
List previous task dependencies.

Expected result:
Describe the expected outcome.

Definition of done:
List concrete completion criteria.

Review focus:
Explain what will be reviewed.

Risk:
Low, medium, or high with short reason.

## Next step

Ask which task to start or whether to start Task 1.
```

## GUIDED_IMPLEMENTATION

```markdown
Current phase: GUIDED_IMPLEMENTATION

## Current task

State the task number and title.

## Objective

Explain what this task must achieve.

## Where to work

Name the relevant class, file, package, module, or layer.

## What to implement or modify

Describe required changes verbally.

## Important logic

Explain logic to add or change without raw code.

## Design reasoning

Explain why the change belongs there.

## Edge cases

List relevant edge cases.

## Tests or validation

Explain what to test or verify.

## Completion checklist

List conditions the user should satisfy before asking for review.

## Next step

Ask the user to implement the task and report back.
```

## CODE_REVIEW

```markdown
Current phase: CODE_REVIEW

## Review verdict

Use one of:
- APPROVED
- APPROVED_WITH_MINOR_NOTES
- REWORK_REQUIRED
- BLOCKED_NEEDS_MORE_CONTEXT

## What is correct

Explain what was implemented well and why.

## Issues found

For each issue:

Location:
Where the issue is.

Problem:
What is wrong or risky.

Why it matters:
Explain the impact.

Recommended correction:
Explain verbally how to fix it.

How to verify:
Explain what confirms the fix.

## Tests and validation

List tests to run, add, or update.

## Task status

Say whether the task is approved or requires rework.

## Next step

If approved, propose the next task. If not approved, ask the user to fix the current task and report back.
```
