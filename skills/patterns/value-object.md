# Value Object Pattern

Value objects are immutable objects without identity. They represent meaningful concepts (Email, Money, Status) and are compared by their values, not identity.

**Category:** pattern  
**Updated:** 2026-04-26

---

## When to Use

Use when representing:
- Immutable concepts (Price, Email, Status, Coordinates)
- Things compared by value, not identity (two Email objects with same address are equal)
- Complex primitives (not just strings or numbers)
- Domain concepts (not just technical types)

Examples: Email, Money, UserId, Status, Coordinates, PhoneNumber.

---

## Core Idea

A value object:
1. **Has no identity** — Not identified by a unique ID
2. **Is immutable** — Never changes; create new instance instead
3. **Compared by value** — Two objects with same values are equal
4. **Self-validating** — Rejects invalid values in constructor
5. **Type-safe** — Domain concepts represented as types, not primitives

---

## Structure

```
Email Value Object:
  Fields (immutable, readonly):
    - value: string
  
  Constructor (validates):
    constructor(value: string):
      if not isValidEmail(value):
        raise error "Invalid email: {value}"
      this.value = value
      // Cannot create Email with invalid value
  
  Comparison (by value):
    equals(other: Email) → boolean:
      return this.value === other.value
  
  Representation:
    toString() → string:
      return this.value
  
  Validation (encapsulated):
    isValidEmail(email: string) → boolean:
      // Check format: something@something.something
      return email matches pattern /^[^@]+@[^@]+\.[^@]+$/

// Usage example
email1 = Email("user@example.com")
email2 = Email("user@example.com")
email1.equals(email2)  // → true (same value)

email3 = Email("other@example.com")
email1.equals(email3)  // → false (different value)

Email("invalid")  // → throws error (validation in constructor)
```

Key points:
- Constructor validates; invalid values are rejected immediately
- All fields immutable (cannot change after creation)
- Comparison by values, not object identity
- No unique ID (no identity field)
- Validation logic is part of the value object, not scattered elsewhere

---

## Why This Works in DDD + Hexagonal

**Type Safety:** Email is a type, not a string. Compiler catches wrong type usage.

**Validation:** Validation happens once in constructor, not scattered everywhere.

**Domain Language:** Code reads like domain language: `user.getEmail().equals(otherEmail)` not `user.email === otherEmail`.

**Immutability:** No state mutation surprises. Easier to reason about.

**Reusability:** Value object used in many entities. Logic centralized.

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Value object mutable | State can change unexpectedly | Make all fields readonly |
| No validation | Invalid objects created | Validate in constructor, throw if invalid |
| Comparison by identity | Two equal objects not recognized as equal | Implement equals method comparing values |
| Too complex | Value object with too much behavior | Keep focused on single concept (Email, not EmailManager) |
| Missing toString | Hard to debug/log | Implement toString for readability |
| Primitive wrapper (unnecessary) | False type safety; still acts like primitive | Use only for concepts with validation or behavior |
| Mutable nested objects | Immutability broken if contains mutable object | Use immutable types inside |

---

## Common Value Objects

- **Identity:** UserId, OrderId, ProductId
- **Concepts:** Email, PhoneNumber, Status, Priority
- **Quantities:** Money, Distance, Duration, Temperature
- **Measurements:** Coordinates, Dimensions, RGB (color)
- **Domain concepts:** Address, URL, IBAN

---

## Related Patterns

- [Domain Entity](domain-entity.md) — Entities use value objects to represent properties
- [Repository](repository.md) — Value objects persisted as part of entities
- [Use Case](use-case.md) — Business flows using value objects

---

**Updated:** 2026-04-26
