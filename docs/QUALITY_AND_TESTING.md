# Engineering and Operations Guide

CloudNexus is a cloud-oriented project workspace. This guide is intentionally provider-neutral: use the repository's actual source and infrastructure files to identify the cloud provider, runtime, deployed components, and supported commands before documenting a specific service.

## Discover the implementation

From the repository root:

```bash
git status --short
git ls-files
```

Review manifests, container definitions, infrastructure files, CI workflows, and environment-variable references. Document the actual startup/build/test commands from those files. Do not commit credentials or copied production configuration.

## Configuration

Maintain a documented list of environment variables with:
- Name and purpose
- Required or optional status
- Safe example value
- Secret/non-secret classification
- Validation behavior when missing or malformed

Use least-privilege identities and a secret manager for credentials. Do not expose secrets in health endpoints, client responses, logs, or committed example files.

## Health and deployment validation

Where services exist, distinguish:
- **Liveness:** the process is running and can continue.
- **Readiness:** the service is prepared to accept traffic and required dependencies are available.

Health checks should return stable status codes without exposing internal stack traces or credentials. Test missing configuration, dependency timeouts, and failed startup. Avoid reporting healthy when a required dependency makes the service unusable.

## Testing and CI

Use the commands defined by the project's current manifests and CI workflows. Add tests for configuration parsing, error paths, authorization boundaries, and critical service behavior. Use mocked cloud services or isolated test resources to avoid accidental costs and production mutations.

For infrastructure changes, run the relevant formatter, validator, plan, or dry-run command before applying changes. Never run destructive infrastructure operations against a live environment as part of ordinary tests.

## Deployment and rollback

A deployment guide should record prerequisites, configuration, health verification, log locations, rollback steps, and recovery limitations. Roll back to a known-good artifact/configuration when verification fails; do not delete stateful resources as a rollback shortcut.

## Pull-request checklist

- [ ] Source and infrastructure changes match the documented architecture.
- [ ] No credentials or real environment values are committed.
- [ ] Tests/validators and build commands are recorded with results.
- [ ] Health checks and failure behavior are verified where implemented.
- [ ] Deployment status is claimed only when a deployment was actually checked.
