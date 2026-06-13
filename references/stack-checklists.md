# Stack Checklists

Read only the sections relevant to the task.

## Generic Engineering

Apply across languages and frameworks:

- keep responsibilities clear;
- avoid hidden coupling;
- avoid unnecessary abstraction;
- avoid duplicating business rules;
- keep input validation near system boundaries;
- keep business logic in domain or application layers, not transport-specific layers;
- keep persistence concerns isolated;
- isolate external integrations behind clear boundaries;
- prefer small, testable units;
- make side effects explicit;
- preserve backward compatibility unless explicitly changing it;
- consider failure modes, security, and observability.

## Java And Spring Boot

Use existing architecture and conventions first.

Layering:

- keep controllers thin;
- put business logic in services, application layer, or domain layer according to the project;
- keep repositories focused on persistence;
- avoid repositories directly from controllers;
- use DTOs for API input and output when the project does;
- avoid leaking JPA entities through API responses unless intentional;
- keep mapping explicit and consistent.

Controllers should:

- receive HTTP requests;
- trigger boundary validation;
- delegate to services or use cases;
- map results to HTTP responses;
- avoid business decisions and persistence logic.

Services or application layer should:

- own use case orchestration;
- coordinate repositories and domain logic;
- define transaction boundaries;
- enforce application-level rules;
- call external integrations through abstractions;
- return results suitable for API mapping.

Domain logic should:

- express business rules;
- protect state transitions;
- avoid framework-specific dependencies when possible;
- avoid being scattered across controllers or unrelated services.

Repositories should:

- hide persistence details;
- expose intent-oriented queries;
- avoid business decisions;
- avoid returning broad data when a specific query is needed.

Validation placement:

- syntactic request validation at boundaries;
- business validation in service or domain logic;
- persistence constraints in the database;
- cross-field validation where project convention supports it.

Transaction review:

- write operations;
- multi-entity updates;
- lazy loading;
- consistency;
- rollback behavior;
- external calls inside transactions;
- optimistic locking;
- idempotency.

Common review issues:

- fat controllers;
- repositories used directly by controllers;
- DTOs containing business logic;
- entities exposed directly by accident;
- transaction boundaries in the wrong layer;
- duplicated business rules;
- inconsistent exception handling;
- unpredictable validation split;
- tests that only check happy paths;
- mocks hiding persistence or mapping risks.

## Microservices

Consider:

- service boundaries and data ownership;
- synchronous versus asynchronous communication;
- API contracts and backward compatibility;
- idempotency;
- retries, timeouts, and circuit breakers;
- message ordering and duplicates;
- eventual consistency;
- observability, correlation IDs, and tracing;
- failure isolation;
- deployment impact.

Do not introduce distributed complexity unless the feature actually requires it.

## Docker And Kubernetes

Consider:

- environment variables;
- secrets and config maps;
- health checks;
- readiness and liveness probes;
- resource limits;
- startup order;
- networking and service discovery;
- persistence;
- migrations;
- rollout and rollback;
- logs and metrics.

Avoid changing deployment behavior unless necessary for the task.

## Frontend

Apply equivalent responsibility boundaries:

- keep UI components focused;
- separate state management from rendering when useful;
- isolate API access;
- validate inputs at boundaries;
- preserve accessibility;
- handle loading, error, empty, and success states;
- avoid duplicating backend business rules unless required;
- test important user flows;
- review usability and maintainability.

## Database

Consider:

- schema migrations;
- backward compatibility;
- data migration;
- indexes;
- constraints;
- nullable versus non-nullable fields;
- default values;
- locking;
- transaction safety;
- rollback strategy;
- performance impact;
- validity of existing data.

Do not suggest destructive migrations without explicitly discussing risk.

## Security

Review for:

- authorization;
- authentication boundaries;
- input validation;
- injection risks;
- sensitive data exposure;
- logging of secrets;
- insecure defaults;
- unsafe deserialization;
- dependency or integration risks;
- privilege escalation;
- multi-tenant data isolation.

Treat serious security risk as blocking.

## Performance

Review for:

- unnecessary database queries;
- N+1 query patterns;
- inefficient loops over large datasets;
- missing indexes;
- excessive memory use;
- blocking calls;
- repeated external calls;
- unnecessary serialization;
- cache consistency risks.

Do not over-optimize without evidence.

## Refactoring

For refactoring tasks:

- identify the current pain point;
- define the target structure;
- preserve behavior;
- break the refactor into safe steps;
- recommend characterization tests when behavior lacks coverage;
- avoid mixing refactor and feature changes unless planned;
- review that behavior remains equivalent.

## Bugfix

For bugfix tasks:

- reproduce or understand the bug;
- identify expected versus actual behavior;
- locate the smallest responsible area;
- explain root cause;
- propose a minimal safe fix;
- add or update regression tests;
- verify the fix does not mask symptoms while leaving root cause intact.

## Greenfield

For new projects:

- clarify goals and constraints;
- identify core domain concepts;
- define architecture at a practical level;
- avoid unnecessary complexity;
- propose incremental milestones;
- create atomic implementation tasks;
- define validation criteria per milestone;
- keep the user responsible for implementation.
