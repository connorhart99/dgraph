# Bootstrap Log

## What was done

- Cloned the upstream Dgraph repository into this workspace.
- Created initial planning documents for the runtime-types fork.

## Why this structure

- `roadmap.md` tracks the implementation path.
- `agents.md` defines work ownership and guardrails.
- `agent-logs/` stores concise technical rationale and decision history.

## Important note

- These logs are design-rationale notes, not hidden private reasoning.
- They should capture decisions, assumptions, tradeoffs, and open questions in a reviewable form.

## Next suggested steps

- Map the current schema, query, GraphQL, and auth entry points.
- Decide where runtime descriptors should be stored and replicated.
- Define benchmark baselines before code changes.
