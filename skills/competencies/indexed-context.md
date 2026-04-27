# Indexed Context

Build a lightweight index as you work. Document what you learn, not what you analyze. Avoid the trap of bloated context.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without indexing:
- AI reads entire codebase to understand structure
- Loads gigabytes of code into context
- Wastes tokens on re-reading same code
- Becomes slower as project grows
- Can't reference back efficiently

With indexing:
- Document each piece once as you encounter it
- Future work references index, not code
- Load only what you need to understand
- Keep context tight and focused
- Reference back in seconds, not minutes

**Impact:** Index reduces context size by 80-95%. Work becomes 10x faster.

---

## Core Concept

As you work on code, maintain a lightweight PROJECT_INDEX.md. For each piece you understand, write a self-contained extract (what it does, why, key details) + metadata (where it is, what it connects to). Future work: reference index first, load code only when necessary.

---

## Key Principles

### Extract Over Code

When you understand a piece of code, don't keep it loaded. Write an extract.

**Extract is:**
- One paragraph per piece
- Self-contained (reader doesn't need to understand other code)
- Actionable (reader can use it to understand the piece)
- Linked (tells reader where to find code if they need details)

**Bad extract:** "This is a controller"
**Good extract:** "OrderController (HTTP entry point for POST /orders). Validates userId and productIds, calls CreateOrderUseCase, returns orderId and totalPrice. Auth required: bearer token in Authorization header."

### Flows as Sequential Lists

When multiple files work together in a process, document as ordered sequence:
```
1. FileA - Anterior: none, Siguiente: FileB - Qué hace
2. FileB - Anterior: FileA, Siguiente: FileC - Qué hace
3. FileC - Anterior: FileB, Siguiente: none - Qué hace
```

Reader understands flow without reading any code.

### Index is Living Documentation

Index is not static. You maintain it actively as you work:
- **Discover a piece:** Extract it and add to index
- **Understand a flow:** Document it as sequential list
- **Refactor code:** Update extract to reflect changes
- **Rediscover something:** If extract was incomplete, enrich it
- **Architecture changes:** Reorganize flows and relationships
- **Code deleted:** Remove from index
- **Over weeks/months:** Index evolves alongside codebase

**Key:** Index is editable by AI. When you refactor, you update the index. When you find an extract was wrong, you fix it. The index lives alongside the code, not separately.

### Load Only What You Need

Rule: If it's in index, don't load code. If you need details:
1. Check index first
2. If extract is enough, stop
3. If you need more: click link, load code
4. After learning: update extract

This keeps context small and focused.

---

## What This Looks Like

### ✅ Done Well

**Index structure:**
```markdown
# PROJECT_INDEX.md

## Flujos

### Flujo: CreateOrder
1. OrderController - Siguiente: CreateOrderUseCase
2. CreateOrderUseCase - Anterior: OrderController, Siguiente: UserRepository
3. UserRepository - Anterior: CreateOrderUseCase, Siguiente: Order
4. Order - Anterior: UserRepository, Siguiente: OrderRepository
5. OrderRepository - Anterior: Order, Siguiente: OrderController

## Entidades

### User (domain/User)
Identity: userId (value object). State: email, status, lastLogin.
Methods: recordLogin(), deactivate(). Related flows: [CreateOrder, Auth]

### Order (domain/Order)
Aggregation root containing Items, Discounts. Methods: getTotalPrice(), 
markAsShipped(). Related flows: [CreateOrder, PaymentProcessing]
```

**Using index:**
- New task: "Add new payment method"
- Check index → see PaymentProcessing flow
- Read sequence: PaymentUseCase → PaymentProcessor → PaymentRepository → Order
- Load only these 4 files, not entire codebase
- Update index with new learnings

### ❌ Done Poorly

**Without index:**
- "I need to understand CreateOrder flow"
- Load: OrderController, CreateOrderUseCase, UserRepository, OrderRepository, User, Order
- Read all 6 files line-by-line
- 30 minutes of context loading
- Next task: repeat same process, reload same 6 files

**No extraction:**
- Understand User entity
- Next time: reload and re-understand (no extract to reference)
- Tokens wasted, time wasted

---

## How to Apply

### Step 1: Create PROJECT_INDEX.md

At project root:
```markdown
# PROJECT_INDEX.md

## Flujos

## Entidades

## Repositorios

## Use Cases

## Servicios
```

### Step 2: As You Work, Extract

When you understand a file:
1. Write one-paragraph extract
2. Note where it is (filepath)
3. Add to appropriate section
4. Link to related pieces

### Step 3: Document Flows

When multiple files work together:
1. List them in order (1, 2, 3...)
2. Each item: Anterior / Siguiente
3. Each item: what it does
4. Total: reader understands flow without code

### Step 4: Update Index When Adding Code

New file? Extract it before committing.
New flow? Document it in index.
Modified existing? Update extract if behavior changed.

### Step 5: Reference Index First

Next task:
1. Check index (5 seconds)
2. Is extract enough? Use it, skip code
3. Need details? Load only that file
4. Learned something new? Update extract

### Step 6: Update Index During Refactoring

When you refactor code:
1. Make changes to code
2. Update corresponding extract in index
3. If flow changed: update sequence (Anterior/Siguiente)
4. If new relationships: add cross-references
5. Commit both code and updated index

**Example:** You refactor UserRepository to use connection pool:
- Before: "Queries storage for email existence check"
- After: "Queries storage via connection pool (reuses connections). Caches recent users (TTL 5 min)."

### Step 7: Maintain Index Quality

**Weekly:**
- Scan extracts for accuracy
- Check if any refactored code has stale descriptions
- Add new pieces you encountered
- Remove code that was deleted

**During refactoring:**
- Never refactor without updating index
- If extract becomes misleading: fix immediately
- If architecture changes: reorganize flows

**Before commit:**
- Code + index updates in same commit
- Index reflects final state of code

### When to Use This Skill

- **Always:** Every time you touch code, consider extracting it
- **Especially for:** Complex flows, shared dependencies, frequently-accessed code
- **Critical for:** Large projects, long-term work, handoff to other AI

---

## Verification

Before committing code:

- [ ] Any code you understood: extracted to index
- [ ] Any code you refactored: extract updated to reflect changes
- [ ] Deleted code: removed from index
- [ ] Extracts are self-contained (reader doesn't need other files)
- [ ] Extracts have links to actual code (filepath)
- [ ] Multi-file flows documented as sequences (Anterior/Siguiente)
- [ ] New files added to index
- [ ] Index is lightweight (can be read in 5 minutes)
- [ ] Extracts include: what it does, why, key methods/params
- [ ] Related flows noted (cross-references)
- [ ] Index changes committed alongside code changes
- [ ] Stale extracts identified and updated

If ANY unchecked → Update index before committing.

---

## Extract Format

**Minimum extract:**
```
### [Name] ([filepath])
[One paragraph: what it does, why it exists, key behavior]
Related flows: [list]
Key methods/props: [list if entity or service]
```

**Example:**
```
### UserRepository (infrastructure/persistence/UserRepository)
CRUD repository for User entities. Implements UserRepository interface.
Methods: save(user), findById(id), findByEmail(email), delete(id).
Maps data from storage to User entities. No business logic,
only persistence. Related flows: [CreateOrder, UserAuthentication]
```

---

## Flow Format

**Ordered sequence:**
```
### Flujo: [Name]

1. **[File/Function]** ([filepath])
   - Anterior: [previous]
   - Siguiente: [next]
   - Qué hace: [one line]
   - Input: [what enters]
   - Output: [what exits]
```

**Example:**
```
### Flujo: CreateOrder

1. **OrderController** (api/OrderController)
   - Anterior: HTTP request
   - Siguiente: CreateOrderUseCase
   - Qué hace: Validates request, extracts userId and productIds
   - Input: POST request with userId, productIds
   - Output: validated data

2. **CreateOrderUseCase** (application/CreateOrderUseCase)
   - Anterior: OrderController
   - Siguiente: UserRepository.findById()
   - Qué hace: Orchestrates order creation, validates user
   - Input: userId, productIds
   - Output: User entity validation passed
```

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Index too detailed | Becomes another code copy; defeats purpose | Keep to one paragraph per piece |
| Not updating index after refactoring | Extracts become stale and misleading | Update every time code changes |
| Extract requires reading other files | Not self-contained | Rewrite to include context |
| Skipping extracting | No benefit later (same re-reading) | Extract everything you understand |
| Index in wrong format | Hard to scan and use | Follow template: flows as sequences, pieces as paragraphs |
| No links to code | Reader has to search for file | Always include filepath |
| Too many files in one flow | Sequence becomes unwieldy | Split into smaller flows |
| Loading code instead of checking index | Wastes context | Habit: check index first, always |
| Treating index as read-only | Stale extracts become misleading | Index is living doc; edit it constantly during work |
| Not committing index updates with code | Index diverges from reality | Always commit index + code together |
| Refactoring code without updating index | Next AI wastes time re-discovering | Never refactor without updating extract |

---

## Editing Index During Work

### When to Edit Extract

**You refactored a method:**
```
Before: "Validates email format and checks uniqueness"
After: "Validates email format, checks uniqueness, now caches 
        validation result for 1 hour to reduce DB queries"
```

**You discovered behavior was different than extract said:**
```
Extract said: "Returns null if not found"
Actual: "Throws UserNotFound exception if not found"
Action: Fix extract immediately
```

**You added new validation or error case:**
```
Extract said: "Validates user exists"
Added: "Also validates user is not deleted"
Action: "Validates user exists and is not deleted (throws if deleted)"
```

**You changed a dependency:**
```
Before: "Uses synchronous DB driver"
After: "Uses async DB driver with connection pooling"
```

### When to Update Flows

**You refactored the sequence:**
- Broke one flow into two smaller flows → create new section
- Merged two flows → consolidate into one
- Changed order of operations → update Anterior/Siguiente

**You added new middleware or interceptor:**
- New step in flow → insert with correct position
- Update Anterior/Siguiente of affected steps

### Never Commit Without Updating Index

**Rule:** Code changes + index updates in same commit.

**Process:**
1. Refactor code
2. Update extract(s)
3. Update flow(s) if affected
4. Commit both together

**Commit message:**
```
Refactor UserRepository caching

- Add caching layer to findById (1 hour TTL)
- Update index: UserRepository extract, Create Order flow
- Improves performance, reduces storage load
```

---

## Index Maintenance Schedule

**During work (continuous):**
- Edit extract immediately after code change
- Update flow when adding/removing steps
- Delete extract when code deleted

**End of task (before commit):**
- Review all changed extracts for accuracy
- Verify flows reflect current architecture
- Check links are valid

**Weekly:**
- Scan entire index for stale entries
- Update outdated descriptions
- Reorganize if structure changed

**Monthly:**
- Consolidate similar flows
- Remove dead extracts
- Reorganize sections if codebase structure changed

**Before handing off to another AI:**
- Ensure index is complete and current
- Verify all extracts are accurate
- Test that index alone can explain architecture

---

## Why This Works

**Tokens saved:** 1M tokens bloat → 50K index = 95% reduction
**Time saved:** Reload code (30 min) → check index (30 sec) = 60x faster
**Clarity:** Flow sequence → reader understands without code
**Scalability:** Index doesn't grow linearly with codebase size
**Reusability:** Extract useful for current and future work

---

## Related Skills

- [Code Organization & Modular Structure](code-organization.md) — Organization enables efficient indexing
- [Initial Assessment](../procedures/initial-assessment.md) — Index used to assess architecture quickly
- [Decision Rigor & Clarification-First](decision-rigor.md) — Index clarifies constraints before deciding

---

## Questions to Ask Yourself

- Have I extracted everything I understand, or just some pieces?
- If another AI needs to work on this: could they use the index to understand structure?
- Are flows documented as sequences, or scattered descriptions?
- When was the last time I checked the index vs. loading code?
- Is the index up-to-date with current codebase?

---

**Updated:** 2026-04-26
