# Go 1.25 Production Pull Request Guidelines

These guidelines define what “high‑quality Go production code” means for this repository.
Reviewers and automation should evaluate new pull requests against the principles below.

## 1. Keep `main` thin, logic in packages

- Restrict `main` packages to configuration, wiring, and process lifecycle (startup, shutdown, signal handling).
- Place business logic in importable packages so it can be tested, reused, and composed in other binaries or tools.

## 2. Follow idiomatic Go style

- Follow Effective Go and the standard library for naming, error handling, and control flow; avoid importing patterns from other languages.
- Less code is better.
- Enforce `gofmt`, `go vet`, and a linter (eg: docker image at golangci/golangci-lint:latest-alpine) in CI so style is consistent and not debated during review.

## 3. Prefer small, cohesive APIs

- Keep packages and interfaces narrowly focused; start unexported and export only when real external consumers exist.
- Avoid “god” packages and overly generic interfaces that make the codebase hard to navigate and refactor.

## 4. Handle errors explicitly and with context

- Return `error` and always check it; do not use panics for normal control flow or expected failures.
- Wrap errors with useful context and rely on `errors.Is` / `errors.As` instead of string matching.

## 5. Use `context.Context` on long‑running and I/O paths

- Accept `context.Context` as the first argument in any function that performs I/O, RPCs, or may block.
- Propagate contexts through all layers and ensure they carry deadlines or timeouts where appropriate.

## 6. Treat concurrency as a design concern

- Make ownership and lifetime of data and goroutines explicit and easy to reason about.
- Use well‑defined worker patterns and channels rather than spawning ad‑hoc goroutines without clear responsibilities.

## 7. Prevent goroutine and resource leaks

- Close files, network connections, and response bodies with `defer` immediately after successful acquisition.
- Ensure every goroutine has a termination path (context, done channel, or `WaitGroup`) and verify shutdown behavior in tests.

## 8. Write fast, deterministic tests (including concurrency)

- Keep tests small, fast, parallel and deterministic;
- Structure tests so they can run reliably in CI, without depending on timing or external state;
- Use property based tests and behavior based tests, don't test only functions "blindly".

## 9. Run the race detector and fix races

- Use `go test -race ./...` for important packages and before releases where feasible.
- Fix data races before merging; do not accept pull requests with known races into production branches.

## 10. Ensure observability: logs, metrics, traces

- Use structured logging with consistent fields (for example, request IDs) so production behavior is easy to inspect.
- Expose metrics and, where relevant, traces for latency, error rates, and resource usage to support debugging in live environments.

## 11. Profile and optimize using real data

- Use profiling tools (CPU, memory, and blocking profiles) to find hotspots rather than guessing where to optimize.
- Only apply optimizations that are justified by measurements and keep code readable after optimization.

## 12. Respect container and environment constraints

- Allow the runtime to adapt to container CPU limits (for example through `GOMAXPROCS` behavior) instead of hard‑coding CPU counts.
- Stream large payloads and reuse buffers where possible, avoiding unbounded memory growth in long‑lived services.

## 13. Use Go 1.25 features deliberately

- Treat new or experimental features in Go 1.25 (https://go.dev/doc/go1.25) as opt‑in and roll them out gradually.
- Track and apply Go 1.25 patch releases to benefit from bug fixes and security updates in the runtime and standard library.

## 14. Externalize configuration and protect secrets

- Keep configuration in environment variables or configuration files, not hard‑coded constants.
- Store secrets in dedicated secret‑management systems and never commit them to the repository.

## 15. Automate development workflow with Makefile

- Centralize workflow in a Makefile. Use these Makefile targets from the GitHub actions too.
- Use docker images instead of binaries wherever possible.

## 16. Automate deployment, health checks, and rollbacks

- Provide health and readiness endpoints and ensure they accurately reflect service status.
- Support safe rollouts and quick rollbacks so new Go changes can be deployed frequently with low operational risk.
- Use git stash or commits to help me rollback between your major changes

## 17. Security

- Validate proposed code against defensive coding principles and OWASP top 10 (https://owasp.org/Top10/2025/0x00_2025-Introduction/).

***

Extra references: 

- https://go-proverbs.github.io/
