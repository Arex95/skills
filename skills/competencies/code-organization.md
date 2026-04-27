# Code Organization & Modular Structure

Every piece of code belongs somewhere. No spaghetti code, no dumping grounds. Clear module boundaries.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without organization:
- Logic scattered across files randomly
- No clear reason why code is in location A vs B
- Adding feature requires modifying unrelated modules
- Dependencies tangled (circular, unclear)
- New developer can't find where to put code

With organization:
- Every code piece has a clear, specific purpose
- Every piece belongs in a specific location
- Adding features extends existing modules
- Dependencies flow clearly
- New developer can follow pattern

---

## Core Concept

Code is never "placed somewhere"—it belongs somewhere. Before writing code, identify its responsibility, find the responsible module, add to that module.

---

## Key Principles

### Every Piece Has a Place

**Pattern:**
```
Feature request → Identify responsibility → Find module → Add to module
```

Never: Put code in convenient location. Always: Put code in responsible location.

### Module Boundaries Are Clear

Each module has:
- **Single Responsibility** — One reason to change
- **Clear Purpose** — What it does (in name, organization, intent)
- **Public Interface** — What it exposes
- **Private Implementation** — How it works (hidden)
- **Clear Neighbors** — Which modules it depends on

### No Tangled Logic

Tangled code:
- Presentation mixed with business logic
- Data access mixed with domain logic
- Utilities scattered across modules
- Callbacks/hooks everywhere, no clear flow

Organized code:
- Each concern in its layer
- Clear data flow
- Utilities grouped by responsibility
- Control flow is traceable

### Layered Organization

Code organized in clear layers:
- **Core (Domain)** — Business logic, entities, rules
- **Ports (Contracts)** — Interfaces defining boundaries
- **Adapters (Infrastructure)** — Database, HTTP, external services
- **Application** — Orchestration, use cases, workflows

---

## What This Looks Like

### ✅ Done Well

- Code organized by responsibility, not type
- Module names reflect purpose
- Clear public interface, private details hidden
- No God classes/modules (reasonable size)
- Utilities grouped by responsibility
- Dependencies flow clearly (inward)
- New developer can find where to add code

### ❌ Done Poorly

- Code scattered across modules randomly
- Module names don't describe purpose
- Everything exposed publicly
- God modules (5000+ line files)
- `utils/` dumping ground (thousands of functions)
- Circular dependencies everywhere
- No way to navigate where code belongs

---

## How to Apply

### Step 1: Identify Responsibility

What is this code's responsibility? What problem does it solve?

### Step 2: Find Responsible Module

Which module owns this responsibility?

### Step 3: Verify Module Exists

Does that module exist? If not, create it.

### Step 4: Add to Module

Never scatter code. Add to module that owns it.

### When to Use This Skill

- **Always:** Every piece of code you write
- **Especially for:** Cross-module code (most likely to be scattered)

---

## Verification

- [ ] Every piece of code has a clear responsibility
- [ ] Responsibility belongs in a specific module
- [ ] Code doesn't scatter across modules
- [ ] Module structure reflects responsibilities
- [ ] Layer boundaries clear (core, ports, adapters)
- [ ] No tangled dependencies
- [ ] God classes/modules broken up
- [ ] Utilities grouped by responsibility

If ANY unchecked → Reorganize.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Code in convenient location | Hard to find; scattered logic | Move to responsible module |
| Circular dependencies | Breaks entire graph; can't untangle | Introduce contract as mediator |
| Scattered duplicate logic | Maintenance nightmare; bugs in multiple places | Extract to shared module immediately |
| Missing public interface | Module exposes everything; can't change internals | Define explicit public interface |
| God classes (5000+ lines) | Multiple unrelated responsibilities | Split into smaller, focused modules |
| `utils/` dumping ground | Thousands of unrelated functions | Group by responsibility |
| No clear layer separation | Logic mixed across layers | Organize: core, ports, adapters, app |

---

## Related Skills

- [Architecture](architecture.md) — How DDD + Hexagonal provides organization
- [Dependency Inversion](dependency-inversion.md) — How dependencies should flow
- [Code Rigor](code-rigor.md) — How linters enforce organization

---

## Questions to Ask Yourself

- If I need to find similar code, where would I look?
- Could another developer understand where to add new code?
- Are any modules doing multiple, unrelated things?
- Are there circular dependencies in the codebase?

---

**Updated:** 2026-04-26
