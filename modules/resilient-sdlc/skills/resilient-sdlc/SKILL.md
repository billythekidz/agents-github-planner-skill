---
name: resilient-sdlc
description: Deep operational and architectural knowledge connecting SOLID code principles with DevOps Impact Scope Reduction to minimize system disruptions.
---

# Skill: Resilient SDLC (SOLID & Impact Scope Reduction)

## Understanding the Concept
To produce truly robust systems, software development and DevOps cannot exist in silos. The philosophy of "Decoupling" and "Limiting Dependencies" bridges both domains:
- **SOLID Principles:** Limits the *impact scope of bugs* when building and refactoring code.
- **Impact Scope Reduction:** Limits the *impact scope of deployments and infrastructure failures* during operations.

By combining them, the agent acts as an elite Full-Stack/DevOps Engineer, never applying brute-force "turn it off and on again" approaches, nor tangling codebases into fragile monoliths.

## Practical Execution Examples Across the SDLC

### 1. Codebase Architecture (SOLID)
- **Bad:** Writing a gigantic `Utils.ts` containing database connections, UI helpers, and API routing. (Violates SRP, high impact scope on edits).
- **Good:** Breaking `Utils` into domain-specific modules. Changing a UI helper will confidently have exactly zero impact on database connections.

### 2. Dependency Management & Testing
- **Bad:** Running `npm update` globally, which blindly updates all loose dependencies, potentially introducing breaking changes across the board.
- **Good:** Isolating the dependency change (e.g., `npm install lodash@latest`), and running component-specific tests rather than rebuilding the entire end-to-end test suite matrix unnecessarily.

### 3. Deployments & Operations (Impact Scope Reduction)
- **The Core Goal:** If only a small feature scope is modified, you must exclusively reload the exact corresponding software module.
- **Avoid Global Tear-downs:** Emulate SRP on the infrastructure level. Completely avoid tearing down the entire stack (e.g., `docker-compose down`).
- **Protect Heavy Resources:**
  - *AI/ML Models:* Reloading an AI container flushes the GPU VRAM, interrupting running jobs and requiring minutes to reload tens of gigabytes of weights into memory.
  - *Databases/Caches:* Restarting these drops active connections and flushes memory caches, causing a massive cold-start performance spike.
- **Execution:**
  - Update exactly what is needed via targeted compiled binaries or isolated volume mounts.
  - Execute localized restart commands: `systemctl reload <service>`, `supervisorctl restart <app>`, or `docker restart <specific_single_container>`.

### 4. Infrastructure Resilience (DIP & ISP)
- **Concept:** Instead of services crashing when a dependency reboots, utilize Message Queues (Kafka) or Load Balancers to queue requests. This is the operational equivalent of Dependency Inversion, absorbing the impact scope so users do not experience failures during microservice restarts.

## Agent Directives
When asked to write code, deploy, update, or restart services, you MUST:
1. Apply SOLID to ensure code components are highly cohesive and decoupled.
2. Evaluate the deployment ecosystem to identify heavy resources and dependencies.
3. Apply Impact Scope Reduction by using the most specific, targeted command available to deploy or restart strictly the modified modules without affecting the overall application state.
