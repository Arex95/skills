# Getting Started

New to this project? Follow these steps before writing any code.

---

## Step 1: Understand the Project Structure

**Check for PROJECT_INDEX.md in project root:**

```bash
ls PROJECT_INDEX.md
```

**If it exists:**
- Read it (takes 5 minutes)
- You'll understand: entities, repositories, use cases, flows
- You can navigate the codebase without reading code

**If it doesn't exist:**
- That's OK, you'll create it as you work
- Read [Indexed Context skill](./skills/competencies/indexed-context.md) first

---

## Step 2: Read Initial Assessment Procedure

This is your map before implementing anything.

**File:** [skills/procedures/initial-assessment.md](./skills/procedures/initial-assessment.md)

**Time:** ~25 minutes  
**What you'll do:** 7 steps that clarify what you're building before you write code

**The 7 steps:**
1. Read context (5 min) — git log, recent changes, current branch
2. Understand architecture (5 min) — Read [SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md) + PROJECT_INDEX.md
3. Clarify requirements (5 min) — Ask questions if ambiguous
4. Create plan (5 min) — What files will you touch, what will change
5. Present & approve (5 min) — Confirm with user before starting
6. Implement (follow plan exactly)
7. Verify against plan

---

## Step 3: Know the Core Principles

These are non-negotiable in this codebase:

- **Architecture First:** Core logic isolated from infrastructure (DDD + Hexagonal)
- **Type Safety:** Errors caught at compile-time, not runtime
- **Decision Rigor:** Ask before deciding. Clarify ambiguity. Present trade-offs.
- **Indexed Context:** Document what you learn. Don't load code you don't need.
- **Enforcement:** Tools (linter, typecheck, formatter) enforce quality at commit gates
- **Organization:** Every piece of code has a responsible place

If these feel unfamiliar, read [SKILLS-OVERVIEW.md](./SKILLS-OVERVIEW.md).

---

## Step 4: Explore the Skills System

**Location:** `skills/`

**Three types of skills you'll reference:**

### Competencies (how to think)
When making architecture or implementation decisions:
- [Architecture](./skills/competencies/architecture.md) — DDD + Hexagonal
- [Type Safety](./skills/competencies/type-safety.md) — Compile-time errors
- [Decision Rigor](./skills/competencies/decision-rigor.md) — How to decide well
- [Indexed Context](./skills/competencies/indexed-context.md) — Avoid bloated context
- [Code Organization](./skills/competencies/code-organization.md) — Where code belongs

### Patterns (how to solve recurring problems)
When implementing domain logic:
- [Domain Entity](./skills/patterns/domain-entity.md) — How to model a business concept
- [Value Object](./skills/patterns/value-object.md) — Immutable concepts (Email, UserId)
- [Repository](./skills/patterns/repository.md) — How to persist entities
- [Use Case](./skills/patterns/use-case.md) — How to orchestrate business flows
- [Dependency Injection](./skills/patterns/dependency-injection.md) — How to wire dependencies

### Tools (what must pass before commit)
Before committing code:
- [Linter](./skills/tools/linter.md) — Style and mistake detection
- [Typecheck](./skills/tools/typecheck.md) — Type safety in strict mode
- [Formatter](./skills/tools/formatter.md) — Consistent formatting
- [Test Coverage](./skills/tools/test-coverage.md) — Behavioral verification
- [Security Audit](./skills/tools/security-audit.md) — Dependency security

**All skills follow the same structure:** Why it matters → Core concept → How to apply → Verification

---

## Step 5: Start Your First Task

**Follow Initial Assessment exactly:**

1. ✅ Read context (git log, recent changes)
2. ✅ Understand architecture (read PROJECT_INDEX.md if exists)
3. ✅ Clarify requirements (ask questions)
4. ✅ Create plan (what you'll change)
5. ✅ Present plan (confirm before implementing)
6. ✅ Implement (follow plan, don't deviate)
7. ✅ Verify (did you match the plan?)

**Before committing:**
- All enforcement gates pass: linter → typecheck → formatter → tests → audit
- Code reflects plan (no scope creep)
- PROJECT_INDEX.md updated with what you learned

---

## Step 6: Maintain PROJECT_INDEX.md

As you work, keep the index updated:

**When you understand a piece of code:**
- Add one-paragraph extract to index
- Include filepath and what it does

**When code changes:**
- Update corresponding extract
- Reflect in flows (Previous/Next)

**When you complete a task:**
- Commit code + updated index together
- Index and code always in sync

See [Indexed Context skill](./skills/competencies/indexed-context.md) for detailed guidance.

---

## Quick Reference: Where to Find Things

| What you need | Where to find it |
|---|---|
| How to start a task | [Initial Assessment](./skills/procedures/initial-assessment.md) |
| Architecture principles | [Architecture skill](./skills/competencies/architecture.md) |
| How to model entities | [Domain Entity pattern](./skills/patterns/domain-entity.md) |
| How to persist entities | [Repository pattern](./skills/patterns/repository.md) |
| How to organize code | [Code Organization skill](./skills/competencies/code-organization.md) |
| How to avoid context bloat | [Indexed Context skill](./skills/competencies/indexed-context.md) |
| What must pass before commit | [Implementation Standards](./skills/procedures/implementation-standards.md) |
| Enforcement gates | `skills/tools/` (linter, typecheck, formatter, test, audit) |

---

## Context Budget: How Much Should You Load?

**The entire skills system is ~27K tokens.**

You don't need all of it. Here's what you actually load:

### Scenario: Starting a Task

**Minimum (to understand what to do):**
- GETTING_STARTED.md: 2.4K tokens
- Initial Assessment: 2.2K tokens
- PROJECT_INDEX.md (if exists): 1K tokens
- **Total: ~5.6K tokens**

**For a typical feature:**
- Entry points: 2.4K tokens
- Relevant competencies (2-3): 3-5K tokens
- Relevant patterns (1-2): 1.5-2K tokens
- Relevant tools (2-3): 2-3K tokens
- PROJECT_INDEX.md: 1K tokens
- **Total: ~10-15K tokens**

**With good Indexed Context (ideal):**
- PROJECT_INDEX.md only: 0.5-1K tokens
- Load skills on demand as needed
- **Total: ~1-3K tokens constant**

### The Trap: Don't Load Everything

**Bad approach:**
```
❌ "Let me load ALL 27K tokens to understand everything"
❌ Load all 9 competencies (10K tokens) even if only need 1-2
❌ Load all 5 patterns even if need 1
❌ Load all 5 tools even if 2 are relevant
Result: 27K tokens wasted, context bloated, session slower
```

**Good approach:**
```
✅ Load GETTING_STARTED (2.4K)
✅ Load Initial Assessment (2.2K)
✅ Read PROJECT_INDEX.md (1K) - understand architecture
✅ Load only competencies/patterns you need for THIS task
✅ Load tools section when about to commit
✅ Reference, don't load. Skills are hyperlinked, use links
Result: 5-15K tokens, sharp focus, fast iterations
```

### How to Know What You Need

**Before loading a skill:**
1. Check the title and intro (80% of the time that's enough)
2. Does it directly relate to your task? 
   - No? Skip it (save tokens)
   - Yes? Load it

**Example:**
- Task: "Add new validation to User entity"
  - Load: [Domain Entity pattern](./skills/patterns/domain-entity.md) ✅
  - Load: [Type Safety](./skills/competencies/type-safety.md) ✅
  - Skip: [Repository pattern](skills/patterns/repository.md) (not changing persistence)
  - Skip: [Payment processing](...) (not relevant)
  - Save: 3K tokens minimum

---

## One More Thing: The Trap to Avoid

**Don't do this:**
```
❌ Read entire codebase to understand it
❌ Load all 27K tokens of skills "just in case"
❌ Assume popular solution is correct
❌ Commit code without updating index
```

**Do this:**
```
✅ Read Initial Assessment (guides your understanding)
✅ Read PROJECT_INDEX.md (architecture reference, 1K tokens)
✅ Load only skills relevant to THIS task (5-8K tokens max)
✅ Choose solutions FOR your constraints
✅ Update index as you learn, commit together with code
✅ Reference skills hyperlinked, don't preload
```

---

## Ready?

1. Run Initial Assessment (25 minutes)
2. Start your first task following those 7 steps
3. Reference skills as needed
4. Keep PROJECT_INDEX.md updated
5. Run enforcement gates before commit

Let's go.

---

**Updated:** 2026-04-26
