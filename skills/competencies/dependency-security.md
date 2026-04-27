# Dependency Security & Intentionality

Never use packages published less than 48 hours ago. Always make intentional, vetted dependency decisions.

**Category:** competency  
**Updated:** 2026-04-26

---

## Why This Matters

Without care:
- Malicious package published → your app compromised
- Package with vulnerability → exploited in production
- Package too new → undetected bugs
- Transitive dependencies unknown → supply chain attack

With the 48-hour rule:
- Community has time to discover issues
- Vulnerabilities get disclosed and patched
- Real-world testing validates package
- Risk is mitigated significantly

---

## Core Concept

The 48-hour rule: NO package versions published less than 48 hours ago. This gives the community time to discover and report issues before you use it.

---

## Key Principles

### The 48-Hour Minimum

**Rule:** Never use any package version published less than 48 hours ago.

**Applies to:**
- Direct dependencies (explicitly added)
- Transitive dependencies (pulled in by other packages)
- All environments (dev, staging, production)

**Why 48 hours:**
- Catches obvious bugs (immediate complaints)
- Reveals security issues (early disclosures)
- Allows patch releases
- Demonstrates real-world viability

### Intentional Dependency Decisions

Every dependency added must be:

1. **Necessary** — Can't build simply with core language
2. **Vetted** — Used elsewhere at scale, proven stable
3. **Maintained** — Active maintainer, responsive to issues
4. **Secure** — No known vulnerabilities
5. **Minimal** — Smallest possible surface area

### Dependency Audit

Before adding any dependency:
- Check last release date (>48 hours old)
- Check security advisories
- Check maintenance status
- Check dependency count (transitive deps)
- Check code quality (tests, type coverage)

Missing ANY = red flag.

### Transitive Dependency Awareness

You inherit risk from ALL transitive dependencies.

**Principle:**
- You're responsible for entire dependency tree
- Lock files must be committed (reproducible builds)
- Regular audits of entire tree, not just direct deps

---

## What This Looks Like

### ✅ Done Well

- Package published >48 hours ago
- No security vulnerabilities detected
- Maintainer actively responding to issues
- Lock file committed
- Dependency tree audited regularly
- Intentional choice documented

### ❌ Done Poorly

- Package published yesterday
- Known vulnerabilities ignored
- Maintainer inactive (last commit 2 years ago)
- Lock file not committed
- No audit of transitive dependencies
- Added because "it's cool"

---

## How to Apply

### Step 1: Identify What Problem It Solves

What problem does this dependency solve?

### Step 2: List Candidate Packages

Which packages solve this problem?

### Step 3: Vet Each Candidate

- Publication date (>48 hours)
- Maintenance status (active)
- Security (no known vulns)
- Size (minimal surface area)
- Tests and types (quality signal)

### Step 4: Select the Safest, Most Maintained

Not the most popular. Not the newest. The safest, most maintained.

### Step 5: Document the Decision

Why this dependency? Why not others?

### When to Use This Skill

- **Always:** Every dependency decision
- **Even for:** One-line utilities (consider: is it necessary?)

---

## Verification

- [ ] Package version published >48 hours ago
- [ ] No known security vulnerabilities
- [ ] Maintainer actively responding to issues
- [ ] Package actually necessary (not convenience)
- [ ] Transitive dependency count reasonable
- [ ] Lock file committed
- [ ] Security audit tool configured and passing
- [ ] Dependency choice documented

If ANY unchecked → Do not add dependency.

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Using brand-new package | Undetected bugs; could be malicious | Wait 48 hours minimum |
| Ignoring transitive deps | Inherit unknown vulnerabilities | Audit entire tree regularly |
| Using unmaintained package | No patches for bugs/security issues | Check last commit date |
| Adding for convenience | Technical debt; hard to remove later | Consider: is it really necessary? |
| Not committing lock file | Different versions per developer | Always commit lock files |
| No security audit | Vulnerabilities slip through | Run security audit before every commit |

---

## Related Skills

- [Code Rigor](code-rigor.md) — How security audit is enforced
- [Avoiding Generic Solutions](avoiding-generic-solutions.md) — How to make intentional choices

---

## Questions to Ask Yourself

- Is this package really necessary, or could I build it?
- Has this version been in the wild for >48 hours?
- Does the security audit show any vulnerabilities?
- Is the maintainer actively responding to issues?

---

**Updated:** 2026-04-26
