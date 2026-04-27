# Avoiding Generic Solutions

Popular solutions are optimized for average problems. Your system is NOT average. Choose solutions FOR your constraints, not despite them.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without constraint-driven decisions:
- Default to popular solution because it's well-known
- System scales, popular solution causes pain
- Heavy refactoring required to move away from it
- Time/cost spent fixing bad initial choice exceeds time to build custom solution

With constraint-driven decisions:
- Solution chosen FOR your specific constraints
- Scales cleanly without workarounds
- Custom solution (when needed) is simpler than generic + patches
- First choice is right choice

**Impact:** At scale (100K+ users), constraint-optimized systems outperform generic ones by 10x.

---

## Core Concept

Every system has constraints (data model, scaling pattern, trust model, failure modes, integration points, team size). Solution should be chosen FOR YOUR CONSTRAINTS, not despite them. Popularity is not evidence of fitness.

---

## Key Principles

### Constraints Determine Solution

Every system has specific constraints:
- **Data model** — Shape of entities and relationships
- **Scaling pattern** — Read-heavy? Write-heavy? Both?
- **Trust model** — Who can access what?
- **Failure modes** — What must NEVER fail? What can degrade?
- **Integration points** — How does it connect to other systems?
- **Team size** — Can small team maintain it?

**Rule:** Identify constraints first, then choose solution that honors them naturally (not via workarounds).

### Popularity ≠ Correct

Popularity means:
- Solves many average problems
- Has good documentation
- Large community exists

Popularity does NOT mean:
- Correct for your constraints
- Scales to your size
- Fits your domain

**Rule:** Consult your constraints, not popularity metrics.

### Custom Solution When Constraints Conflict

Custom solution is appropriate when:
- Generic solution requires workarounds for core behavior
- Scaling bottleneck is IN the generic solution
- System constraints conflict with solution design
- Team can sustain and maintain it

---

## What This Looks Like

### ✅ Done Well

- System constraints explicitly documented before choosing solution
- Generic solution chosen because it fits constraints naturally
- If custom solution built: clear constraint it solves for
- If custom solution built: simpler than generic + workarounds
- No "future-proofing" beyond actual constraints
- Solution naturally handles primary constraint (not via workaround)

### ❌ Done Poorly

- Solution chosen because it's popular or "everybody uses it"
- Constraints discovered during implementation (too late)
- Generic solution + multiple workarounds (code smell)
- Custom solution over-engineered to handle hypothetical problems
- Team can't maintain custom solution (becomes technical debt)
- No documentation of why this solution over alternatives

---

## How to Apply

### Step 1: Identify Constraints

Write down actual system constraints:
- What is the primary characteristic? (Read-heavy? Complex domain? High concurrency?)
- What is the worst-case failure? (Data loss? Unavailable? Inconsistency?)
- What scales fastest (data? Users? Complexity)?

### Step 2: Test Generic Solutions

For each leading option:
- Does it handle your primary constraint naturally? (Not via workaround)
- At your expected scale, where is the first bottleneck?
- How much code is workaround vs. core feature?

### Step 3: Evaluate Custom Path

- What is the simplest custom solution?
- Can team maintain it?
- Does it honor all constraints?
- Is it simpler than generic + workarounds?

### Step 4: Decide Based on Constraints

If custom is simpler and fits constraints better → build custom.
If generic handles constraints elegantly → use generic.

### When to Use This Skill

- **Always:** Architecture decisions, framework selection, solution design
- **Especially for:** When choosing between popular option vs. custom approach

---

## Verification

Before implementing any solution:

- [ ] Constraints of system explicitly documented
- [ ] Generic solution evaluated against these specific constraints
- [ ] Decision justified by constraints, not popularity
- [ ] If custom solution: clear constraint it solves for
- [ ] If custom solution: simpler than generic + workarounds
- [ ] Team capability assessed (can maintain it?)
- [ ] No "future-proofing" beyond actual constraints
- [ ] Solution naturally handles primary constraint (not via workaround)

If ANY unchecked → Revisit decision.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Default to popular solution | Choosing without examining constraints | Document constraints first, evaluate solution against them |
| "Everybody uses it" | Popularity is not evidence of fitness | Consult YOUR constraints, not popularity metrics |
| Avoiding "reinventing the wheel" | Sometimes the wheel needs different shape for your track | Optimize for your constraints, not generality |
| Building custom too early | Custom before understanding constraints | Understand constraints before choosing custom |
| Over-engineering custom solution | Becomes more complex than generic + workarounds | Solve YOUR problem, not all problems |
| Ignoring team capability | Custom solution team can't maintain becomes debt | Assess team before committing to custom |
| Not documenting why custom | Future devs assume it's unnecessary complexity | Explicitly document constraints it solves for |

---

## Related Skills

- [Decision Rigor & Clarification-First](decision-rigor.md) — How to clarify constraints systematically
- [Code Organization & Modular Structure](code-organization.md) — How organization enables constraint-driven choices
- [Dependency Inversion](dependency-inversion.md) — How dependencies should flow based on constraints

---

## Questions to Ask Yourself

- Have I documented actual constraints, or am I guessing?
- Would a generic solution handle my primary constraint naturally?
- Am I choosing this solution because it fits my constraints, or because it's popular?
- If custom: is it simpler than generic + workarounds?
- Can my team sustain this solution over time?

---

**Updated:** 2026-04-26
