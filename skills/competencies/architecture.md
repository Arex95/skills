# Domain-Driven Design + Hexagonal Architecture

Isolate business logic from infrastructure so systems scale without constant refactoring.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without architecture:
- Business logic gets tangled with database/HTTP/framework details
- Adding features requires modifying unrelated code
- Testing requires spinning up full infrastructure
- Scaling to microservices means rewriting core logic

With DDD + Hexagonal:
- Business logic lives in isolated core
- Infrastructure is replaceable (swap database, change framework)
- Core testable without external dependencies
- Same core logic scales from monolith to distributed system

---

## Core Concept

**Domain-Driven Design:** Business logic is separate from delivery mechanisms.  
**Hexagonal Architecture:** Core logic talks to external world ONLY through defined contracts (ports), implemented by adapters.

---

## Key Principles

### Core Owns Contracts, Infrastructure Implements Them

Core defines what it needs (interfaces). Infrastructure provides implementations. Core never imports infrastructure directly.

### Dependencies Flow Inward

Infrastructure → Adapters → Ports → Core

Core never points outward. Core doesn't know about databases, HTTP, external APIs.

### Layers Are Distinct

- **Core:** Domain entities, services, business logic
- **Ports:** Interfaces defining what core needs
- **Adapters:** Database, HTTP handlers, external API clients

---

## What This Looks Like

### ✅ Done Well

- Core module defines interfaces for what it needs
- Infrastructure modules implement those interfaces
- Core uses injected implementations, never imports infrastructure modules directly
- Swapping a persistence implementation requires only adapter changes
- Core testable with fake implementations

### ❌ Done Poorly

- Core directly imports database models or infrastructure code
- Database changes break core services
- Core can't be tested without full infrastructure
- Adding feature requires modifying multiple layers
- Tight coupling to framework/database details

---

## How to Apply

### Step 1: Identify Boundaries

What does core need from infrastructure? (Persistence, authentication, external APIs)

### Step 2: Define Contracts

Create interfaces in core for each boundary (UserRepository, EmailService, PaymentProcessor).

### Step 3: Implement in Adapters

Infrastructure modules implement those contracts.

### Step 4: Inject Contracts

Core receives implementations via constructor injection. Never constructs dependencies.

### When to Use This Skill

- **Always:** All systems, from MVP onward
- **Even for:** Simple CRUD apps (prevents lock-in later)

### When NOT to Use This Skill

- Never. This applies universally.

---

## Verification

- [ ] Core has zero imports from infrastructure modules
- [ ] All external dependencies entered via contracts (interfaces)
- [ ] No circular imports (core → infrastructure or reverse)
- [ ] Core testable without external infrastructure
- [ ] Each layer has single clear responsibility
- [ ] Contracts defined before implementations exist

If ANY unchecked → Refactor before proceeding.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Core imports concrete models from modules | Couples logic to implementation; changes break core | Create contract in core, implement in module, inject |
| Infrastructure depends on other infrastructure | Creates tangled web; hard to test, hard to swap | All infrastructure dependencies via core contracts |
| Contracts defined after implementation | Interfaces become wrappers, not real contracts | Design contract first, then implement |
| Contracts describe implementation (what class does) instead of capability (what core needs) | Over-specifies interface; limits swapping | Focus on capability: "Give me a user by ID", not "Query the Users table" |

---

## Related Skills

- [Dependency Inversion](dependency-inversion.md) — How to structure dependencies properly
- [Code Organization](code-organization.md) — How to place code in correct modules
- [Decision Rigor](decision-rigor.md) — How to choose this architecture

---

## Questions to Ask Yourself

- If I swapped my database tomorrow, how many files would I need to change? (Answer: Only adapters. If more, architecture is wrong.)
- Can I test this core logic without starting a database? (Answer: Yes, always. If no, core has infrastructure dependency.)
- Is my interface naming focused on what the core needs (capability) rather than how it's implemented (specifics)? (Answer: Yes, always. The name expresses the responsibility or need, independent of implementation details.)

---

**Updated:** 2026-04-26
