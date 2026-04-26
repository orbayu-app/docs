<!--
Maintenance notes:
- Keep this file as a short cheat sheet, not a long guide.
- One idea per short line.
- Use `Term: meaning`.
- Add examples only when they prevent confusion.
- Optimize for reading after a two-week pause.
-->

# GitHub Workflow

Short rules for issues and project board hygiene.

## Issue Types

`bug`: something should work, but does not.

`feature`: new user-facing behavior.

`task`: technical, documentation, infrastructure, or project work.

## Labels

`ready`: clear scope, can be picked up.

`needs-refinement`: valid idea, but scope or done criteria are unclear.

`blocked`: waiting for another issue, decision, or external dependency.

`someday`: valid idea, not planned soon.

## Milestones

Milestone = planned phase.

No milestone = backlog.

Cross-repository milestone strategy: [ADR-002](adr/002-milestones-strategy.md).

## Size

`XS`: up to 30 minutes.

`S`: up to 2 hours.

`M`: one evening.

`L`: several evenings, consider splitting.

`XL`: not actionable, split first.

Prefer `XS` and `S` for side-project work.

## Optional Fields

Avoid estimates unless needed.

Use target dates only for real deadlines.

Do not use priority unless work becomes hard to choose.

## Assignees

Assignee = active owner.

Unassigned = backlog or no owner yet.

Do not assign many issues "just in case".

## Project Status

`Backlog`: saved, not planned.

`Todo`: planned soon.

`In Progress`: being done now.

`Done`: closed or finished.

Solo rule: keep `In Progress` to one issue when possible.

## Status vs Labels

Status = when.

Label = state.

Examples:

- `Backlog` + `ready`: clear, not planned
- `Todo` + `ready`: planned, can start
- `Backlog` + `needs-refinement`: saved, unclear
- `Todo` + `blocked`: planned, waiting for blocker

## Relationships

Use `blocked by` when another issue must finish first.

Add `blocked` label to the waiting issue.

Use `parent` only for big work split into smaller issues.

Do not use relationships for "related".

Use `Refs orbayu-app/repo#N` for loose references.

Cross-repo issue link: `orbayu-app/repo#N`.

## Picking Work

The GitHub Project is organization-wide.

Pick issues from any Orbayu repo.

Prefer `Todo` + `ready`.

## Issue Body

Keep issues short.

Ready issue must answer:

- what needs to be done
- what is out of scope, if useful
- when it is done

If an issue feels bigger than one evening, split it first.
