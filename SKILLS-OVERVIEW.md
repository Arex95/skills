# Skills System Overview

This repository uses a centralized **skills system** to document how work is done. Skills are tool-agnostic, methodology-focused documentation that ANY AI can use to understand how to work on projects without defaulting to generic solutions.

## What Are Skills?

Skills are not project documentation. They are meta-documentation: **how to think about and work on any project using this methodology.**

When you start work on any project in this codebase:
- Don't assume the architecture is like other projects
- Don't default to popular frameworks or libraries
- Don't skip planning or make assumptions
- Instead: read the skills, understand the methodology, follow the procedures

## Why Skills Matter

**Problem:** Each AI system has different defaults. Different systems might default to different frameworks or solutions. Generic solutions optimize for average problems, not your constraints.

**Solution:** Centralized skills document the unique methodology. Any AI (Claude, Gemini, DeepSeek, or future systems) reads the skills and works the same way.

**Outcome:** Consistent code quality, architecture, and decision-making across all projects, regardless of which AI is working on it.

## The Four Categories

### 1. Competencies

**What:** Core knowledge and principles every AI must understand.

**When to read:** Before any architectural or implementation decision.

**Examples:**
- How to organize code (Code Organization)
- How to ensure type safety (Type Safety)
- How dependencies should flow (Dependency Inversion)
- How to make good decisions (Decision Rigor)

All 9 competencies should be understood at the start of work.

### 2. Procedures

**What:** Step-by-step how to act at specific moments: before starting, during implementation, before committing.

**When to follow:** As your workflow. Before writing any code → read Initial Assessment. While writing code → follow Implementation Standards. Before committing → run enforcement gates.

**Examples:**
- Initial Assessment: 7 steps to plan before implementation starts
- Implementation Standards: Checklist for architectural rules, type safety, organization, enforcement gates

### 3. Patterns

**What:** Concrete, proven solutions for recurring problems in DDD + Hexagonal architecture.

**When to use:** When implementing a specific problem (e.g., "how do I model a domain entity?", "how do I create a repository?").

**Patterns included:** Domain entity, value object, repository, use case, dependency injection.

### 4. Tools

**What:** Specifications for validation gates and enforcement mechanisms.

**When to use:** Before committing code. All tools must pass before code enters the repository.

**Tools included:** Linter enforcement, typecheck strict mode, code formatter, test coverage, security audit.

## How to Start Work

1. **Read Initial Assessment** (`skills/procedures/initial-assessment.md`)
   - 7-step process: read context → understand architecture → clarify requirements → plan → present → approve → implement
   - Takes ~25 minutes total
   - Clarifies what you're building and how before you write any code

2. **Reference competencies during planning**
   - Architecture decisions? Read [Architecture](skills/competencies/architecture.md) + [Decision Rigor](skills/competencies/decision-rigor.md)
   - Choosing a library? Read [Avoiding Generic Solutions](skills/competencies/avoiding-generic-solutions.md) + [Dependency Security](skills/competencies/dependency-security.md)
   - Structuring code? Read [Code Organization](skills/competencies/code-organization.md)

3. **Follow Implementation Standards** (`skills/procedures/implementation-standards.md`)
   - Before writing code: verify plan is approved
   - While writing: follow architectural rules, use type safety, organize code properly
   - Before committing: all enforcement gates must pass

4. **Run enforcement gates**
   - Linter (catch style violations)
   - Typecheck (catch type errors)
   - Formatter (ensure consistency)
   - Tests (verify behavior)
   - Security audit (check dependencies)

## Core Principles

These appear across all skills and are non-negotiable:

- **Decision Rigor:** Ask before deciding. Clarify ambiguity. Present trade-offs. Get approval.
- **Constraint-Driven:** Choose solutions FOR your constraints, not despite them.
- **Architecture First:** Core logic isolated from infrastructure (DDD + Hexagonal).
- **Type Safety:** Errors caught at compile-time, never at runtime.
- **Enforcement:** Tools enforce quality at commit gates, not code review.
- **Organization:** Every piece of code has a clear, responsible place.
- **Intentionality:** Never convenient, always deliberate. No defaults to popular solutions.
- **Indexed Context:** Build a lightweight index as you work. Avoid bloated context. Reference what you've learned, not what you're analyzing.

## What Skills Are NOT

- **Not project documentation:** This isn't a README. It doesn't explain what the system does.
- **Not code style guide:** It doesn't dictate "use 2 spaces" or "camelCase".
- **Not tool-specific:** It doesn't say "use [specific-tool-X]" or "use [specific-tool-Y]". It says "use type safety" or "use dependency injection".
- **Not complete:** Skills are evolving. New patterns and tools are added as the methodology evolves.

## Reading Skills

Each skill follows a consistent structure:

```
Title + Intro
Category + Updated date

Why This Matters
(consequences of ignoring, benefits of following)

Core Concept
(one-paragraph distillation of the skill)

Key Principles
(2-3 main principles with explanations)

What This Looks Like
(✅ Done well / ❌ Done poorly)

How to Apply / When to Use
(step-by-step process)

Verification Checklist
(before moving forward, check these)

Common Mistakes
(table: what goes wrong and how to fix it)

Related Skills
(cross-references to other skills)

Questions to Ask Yourself
(self-reflection questions)
```

This structure makes skills easy to navigate and understand.

## FAQ

**Q: Can I ignore a skill if I think it's wrong?**
A: No. Skills represent proven methodology. If something seems wrong, discuss it — skills are maintained, not gospel.

**Q: What if a skill conflicts with the codebase?**
A: The codebase takes precedence. But this usually means the codebase needs refactoring to align with skills (not the reverse).

**Q: Do I need to read all skills before starting?**
A: Read [Initial Assessment](skills/procedures/initial-assessment.md) before any work. Reference other skills as needed. You'll internalize them over time.

**Q: What if I'm blocked and the skills don't cover my situation?**
A: This is feedback for the skills system. Flag it, and we'll add a pattern or procedure to cover the gap.

---

**To get started:** Read `Initial Assessment` (`skills/procedures/initial-assessment.md`), then begin work following its 7 steps.

**Skills location:** `skills/` (organized by category: competencies, procedures, patterns, tools)

**Updated:** 2026-04-26
