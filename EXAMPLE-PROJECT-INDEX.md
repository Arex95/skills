# Example: PROJECT_INDEX.md

Template showing how PROJECT_INDEX.md should look. This example uses generic concepts that apply to any project type (backend, frontend, mobile, etc.).

---

## Flows

### Flow: Fetch and Display Data

1. **UserInterface** (ui/UserInterface)
   - Previous: User triggers action (button click, page load, etc.)
   - Next: DataService.fetch()
   - What it does: Captures user intent, initiates data request
   - Input: user action or parameter
   - Output: request to fetch data

2. **DataService.fetch()** (services/DataService)
   - Previous: UserInterface
   - Next: Repository.query()
   - What it does: Prepares request, applies business rules
   - Input: parameters or filters
   - Output: validated query

3. **Repository.query()** (persistence/Repository)
   - Previous: DataService.fetch()
   - Next: Data transformation
   - What it does: Retrieves data from storage layer
   - Input: validated query
   - Output: raw data

4. **Data transformation** (services/DataTransformer)
   - Previous: Repository.query()
   - Next: UserInterface.display()
   - What it does: Converts raw data to presentable format
   - Input: raw data from storage
   - Output: formatted data

5. **UserInterface.display()** (ui/UserInterface)
   - Previous: Data transformation
   - What it does: Renders formatted data to user
   - Input: formatted data
   - Output: visible result to user

---

### Flow: Save User Action

1. **UserInterface** (ui/UserInterface)
   - Previous: User submits form or triggers save
   - Next: ValidationService.validate()
   - What it does: Collects user input
   - Input: form data or user action
   - Output: raw input data

2. **ValidationService.validate()** (services/ValidationService)
   - Previous: UserInterface
   - Next: BusinessLogic.process()
   - What it does: Validates input against rules
   - Input: raw input data
   - Output: validated data or error

3. **BusinessLogic.process()** (logic/BusinessLogic)
   - Previous: ValidationService.validate()
   - Next: Repository.save()
   - What it does: Applies business rules, transforms data
   - Input: validated data
   - Output: processed entity

4. **Repository.save()** (persistence/Repository)
   - Previous: BusinessLogic.process()
   - Next: UserInterface confirmation
   - What it does: Persists data to storage
   - Input: processed entity
   - Output: confirmation or error

5. **UserInterface confirmation** (ui/UserInterface)
   - Previous: Repository.save()
   - What it does: Shows success/failure to user
   - Input: save result
   - Output: user-visible confirmation

---

## Entities

### DataModel (domain/DataModel)
**Identity:** id (unique identifier)  
**State:** core attributes, metadata, status flags  
**Methods:** validate() → checks integrity, transform() → prepares for output  
**Related flows:** [Fetch and Display Data, Save User Action]  
**Invariants:** id immutable, required fields always present

### ValidationRule (domain/ValidationRule)
**Type:** Value object  
**Identity:** rule name and criteria  
**Purpose:** Defines what makes data valid or invalid  
**Used by:** [Save User Action flow]

---

## Repositories

### Repository (ports/Repository - Interface)
**Methods:** query(filter) → data, save(entity) → result, delete(id) → result  
**Implementation:** Concrete repository for your storage layer  
**Used by:** All flows that need to read or write data

---

## Services

### ValidationService (services/ValidationService)
**Methods:** validate(data, rules) → valid/invalid, getErrors() → error list  
**Purpose:** Centralizes validation logic, reusable across flows  
**Used by:** [Save User Action flow]

### DataTransformer (services/DataTransformer)
**Methods:** transform(raw) → formatted, reverse(formatted) → raw  
**Purpose:** Converts between storage format and presentation format  
**Used by:** [Fetch and Display Data flow]

### BusinessLogic (logic/BusinessLogic)
**Methods:** process(input) → output, applyRules(data) → result  
**Purpose:** Applies domain rules and business logic  
**Used by:** [Save User Action flow]

---

## How to Use This Template

1. **Identify your flows** - What sequences of actions happen in your app?
   - Example: login, search, filter, save, delete, etc.

2. **Document each flow** - List steps in order with Previous/Next relationships
   - First step: Previous is external trigger (user action, system event)
   - Middle steps: chain them together
   - Last step: shows what user/system sees

3. **Extract the entities** - What data objects matter in your domain?
   - What are their core properties?
   - What methods do they have?

4. **Note repositories** - How and where does data persist?
   - Interface (contract)
   - Implementation (your specific storage choice)

5. **Document services** - What shared logic crosses multiple flows?
   - Validation, transformation, calculations, etc.

---

## Maintenance Rules

### When to update?

**You added a new flow:**
```
Added: "User filters data"
Action: Add new flow section with complete sequence
```

**You refactored code:**
```
Before: "Validation happens in UI"
After: "Validation happens in ValidationService"
Action: Update which component does what
```

**You discovered behavior was wrong in the index:**
```
Extract said: "Saves to database"
Found: "Actually saves to cache first, then database in background"
Action: Fix extract immediately
```

### Always update index with code changes

**Rule:** Code changes + index updates in same commit

```
git commit "Extract validation to service

- Create ValidationService
- Update index: Save User Action flow, services section
"
```

### Update frequency

- **During work:** Edit extract when code changes
- **Before commit:** Verify all extracts match actual code
- **Weekly:** Scan for outdated descriptions
- **Monthly:** Remove deleted components from index

---

## Important Notes

- **This is a template** - Adapt it to your project's actual flows
- **Language/framework agnostic** - Works for web, mobile, desktop, backend
- **Index should match code** - If code changed, index must change
- **Index is for humans** - Should be readable and useful, not academic
