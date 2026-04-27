# Security Audit Tool

Security audit verifies dependencies are safe and free of known vulnerabilities. It's the gate preventing malicious or vulnerable code from entering repository.

**Category:** tool  
**Updated:** 2026-04-26

---

## What It Verifies

- **Known vulnerabilities** — Dependencies with published security issues
- **Package age** — Dependencies must be >48 hours old
- **Maintenance status** — Dependencies actively maintained
- **Transitive dependencies** — All dependencies of dependencies
- **Dependency integrity** — Lock file matches current state

---

## Configuration Requirements

**Minimum requirements:**
- Security audit tool configured and passing
- Lock file committed (reproducible builds)
- No known vulnerabilities allowed
- All dependencies >48 hours old
- Regular audits (at least weekly)

**Tool-agnostic approach:** Use whatever security audit your package manager provides.

---

## Execution

**Pre-commit:** Security audit must pass.

**In CI:** Security audit must pass on every commit.

---

## The 48-Hour Rule

**Rule:** Never use package version published less than 48 hours ago.

**Why:**
- Gives community time to discover malicious code
- Allows bug reports and patches
- Demonstrates real-world viability
- Prevents being first user of potentially broken code

**Applies to:**
- Direct dependencies (explicitly added)
- Transitive dependencies (pulled in by others)
- All environments (dev, staging, production)

---

## What Passes vs. Fails

**Passes:**
- No known vulnerabilities detected
- All dependencies >48 hours old
- Lock file committed and matches current dependencies

**Fails:**
- Known vulnerabilities detected in any dependency
- Dependency published less than 48 hours ago
- Lock file not committed (dependencies not reproducible)

---

## If Audit Fails

**Never commit code that fails security audit.**

**Process:**

1. **If vulnerability in direct dependency:**
   - Update to patched version of that dependency
   - If no patch available: remove dependency or isolate its usage
   - Document in PR why you kept vulnerable dependency (rare)

2. **If vulnerability in transitive dependency:**
   - Update the parent dependency
   - If update not available: report issue to maintainer
   - Contact dependency maintainer through public channels

3. **If package too new:**
   - Wait 48 hours
   - Add later

4. **If lock file missing:**
   - Commit lock file to repository

---

## Dependency Decision Process

Before adding any dependency:

1. **Identify what problem it solves**
2. **List candidate packages**
3. **Check each candidate:**
   - Published >48 hours ago? ✓
   - No security vulnerabilities? ✓
   - Actively maintained? ✓
   - Reasonable size (transitive deps)? ✓
4. **Evaluate necessity:** Is it really needed or convenience?
5. **Choose safest, most maintained (not newest, not most popular)**
6. **Document the decision** (in PR or code comment)

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Using brand-new package | Undetected bugs, might be malicious | Wait 48 hours minimum |
| Ignoring transitive dependencies | Inherit vulnerabilities you don't control | Audit entire tree regularly |
| Adding for convenience | Technical debt; hard to remove | Evaluate necessity first |
| Not committing lock file | Dependencies vary per developer | Always commit lock files |
| No security audit in CI | Vulnerabilities slip through undetected | Configure audit tool in pipeline |
| Suppressing audit findings | Defeats purpose of auditing | Fix vulnerabilities, don't suppress |
| Assuming package manager automatically safe | Package managers don't verify security | Always run audit before commit |

---

## Transitive Dependency Management

**Reality:** You inherit risk from all transitive dependencies.

**Best practice:**
- Know your direct dependencies
- Audit transitive dependencies regularly
- Monitor for updates to critical transitive deps
- Understand supply chain risks


---

## Regular Auditing

**Weekly:**
- Run security audit
- Check for updates to critical dependencies
- Monitor security advisories

**Monthly:**
- Audit entire dependency tree
- Update patch versions (1.2.3 → 1.2.4)
- Review new vulnerabilities in ecosystem

**On risk:**
- Zero-day vulnerability disclosed
- Dependency maintainer compromised
- New attack pattern emerges

---

## Supply Chain Security

**Principles:**
- Verify package integrity (checksums, signatures)
- Trust only official package sources
- Review package source code (if critical)
- Use lock files for reproducibility
- Audit regularly

**Red flags:**
- Package name similar to popular package (typosquatting)
- Package published with no history
- Package deleted from registry then reappeared
- Package unusual for stated purpose
- Maintainer suddenly changed
- Package requires unusual permissions

---

## Related Tools

- [Linter](linter.md) — Code quality enforcement
- [Typecheck](typecheck.md) — Type safety
- [Formatter](formatter.md) — Format consistency
- [Test Coverage](test-coverage.md) — Behavioral verification

---

**Updated:** 2026-04-26
