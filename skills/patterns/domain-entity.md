# Domain Entity Pattern

Entities represent core business concepts with identity, state, and behavior. They live in the domain core, isolated from infrastructure.

**Category:** pattern  
**Updated:** 2026-04-26

---

## When to Use

Use when modeling something that:
- Has a unique identity (not just values)
- Changes state over time
- Has behavior (not just data)
- Is a core business concept (not a data transfer object)

Examples: User, Order, Product, Account, Task, Invoice.

---

## Core Idea

An entity is an object that has:
1. **Identity** — Can be uniquely identified (by ID, not by all properties)
2. **Mutable state** — Can change over time
3. **Behavior** — Methods that represent business logic
4. **Domain language** — Names and methods reflect business, not technical terms

---

## Structure

```
User Entity:
  Identity (immutable):
    - userId: UserId (never changes)
  
  State (mutable, private):
    - email: Email
    - status: UserStatus (ACTIVE, INACTIVE, DELETED)
    - createdAt: Date
    - lastLogin: Date (optional)
  
  Constructor (minimal required data):
    constructor(userId, email)
      this.userId = userId
      this.email = email
      this.status = ACTIVE
      this.createdAt = now
      (lastLogin is not set initially)
  
  Behavior (business logic, not getters/setters):
    recordLogin():
      this.lastLogin = now
    
    deactivate():
      if status == DELETED:
        raise error "Cannot deactivate deleted user"
      this.status = INACTIVE
    
    getId():
      return this.userId
```

Key points:
- Identity (userId) is immutable — never changes after creation
- State is encapsulated (private) — not exposed as public fields
- Behavior includes validation before state changes
- Constructor only accepts minimal data needed for valid entity
- Business method names reflect behavior, not data manipulation (recordLogin, not setLastLogin)

---

## Why This Works in DDD + Hexagonal

**Domain Core:** Entity lives in domain/core, knows nothing about databases, APIs, or external systems.

**Dependency Inversion:** Entity defines what it needs via value objects and domain services. It never constructs dependencies.

**Type Safety:** Identity is a value object (UserId, not string). Status is an enum, not a string. Email is a value object, not a string.

**Testability:** Entity behavior tested in isolation. No database, no external calls. Pure business logic.

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Entity as dumb data holder | No validation; logic scattered elsewhere | Add business logic methods to entity |
| Identity mutable | Breaking invariant; identity can change unexpectedly | Make identity immutable |
| Public getters/setters | Breaks encapsulation; state changed from anywhere | Make state private, use behavior methods |
| Too many properties | Entity becomes God object | Split into multiple entities with relationships |
| Constructor takes too much | Hard to create valid entity; validation scattered | Constructor only takes minimal data, rest via methods |
| Dependencies constructed in entity | Entity coupled to infrastructure | Inject dependencies, never construct them |
| Strings for identity | ID not type-safe (UserId vs OrderId confused) | Use value object for identity (UserId type) |

---

## Related Patterns

- [Value Object](value-object.md) — Immutable objects without identity (Email, UserId, Status)
- [Repository](repository.md) — How entities are persisted and retrieved
- [Use Case](use-case.md) — Business flows using entities
- [Dependency Injection](dependency-injection.md) — How entities receive their dependencies

---

**Updated:** 2026-04-26
