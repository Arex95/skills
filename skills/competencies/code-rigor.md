# Code Rigor & Enforcement

Enforce code quality through tools (linters, typechecks, formatters) at commit-time, not through code review or comments.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without enforcement:
- Code quality depends on reviewer attention
- Type errors discovered in production
- Style inconsistencies pile up
- Each developer writes differently

With enforcement:
- Linters catch violations before commit
- Typechecks verify correctness automatically
- Formatter ensures consistency
- Every commit meets same standard

---

## Core Concept

Code rigor is enforced through tools (linters, typechecks, formatters) at commit gates. Not through comments. Not through code review. Through automated gates that reject code that fails.

---

## Key Principles

### Tools Are Gates

**Linters catch:**
- Unused variables and imports
- Style violations
- Common mistakes
- Security issues

**Typechecks catch:**
- Type mismatches
- Null/undefined access
- Missing methods
- Incorrect inheritance

**Code formatter ensures:**
- Consistent spacing
- Consistent line breaks
- Consistent style
- No style debate

### No Comments in Code

Code should be clear enough without comments.

If code needs explanation:
- Rename variables to be clearer
- Extract logic into named functions
- Split into smaller, understandable pieces
- Use documentation tools

**When comments are acceptable:**
- Language-specific documentation
- Explaining WHY (not what)
- Documenting non-obvious constraints

**Never comment:**
- What code does (read it)
- Step-by-step explanations (refactor instead)
- TODO/FIXME (use issue tracker)
- Obvious code

### Strictest Settings Always

Configure every tool at maximum strictness:
- Linters: All rules enabled
- Typechecks: Strict mode, no implicit `any`
- Formatter: Consistent, non-negotiable

---

## What This Looks Like

### ✅ Done Well

- Linter passes 100%
- Typechecker passes in strict mode
- Code formatted automatically
- Pre-commit hooks run all gates
- Code rejected if any gate fails

### ❌ Done Poorly

- Linter warnings ignored
- Typechecker in loose mode
- Code not formatted
- Manual style enforcement via comments
- Type errors discovered in production

---

## How to Apply

### Step 1: Configure Tools at Strictest Level

Linter (maximum strictness), typechecker (strict mode), formatter (enabled).

### Step 2: Set Up Pre-Commit Hooks

Before code enters repository: linter → typecheck → formatter → tests → audit.

### Step 3: Run Gates Before Commit

All gates must pass 100%. No exceptions.

### Step 4: Document Suppressions Only When Necessary

If suppression required: document reason. Suppression is exception, not accommodation.

### When to Use This Skill

- **Always:** Every commit, every developer
- **No exceptions:** Even "obvious" code must pass

---

## Verification

- [ ] Linter configured at strictest level
- [ ] Typechecker enabled in strict mode
- [ ] Code formatter installed and running
- [ ] Pre-commit hooks run all gates
- [ ] No comments in code (only language-specific docs)
- [ ] Language-specific docs present for public functions
- [ ] No suppressions without documented reason
- [ ] Code that fails any gate is rejected

If ANY unchecked → Configure enforcement.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Linter warnings ignored | Violations accumulate; code quality declines | Configure pre-commit hook to reject |
| Typechecker in loose mode | Type errors discovered in production | Switch to strict mode, resolve violations |
| No code formatter | Manual style enforcement via PR comments | Install formatter, run on every commit |
| Comments explaining code | Code becomes harder to read, comments rot | Refactor for clarity, rename variables |
| Suppressions without reason | Defeats purpose of tools | Document reason or fix violation |

---

## Related Skills

- [Type Safety](type-safety.md) — How types are enforced
- [Code Organization](code-organization.md) — Structure that enables linting
- [Implementation Standards](../procedures/implementation-standards.md) — Gates checklist

---

## Questions to Ask Yourself

- Does my linter pass at strictest level?
- Does my typechecker pass in strict mode?
- Did I suppress any violations? Is the reason documented?
- Could this code be clearer without comments?

---

**Updated:** 2026-04-26
