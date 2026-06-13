# Inspection And Review

Use this reference when analyzing a repository or reviewing user changes.

## Repository Inspection

When code is available, inspect before planning.

Start with low-cost orientation:

- check working tree status;
- list files with `rg --files` when available;
- inspect package manifests, build files, route declarations, module boundaries, tests, and configuration;
- search for the domain terms in the user request;
- read the smallest set of files needed to understand ownership and data flow.

Prefer repository evidence over assumptions. If the project has conventions, follow them.

Do not ask for the whole project when only specific context is missing. Ask for exact files, logs, diffs, schemas, API contracts, stack traces, or tests.

## Analysis Checklist

During analysis, identify:

- technical objective;
- expected behavior;
- current behavior when relevant;
- affected layers and modules;
- likely owners of the use case;
- data model and persistence impact;
- external integration impact;
- validation and authorization boundaries;
- error handling expectations;
- concurrency, idempotency, or migration risks;
- test surfaces;
- unknowns that affect planning.

## Review Inspection

When the user asks for review:

- inspect current `git status` or equivalent changed-file view;
- inspect diffs for files relevant to the current task;
- read nearby code needed to understand context;
- inspect tests added or changed;
- run or request relevant validation only when it fits the environment and the user's workflow.

Do not review only the changed lines if surrounding code determines correctness.

## Review Criteria

Review for:

- fit with approved plan and task objective;
- correctness of behavior;
- responsibility ownership;
- architecture and layering;
- maintainability and readability;
- validation placement;
- error handling and error mapping;
- transaction and persistence consistency;
- backward compatibility;
- security and authorization;
- performance and query behavior;
- tests and regression coverage;
- consistency with project conventions.

## Verdicts

Use exactly one:

- `APPROVED`: the task meets the definition of done.
- `APPROVED_WITH_MINOR_NOTES`: the task can move forward; notes are non-blocking.
- `REWORK_REQUIRED`: blocking issues must be corrected before moving forward.
- `BLOCKED_NEEDS_MORE_CONTEXT`: review cannot be completed because needed code or information is unavailable.

## Issue Format

For every issue, include:

- `Location`: file, class, method, route, test, or configuration area.
- `Problem`: what is wrong or risky.
- `Why it matters`: impact on behavior, maintainability, security, data, or operations.
- `Recommended correction`: verbal correction, not a patch.
- `How to verify`: test, scenario, command, or inspection that confirms the fix.

## Approval Discipline

Do not approve a task just because it compiles or because the implementation resembles the plan.

Approve only when the implementation:

- satisfies the objective;
- preserves required behavior;
- keeps responsibilities in the right place;
- has no known blocking correctness, data, or security issues;
- has appropriate tests or a clear validation path.

## Missing Context

If code cannot be inspected, ask for the smallest useful context.

Good request:

`To review this correctly, I need the changed service file, the controller or entry point that calls it, and the tests you added for invalid state transitions.`

Poor request:

`Send me the whole project.`
