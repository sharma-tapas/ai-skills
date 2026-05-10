---
name: tdd-workflow
description: Use this skill when writing new features, fixing bugs, or refactoring code. Triggers on TDD, test-driven development, writing tests, adding coverage, RED-GREEN-REFACTOR, tracer bullet, or when the user asks to implement a feature with tests. Always invoke before writing any production code — it enforces vertical-slice TDD (one test → one implementation), git checkpoints at each stage, and 80%+ behavior-driven coverage.
origin: community
---

# Test-Driven Development

## Philosophy

**Core principle**: Tests should verify behavior through public interfaces, not implementation details. Code can change entirely; tests shouldn't.

**Good tests** exercise real code paths through public APIs. They describe _what_ the system does, not _how_ it does it. "User can checkout with valid cart" tells you exactly what capability exists. These tests survive refactors because they don't care about internal structure.

**Bad tests** are coupled to implementation — they mock internal collaborators, test private methods, or verify through back-channels (e.g., querying a database directly instead of using the service interface). The warning sign: your test breaks on a refactor but behavior hasn't changed.

See [tests.md](tests.md) for examples and [mocking.md](mocking.md) for mocking guidelines.

## Anti-Pattern: Horizontal Slices

**Do not write all tests first, then all implementation.** This is "horizontal slicing" — treating RED as "write all tests" and GREEN as "write all code."

This produces tests that verify imagined behavior, test the shape of data structures rather than outcomes, and break on refactors that don't change anything the user sees.

**Correct approach**: Vertical slices via tracer bullets. One test → one implementation → repeat. Because you just wrote the code, you know exactly what behavior matters and how to verify it.

```
WRONG (horizontal):
  RED:   test1, test2, test3, test4, test5
  GREEN: impl1, impl2, impl3, impl4, impl5

RIGHT (vertical):
  RED→GREEN: test1→impl1
  RED→GREEN: test2→impl2
  RED→GREEN: test3→impl3
```

## Workflow

### 1. Planning

Before writing any code:

- [ ] Confirm with user what interface changes are needed
- [ ] Confirm with user which behaviors to test (prioritize critical paths)
- [ ] Identify opportunities for [deep modules](deep-modules.md) (small interface, deep implementation)
- [ ] Design interfaces for [testability](interface-design.md)
- [ ] List the behaviors to test — not implementation steps, behaviors
- [ ] Get user approval on the plan

Use the project's domain glossary so test names and interface vocabulary match the project's language. Respect ADRs in the area you're touching.

**You can't test everything.** Focus on critical paths and complex logic, not every edge case.

### 2. Tracer Bullet

Write ONE test that confirms ONE thing about the system.

**RED**: Write the test → run it → confirm it fails for the right reason (missing behavior, not syntax error or broken test setup).

If under Git:
```
git commit -m "test: add reproducer for <feature or bug>"
```

**GREEN**: Write the minimal code to pass → run → confirm it passes.

If under Git:
```
git commit -m "fix: <feature or bug>"
```

This tracer bullet proves the end-to-end path works.

### 3. Incremental Loop

For each remaining behavior:

```
RED:   Write next test → confirm it fails for the right reason
GREEN: Write minimal code to pass → confirm it passes
```

Rules:
- One test at a time
- Only enough code to pass the current test
- Don't anticipate future tests
- Keep tests focused on observable behavior

Git commits follow the same pattern: one commit per confirmed RED, one per confirmed GREEN.

### 4. Refactor

After all tests pass, look for [refactor candidates](refactoring.md):

- [ ] Extract duplication
- [ ] Deepen modules (move complexity behind simple interfaces)
- [ ] Apply SOLID principles where natural
- [ ] Consider what new code reveals about existing abstractions
- [ ] Run tests after each refactor step

**Never refactor while RED.** Get to GREEN first.

If under Git, commit after refactoring:
```
git commit -m "refactor: clean up after <feature or bug> implementation"
```

## Checklist Per Cycle

```
[ ] Test describes behavior, not implementation
[ ] Test uses public interface only
[ ] Test would survive internal refactor
[ ] Code is minimal for this test
[ ] No speculative features added
[ ] RED confirmed (compiled and executed) before writing implementation
[ ] GREEN confirmed before refactoring
```

## RED Gate

A test that was only written but not compiled and executed does not count as RED.

Valid RED states:
- **Runtime RED**: test target compiles, test executes, result is RED — failure caused by the intended missing behavior, not by broken setup or unrelated regressions
- **Compile-time RED**: the new test exercises the buggy code path and the compile failure is itself the RED signal

Do not edit production code until RED is confirmed.

## Coverage

Aim for 80%+ coverage as a _result_ of thorough behavior testing — not as a goal in itself. Cover happy paths, error and exception paths, and boundary conditions.

Verify:
```bash
npm run test:coverage
# or
go test ./... -cover
# or
uv run pytest --cov
```

## Test Types

| Type | What it covers | Speed |
|---|---|---|
| Unit | Individual functions, pure logic, no I/O | < 50ms each |
| Integration | API endpoints, DB operations, service wiring | seconds |
| E2E (Playwright) | Critical user flows, browser automation | minutes |

For concrete code patterns, see [tests.md](tests.md). For what and when to mock, see [mocking.md](mocking.md).

## Test File Organization

```
src/
├── components/
│   └── Button/
│       ├── Button.tsx
│       └── Button.test.tsx        # unit tests co-located
├── app/
│   └── api/
│       └── markets/
│           ├── route.ts
│           └── route.test.ts      # integration tests
└── e2e/
    └── markets.spec.ts            # E2E tests
```

For Go/Python layouts, follow the conventions in `architecture.rules` or the project's existing structure.

## CI/CD Integration

```yaml
# GitHub Actions
- name: Run Tests
  run: npm test -- --coverage
- name: Upload Coverage
  uses: codecov/codecov-action@v3
```

Watch mode during development:
```bash
npm test -- --watch
```

## Git Checkpoint Rules

- Count only commits on the current active branch for the current task
- Do not treat commits from other branches or earlier unrelated work as checkpoints
- Before marking a checkpoint satisfied, verify the commit is reachable from `HEAD` on the active branch
- Never skip or squash checkpoint commits until the full TDD cycle is complete
