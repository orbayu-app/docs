# ADR-000: ADR Format

## Status
Accepted

## Context
We need a consistent way to document important architectural and
technical decisions in the project.

Without a standard format, ADRs become inconsistent and harder to read
and maintain.

## Decision
We adopt a simplified ADR (Architecture Decision Record) format based
on Michael Nygard's template.

Each ADR must include the following sections:

- Status
- Context
- Decision
- Alternatives (optional)
- Consequences

Writing rules:
- Write decisions in present tense, as accepted facts.
- Separate accepted decisions from current implementation state.
- If a decision is accepted but not implemented yet, say so explicitly.
- ADRs are not task lists, roadmaps, or operational guides.
- Keep implementation instructions in README files, docs guides, or issues.

Current state convention:
The `Current state` block is a local convention. It is added inside Decision
when implementation differs from the accepted decision. This deviates from
the canonical immutable-ADR approach but fits a solo project where issuing
a follow-up ADR for every implementation step is overkill.

ADR files are stored in /docs/adr directory.

Naming convention:
NNN-short-title.md

Examples:
000-adr-format.md
001-project-license.md

Status values:
- Proposed
- Accepted
- Deprecated

## Consequences
Pros:
- Consistent structure for all decisions
- Easier to read and understand project history
- Improves project quality for portfolio

Cons:
- Requires discipline to maintain
- Adds small overhead when documenting decisions
