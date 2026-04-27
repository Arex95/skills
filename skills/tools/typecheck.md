# Typecheck Tool

Typecheck enforces type safety. Errors caught at compile-time, never at runtime.

**Category:** tool  
**Updated:** 2026-04-26

---

## What It Verifies

- **Type mismatches** — Passing wrong type to function
- **Null/undefined access** — Using value that might not exist
- **Missing properties** — Accessing property that doesn't exist on type
- **Generic types** — `any` type used (implicit coupling to anything)
- **Inheritance violations** — Incorrectly overriding methods
- **Return type mismatches** — Function returns wrong type

---

## Configuration Requirements

Typecheck must be configured at **strict mode.** No loosened settings.

**Minimum settings:**
- `strict: true` (or equivalent)
- `noImplicitAny: true` — Reject implicit `any`
- `noImplicitThis: true` — Reject implicit `this`
- `strictNullChecks: true` — Reject null/undefined without explicit handling
- `strictFunctionTypes: true` — Strict function parameter/return checking
- `noUnusedLocals: true` — Reject unused variables
- `noUnusedParameters: true` — Reject unused parameters
- `noImplicitReturns: true` — Reject functions with non-all-paths return

**Tool-agnostic approach:** Use whatever type system your language provides in strict mode.

---

## Execution

**Pre-commit:** Typecheck must pass before code is committed.

**In CI:** Typecheck must pass on every commit.

---

## What Passes vs. Fails

**Passes:**
```
// ✅ Types explicit, null handling explicit
User (interface):
  getId() → UserId
  getEmail() → Email

findUser(id: UserId) → User or null:
  user = userRepository.findById(id)
  if user is null:
    return null
  return user
  // Type system knows: result is User or null (explicit)
```

**Fails:**
```
// ❌ Implicit any (parameter type missing), null not handled
findUser(id):  // ← What type is id?
  user = userRepository.findById(id)
  return user.getEmail()  // ← Might be null, not handled

// ❌ Generic/any type, anything can be accessed
processData(data: any):  // ← any type means anything can happen
  return data.something  // ← No verification something exists
```

---

## Type Annotations Required

**All of:**
- Function parameters
- Function return types
- Variable types (inferred types acceptable, but explicit is clearer)
- Class properties
- Object properties

**Example:**
```
// ❌ No types
calculateTotal(items):  // ← What type is items?
  return items.reduce((sum, item) => sum + item.price, 0)
  // Type system knows nothing about items, sum, or item

// ✅ Full types
calculateTotal(items: OrderItem[]) → Money:
  return items.reduce((sum: Money, item: OrderItem) →
    sum.add(item.getPrice()),
    Money.zero()
  )
  // Type system knows: items is OrderItem[], sum is Money, returns Money
```

---

## If Typecheck Fails

**Never commit code that fails typecheck.**

**Options:**
1. **Fix the type violation** (90% of cases)
   - Add missing type annotation
   - Handle null/undefined case
   - Use correct type
   - Fix return type

2. **Suppress with generic type** (rare, needs documentation)
   - Only when type truly unknown or external
   - Requires explicit marking (not implicit)
   - Explain in comment

```
// Type from external API, can't guarantee structure
externalData: AnyType = fetchFromAPI()
  // REASON: External API response structure is dynamic/unknown
user = parseUser(externalData)
```

**Never use implicit/loose typing. Always explicit, always documented.**

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Implicit any allowed | Loose coupling; defeats purpose | Configure `noImplicitAny: true` |
| Loose mode enabled | Type errors not caught | Switch to strict mode |
| Using `any` to avoid fixing types | Coupling and bugs accumulate | Add proper types, handle null explicitly |
| Missing return type | Function behavior unclear | Specify return type explicitly |
| Null/undefined not handled | Runtime null access errors | Use null coalescing, optional chaining, guards |
| No type for complex objects | `object` type too generic | Create interfaces for structures |
| Generic `T` without constraints | Type variable too loose | Constrain `<T extends Base>` |

---

## When Strictness Must Be Relaxed

**Only if:**
1. Type is truly unknown (external API, dynamic data)
2. Explicit `any` used (never implicit)
3. Comment explains why
4. Creates technical debt ticket to fix later

**Never:**
- Disable strict mode
- Ignore typecheck errors
- Use implicit `any` to avoid fixing

---

## Related Tools

- [Linter](linter.md) — Style and mistake enforcement
- [Formatter](formatter.md) — Format consistency
- [Test Coverage](test-coverage.md) — Behavioral verification
- [Security Audit](security-audit.md) — Dependency security

---

**Updated:** 2026-04-26
