# ADR-003: Commit Message and Branch Naming Conventions

## Status
Accepted

## Context
We need a consistent and readable approach to commit messages
and branch naming.

Goals:
- Keep git history easy to read and navigate
- Link code changes to issues
- Avoid unnecessary complexity and tooling overhead

## Decision

### Commit Message Format

Commits follow a three-part structure:

<subject>

<body>

<footer>

Each section is separated by a blank line.

#### Subject (required)
- Describes what changed
- Imperative mood (e.g. "Add login endpoint", "Fix token refresh")
- ~50 characters, hard limit 72
- No trailing dot

#### Body (optional)
- Explains why the change was made
- Adds context when subject is not sufficient
- Wrap lines at 72 characters

#### Footer (optional)
- References related issues

Format:
Refs #123

- No colon is used
- Multiple references allowed: Refs #123, #456
- Cross-repo references use full issue names: Refs orbayu-app/api#123
- Refs is used to avoid automatic issue closing

### Branch Naming

Format:

<issue-id>-<short-description>

Examples:
- 3-health-commit-hash
- 7-configure-xdebug

Rules:
- Issue ID is the issue number from the current repository
- Description is lowercase, kebab-case
- Keep it short and meaningful
- Do not use prefixes like feature/ or bugfix/

Branches without issue ID are allowed for small changes without a GitHub issue:

- refactor-auth-service
- update-readme

Issue references in commits are the main traceability mechanism.

## Alternatives

### Conventional Commits
Rejected.

Conventional Commits adds a rigid prefix format (feat:, fix:, chore:) to every
commit subject. The main benefit is automation: changelog generation, semver
bumps, release tooling. These are weak justifications for polluting every
commit subject in any project.

Costs that outweigh the benefits:
- Subjects become noisier and harder to read in `git log`
- Adds a tooling layer (commitlint, husky) just to enforce a format

If automation is needed, it can be triggered by tags, branches, or labels —
not by parsing commit subjects.

## Consequences

Pros:
- Clean and readable git history
- Easy navigation between commits and issues
- Low cognitive overhead

Cons:
- No automatic issue closing
- Less strict than Conventional Commits
- Relies on discipline rather than tooling

Conventions are enforced by review, not tooling.
They can be refined by a future ADR.
