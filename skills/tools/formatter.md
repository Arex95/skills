# Formatter Tool

Code formatter enforces consistent style automatically. No style debates. No manual formatting. Machine-enforced consistency.

**Category:** tool  
**Updated:** 2026-04-26

---

## What It Does

- **Consistent spacing** — Indentation, line breaks, whitespace
- **Consistent line length** — Long lines wrapped consistently
- **Consistent quotes** — Single vs. double quotes unified
- **Consistent semicolons** — All lines have or don't have semicolons (consistently)
- **Consistent imports** — Import statements ordered and grouped
- **Consistent operators** — Spacing around operators unified

---

## Configuration Requirements

Formatter must be configured with **strict, non-negotiable rules.**

**Minimum settings:**
- Line length: consistent (commonly 80, 100, or 120)
- Indentation: consistent spaces or tabs (not mixed)
- Quote style: unified (all single, all double, or templates where appropriate)
- Semicolons: all present or all absent (consistently)
- Trailing commas: consistent in multi-line structures
- Arrow function parentheses: consistent
- No configuration changes per file (one style for entire codebase)

**Tool-agnostic approach:** Use whatever formatter your language provides with strict, unified settings.

---

## Execution

**Pre-commit:** All code must be formatted.

**In pre-commit hook:** Formatter runs automatically before commit.

---

## What Passes vs. Fails

**Passes:**
```
// ✅ Consistent: 2-space indent, double quotes, semicolons on all lines
User (interface):
  id: string;
  email: string;
  getName(): string;

user: User = {
  id: "123";
  email: "user@example.com";
  getName: () => "John";
};
// All lines follow same formatting rules
```

**Fails:**
```
// ❌ Inconsistent: mixed indentation, quotes, semicolons
User{
    id:string;
    email:string     ← no semicolon
    getName():string;
}
user:User = {
  id:'123';        ← single quotes instead of double
  email:  'user@example.com'  ;  ← extra spaces
  getName:()=>"John",      ← inconsistent spacing
}
// Mix of styles: some have semicolons, some don't; quotes mixed
```

---

## If Formatter Fails

**Never commit unformatted code.**

**Process:**
1. Run formatter automatically
2. Review changes
3. Commit formatted code

**That's it. No debates. No manual fixing.**

---

## In CI/CD

**Formatter check in pipeline:**

If code not formatted:
- Pipeline fails
- Developer must format and recommit
- No manual review of formatting

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| No formatter | Manual formatting, inconsistency | Install and configure formatter |
| Multiple formatters | Conflicting rules, debates | Choose one formatter, disable others |
| Configuration per developer | Different formatting per file | One unified config in repo root |
| Manual formatting after formatter | Defeats automation | Run formatter before committing |
| Formatter disabled for some files | Inconsistency | Apply formatter everywhere |
| Formatter output not committed | CI fails on formatting | Always commit formatted code |

---

## Formatter vs. Linter

**Linter:**
- Catches mistakes and style violations
- Configurable (can enable/disable rules)
- Some violations auto-fixable, some require manual fix
- Opinionated but flexible

**Formatter:**
- Enforces consistent code style
- Non-negotiable (almost no configuration)
- All violations auto-fixable
- Removes style debates entirely

**Use both:** Linter for mistakes and best practices. Formatter for consistency.

---

## Editor Integration

Configure your editor to:
1. Run formatter on save
2. Run formatter on paste
3. Show formatting violations

This way, code is always formatted before you commit.

---

## Related Tools

- [Linter](linter.md) — Mistake and style enforcement
- [Typecheck](typecheck.md) — Type safety
- [Test Coverage](test-coverage.md) — Behavioral verification
- [Security Audit](security-audit.md) — Dependency security

---

**Updated:** 2026-04-26
