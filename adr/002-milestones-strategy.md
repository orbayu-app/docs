# ADR-002: Cross-Repository Milestone Strategy

## Status
Accepted

## Context
The project consists of multiple repositories (api, mobile, infra, docs)
within a single GitHub organization.

We need a way to track progress across all repositories using milestones.

GitHub does not support organization-level milestones, so we need
a consistent cross-repository strategy.

## Decision
We use duplicated milestones across all repositories.

Rules:
- Milestones have identical names in all repositories
- Naming format: vX.Y - Name (e.g. v0.1 - Foundation)
- Each milestone has a short description explaining scope
- Milestone due dates are used for ordering in GitHub UI, not as hard deadlines
- Synchronization across repositories is automated via a script in the docs repository

Current state:
- Milestones are maintained manually
- Synchronization script accepted but not implemented yet

Semantics:
- Milestones represent product phases, not code versions
- Git tags in repositories remain independent

## Alternatives

### Milestone placement

1. GitHub Project custom field (Single Select)  
Rejected: lacks progress tracking, due dates, and completion percentage.

2. Milestones in a single repository (e.g. api)  
Rejected: breaks repository isolation and requires cross-repo issues.

3. No milestones, only Project Board  
Rejected: boards track status, not phases.

### Naming format

4. Sequential (M1, M2)  
Rejected: lacks semantic meaning.

5. Version only (v0.1)  
Rejected: not descriptive in issue lists.

6. Name only (Foundation, Tides)  
Rejected: lacks ordering.

7. Date-based (March 2026)  
Rejected: no fixed cadence for a solo project.

8. Semver (v0.1.0)  
Rejected: implies release semantics, not applicable to milestones.

## Consequences

Pros:
- Consistent cross-repository milestone structure
- Each repository remains self-contained
- Works well with GitHub Project Board grouping
- Naming is both ordered and human-readable

Cons:
- Requires duplication across repositories
- Needs script maintenance
- Manual updates can drift between repositories

Milestones and Git tags are intentionally independent concepts.
