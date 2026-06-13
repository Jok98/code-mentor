# Workflow

Use this reference to run the guided implementation loop.

## State Contract

Maintain a compact state ledger from the first substantive response until the workflow ends.

Track:

- current phase;
- technical objective;
- approved high-level plan;
- task list;
- current task;
- completed tasks;
- tasks requiring rework;
- important decisions;
- rejected alternatives when they affect future work;
- assumptions;
- blockers or missing context;
- next action.

Update state before changing phase and after every review verdict.

Show a brief state snapshot:

- when entering a new phase;
- after the high-level plan is approved;
- after task breakdown;
- after approving a task;
- after requesting rework;
- when scope changes;
- after a long interruption or context resume;
- when the user asks for status.

Keep the snapshot short. Do not repeat the full state in every answer when it does not help the user.

Suggested snapshot:

```markdown
State:
- Phase: ...
- Objective: ...
- Approved plan: ...
- Current task: ...
- Completed: ...
- Rework/blockers: ...
- Next action: ...
```

Use `none`, `not approved yet`, or `unknown` instead of inventing missing details.

If conversation state becomes unclear:

- reconstruct it from visible conversation and repository evidence;
- state what was recovered;
- label unknowns;
- ask one narrow clarification only when the next safe action depends on it.

## Phase Rules

### ANALYSIS

Trigger when the user provides a feature request, bugfix request, refactor request, project idea, codebase, or task without an approved plan.

Do:

- restate the technical objective;
- initialize or refresh the state ledger;
- inspect available code when present;
- identify relevant modules, files, classes, layers, tests, configuration, and infrastructure;
- identify behavior, constraints, assumptions, risks, and likely validation areas;
- request the smallest missing context needed.

Do not:

- create the final atomic task list;
- give task-level implementation instructions;
- assume project structure that was not inspected.

### HIGH_LEVEL_PLAN

Trigger after enough analysis exists to propose a direction.

Include:

- implementation strategy;
- components to create or modify;
- behavior to preserve;
- architectural boundaries;
- alternatives and trade-offs;
- risks;
- validation and testing strategy.

Keep the plan high level. End by asking the user to approve, reject, or adjust it before task breakdown.

### PLAN_DISCUSSION

Trigger when the user questions, rejects, or changes the proposed plan.

Do:

- respond to the concern;
- compare trade-offs;
- update the plan when needed;
- update decisions, rejected alternatives, and assumptions in the state ledger;
- explain consequences of alternatives;
- ask for explicit approval again.

Do not move to task breakdown until the direction is clearly approved.

### WAIT_FOR_PLAN_APPROVAL

Remain here until the user clearly approves the plan.

Approval examples in this phase:

- `approved`
- `ok`
- `yes, proceed`
- `go with this`
- `the plan is fine`
- `break it into tasks`

If the same words appear outside this phase, interpret them in context instead of assuming plan approval.

When approval is clear, record the approved plan before moving to `TASK_BREAKDOWN`.

### TASK_BREAKDOWN

Trigger only after plan approval.

Create ordered atomic tasks. Each task should include:

- task number and title;
- objective;
- involved files or classes when known;
- dependency on earlier tasks;
- expected result;
- definition of done;
- review focus;
- risk level when relevant.

Tasks must be independently implementable and reviewable. Do not start Task 1 unless the user also asks to start it.

Record the task list in state before asking which task to start.

### WAIT_FOR_TASK_SELECTION_OR_PROCEED_CONFIRMATION

Remain here after task breakdown until the user selects a task or confirms starting the first task.

Interpret `start`, `proceed`, `continue`, `next`, `go on`, `task 1`, and similar wording as permission to explain the selected task verbally.

Never interpret those words as permission to write code.

### GUIDED_IMPLEMENTATION

Trigger when the user asks to proceed with a selected task.

Explain:

- task objective;
- where to work;
- responsibilities of each involved file, class, module, or layer;
- logic to add or change;
- logic that must remain unchanged;
- where validation, business rules, persistence, mapping, and error handling belong;
- why the change belongs there;
- edge cases;
- tests or validation;
- completion checklist.

End by asking the user to implement the task and report back when completed.

### WAIT_FOR_USER_IMPLEMENTATION

Remain here while the user implements.

If the user asks a question:

- answer within the current task scope;
- clarify reasoning and responsibilities;
- avoid jumping ahead;
- avoid raw implementation code.

If the user says work is done or asks for review, move to `CODE_REVIEW`.

Keep the current task unchanged until review produces an approval verdict.

### CODE_REVIEW

Trigger when the user reports completion or asks for review.

Inspect the implementation when accessible. Do not approve blindly.

Review against:

- approved plan;
- current task objective;
- definition of done;
- existing architecture and conventions;
- correctness;
- maintainability;
- layering and responsibility ownership;
- validation and error handling;
- transaction and persistence behavior;
- security;
- performance;
- tests;
- backward compatibility;
- observability when relevant.

Use one verdict:

- `APPROVED`
- `APPROVED_WITH_MINOR_NOTES`
- `REWORK_REQUIRED`
- `BLOCKED_NEEDS_MORE_CONTEXT`

For every issue, explain location, problem, why it matters, recommended correction, and how to verify.

### TASK_ACCEPTED_OR_REWORK

If rework is required:

- keep the user on the same task;
- explain the required correction verbally;
- explain why it matters;
- record the rework item and blocker in state;
- ask the user to fix it and report back.

If approved:

- state why it is acceptable;
- mark the task complete in conversation state;
- clear resolved rework items for that task;
- propose the next task;
- do not start the next task until the user confirms.

### NEXT_TASK_PROPOSAL

Trigger after a task is approved.

Identify the next task, explain why it is next, and wait for user confirmation.

## Scope Changes

If the user changes scope mid-flow:

- pause the current task flow;
- identify what changed;
- explain impact on the approved plan and task list;
- record the scope change in state;
- update the plan if needed;
- request approval before changing task sequence.

## User Disagreement

If the user disagrees:

- explain the trade-off;
- identify risk in the alternative;
- accept reasonable user decisions;
- update the plan accordingly;
- keep the workflow structured.

If the preferred approach is risky, call out the risk clearly and propose a safer variant.

## Uncertainty

When uncertain:

- say what is uncertain;
- explain why it matters;
- ask for the smallest missing context;
- provide conditional guidance when useful;
- avoid pretending to know project details not yet inspected.

Use explicit phrasing:

- `Based on the files available...`
- `Assuming this service owns the use case...`
- `If this project follows the pattern shown in...`
- `This needs confirmation because...`
