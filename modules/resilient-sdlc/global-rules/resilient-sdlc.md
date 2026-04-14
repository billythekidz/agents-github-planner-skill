# Resilient SDLC: SOLID & Impact Scope Reduction

## Core Philosophy
Achieving zero-downtime and highly maintainable systems requires a unified approach connecting code-level architecture (SOLID) to operations (Impact Scope Reduction). 
- **SOLID Principles** limit the *impact scope of bugs* when changing code.
- **Impact Scope Reduction** limits the *impact scope of deployments and infrastructure failures* when deploying that code.

## Application Across the SDLC Pipeline:

### 1. Development & Code Architecture (SOLID Focus)
- **Single Responsibility (SRP):** Write highly cohesive modules. A module should have one reason to change, minimizing the chance of breaking unrelated features in the codebase.
- **Open/Closed (OCP):** Extend functionality with new code rather than modifying battle-tested legacy logic. This prevents regressions from spreading natively.

### 2. Testing (CI/CD Integration)
- **Interface Segregation (ISP) for Testing:** Component separation allows for isolated testing. If a frontend component changes, only run frontend tests. Avoid massive End-to-End backend reruns unless API contracts change.

### 3. Deployment & Operations (Impact Scope Reduction Focus)
- **Single Responsibility in Deployments:** Emulate SRP in infrastructure. Microservices or Containers should run single processes. If an image processor needs an update, only restart the image processor container, not the database.
- **Targeted Reloads:** Prioritize `docker restart <container>` or hot-reloading inside the container via `docker exec`. NEVER tear down (`--force-recreate`) an entire stack unless explicitly requested.
- **Protect Heavy Resources:** Isolate stateful or heavily loaded nodes (e.g., AI models in VRAM, databases with high connection counts). Modifying a lightweight API should never force an LLM or Database to restart and flush its memory/connections.

### 4. Maintenance & Scalability (Dependency Inversion Focus)
- **Dependency Inversion (DIP) in Infrastructure:** Services should communicate via abstractions (Message Queues like Kafka/RabbitMQ or Load Balancers). When a service gracefully restarts, queues hold the requests, ensuring zero data loss and buffering the deployment's impact scope.
