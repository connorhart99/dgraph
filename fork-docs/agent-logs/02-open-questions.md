# Open Questions

## Technical questions to resolve early

1. Where should runtime type descriptors live so they are strongly consistent and cheap to cache?
2. Which subsystems currently assume globally static schema state?
3. Can GraphQL support be safely deferred for runtime types in the MVP?
4. How should physical predicate ids be allocated and garbage-collected?
5. What is the activation contract for new indexes and promoted fields?
6. How do rolling upgrades behave if some nodes understand runtime descriptors and others do not?

## Security questions

1. What are the minimum schema-control privileges?
2. What quotas are required to prevent type and index explosion?
3. How is tenant identity enforced in cache keys, metadata lookups, and background jobs?

## Performance questions

1. What descriptor cache hit rate is required to keep query overhead negligible?
2. How much metadata churn can the cluster absorb without affecting unrelated tenants?
3. What worst-case traversal patterns should be part of the benchmark suite?
