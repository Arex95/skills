# Initial Assessment Before Implementation

Read project context, understand architecture, clarify requirements, create plan, get approval, then implement.

**Category:** procedure  
**Updated:** 2026-04-26

---

## Why This Matters

Jumping straight to code:
- Code ends up in wrong module
- Violates architecture without knowing
- Doesn't match what user actually needs
- Requires rework

Spending 15 minutes on assessment:
- Code goes in correct location
- Architecture preserved
- Implementation matches need
- First attempt is correct

**Impact:** 15 minutes upfront saves 2+ hours rework.

---

## Core Concept

Before writing code: read context → understand architecture → clarify requirements → plan → get approval → implement.

---

## Step-by-Step Process

### Step 1: Read Project Context (5 minutes)

Read:
- `README.md` — Project overview and structure
- `AGENTS.md` — Architectural rules and constraints
- `METHODOLOGY.md` — Architecture philosophy
- `SKILLS_MAPPING.md` — Development workflow (if exists)
- `backlog/DECISIONS.md` — What decisions already made

**Question to answer:** "What makes this project unique? What are its non-negotiable rules?"

### Step 2: Understand Existing Architecture (5 minutes)

Look at:
- Project folder structure (modules, organization)
- Core layers (domain, ports, adapters)
- Where similar code exists
- How existing features are implemented

**Question to answer:** "Where would code like this belong? What pattern should I follow?"

### Step 3: Clarify Requirements (5 minutes)

Ask specific questions:

**Scope:** What exactly needs to be built? What's IN scope? OUT of scope?  
**Success:** How do we know this is done? What's the success criteria?  
**Constraints:** Performance? Security? Compatibility requirements? Timeline?  
**Trade-offs:** Do you prefer simple-but-limited OR complex-but-flexible? Speed OR quality?  
**Integration:** How fits with existing architecture? New modules or extend existing?

**Rule:** Don't assume. Ask until clear.

### Step 4: Create Implementation Plan (5 minutes)

Document:
- **Summary** — One paragraph overview
- **Architecture Changes** — What changes to overall structure
- **Files to Change** — Specific files and what changes
- **Implementation Steps** — Numbered steps to completion
- **Risks/Unknowns** — What could go wrong
- **Trade-Offs** — What chosen, what given up

**Question to answer:** "If someone reads this plan, do they understand exactly what will change?"

### Step 5: Present Plan & Get Approval (5 minutes)

Show plan to user:
- Explain architecture changes
- Highlight trade-offs
- Ask for approval

**Wait for:**
- Explicit approval ("yes, that's right")
- Corrections ("no, change X to Y")
- Clarifications ("what about Z?")

**DO NOT proceed until approved.**

### Step 6: Implement According to Plan

**Rules:**
- Follow plan exactly
- No scope creep (only what was clarified)
- No "optimizations" beyond what planned
- No extra features ("while I'm here")

**If something changes during implementation:**
- Stop
- Go back to user
- Ask: "This requires changing the plan. OK?"
- Get approval before proceeding

### Step 7: Verify Against Plan

After implementation:
- Does code match plan?
- All changes accounted for?
- Architecture preserved?
- Any unexpected changes?

If discrepancies:
- Explain what changed and why
- Get user approval
- Update documentation

---

## What This Looks Like

### ✅ Done Well

- 20 minutes reading + clarifying
- Clear plan created
- User approves plan
- Implementation matches plan exactly
- Code in correct location
- First attempt succeeds

### ❌ Done Poorly

- No reading of project context
- Assumptions about requirements
- No plan, jump straight to code
- Code in wrong location
- Work doesn't match user's need
- Rework required

---

## Verification

Before starting implementation:

- [ ] Project context read (README, AGENTS, METHODOLOGY)
- [ ] Existing architecture understood
- [ ] All clarifying questions asked
- [ ] Plan created and documented
- [ ] Plan presented to user
- [ ] Plan explicitly approved
- [ ] No assumptions about requirements

If ANY unchecked → Continue clarifying, don't start code.

---

## When to Skip This Process

**Skip only for:**
- Obvious typo fixes
- Simple bug fixes following existing pattern
- Documentation updates (no code changes)

**Don't skip for:**
- New features
- Architecture changes
- Cross-module refactoring
- New patterns

---

## Related Skills

- [Decision Rigor](../competencies/decision-rigor.md) — How to ask good clarifying questions
- [Code Organization](../competencies/code-organization.md) — How to identify where code belongs
- [Implementation Standards](implementation-standards.md) — What to do after plan is approved

---

## Questions to Ask Yourself

- Have I read the project context, or am I guessing about architecture?
- Do I understand where this code belongs?
- Have I asked all clarifying questions, or am I assuming?
- Do I have explicit approval to proceed, or just permission?

---

**Updated:** 2026-04-26
