# Implementation Standards

Write code that follows architectural rules, enforcement gates, and clear standards.

**Category:** procedure  
**Updated:** 2026-04-26

---

## Why This Matters

Without standards:
- Code organization inconsistent
- Type violations slip through
- Dependencies become tangled
- Refactoring breaks unknown code

With standards:
- All code meets same bar
- Violations caught before commit
- Architecture preserved
- Refactoring is safe

---

## Core Concept

Before writing code, during writing, and before committing: verify code follows architectural rules, enforcement gates pass, and organization is clear.

---

## Before Writing Any Code

Checklist:

- [ ] Plan approved by user
- [ ] Target module/file identified
- [ ] Dependencies understood (what this needs)
- [ ] Public interface designed (what this exposes)
- [ ] No circular dependencies will be introduced

If ANY unchecked → Go back to planning.

---

## While Writing Code

### Architectural Rules

**Domain-Driven Design + Hexagonal:**
- Core logic separate from infrastructure
- Dependencies injected, never constructed
- Clear layer boundaries
- Contracts defined before implementations

### Type Safety

**For every function:**
- [ ] Parameter types declared
- [ ] Return type declared
- [ ] Specific types (not generic)
- [ ] Nullable types marked

### Code Organization

**Before adding code:**
- Where does this responsibility live?
- Does that module exist?
- If not, create it

**While adding code:**
- One file per responsibility
- Clear module names
- Single responsibility per function
- Reasonable file sizes (hundreds of lines, not thousands)

### No Inline Comments

**Rule:** Code clarity is the goal.

If code needs explanation:
- Rename variable (`x` → `retryCount`)
- Rename function (`fn` → `calculateUserBalance`)
- Extract complex logic into named functions
- Use documentation tools for WHY

Comment only when:
- **Why** something works a specific way (not obvious)
- **Constraint** this code works around
- **Warning** about side effects or gotchas

Never comment:
- What code does (read the code)
- Step-by-step explanations (refactor for clarity)
- TODO/FIXME (use issue tracker)
- Obvious code

### Dependencies

**Rule:** All dependencies injected, never constructed.

Core receives what it needs. Core never creates dependencies.

### No Spaghetti Code

**While implementing, check:**
- Dependencies flow in one direction (acyclic)
- Each responsibility in one place
- No duplicate logic
- Clear module boundaries
- Public interface clear, implementation hidden

---

## Enforcement Gates

Before committing, these MUST pass:

### 1. Linter

Must pass at strictest level. No suppressions without reason.

### 2. Typechecker

Must pass in strict mode. No `any` types without documented reason.

### 3. Code Formatter

Code must be properly formatted.

### 4. Tests (If Applicable)

All tests pass. New code has corresponding tests.

### 5. Dependency Audit

No security vulnerabilities. All dependencies >48 hours old.

**Rule:** Code that fails ANY gate is rejected. No exceptions.

---

## Commit Checklist

Before committing:

- [ ] All gates pass (linter, typecheck, formatter, tests, audit)
- [ ] Architectural rules followed
- [ ] Module boundaries respected
- [ ] No spaghetti code
- [ ] Names are clear (no comments needed)
- [ ] Language-specific docs present for public functions
- [ ] No dependencies <48 hours old
- [ ] Only planned work (no scope creep)
- [ ] Changes match approved plan

If ANY unchecked → Fix before committing.

---

## What This Looks Like

### ✅ Done Well

- Code in correct module
- Types complete and specific
- Linter passes
- Typechecker passes
- No comments needed (names are clear)
- Dependencies injected
- All gates pass
- Matches approved plan

### ❌ Done Poorly

- Code scattered across modules
- Types incomplete or generic
- Linter warnings ignored
- Type errors suppressed
- Inline comments explaining code
- Dependencies constructed internally
- Tests failing
- Scope creep beyond plan

---

## When Stuck

If stuck during implementation:

1. **Stop writing code**
2. **Go back to plan** — Does plan need adjustment?
3. **Ask clarifying questions** — "If we do X, should Y change?"
4. **Get user approval** before changing plan
5. **Update plan** with new understanding
6. **Resume implementation** with updated plan

**Rule:** Don't hack your way out. Clarify and replan.

---

## Verification

Before submitting for review:

- [ ] Linter/typecheck pass (automated, not manual review)
- [ ] Architectural rules followed
- [ ] Module organization clear
- [ ] Type annotations complete
- [ ] No inline comments (only language-specific docs)
- [ ] Tests pass
- [ ] Security audit passes
- [ ] Changes match approved plan exactly
- [ ] No scope creep

If ANY unchecked → Fix before submitting.

---

## Related Skills

- [Initial Assessment](initial-assessment.md) — How to plan before this step
- [Code Rigor](../competencies/code-rigor.md) — How enforcement gates work
- [Code Organization](../competencies/code-organization.md) — How to organize code
- [Type Safety](../competencies/type-safety.md) — How to implement type safety

---

## Questions to Ask Yourself

- Does this code belong in this module?
- Can I explain what this does without comments?
- Would linter/typecheck pass this?
- Do I have explicit approval for what I'm implementing?

---

**Updated:** 2026-04-26
