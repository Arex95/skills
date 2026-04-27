# Type Safety

Catch errors at compile-time instead of runtime by enforcing complete type information and mandatory static analysis.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without type safety:
- Wrong parameter type discovered in production (not dev)
- Return value ambiguous; caller can't trust it
- Method called that doesn't exist (runtime error)
- Refactoring breaks unknown code paths silently

With type safety:
- Type mismatches caught before commit
- Static analyzer proves all paths are safe
- Refactoring shows all impacts immediately
- Code is self-documenting (types describe intent)

---

## Core Concept

Every function/method must declare parameter types, return types, and collection element types. Static analyzer must be able to prove correctness without running code.

---

## Key Principles

### Complete Type Information

Every public function declares:
- Parameter types (what inputs accepted)
- Return type (what output produced)
- Specific types (not generic: `array<string, User>`, not `array`)
- Nullable types marked explicitly (`?string` vs `string`)

### Static Analysis is Mandatory

Typechecker runs before commit. Code that fails CANNOT be committed.

Must pass at highest strictness:
- Strict mode enabled
- No implicit `any` types
- All transformations type-safe
- All paths verified

### Type Precision

Generic `array` is worthless. Specific `array<string, User>` is information.

---

## What This Looks Like

### ✅ Done Well

- Function declares `findUserById(int $id): ?User` — clear parameter and return types
- Typechecker passes in strict mode
- IDE shows exact type information on hover
- Adding wrong type triggers immediate analyzer error

### ❌ Done Poorly

- Function declares `findUserById($id)` — no types
- Parameter could be anything; return value unknown
- Typechecker warnings ignored
- Wrong type discovered in production

---

## How to Apply

### Step 1: Enable Strict Mode

Configure typechecker at highest strictness level.

### Step 2: Declare All Types

Every function parameter and return type must be explicit.

### Step 3: Run Analyzer Before Commit

Analyzer must pass 100%. No suppressions without documented reason.

### Step 4: Documentation

Add type documentation if needed for IDE hints.

### When to Use This Skill

- **Always:** Every function, every parameter, every return
- **No exceptions:** Even "obvious" functions need types

---

## Verification

- [ ] Every public function has parameter types
- [ ] Every function has return type
- [ ] Array/collection types are specific (not generic)
- [ ] Nullable types marked as nullable
- [ ] Typechecker passes in strict mode
- [ ] No `any` types (unless documented with reason)
- [ ] Static analysis passes 100%
- [ ] Language-specific docs present for public APIs

If ANY unchecked → Fix before commit.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Missing parameter types | Caller doesn't know what to pass; wrong type silently fails | Add parameter type: `findUser(int $id)` |
| Missing return type | Caller doesn't know what to expect; returns unknown | Add return type: `: User` |
| Generic `array` type | Could contain anything; no verification possible | Specify: `array<string, User>` |
| Implicit `any` type | Disables type checking; defeats purpose | Add explicit type or document why any is necessary |
| No static analysis | Type errors discovered in production | Configure analyzer, run before every commit |

---

## Related Skills

- [Code Rigor](code-rigor.md) — How to enforce types via linters and gates
- [Architecture](architecture.md) — Type safety enables clean architecture

---

## Questions to Ask Yourself

- If I hover over this variable in my IDE, do I see exact type information? (Answer: Always yes.)
- Could someone call this function with the wrong type? (Answer: No, analyzer prevents it.)
- Does my typechecker pass at strict mode? (Answer: Yes, or code isn't committed.)

---

**Updated:** 2026-04-26
