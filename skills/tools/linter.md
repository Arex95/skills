# Linter Tool

Linter enforces code style, catches common mistakes, and prevents obvious bugs before code enters repository.

**Category:** tool  
**Updated:** 2026-04-26

---

## What It Verifies

- **Style violations** — Inconsistent spacing, naming conventions
- **Common mistakes** — Unused variables, unreachable code, missing break statements
- **Security issues** — Hardcoded secrets, SQL injection patterns
- **Best practices** — Unused imports, debugging output in production code
- **Complexity** — Cyclomatic complexity, cognitive complexity

---

## Configuration Requirements

Linter must be configured at **strictest level.** No relaxed settings.

**Minimum settings:**
- All built-in rules enabled
- No rules disabled or ignored globally
- No rules set to "warning" (must be "error")
- Custom rules for project-specific patterns (if any)

**Tool-agnostic approach:** Use whatever linter your language provides configured at strictest level.

---

## Execution

**Pre-commit:** Linter must pass before code is committed.

**In CI:** Linter must pass on every commit.

---

## What Passes vs. Fails

**Passes:**
```
// ✅ Clear variable names, no unused variables
calculateUserAge(user: User) → number:
  birthDate = user.getBirthDate()
  return getCurrentYear() - birthDate.getFullYear()
  // All variables used, naming is clear
```

**Fails:**
```
// ❌ Unclear naming (fn, u, x), unused variable
fn(u):  // ← Unclear: what is fn? what is u?
  x = getCurrentYear()  // ← Unclear: what is x?
  age = x - u.getBirthDate().getFullYear()
  unused = "something"  // ← Unused variable
  return age
  // Linter catches: unclear names, unused variable
```

---

## If Linter Fails

**Never commit code that fails linter.**

**Options:**
1. **Fix the violation** (90% of cases)
   - Rename variable for clarity
   - Remove unused code
   - Fix style inconsistency

2. **Suppress the violation** (rare, needs documentation)
   - Only when violation is unavoidable
   - Requires comment explaining why
   - Document in PR description

```
// SUPPRESS linter-rule: no-eval
// Reason: User-defined formulas require dynamic evaluation
result = eval(formula)
// Document in PR: "Suppressed no-eval on line X because..."
```

**Never suppress without documented reason.**

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Linter in warning mode | Violations ignored, quality declines | Configure all rules as errors |
| Global disable of rules | Defeats purpose of linting | Keep rules enabled; suppress only specific lines with reasons |
| No auto-fix | Manual fixing time-consuming | Use linter's auto-fix for fixable violations |
| Suppression without reason | Future dev doesn't know why violated | Always document reason for suppression |
| Ignoring entire files | Code quality inconsistent | Keep entire codebase linted |

---

## Related Tools

- [Typecheck](typecheck.md) — Type safety enforcement
- [Formatter](formatter.md) — Code format consistency
- [Test Coverage](test-coverage.md) — Behavioral verification
- [Security Audit](security-audit.md) — Dependency security

---

**Updated:** 2026-04-26
