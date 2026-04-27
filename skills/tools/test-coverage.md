# Test Coverage Tool

Tests verify code behavior. Coverage requirements ensure new code is tested before entering repository.

**Category:** tool  
**Updated:** 2026-04-26

---

## What It Verifies

- **Unit tests** — Individual functions/methods work correctly
- **Integration tests** — Modules work together correctly
- **Coverage metrics** — Percentage of code covered by tests
- **Regression prevention** — Changes don't break existing functionality

---

## Configuration Requirements

**Minimum requirements:**
- All new code must have corresponding tests
- Coverage threshold: 80%+ (adjust per project)
- Tests must pass 100% (no flaky tests)
- Tests must run in CI before code is merged

**What counts as tested:**
- Happy path (normal execution)
- Error cases (exceptions thrown)
- Edge cases (boundary conditions)
- Integration (modules working together)

**What doesn't guarantee quality:**
- High coverage percentage (can test trivial code)
- Passing tests (can test wrong behavior)
- Tests that don't fail when code is wrong

---

## Execution

**Pre-commit:** Tests for changed code must pass.

**In CI:** All tests must pass.

---

## What Passes vs. Fails

**Passes:**
```
// ✅ Function with tests covering happy path, errors, and edge cases
calculateUserAge(user: User) → number:
  if user is null:
    throw error "User required"
  birthDate = user.getBirthDate()
  if birthDate is null:
    throw error "Birth date required"
  return getCurrentYear() - birthDate.getYear()

Tests for calculateUserAge:
  1. Happy path: valid user with birth date
     - Input: User with birthDate = 1990
     - Expected: 2026 - 1990 = 36
     - Verify: age equals 36
  
  2. Error case: null user
     - Input: null
     - Expected: throw "User required"
     - Verify: error is thrown with correct message
  
  3. Error case: missing birth date
     - Input: User with birthDate = null
     - Expected: throw "Birth date required"
     - Verify: error is thrown with correct message
// All paths tested: happy path + error cases
```

**Fails:**
```
// ❌ Function with no tests
calculateUserAge(user: User) → number:
  return getCurrentYear() - user.getBirthDate().getYear()
// No tests: if user is null or birthDate is null, crashes at runtime
```

---

## What Needs Tests

**Always test:**
- Business logic (use cases, entities, domain services)
- Error handling (exceptions, validation)
- Edge cases (null, empty, boundary values)
- Integration between modules
- API endpoints (happy path + error cases)

**Sometimes test:**
- Utility functions (if complex)
- Configuration (if it affects behavior)

**Don't test:**
- Trivial getters/setters
- Framework-generated code
- External libraries (trust them)

---

## If Tests Fail

**Never commit code with failing tests.**

**Process:**
1. Run tests
2. Identify failures
3. Fix code or fix tests (if test is wrong)
4. All tests pass
5. Commit

**If test failure is unrelated to your change:**
- Don't ignore it
- Fix the failing test
- Or create ticket to fix later (but commit your changes after fixing the pre-existing issue)

---

## Coverage Reporting

**Output:** percentage of code covered
- Statements: target 80%+
- Branches: target 80%+
- Functions: target 90%+
- Lines: target 85%+

**Target:** 80%+ coverage (adjust per project).

**Reality:** 100% coverage possible but expensive. Focus on:
- Critical business logic: 95%+
- Domain core: 90%+
- Integration: 80%+
- Utilities: 70%+ (optional if simple)

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| No tests for new code | Behavior not verified, bugs slip through | Write tests for all new code |
| Tests that always pass | Not actually testing anything | Tests should fail if code is wrong |
| Mocking everything | Testing mock, not real code | Use real objects, mock only external dependencies |
| Slow tests | Test suite takes 10+ minutes, rarely run | Keep tests fast (< 5 seconds per test) |
| Flaky tests (sometimes pass, sometimes fail) | Can't trust test suite | Fix race conditions, use deterministic test data |
| No error case testing | Happy path works, errors crash | Test exceptions and error handling |
| Coverage percentage as goal | High coverage ≠ good tests | Focus on critical paths, not percentage |

---

## Test-Driven Development

**Optional but recommended:**
1. Write test first (fails)
2. Write code to make test pass
3. Refactor code
4. Commit

**Benefit:** Tests guide design. Code testable by default.

---

## Related Tools

- [Linter](linter.md) — Code quality enforcement
- [Typecheck](typecheck.md) — Type safety
- [Formatter](formatter.md) — Format consistency
- [Security Audit](security-audit.md) — Dependency security

---

**Updated:** 2026-04-26
