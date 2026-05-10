# Skill: plan-first

---
name: plan-first
description: "Before any multi-file or non-trivial change, write a short plan to a scratch file. Prevents mid-task drift and makes intent auditable."
tags: [planning, workflow, discipline]
version: 1.0.0
---

# plan-first

Use when the task touches 2+ files, requires new dependencies, or changes a public interface. Skip for single-line fixes and typos.

## When NOT to use
- Single-file, single-function edit
- Typo / rename that has one obvious correct answer
- Reverting a known-bad commit

## Steps

1. **Read the relevant code.** Minimum: the file you'll touch, its direct callers, and its direct callees. Make a list of those file paths before planning.
2. **Write `.hermes/plans/<task>.md`** with these sections:
   - **Goal** — one sentence, success condition explicit.
   - **Files to change** — absolute paths, grouped by purpose.
   - **Steps** — numbered, small enough each could ship alone.
   - **Tests** — which tests change or get added, and what they verify.
   - **Risks** — what could break elsewhere.
3. **Stop and check the plan** against the goal before writing a single line of code. If the plan is longer than the feature, simplify.
4. **Execute one step at a time.** After each step, re-read the plan and mark progress.
5. **When finished, delete the plan** or move it to `docs/decisions/` if it captured a tradeoff worth keeping.

## Pitfalls

- **Plan that's a wishlist.** If every step says "refactor X for cleanliness," you're planning a rewrite, not a feature. Revert to the smallest-diff version.
- **Plan that skips tests.** A plan without a tests section is wrong. Add one even if the answer is "no new tests — existing coverage sufficient."
- **Planning forever.** Cap the plan at 1 page. If it's longer, break the task.

## Verification

- [ ] Plan file exists before any code change
- [ ] All files-to-change were read first
- [ ] Each step produced a reviewable commit (or diff)
- [ ] Plan got deleted or archived at the end
