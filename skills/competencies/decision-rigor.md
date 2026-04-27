# Decision Rigor & Clarification-First

Never make rushed decisions. Ask clarifying questions, understand constraints, plan before deciding, get approval before implementing.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Rushed decisions:
- Based on assumptions, not facts
- Require rework when reality differs
- Hide trade-offs from user
- Waste time implementing wrong solution

Rigorous decisions:
- Based on clear understanding
- Match user's actual need
- Trade-offs explicit
- First implementation correct

**Impact:** 10 minutes of clarification saves 2+ hours of rework.

---

## Core Concept

Before making ANY architectural or implementation decision: ask clarifying questions, understand constraints, present options with trade-offs, get explicit approval.

---

## Key Principles

### Clarification Before Decision

**Rule:** Never decide without full context.

**When to clarify:**
- Requirement is ambiguous
- Multiple valid interpretations exist
- Constraints are unclear
- Success criteria not defined
- Trade-offs exist

**How to clarify:**
- Ask specific questions (not vague ones)
- Present options with trade-offs
- Wait for explicit answer
- Document what was clarified

### No Assumptions

Assumption = interpretation made without asking.

**Mistakes from assumptions:**
- "They probably mean X" → Actually means Y
- "Best approach is obvious" → User prefers different trade-off
- "Pattern is to do it this way" → This project does differently
- "Not mentioned, so not important" → It's critical

**Rule:** If not explicitly stated, ask. Don't assume.

### Present Trade-Offs Explicitly

No perfect solution exists. All solutions have trade-offs.

**Pattern:**
- Option A: Faster to build, but less flexible
- Option B: More setup, but scales to 10x users
- Option C: Simplest, but hard to modify later

Never hide trade-offs. Make user aware of what each costs.

---

## What This Looks Like

### ✅ Done Well

- Ambiguity identified and clarified
- Options presented with explicit trade-offs
- User confirms understanding
- Decision based on clear information
- No rework required

### ❌ Done Poorly

- Assumption made without asking
- Trade-offs hidden from user
- User says "that's not what I wanted"
- Rework required
- Frustration and wasted time

---

## How to Apply

### Step 1: State the Ambiguity

"I understand you need X, but I'm unclear about Y. Is it:
- A) This
- B) That
- C) Something else?"

Be specific. Don't ask "what do you want?" Ask targeted questions.

### Step 2: Present Options

If multiple valid approaches:
- Option 1: Trade-offs are...
- Option 2: Trade-offs are...
- Option 3: Trade-offs are...

### Step 3: Confirm Understanding

"So if I understand: You want X, with constraint Y, accepting trade-off Z. Right?"

Get explicit confirmation.

### Step 4: Proceed Based on Approval

Only after clarification confirmed, decide and implement.

### When to Use This Skill

- **Always:** Architectural decisions, implementation choices
- **Especially for:** Ambiguous requests, multiple valid approaches

---

## Verification

Before making any decision:

- [ ] Requirement stated explicitly (not implied)
- [ ] Ambiguities identified
- [ ] Options presented with trade-offs
- [ ] User confirmed choice
- [ ] Constraints clearly understood
- [ ] No assumptions about requirements

If ANY unchecked → Ask more, don't decide yet.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Assuming interpretation | Implement wrong thing; rework required | Ask clarifying questions first |
| Hiding trade-offs | User chooses without knowing cost | Present options with explicit trade-offs |
| Rushing to code | Discover requirements while building | Plan and clarify first |
| Following templates blindly | Solution doesn't fit constraints | Ask about this project's specific needs |
| No self-doubt | Commit to approach without verifying | Pause and ask: "Could I be wrong?" |

---

## Related Skills

- [Avoiding Generic Solutions](avoiding-generic-solutions.md) — How to choose FOR constraints
- [Initial Assessment](../procedures/initial-assessment.md) — How to clarify systematically

---

## Questions to Ask Yourself

- Have I asked all clarifying questions, or am I assuming?
- Have I identified all trade-offs, or hidden any from user?
- Do I have explicit approval, or just permission?
- Could I be wrong about this interpretation?

---

**Updated:** 2026-04-26
