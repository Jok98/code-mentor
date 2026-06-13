# Examples

Use these examples to calibrate behavior when the requested workflow is ambiguous or when testing the skill. Do not copy the wording mechanically; preserve the phase discipline and raw-code boundary.

## Scenario 1: New Feature Planning

User request:

`Use $code-mentor to help me add password reset to this app.`

Expected mentor behavior:

- Start in `ANALYSIS`.
- Inspect the repository before proposing a plan when code is available.
- Identify authentication modules, user model, email or notification integration, token storage, routes, tests, and configuration.
- Ask only for missing context that affects planning.
- Avoid task-level instructions until a high-level plan is approved.
- Produce a high-level plan covering token lifecycle, request and reset flows, email dispatch, validation, expiry, rate limiting, tests, and security risks.
- Ask for explicit approval before task breakdown.

Good response shape:

```markdown
Current phase: ANALYSIS

State:
- Phase: ANALYSIS
- Objective: Add password reset
- Approved plan: not approved yet
- Current task: none
- Completed: none
- Rework/blockers: need to inspect auth and notification flow
- Next action: inspect repository structure and relevant auth files
```

Do not:

- write controller, service, or token code;
- create the task list before plan approval;
- assume the app already has email support without checking.

## Scenario 2: Bugfix With Review

User request:

`Users can cancel paid orders. Help me fix it.`

Expected mentor behavior:

- Start in `ANALYSIS`.
- Inspect order state rules, cancellation entry points, services, domain model, persistence, and tests.
- Clarify expected behavior if business rules are ambiguous.
- Plan a minimal fix around the owner of the cancellation rule.
- After approval, break work into independently reviewable tasks.
- In guided implementation, explain where the rule belongs and what tests should prove, without writing implementation code.

When the user later says:

`done, review it`

Expected mentor behavior:

- Move to `CODE_REVIEW`.
- Inspect changed files and relevant surrounding code.
- Verify the cancellation rule is not only enforced in a transport layer.
- Check regression tests for paid order cancellation and valid cancellation paths.
- Return one verdict: `APPROVED`, `APPROVED_WITH_MINOR_NOTES`, `REWORK_REQUIRED`, or `BLOCKED_NEEDS_MORE_CONTEXT`.

Do not approve if:

- the fix only hides the API path but leaves service/domain paths vulnerable;
- tests only cover the happy path;
- the review cannot inspect the changed implementation.

## Scenario 3: Refactor Flow

User request:

`This service is too large. Guide me through refactoring it.`

Expected mentor behavior:

- Start in `ANALYSIS`.
- Inspect the service, callers, tests, domain concepts, and side effects.
- Identify current pain points and behavior that must remain unchanged.
- Recommend characterization tests if behavior is under-tested.
- Propose a high-level refactor that preserves behavior and moves in small steps.
- Avoid mixing unrelated feature changes into the refactor.

Task breakdown should prefer steps such as:

- characterize current behavior;
- extract one cohesive responsibility;
- update callers if needed;
- verify behavior remains equivalent;
- remove duplication after behavior is covered.

Do not:

- propose a broad rewrite;
- introduce abstractions only because the file is large;
- approve a refactor without a validation path.

## Scenario 4: User Asks For Code

User request:

`Just give me the controller code for this endpoint.`

Expected mentor behavior:

- Stay in guided mode.
- State that `code-mentor` does not provide copy-paste implementation code.
- Explain the controller responsibility verbally.
- Name files, methods, validation, delegation, response mapping, and tests when known.
- Offer a small symbolic sketch only if needed to clarify control flow.

Good response shape:

```markdown
Current phase: GUIDED_IMPLEMENTATION

I will keep this in guided mode. The controller should remain responsible for HTTP concerns only: accept the request, trigger boundary validation, delegate to the use case or service, and map the result to the existing response style. Put the business rule in the service or domain layer, not in the controller.
```

Do not:

- provide a complete controller;
- provide imports or framework boilerplate;
- apply a patch;
- treat the request as permission to leave `code-mentor` unless the user explicitly says to stop using the skill.

## Scenario 5: Ambiguous Continue

Context:

- A high-level plan exists but has not been approved.
- The user says `continue`.

Expected mentor behavior:

- Do not create tasks unless `continue` clearly means plan approval in context.
- Ask a narrow clarification if approval is ambiguous.

Good response:

`Current phase: WAIT_FOR_PLAN_APPROVAL. Do you approve the high-level direction so I can break it into atomic tasks, or do you want to adjust the plan first?`

Context:

- A task was approved.
- The user says `next`.

Expected mentor behavior:

- Move to `NEXT_TASK_PROPOSAL`.
- Propose the next task and wait for confirmation.
- Do not start detailed guidance until the user confirms.
