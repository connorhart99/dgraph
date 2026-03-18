# Architecture Direction

## Current direction

- Proceed with a forked-Dgraph exploration focused on native runtime types.
- Use UUID-backed type and field identity.
- Treat user-visible names as aliases only.

## Why this direction was chosen

- The goal requires runtime type creation without manual schema migration.
- Native resolution inside the query and mutation path gives the best chance of retaining Dgraph-like performance for hot workloads.
- A fork lets us explore deep planner and storage optimizations that are not available through a pure gateway approach.

## Known risks

- Long-lived fork maintenance burden is high.
- GraphQL compatibility for dynamic runtime types is likely the highest-risk subsystem.
- Runtime index creation can destabilize write latency without strong quotas and async activation.

## Guardrails

- Preserve existing static behavior where possible.
- Keep runtime schema metadata tenant-scoped and versioned.
- Avoid synchronous expensive index work on the request path.
