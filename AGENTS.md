# Guidance for AI/LLM Assistants

You're reading this because you're about to work on a project using this methodology. This guide explains what you need to know.

---

## The System: Skills-Based Methodology

This repository contains a centralized **skills system** — meta-documentation that teaches any AI how to work consistently across projects.

**You don't memorize it. You reference it.**

### What's Here

- **[GETTING_STARTED.md](./GETTING_STARTED.md)** — Start here. 10-minute orientation.
- **[skills/](./skills/)** — 21 documented skills organized by category
- **[SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md)** — Understand the system (why it exists, how it works)
- **[EXAMPLE-PROJECT-INDEX.md](./EXAMPLE-PROJECT-INDEX.md)** — Template for PROJECT_INDEX.md

### Quick Navigation

| I need to... | Read |
|---|---|
| Understand what this is | [GETTING_STARTED.md](./GETTING_STARTED.md) (10 min) |
| Learn about architecture | [skills/competencies/architecture.md](./skills/competencies/architecture.md) |
| Understand the methodology | [SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md) |
| Plan before implementing | [skills/procedures/initial-assessment.md](./skills/procedures/initial-assessment.md) |
| Know the rules before commit | [skills/procedures/implementation-standards.md](./skills/procedures/implementation-standards.md) |
| See a working example | [EXAMPLE-PROJECT-INDEX.md](./EXAMPLE-PROJECT-INDEX.md) |

---

## Core Principles (Non-Negotiable)

These apply everywhere:

1. **Architecture First** — DDD + Hexagonal. Core logic isolated from infrastructure.
2. **Type Safety** — Errors at compile-time, never runtime.
3. **Decision Rigor** — Ask before deciding. Present trade-offs. Get approval.
4. **Indexed Context** — Build lightweight PROJECT_INDEX.md. Reference it, don't load code.
5. **Constraint-Driven** — Choose solutions FOR your constraints, not despite them.
6. **No Generic Defaults** — Never use "popular solutions." Always ask first.

---

## Your Workflow

### Before Starting Any Task

1. **Run Initial Assessment** (25 min)
   - File: [skills/procedures/initial-assessment.md](./skills/procedures/initial-assessment.md)
   - 7 steps: read context → understand architecture → clarify requirements → plan → present → approve → implement

2. **Reference Skills as Needed**
   - Check [skills/SKILLS.md](./skills/SKILLS.md) for the index
   - Load relevant skills via hyperlinks
   - Don't preload everything (that's the "context bloat" trap)

3. **Maintain PROJECT_INDEX.md**
   - Template: [EXAMPLE-PROJECT-INDEX.md](./EXAMPLE-PROJECT-INDEX.md)
   - Update it as you discover/refactor code
   - This is how future AIs understand architecture in 5 minutes

### Before Committing Code

1. **Verify You Followed the Plan**
   - Did you stick to what you said you'd do?
   - Scope creep? Don't add it.

2. **Run Enforcement Gates**
   - Check: [skills/procedures/implementation-standards.md](./skills/procedures/implementation-standards.md)
   - All gates must pass before commit

3. **Update PROJECT_INDEX.md**
   - Any code you understood? Extract it.
   - Code you refactored? Update the extract.
   - New files? Add to index.
   - Commit code + index updates together.

---

## Project Structure (Standard)

---

## When Working on a Specific Project

Each project using this methodology will have its own guidance file (also called AGENTS.md). That file will reference this system and add project-specific rules.

**Look for in your project:**
- **AGENTS.md** — Project-specific guidance (references this system)
- **PROJECT_INDEX.md** — Architecture overview (built using template from docs/EXAMPLE-PROJECT-INDEX.md)
- **docs/** — Project patterns and decisions

---

## Key Skills You'll Reference Most

These skills come up constantly. Bookmark them:

1. **[Indexed Context](./skills/competencies/indexed-context.md)** — How to build PROJECT_INDEX.md, when to extract, how to avoid bloated context
2. **[Architecture](./skills/competencies/architecture.md)** — DDD + Hexagonal explained
3. **[Initial Assessment](./skills/procedures/initial-assessment.md)** — 7 steps before implementing
4. **[Decision Rigor](./skills/competencies/decision-rigor.md)** — How to decide well and ask the right questions

---

## The Trap: Don't Load Everything

**Bad approach:**
- Load all 21 skills at once (27K tokens)
- Read entire codebase before starting
- Trust your instincts on architecture

**Good approach:**
- Load GETTING_STARTED.md first
- Reference skills via hyperlinks as needed
- Build PROJECT_INDEX.md as you work
- Always check the index before loading code

---

## Testing Your Understanding

**You understand this system when you can:**

1. ✅ Explain why indexed context matters (5 seconds)
2. ✅ Navigate to any skill needed by name (10 seconds)
3. ✅ Run Initial Assessment and create a plan (25 minutes)
4. ✅ Recognize when a decision needs approval vs. when you can implement
5. ✅ Update PROJECT_INDEX.md as you refactor
6. ✅ Know which enforcement gates must pass before commit

---

## Resources

- **Get started:** [GETTING_STARTED.md](./GETTING_STARTED.md)
- **Understand the system:** [SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md)
- **See the skills:** [skills/SKILLS.md](./skills/SKILLS.md)
- **Example project structure:** [EXAMPLE-PROJECT-INDEX.md](./EXAMPLE-PROJECT-INDEX.md)

---

Last updated: 2026-04-26
