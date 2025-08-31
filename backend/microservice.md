# LLM Prompt Policy
✅ **This template must be reviewed and updated before merging new features.**

---
### Source documentation
Any original research paper, website, book.. to know as a pre-requisite for this work
* TBD

---
### Framework Stack

* **Language & version**: `TBD` (e.g., Go 1.24, Python 3.13, Java 21).
* **Frameworks & libraries**:

  * `TBD` (e.g., `gin-gonic v1.10`, `grpc-go v1.62`, `aws-sdk-go v1.50.2`)
  * Specify exact versions for reproducibility (go.mod, poetry toml..).
  * Use official or well-maintained libraries.
  * Avoid deprecated or unmaintained packages.

---

### Running Architecture

* **Deployment mode**: `TBD` (e.g., helm chart in GitHub Release page).
* **Runtime context**: `TBD` (e.g., Linux node being part of AKS v1.32.5, with 32GB of RAM DDR5, Intel core I7 8 cores, SSD NVMe disk with 300GB available).
* Ensure platform-specific configurations are documented.
* Define scaling strategy (e.g., HPA, cluster autoscaler).
* Document resource constraints (CPU/memory).

---
### Resource constraints
* Time limits: TBD
* Memory limits: TBD
* CPU/vCPU: limits: TBD
* Database/Storage limits: TBD

---
### Application Context

* **Project description**: `TBD` (brief summary of the app and its main business goals).
* **Integration point**: `TBD` (where the requested feature/function will plug in).
* Ensure the new code aligns with the app’s goals.
* Avoid duplication of existing logic.
* Respect architectural boundaries (DDD, layers, hexagonal, etc.).

---

### Security

* **Auth protocol**: `TBD` (e.g., OAuth2, JWT, mTLS).
* **Secrets management**: Secrets **must only** come from environment variables or secret stores.
* No hardcoded secrets.
* Enforce secure defaults (TLS, HTTPS).
* Adopt Secure Software Development Lifecycle (SSDLC).
* Follow language-specific security best practices.
* Any Requirements for handling PII, GDPR, or other regulatory compliance?

---

### Clean Coding

  * Keep functions short and focused.
  * The `main` function should be minimal (no business logic).
  * Separate complex logic into dedicated packages/modules.
  * Implement **SAST** in CI/CD pipeline.
  * Enforce formatting, linting, and validation tools.
  * Avoid redundant or duplicate code.
  * Check for race conditions
  * Check for undesired side effects on managed data structures

---

### Naming Conventions

`TBD` (if none, follow the language’s official conventions).

  * Consistent naming across files, packages, variables, and functions.
  * Use meaningful and descriptive identifiers.
  * Avoid abbreviations unless widely accepted in the language ecosystem.

---

### Interfaces

* **Expected function signature**:
TBD
  ```go
  // Example in Go:
  func (r *CronJobReconciler) Reconcile(ctx context.Context, req ctrl.Request) (ctrl.Result, error)
  ```

* Clear, strongly typed interfaces.
* Explicit error handling.
* Avoid leaking internal structures outside public interfaces.

---

### Protocols

* **Expected used protocols**: `TBD` (e.g., REST, gRPC, GraphQL, Kafka).

  * Document supported protocols.
  * Validate input/output at protocol boundaries.
  * Enforce versioning for backward compatibility.

---

### Input Sample
TBD

```json
// Example:
{
  "user_id": "12345",
  "action": "create_order",
  "payload": {
    "item_id": "sku-987",
    "quantity": 2
  }
}
```

---

### Output Sample
TBD
```json
// Example:
{
  "status": "success",
  "order_id": "ORD-2025-0001",
  "timestamp": "2025-08-30T10:15:00Z"
}
```

---
### CI/CD
TBD
* Upstream: GitHub actions
* Local: Makefile

### Unit Tests

* **Coverage goal**: ≥ 80% of code.

  * Cover normal and edge cases.
  * Mock external dependencies.
  * Include failure and retry scenarios.
  * Run tests automatically in CI.

---
### AI/ML
* AI models, model versioning, and bias testing: TBD

---

### Optimization Suggestions
Focus first on the goals above and leave as suggestions for next prompt iterations the following points:

* Decouple external dependencies where possible.
* Introduce caching for repeated calls.
* Implement resilience against network latency/failures (e.g., retries, backoff, circuit breakers).
* Provide consistent and configurable logging.
* Expose metrics APIs for observability.
* Use concurrency safely and only when beneficial.

---

### Documentation
Require inline code comments, API documentation, and README updates for new features.

---
### **PROMPT**
TBD
