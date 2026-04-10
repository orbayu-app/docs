# ADR-005: Deployment Strategy

## Status
Accepted

## Context
Deployment uses two repositories: api (application code) and infra
(Dockerfiles, compose files, configs, scripts). We need a deployment
process for a single VPS that is reproducible and simple to operate.

Goals:
- Deploy api to staging automatically from `master`
- Keep production deploys explicit and tag-based
- Keep builds reproducible by pinning infra version
- Keep infrastructure and application code separated
- Minimize external dependencies during deployment

## Decision
Drone CI runs on the VPS and handles deployment. GitHub Actions
handles CI (lint, analyze, test on push).

Staging deploy:
- push to `master` in api triggers Drone pipeline
- pipeline builds images and deploys staging

Production deploy:
- production does not exist yet
- when production is introduced, deploy is triggered by git tags
- production deploy uses the same pinned-infra strategy

Staging pipeline:
1. Clone infra repo at pinned version
2. Build multi-stage Docker images from scratch
3. Run tests on test target
4. Build production-target runtime images
5. Deploy staging via docker-compose.prod.yaml

Infra version is pinned in api/.drone.yml as a variable.
When infra changes, tag infra and update the version in api.

Images are built and stored locally on VPS. Docker layer cache
handles base layers — no need for a separate registry or
pre-built base images.

Current state:
- staging deploy on push to master works
- production environment does not exist yet
- production tag-based pipeline accepted but not implemented

## Alternatives

### All in one repo (api + infra)
Rejected: infra contains configs, scripts, and compose files that
are not application code. Keeping them separate is cleaner.
Infra changes rarely and has its own versioning.

### GHCR for base images
Rejected for now: adds external dependency during deploy,
requires registry auth on VPS, extra pipeline for building
base images. Docker layer cache achieves the same result.
Can be added later if build times become a problem.

### GitHub Actions for deployment
Rejected: deploying from GitHub requires SSH access to VPS
and storing server credentials in GitHub. Drone runs on the VPS
and has direct access to Docker socket.

### Tag-based staging deploy
Rejected for now: staging is the active development environment.
Deploy-on-master keeps feedback short while there is no production.

Production releases use tag-based deploy.

### Latest infra version (not pinned)
Rejected: not reproducible. A deployment should build the same
way regardless of later infra changes.

## Consequences

Pros:
- Reproducible builds via pinned infra version
- Simple pipeline — one Drone config, no external dependencies
- Clear separation: GitHub for CI, Drone for CD
- Fast staging feedback from `master`
- Production release flow will be explicit and auditable

Cons:
- Updating pinned infra requires updating INFRA_VERSION in api
- First build on clean VPS is slower (no Docker cache)
- Drone is an extra service to maintain on VPS
- Production deploy pipeline still needs implementation
