# Dependency Inversion Principle (DIP)

Make dependencies flow inward toward core. Core defines what it needs; infrastructure provides it.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without DIP:
- Core imports infrastructure (database, HTTP, external services)
- Swapping implementations requires rewriting core
- Testing core requires full infrastructure
- Circular dependencies trap you

With DIP:
- Core defines contracts (interfaces)
- Infrastructure implements those contracts
- Core testable with fake implementations
- Infrastructure swappable without touching core
- Dependencies flow one direction only

---

## Core Concept

Core defines what it needs via interfaces (contracts). Infrastructure provides implementations. Core never imports infrastructure. Both depend on contracts.

---

## Key Principles

### Core Defines Contracts

Core creates interfaces for what it needs: `UserRepository`, `EmailService`, `PaymentProcessor`.

Infrastructure implements those interfaces. Core receives implementations via injection, never constructs them.

### Dependencies Flow Inward

```
Infrastructure → Contracts ← Core
```

Core never points to infrastructure. Infrastructure points to core (via contracts).

### Contract Describes Capability, Not Implementation

Contract: "Give me a user by ID" (what core needs)  
NOT: "Query the Users table" (how implementation works)

---

## What This Looks Like

### ✅ Done Well

- Core defines `UserRepository` interface
- Database module implements `UserRepository`
- Core receives `UserRepository` via constructor
- Swapping database only requires new implementation
- Core testable with fake `UserRepository`

### ❌ Done Poorly

- Core imports database models or infrastructure code directly
- Core creates infrastructure instances internally
- Circular dependencies: Core → Infrastructure → Core
- Database changes force core changes
- Testing core requires full infrastructure setup

---

## How to Apply

### Step 1: Identify External Dependencies

What does core need from outside? (Database, email, payments, logging)

### Step 2: Create Contracts

Define interfaces in core for each dependency.

### Step 3: Implement in Infrastructure

Infrastructure modules implement those contracts.

### Step 4: Inject via Constructor

Core receives implementations at construction time. Never constructs dependencies.

### When to Use This Skill

- **Always:** Every dependency between layers
- **Every module interaction:** If A needs B, use contract

---

## Verification

- [ ] Core has zero imports from infrastructure modules
- [ ] All external dependencies are contracts (interfaces)
- [ ] No circular imports (would indicate violation)
- [ ] All dependencies injected via constructor
- [ ] Contract names describe capability (Repository, Service, Processor)
- [ ] Infrastructure never imported in core
- [ ] Swappable: Could replace implementation without changing core

If ANY unchecked → Refactor.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Core imports infrastructure directly | Couples core to implementation; can't swap | Create contract in core, inject implementation |
| Dependencies constructed internally | Breaks testability; couples to implementation | Inject via constructor parameter |
| No contract, just inject concrete class | Defeats purpose; can't swap | Create interface, pass interface type |
| Circular imports (A→B→A) | Breaks entire dependency graph | Introduce contract as mediator |
| Service locator (global registry lookups) | Hides real dependencies; hard to test | Use constructor injection explicitly |

---

## Related Skills

- [Architecture](architecture.md) — How DIP enables clean architecture
- [Code Organization](code-organization.md) — How to organize code to support DIP

---

## Questions to Ask Yourself

- If I swapped the database, would core code change? (Answer: No, never.)
- Can I test core without infrastructure? (Answer: Yes, always, using fakes.)
- Does core import any infrastructure modules? (Answer: No, it defines contracts.)

---

**Updated:** 2026-04-26
