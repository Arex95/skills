# Use Case Pattern

Use cases orchestrate business flows. They use entities, value objects, and repositories to accomplish a business goal. They live in the application layer, between domain core and infrastructure.

**Category:** pattern  
**Updated:** 2026-04-26

---

## When to Use

Every business action is a use case:
- User registration
- Order creation
- Payment processing
- Report generation
- Search execution

Use cases are how external world (controllers, APIs, jobs) interacts with domain logic.

---

## Core Idea

A use case:
1. **Takes input** — Request data from external world
2. **Uses domain** — Creates/modifies entities, uses repositories
3. **Returns output** — Response to external world
4. **Is testable** — Tests don't need HTTP, database, or external services

Use case is pure orchestration: "if input is valid, do this sequence of domain operations."

---

## Structure

**Input/Output Contracts (defined separately from domain)**
```
CreateOrderRequest:
  - userId: string
  - productIds: array of strings

CreateOrderResponse:
  - orderId: string
  - totalPrice: number
```

**Use Case (orchestrates business flow)**
```
CreateOrderUseCase:
  constructor(userRepository, productRepository, orderRepository)
  
  execute(request: CreateOrderRequest) → CreateOrderResponse:
    1. Load domain objects
       user = userRepository.findById(request.userId)
       if not found: raise "User not found"
       
       products = []
       for each productId in request.productIds:
         product = productRepository.findById(productId)
         products.add(product)
    
    2. Create domain object using entities
       order = Order(new OrderId, user, products, now)
    
    3. Validate business rules (delegated to entity)
       if order.totalPrice > user.creditLimit:
         raise "Order exceeds credit limit"
    
    4. Persist through repository
       orderRepository.save(order)
    
    5. Map entity to output interface
       return CreateOrderResponse(
         orderId: order.id,
         totalPrice: order.totalPrice
       )
```

**External world calls use case (e.g., HTTP controller)**
```
HTTP POST /orders:
  request body: { userId, productIds }
  
  1. Instantiate use case with dependencies
     useCase = CreateOrderUseCase(userRepo, productRepo, orderRepo)
  
  2. Execute use case
     result = useCase.execute(request)
  
  3. Handle result or error
     if success: return HTTP 200 with result
     if error: return HTTP 400 with error message
```

Key points:
- Input/output are separate interfaces (not domain entities)
- All dependencies injected (repositories, domain services)
- Domain logic executed through entities and repositories
- Business rules validated (in entity or use case)
- Errors handled and propagated to external world

---

## Why This Works in DDD + Hexagonal

**Separation of concerns:** Use case is pure orchestration. Domain handles rules. Infrastructure handles persistence.

**Testability:** Test use case with mock repositories. No database needed. No HTTP needed.

**Flexibility:** Same use case can be called by HTTP API, CLI, job queue, or webhook.

**Type Safety:** Input/output interfaces are separate from domain entities. Strong typing at boundaries.

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Business logic in use case | Should be in entities/domain services | Move to entity methods, call from use case |
| Use case returns entity directly | Couples API to domain entity | Define separate output interface, map entity to it |
| Use case validates domain rules | Rules scattered, hard to change | Put validation in entities, use case calls it |
| No error handling | Errors propagate as exceptions | Catch business errors, return meaningful messages |
| Too much in one use case | Hard to test, reuse, understand | Split into smaller use cases |
| Use case constructs dependencies | Coupling, hard to test/swap | Inject all dependencies |
| No input validation | Invalid data reaches domain | Framework/controller validates input before use case |
| Use case has side effects beyond persistence | Hard to test, reason about | Keep side effects limited and documented |

---

## Use Case Naming

Good names:
- `CreateOrderUseCase`
- `PaymentProcessingUseCase`
- `UserRegistrationUseCase`
- `SearchProductsUseCase`

Bad names:
- `OrderService` (too generic, could be many things)
- `Handler` (what does it handle?)
- `Processor` (what does it process?)

Name should describe the business action, not technical role.

---

## Related Patterns

- [Domain Entity](domain-entity.md) — Entities used by use cases
- [Repository](repository.md) — Repositories injected into use cases
- [Dependency Injection](dependency-injection.md) — How dependencies are provided
- [Value Object](value-object.md) — Input/output interfaces use value objects

---

**Updated:** 2026-04-26
