# Skills Index

All skills used in daily development work. Organized by category: competencies (what to know), procedures (how to act), patterns (proven solutions), tools (validation gates).

---

## Competencies

Core knowledge and principles every AI must understand and apply.

- [Architecture](competencies/architecture.md) — DDD + Hexagonal pattern: core logic isolated from infrastructure
- [Type Safety](competencies/type-safety.md) — Catch errors at compile-time, not runtime
- [Dependency Inversion](competencies/dependency-inversion.md) — Dependencies flow inward toward core
- [Code Rigor & Enforcement](competencies/code-rigor.md) — Tools enforce quality at commit gates
- [Dependency Security](competencies/dependency-security.md) — 48-hour minimum publication rule
- [Code Organization & Modular Structure](competencies/code-organization.md) — Every piece of code has a responsible place
- [Decision Rigor & Clarification-First](competencies/decision-rigor.md) — Ask before deciding, present trade-offs
- [Avoiding Generic Solutions](competencies/avoiding-generic-solutions.md) — Choose solutions FOR constraints, not despite them
- [Indexed Context](competencies/indexed-context.md) — Document what you learn, avoid bloated context

---

## Procedures

Step-by-step how to work: before implementation, during implementation, at commit time.

- [Initial Assessment](procedures/initial-assessment.md) — 7 steps before starting: read context → understand architecture → clarify requirements → plan → present → approve → implement
- [Implementation Standards](procedures/implementation-standards.md) — Architectural rules, type safety, organization, no comments, enforcement gates

---

## Patterns

Concrete, proven solutions for common problems in this system.

- [Domain Entity](patterns/domain-entity.md) — Modeling core business concepts
- [Value Object](patterns/value-object.md) — Immutable, self-validating values
- [Repository](patterns/repository.md) — Persistence abstraction
- [Use Case](patterns/use-case.md) — Business operation orchestration
- [Dependency Injection](patterns/dependency-injection.md) — Dependency wiring

---

## Tools

Validation gates and enforcement specifications.

- [Linter](tools/linter.md) — Code style and mistake detection
- [Typecheck](tools/typecheck.md) — Type safety verification
- [Formatter](tools/formatter.md) — Code format consistency
- [Test Coverage](tools/test-coverage.md) — Behavioral verification
- [Security Audit](tools/security-audit.md) — Dependency security

---

## How AIs Should Use These Skills

1. **Before any work:** Read [Initial Assessment](procedures/initial-assessment.md)
2. **During planning:** Reference relevant competencies for architectural decisions
3. **During implementation:** Follow [Implementation Standards](procedures/implementation-standards.md)
4. **Before commit:** Run all enforcement gates specified in Tools

All skills are tool-agnostic. They describe methodology, not specific tools.

---

**Last Updated:** 2026-04-26
