# Skills System

Tool-agnostic, centralized documentation of development methodology. Designed so any AI (Claude, Gemini, etc.) can work on projects without defaulting to generic solutions.

---

## Quick Start

**New to this system?**

1. **Read** [GETTING_STARTED.md](./GETTING_STARTED.md) (10 min) — entry point for any AI
2. **Reference** skills as needed — they're hyperlinked, load on demand
3. **Use** [SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md) to understand the system architecture

---

## What's Here

### Entry Points

- **[GETTING_STARTED.md](./GETTING_STARTED.md)** — First file to read. Explains the system, core principles, context budget guidance
- **[SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md)** — What the skills system is and why it matters. Read if you want to understand the methodology

### Skills System

All skills live in `skills/` and are organized by category:

**Competencies** (9 files)
- How to think about architecture, type safety, dependencies, organization, decision-making, etc.
- Example: [Indexed Context](./skills/competencies/indexed-context.md) — build lightweight index as you work, avoid bloated context

**Procedures** (2 files)
- Step-by-step how to work: before implementation, during implementation, before commit
- [Initial Assessment](./skills/procedures/initial-assessment.md) — 7 steps before starting any work
- [Implementation Standards](./skills/procedures/implementation-standards.md) — rules and enforcement gates

**Patterns** (5 files)
- Concrete solutions for DDD + Hexagonal architecture
- Domain entities, value objects, repositories, use cases, dependency injection

**Tools** (5 files)
- Validation gates that must pass before committing
- Linter, typecheck, formatter, test coverage, security audit specs

### Reference

- **[EXAMPLE-PROJECT-INDEX.md](./EXAMPLE-PROJECT-INDEX.md)** — Template showing how to structure a PROJECT_INDEX.md for any project using this system. This is the "indexed context" in action.

---

## Core Principles

These appear across all skills:

- **Architecture First:** DDD + Hexagonal. Core logic isolated from infrastructure.
- **Type Safety:** Errors caught at compile-time, never runtime.
- **Decision Rigor:** Ask before deciding. Clarify ambiguity. Present trade-offs.
- **Indexed Context:** Build lightweight index as you work. Reference what you've learned, not what you're analyzing.
- **Constraint-Driven:** Choose solutions FOR your constraints, not despite them.
- **Intentionality:** Never convenient, always deliberate. No defaults to popular solutions.

---

## How to Use This

### If You're an AI Starting a Project

1. Read [GETTING_STARTED.md](./GETTING_STARTED.md)
2. Run the Initial Assessment (7 steps from skills/procedures/)
3. Reference skills as needed via hyperlinks — load on demand
4. Keep context tight: 5-15K tokens per task, not more
5. Maintain PROJECT_INDEX.md as you work (see docs/EXAMPLE-PROJECT-INDEX.md)

### If You're Integrating This System Into a Project

1. Add reference to this repo in your project README
2. Reference [GETTING_STARTED.md](./GETTING_STARTED.md) as your onboarding guide
3. Create PROJECT_INDEX.md using the template at EXAMPLE-PROJECT-INDEX.md
4. Keep the index updated as you work

### If You Want to Understand the System

Start with [SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md) (5 min) to understand:
- What skills are (meta-documentation, not project docs)
- Why this matters (consistency across AIs and projects)
- How skills are structured

---

## File Structure

```
skills/
├── SKILLS.md                    # Index of all skills
├── TEMPLATE.md                  # Template all skills follow
├── competencies/                # How to think (9 files)
├── procedures/                  # How to act (2 files)
├── patterns/                    # Proven solutions (5 files)
└── tools/                       # Validation gates (5 files)

GETTING_STARTED.md               # Entry point for new AIs
SKILLS-OVERVIEW.md               # What this system is and why
EXAMPLE-PROJECT-INDEX.md         # Template for PROJECT_INDEX.md
```

---

## Context Budget

The entire system is ~27K tokens. But you don't need all of it:

**Minimum to understand what to do:**
- GETTING_STARTED.md (2.4K)
- Initial Assessment procedure (2.2K)
- PROJECT_INDEX.md if exists (1K)
- **Total: ~5.6K tokens**

**Typical feature task:**
- Entry points above (5.6K)
- 2-3 relevant competencies (3-5K)
- 1-2 relevant patterns (1.5-2K)
- 2-3 relevant tools (2-3K)
- **Total: ~10-15K tokens**

**Ideal with Indexed Context:**
- PROJECT_INDEX.md only (0.5-1K)
- Load skills on demand as needed
- **Total: ~1-3K tokens constant**

The key: reference hyperlinked skills, don't preload everything.

---

## Core Concept: Indexed Context

The innovation that makes this system work: instead of AIs loading entire codebases to understand structure, you maintain a **PROJECT_INDEX.md** as living documentation.

**What it contains:**
- Flows: Multi-file processes as ordered sequences with Previous/Next relationships
- Entities: Self-contained summaries of domain objects
- Repositories: Persistence abstractions
- Use Cases: Business orchestration
- Metadata: Which flows use which entities, showing how everything connects

**Why it matters:**
- Reduces context from gigabytes to kilobytes
- Makes architecture visible without reading code
- Lives alongside code, updated with every refactor
- Next AI referencing index understands structure in 5 minutes, not hours

See [EXAMPLE-PROJECT-INDEX.md](./EXAMPLE-PROJECT-INDEX.md) for a complete template.

---

## Standards

Skills are:
- **Tool-agnostic** — describe methodology, not specific tools
- **Consistent** — all follow the same template structure
- **Self-contained** — each skill stands alone
- **Hyperlinked** — skills reference each other, enabling lazy-loading
- **Compatible with doc generators** — work with various documentation tools

---

## License

This skills system is shared publicly so any AI can learn and apply the methodology. Adapt to your constraints.

---

Last updated: 2026-04-26
