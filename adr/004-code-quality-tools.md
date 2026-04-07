# ADR-004: Code Quality Tools

## Status
Accepted

## Context
We need static analysis and code style enforcement for the Laravel API.

Goals:
- Enforce type hint discipline, strict types, import hygiene
- Catch structural issues: unused variables, dead code, cognitive complexity
- Act as a policy engine, not just a formatter
- Don't let bad code pass silently

## Decision

### Code Style: PHPCS + Slevomat Coding Standard

We use PHP_CodeSniffer with Slevomat Coding Standard for code style
enforcement.

Key capabilities that drove the decision:
- Detects missing type hints without PHPDoc
- Catches unused variables and parameters
- Enforces cognitive complexity limits
- Reports violations without silently fixing them
- Aggressive early exit enforcement

PHPCS acts as a policy engine: it tells you what is wrong and why.
The developer decides how to fix it.

### Static Analysis: PHPStan + Larastan (level 6)

We use PHPStan with Larastan extension for static analysis.

PHPStan finds bugs without running the code: wrong types, calls to
missing methods, dead code, incompatible arguments. PHPCS checks how
code is written (style), PHPStan checks what code does (correctness).

Larastan is required because Laravel relies heavily on magic methods,
facades, and dynamic calls. Without it PHPStan produces false positives
on standard Laravel code.

Level 6: level 5 is too loose (misses useful checks), level 7 is too
strict for a Laravel project (requires strict union type handling that
conflicts with framework conventions).

## Alternatives

### Laravel Pint
Rejected: thin wrapper over PHP CS Fixer. Adds a dependency
without adding control.

### PHP CS Fixer (standalone)
Rejected: fundamentally a formatter, not a linter. Cannot detect
missing type hints without PHPDoc, unused variables, or cognitive
complexity. Cannot report without fixing.

Good at what it does, but we need enforcement, not auto-formatting.

### PHPCS + Slevomat + PHP CS Fixer (together)
Rejected for now: two configs, potential rule conflicts, extra
maintenance. PHPCS + Slevomat covers our needs. Can revisit if
auto-formatting becomes painful.

### Psalm
Rejected: Laravel plugin is abandoned. No viable Laravel support.

### PHPMD (PHP Mess Detector)
Rejected: overlaps with PHPCS + Slevomat (unused variables, complexity)
and PHPStan (unused parameters, type issues). Adding a third tool
with its own config for duplicate coverage is not worth it.

## Consequences

Pros:
- Strict enforcement of type safety and code structure
- Catches issues that formatters and even static analyzers miss
- Ruleset is explicit and version-controlled
- Two tools with clear separation: PHPCS for style, PHPStan for correctness

Cons:
- XML config is verbose compared to PHP CS Fixer
- Not common in Laravel projects, requires building config from scratch
- Noisier output, especially during initial setup
- Two tools to configure and maintain
