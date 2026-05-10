# Skill: tdd-loop

---
name: tdd-loop
description: "RED → GREEN → REFACTOR test-driven loop. Tests before code. Assertions tied to behavior, not shape."
tags: [testing, tdd, workflow]
version: 1.0.0
---

# tdd-loop

Use when adding a feature or fixing a bug where the correct behavior can be specified in a test. Skip for pure UI layout tweaks and config-only changes.

## When NOT to use
- UI alignment / CSS tweak with no behavior change
- Config-only change (versions, env vars, flags)
- Experimental spike that will be thrown away — use a separate `spike` skill

## The loop

### RED — write the failing test first

1. Name the behavior as a sentence: "When X, the function returns Y."
2. Write the test that asserts on **the behavior**, not the shape (e.g., assert `result === expectedAmount`, not `typeof result === 'number'`).
3. Run the test. It **must fail** with a meaningful message. If it passes, your test is wrong.

### GREEN — minimum code to pass

1. Write the smallest change that makes the test pass.
2. Don't refactor yet. Don't handle cases the test doesn't cover. Just green.
3. Run the full test suite. Nothing else should break.

### REFACTOR — clean up without changing behavior

1. Remove duplication, extract helpers, rename for clarity.
2. Run the test suite after every structural change.
3. Stop when the code reads well. Don't keep polishing past that.

## Pitfalls

- **Shape tests instead of behavior tests.** `expect(result).toBeDefined()` is not a test. It's a type check.
- **Too many assertions per test.** One behavior per test. When one fails, you should know which behavior broke.
- **Refactoring during GREEN.** Do one thing at a time. Green first, then clean.
- **Skipping RED.** If you never saw the test fail, you don't know whether the test actually verifies the change.

## Verification

- [ ] Test was seen failing before the code change
- [ ] Test asserts on behavior, not shape
- [ ] Full suite passes after GREEN
- [ ] Refactor made the code cleaner without re-running RED
