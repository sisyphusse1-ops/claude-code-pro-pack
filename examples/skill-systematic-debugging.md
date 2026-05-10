# Skill: systematic-debugging

---
name: systematic-debugging
description: "4-phase root-cause debugging. Understand the bug before fixing it. Prevents the classic 'kept patching symptoms' spiral."
tags: [debugging, workflow, discipline]
version: 1.0.0
---

# systematic-debugging

Use when a fix attempted twice has not landed, or the bug is non-local (symptom in file A, cause in file B). Skip for trivial stack traces that point directly at the bug.

## When NOT to use
- Stack trace literally names the broken line
- Bug is "I forgot to commit" / "wrong branch" class
- Flaky test on a known-flaky CI runner (separate problem)

## The 4 phases

### Phase 1 — Reproduce

1. Write the minimum script or test that reproduces the bug deterministically.
2. If you can't reproduce, **stop**. Instrumentation first, then guessing.
3. Commit the repro as a failing test so you can't forget it.

### Phase 2 — Localize

1. Walk the stack from symptom toward cause. Don't skip frames.
2. For each frame, ask: "Given this frame's inputs, is the output correct?"
3. The first frame where "inputs correct → output wrong" is the cause frame.
4. Write the cause frame path and line number on a scratchpad.

### Phase 3 — Explain

Write **one paragraph** describing the cause: the code path, the wrong assumption, why it didn't fire earlier. If you can't write the paragraph, you haven't localized — return to Phase 2.

### Phase 4 — Fix

1. Change the cause frame, not the symptom frame. Never silently swallow the error upstream.
2. If the fix also requires changes to callers, make those changes explicit (don't hide them in the "fix").
3. Run the Phase 1 repro — it must pass.
4. Run the adjacent tests — they must still pass.

## Pitfalls

- **Patching the symptom.** Adding a null check at the top of the function where the null showed up, when the null was wrong two functions upstream.
- **Guessing from the IDE.** A quick "this might be it" edit without Phase 2 is how bugs proliferate into siblings.
- **Skipping the paragraph.** If you can't explain the bug in prose, you can't fix it without luck.
- **Fixing more than the bug.** If you notice other issues during debugging, write them down and fix them separately.

## Verification

- [ ] Repro script / failing test committed
- [ ] Cause frame named in prose
- [ ] Fix applied at the cause, not the symptom
- [ ] All adjacent tests still pass
- [ ] No unrelated changes in the same commit
