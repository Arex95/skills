# Dependency Injection Pattern

Dependencies are provided from outside, never constructed inside. This enables testing, flexibility, and clean architecture.

**Category:** pattern  
**Updated:** 2026-04-26

---

## When to Use

Always. Every class that needs another class receives it, doesn't create it.

Applies to:
- Use cases receiving repositories
- Repositories receiving database connections
- Services receiving other services
- Anything that needs anything else

---

## Core Idea

**Bad:** Class constructs what it needs.
```
CreateOrderUseCase:
  constructor():
    userRepository = new DatabaseUserRepository(new Database())
    // Coupled to database implementation, can't test without it
```

**Good:** Class receives what it needs.
```
CreateOrderUseCase:
  constructor(userRepository: UserRepository):
    this.userRepository = userRepository
    // Depends on interface, not implementation
    // Can receive any UserRepository (database, mock, file-based)
```

---

## Three Ways to Inject

### 1. Constructor Injection (preferred)

```
CreateOrderUseCase:
  constructor(
    userRepository: UserRepository,
    orderRepository: OrderRepository
  ):
    this.userRepository = userRepository
    this.orderRepository = orderRepository
```

**Why:** Dependencies explicit and required upfront. Can't create instance without providing them.

### 2. Method Injection (when needed)

```
OrderService:
  process(order: Order, repository: OrderRepository):
    // method receives dependency when called
    repository.save(order)
```

**Why:** When dependency changes per call or is temporary/optional.

### 3. Property Injection (avoid)

```
CreateOrderUseCase:
  userRepository: UserRepository  // public, optional

useCase = CreateOrderUseCase()
useCase.userRepository = DatabaseUserRepository()  // set after creation
```

**Why:** Avoid. Dependencies not clear from constructor. Can create instance in invalid state.

---

## Structure

**Domain: defines what it needs (port/interface)**
```
UserRepository (interface):
  findById(id: UserId) → User or null
```

**Use case: receives what it needs (depends on interface)**
```
CreateOrderUseCase:
  constructor(userRepository: UserRepository):
    this.userRepository = userRepository
  
  execute(userId: UserId) → Order:
    user = this.userRepository.findById(userId)
    // ... rest of logic using user
```

**Infrastructure: provides implementation (adapter)**
```
DatabaseUserRepository implements UserRepository:
  constructor(database connection):
    this.db = database
  
  findById(id: UserId) → User or null:
    result = this.db.query("SELECT * FROM users WHERE id = ?", id)
    if result is empty: return null
    else: return User(result.id, result.email)
```

**Wiring: connect everything (bootstrap/setup)**
```
In application startup:
  db = create database connection
  userRepository = DatabaseUserRepository(db)
  useCase = CreateOrderUseCase(userRepository)
  
  // Now useCase is ready to use
  result = useCase.execute(userId)
```

Key points:
- Dependencies explicitly declared in constructor
- Implementations provided from outside
- All wiring happens in one place (bootstrap)
- Easy to swap implementations: use DatabaseUserRepository or MockUserRepository

---

## Why This Works in DDD + Hexagonal

**Dependency Inversion:** Core depends on interfaces (ports), infrastructure provides implementations (adapters).

**Testability:** In tests, inject mock repositories. No database needed.

```
MockUserRepository implements UserRepository:
  findById(id: UserId) → User or null:
    return User(id, "test@example.com")  // hardcoded test data

In test:
  mockRepo = MockUserRepository()
  useCase = CreateOrderUseCase(mockRepo)
  result = useCase.execute(userId)
  
// Tested without real database, no setup/teardown needed
```

**Flexibility:** Change database by changing one line in bootstrap.

**Explicit:** Reading constructor tells you exactly what this class needs.

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Class constructs dependencies | Coupled to implementation, can't test | Inject dependencies |
| Circular dependencies | A needs B, B needs A → infinite loop | Introduce mediator/service, break cycle |
| Too many dependencies | Constructor has 10+ parameters → God class | Split into smaller classes |
| Dependency in static method | Can't inject, can't test | Use instance method, inject dependency |
| No service container (manual wiring) | Wiring scattered everywhere | Use service container or factory |
| Optional dependencies unclear | Might be null, might not → defensive code | Mark optional with `?` type, handle in caller |
| Injecting concrete class instead of interface | Still coupled to implementation | Always inject interface, not concrete class |

---

## Service Container Pattern

For larger systems, use a service container to centrally manage wiring:

```
ServiceContainer:
  register(name: string, factory: function):
    this.services[name] = factory
  
  get(name: string):
    if name not in services:
      raise error "Service not registered"
    return this.services[name]()

// Setup in bootstrap
container = ServiceContainer()

container.register("database", () → 
  Database(connectionString))

container.register("userRepository", () → 
  DatabaseUserRepository(container.get("database")))

container.register("createOrderUseCase", () → 
  CreateOrderUseCase(container.get("userRepository")))

// In application code:
useCase = container.get("createOrderUseCase")
result = useCase.execute(userId)
```

// Use
const useCase = container.get("createOrderUseCase")
```

Benefits:
- Wiring in one place
- Easy to swap implementations
- Lazy loading (services created when needed)
- Dependency resolution automatic

---

## Related Patterns

- [Use Case](use-case.md) — Use cases receive repositories via injection
- [Repository](repository.md) — Repositories injected into use cases
- [Domain Entity](domain-entity.md) — Entities don't construct dependencies
- [Architecture](../competencies/architecture.md) — Dependency Inversion principle

---

**Updated:** 2026-04-26
