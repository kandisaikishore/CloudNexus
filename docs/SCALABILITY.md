# Scalability baseline

## Priorities
- Make API/service instances stateless wherever practical; externalize shared sessions, caches, locks, and scheduled jobs before adding replicas.
- Configure bounded connection pools, startup/readiness/liveness checks, graceful shutdown, and request/upstream timeouts for applicable services.
- Use queues with bounded concurrency and retry policies for long-running tasks; make task handlers idempotent.
- Define resource requests/limits and autoscaling signals from measured CPU, memory, request latency, and queue lag rather than arbitrary thresholds.
- Store secrets in deployment secret managers and separate development, staging, and production configuration.
- Add CI validation, dependency/security checks, deployment smoke tests, rollback procedures, and infrastructure cost controls.

## Load validation
Run normal, peak, and burst scenarios. Measure throughput, p95/p99 latency, error rate, saturation, queue lag, and cost. Verify graceful degradation when external dependencies fail.

## Deployment gates
- [ ] No required local-only state blocks horizontal scaling.
- [ ] Health probes match service readiness semantics.
- [ ] Autoscaling and max-capacity limits are tested.
- [ ] Rollback and backup/restore procedures are validated.
- [ ] Capacity assumptions are documented.

This document is a checklist; it does not assert any tests or deployments have passed.