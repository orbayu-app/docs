# ADR-001: Project License (MIT)

## Status
Accepted

## Context
We need to choose a license for the project.

The project is a pet project intended for:
- personal use
- portfolio demonstration
- possible future monetization

We want the code to be open and easy to use by others,
without introducing legal complexity or restrictions.

## Decision
We choose the MIT License.

MIT is a permissive license that allows:
- use, copy, modification, distribution
- commercial use

The only requirement is to include the original copyright
and license text.

## Alternatives

### GPL / copyleft licenses
Rejected.

GPL requires derivative works to remain open source under the same license.
This conflicts with possible future monetization paths and discourages adoption
in proprietary projects. MIT keeps the door open for both.

### No license (all rights reserved)
Rejected.

Without a license, code is implicitly "all rights reserved", which contradicts
the open-source goal of the project.

## Consequences
Pros:
- Very simple and widely understood license
- No restrictions on usage, including commercial use
- Encourages adoption and contributions
- Matches Laravel ecosystem (MIT)

Cons:
- Anyone can reuse the code, including in proprietary projects
- No obligation to contribute back

Code being open does not prevent monetization.
Value can be provided through hosted service, UX, or data.
