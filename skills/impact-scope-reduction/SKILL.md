---
name: impact-scope-reduction
description: Reduce change blast radius across code and operations using SOLID, change isolation, risk-based testing, and targeted deployments. Use when a request involves SOLID or architecture coupling and cohesion, shared contracts or data changes, or deployment and restart plans that could disrupt unrelated, stateful, or expensive resources. Do not use for isolated low-risk edits with no architectural or operational impact.
---

# Impact Scope Reduction

Limit the impact scope at every layer:

- Cohesive code limits the spread of bugs.
- Focused tests limit unnecessary CI work while protecting changed contracts.
- Targeted deployments limit service disruption and preserve unrelated state.

## Workflow

1. Identify the environment and exact files, modules, services, data, and contracts affected by the request.
2. Trace their callers and dependencies. Note stateful or expensive resources such as databases, caches, queues, and AI models held in GPU memory.
3. Apply SOLID as change-isolation criteria: keep responsibilities cohesive and dependencies narrow, but do not add speculative interfaces, services, or extension points merely to claim compliance.
4. Start with focused tests, then expand according to risk. Shared contracts, schemas or migrations, authentication, authorization, concurrency, backward compatibility, and data-integrity changes require the relevant integration or end-to-end coverage.
5. Choose the smallest deployment unit that contains the change:

   - In development, use hot reload when supported.
   - In production, prefer the platform's supported graceful reload, rolling update, canary, or blue-green mechanism with rollback ready.
   - Restart only the affected service or container when its contracts and dependencies allow independent rollout.
   - Coordinate a wider rollout when shared schemas, configuration, protocols, or libraries require it.
   - Avoid tearing down or force-recreating an entire stack unless the change requires it or the request explicitly asks for it.
   - Do not restart databases, caches, queues, or model-serving processes for an unrelated lightweight service change.

6. Verify the changed service is healthy and that dependent and unrelated services remained available. Check queues or graceful-degradation paths when brief downtime is possible.

## Safety

- Obtain authorization before mutating live infrastructure.
- Preserve data integrity, access controls, observability, compatibility, and a tested rollback path proportional to the risk.
- If the localized operation cannot apply the change safely, explain the wider required scope before executing it.
