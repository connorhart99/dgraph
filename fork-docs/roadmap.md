# Runtime Types Fork Roadmap

## Goal

Fork Dgraph so tenants can create runtime user-defined types safely, without manual schema migrations, while preserving performance, security, and multi-tenant isolation.

## Principles

- Type identity is UUID-backed, not name-backed.
- User-defined names are aliases only and never become raw physical predicate names.
- Schema changes are metadata operations with quotas, policy checks, and versioned activation.
- Query and mutation paths must resolve type metadata from caches, not from full schema scans.
- Index creation is asynchronous and bounded by tenant and cluster policy.

## Phase 0: Baseline and Discovery

- Stand up the fork and confirm local build and test workflow.
- Map Dgraph subsystems involved in schema, query planning, GraphQL, auth, posting lists, and admin APIs.
- Define success metrics for runtime type creation, query latency, write latency, and index build impact.
- Establish fork hygiene: branch strategy, upgrade policy, and architectural decision records.

## Phase 1: Control Plane Foundations

- Add tenant-scoped `TypeDef` and `FieldDef` metadata models.
- Add UUID allocation for types and fields.
- Add versioned descriptor storage and descriptor epoch invalidation.
- Add admin APIs for create, update, deprecate, and inspect runtime types.
- Add quotas and rate limits for type creation, field creation, and index promotion.

## Phase 2: Query and Mutation Resolution

- Implement compiled descriptor caches keyed by tenant, type UUID, and version.
- Add request-time resolution from logical field names to physical predicate ids.
- Validate mutations against compiled descriptors before posting list writes.
- Add negative caching for unknown types and fields.
- Ensure all caches and lookups are tenant-scoped.

## Phase 3: Storage and Index Lifecycle

- Introduce internal physical predicate allocation for runtime fields.
- Add base index rules for essential lookups.
- Add asynchronous index promotion and backfill workflow.
- Add status transitions for field/index activation.
- Add rollback-safe descriptor version cutover.

## Phase 4: Security and Isolation

- Extend ACL/auth paths with schema-control privileges.
- Enforce safe defaults: private types, unindexed fields, no cross-tenant edges by default.
- Add schema abuse protections for type explosion, field explosion, and expensive index requests.
- Add audit logs for all runtime schema operations.

## Phase 5: API Compatibility

- Preserve existing static GraphQL and DQL behavior.
- Add a runtime-type API path first; avoid deep dynamic GraphQL generation in the MVP.
- Define compatibility rules for legacy static types and new UUID-backed types.

## Phase 6: Validation and Launch

- Benchmark runtime type creation under multi-tenant load.
- Benchmark deep traversals, mixed hot/cold fields, and high-cardinality edges.
- Run isolation, abuse, and failover tests.
- Publish go/no-go criteria for production rollout.

## Initial Deliverables

- Type registry design doc
- Descriptor cache design doc
- Admin API spec
- Security model and quota policy
- Benchmark plan and acceptance criteria
