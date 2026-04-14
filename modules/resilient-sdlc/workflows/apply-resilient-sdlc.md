---
description: Apply SOLID and Impact Scope Reduction validations before writing code, deploying tasks, or performing system restarts to ensure maximum resilience.
---

# Workflow: Validate Resilient SDLC (SOLID + Impact Scope)

Use this workflow BEFORE modifying files, refactoring code, restarting services, or rolling out updates to ensure a high-quality SDLC.

### Step 1: Architectural Validation (Code Level)
- **Goal:** Ensure the proposed code change adheres to SOLID principles.
- **Action:** 
  - Does the change violate SRP? (Are we mixing unrelated domains in one file?) -> **If yes, refactor and decouple.**
  - Can we use OCP to add new interfaces/classes instead of heavily modifying legacy logic? -> **If yes, extend instead of mutate.**

### Step 2: Identify the Deployment Scope
- **Goal:** Determine exactly which files, modules, or services are logically modified.
- **Action:** List the specific components changed. Ensure you are not coupling unrelated deployments together.

### Step 3: Identify Disruption Impact (Impact Scope)
- **Goal:** Find out what resources will be affected by your planned deployment or restart strategy.
- **Action:** 
  - Will your restart command tear down the whole stack? (e.g., `docker-compose down && docker-compose up -d`) -> **VIOLATION**.
  - Are there Heavy Resources present (AI Models in VRAM, Databases, Caches) that would be needlessly restarted by your action? -> **VIOLATION**.

### Step 4: Localize and Execute the Update (Ops Level)
- **Goal:** Execute the most localized and decoupled update mechanism available.
- **Action:**
  - **Code:** Hot-reload if applicable.
  - **Docker/Virtual Machines:** Restart only the specific container (`docker restart <affected_container>`) or internal service (`docker exec <container> systemctl reload <service>`). 
  - **Binaries:** Overwrite the binary via volume mounts, then bounce just the executed process.

### Step 5: Verify Graceful Degradation
- **Goal:** Ensure the targeted service is back online while unrelated services maintain continuous uptime via Dependency Inversion.
- **Action:** Check the status of the specific module and ensure background processes or message queues handled the brief downtime smoothly without data loss.
