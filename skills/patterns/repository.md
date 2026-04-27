# Repository Pattern

Repository abstracts persistence. Domain core never knows about databases, APIs, or file systems. Repository provides a collection-like interface for entities.

**Category:** pattern  
**Updated:** 2026-04-26

---

## When to Use

Always. Every entity needs a way to be:
- Created and saved
- Retrieved by identity
- Queried by criteria
- Updated
- Deleted

The repository abstracts HOW this happens. Core knows it saves entities. Infrastructure knows it saves to database.

---

## Core Idea

Repository has two parts:
1. **Port (contract)** — Interface defined in domain core
2. **Adapter (implementation)** — Database-specific implementation in infrastructure

Domain core depends on the port, not the adapter. This is Dependency Inversion in action.

---

## Structure

**In domain/core: the PORT (interface defining what domain needs)**
```
UserRepository
  - save(user: User)
  - findById(id: UserId) → User or null
  - findByEmail(email: Email) → User or null
  - delete(id: UserId)
```

**In infrastructure/adapters: the ADAPTER (implementation for a specific storage)**
```
DatabaseUserRepository implements UserRepository
  constructor(database connection)
  
  save(user: User):
    execute: INSERT INTO users (id, email) VALUES (?, ?)
    return: success or error
  
  findById(id: UserId) → User or null:
    execute: SELECT * FROM users WHERE id = ?
    if no row: return null
    otherwise: reconstruct User from row data
  
  findByEmail(email: Email) → User or null:
    execute: SELECT * FROM users WHERE email = ?
    if no row: return null
    otherwise: reconstruct User from row data
  
  delete(id: UserId):
    execute: DELETE FROM users WHERE id = ?
    return: success or error
```

**In domain/core: use case depends on port, not adapter**
```
CreateUserUseCase
  constructor(userRepository: UserRepository)
  
  execute(email: Email) → UserId:
    userId = create new UserId
    user = create new User(userId, email)
    userRepository.save(user)  ← calls port, not adapter
    return userId
```

Key points:
- Port (interface) defined in domain (what core needs)
- Adapter (implementation) in infrastructure (how to actually persist)
- Dependency flows one direction: use case → port → adapter
- Use case doesn't know whether storage is database, file, API, or memory

---

## Why This Works in DDD + Hexagonal

**Isolation:** Domain core never imports database library. No coupling.

**Testability:** In tests, use memory implementation of repository. No database needed.

**Flexibility:** Switch database by swapping adapter. Behavior unchanged.

**Dependency Inversion:** Domain defines contract. Infrastructure implements it.

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Repository implemented in domain | Couples domain to infrastructure | Define interface (port) in domain, implementation in infrastructure |
| Rich query logic in domain | Domain depends on database API | Repository handles queries, returns domain objects |
| Entities converted to/from DTO in core | Mixing concerns | Convert in repository adapter, not in domain |
| Too many query methods | Repository becomes unmaintainable | Use generic query by criteria, or create specific methods only when needed |
| Repository knows about HTTP layer | Repository couples to controllers | Repository only knows about persistence, not HTTP |
| No abstraction (using database directly) | Impossible to test without database | Always use repository interface |
| Repository returns entity, caller modifies it | Entity state changed accidentally | Return immutable snapshots, or entity returns copy |

---

## Repository Interface Design

Good repository:
- `save(entity)` — Insert or update
- `findById(id)` — Get by identity
- `findAll()` — Get all (use with caution, pagination recommended)
- `delete(id)` — Remove
- `deleteAll()` — Remove all (use with extreme caution)

Sometimes add:
- `findBy(criteria)` — Query by specific criteria
- `count()` — Count matching entities
- `exists(id)` — Check existence

Avoid:
- Raw query methods (caller shouldn't write SQL)
- Methods returning primitives (always return domain objects)
- Methods that modify entities (repository only persists, doesn't change behavior)

---

## Related Patterns

- [Domain Entity](domain-entity.md) — Entities persisted by repositories
- [Use Case](use-case.md) — Use cases use repositories
- [Dependency Injection](dependency-injection.md) — Repository injected into use cases
- [Value Object](value-object.md) — Criteria for queries using value objects

---

**Updated:** 2026-04-26
