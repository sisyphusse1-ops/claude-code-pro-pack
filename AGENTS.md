# AGENTS.md — 12 Rules for Codex / OpenCode / Cursor

Same 12 rules as `CLAUDE.md`, filename change for Codex-style tooling that looks for `AGENTS.md`.

## Rules

1. **Think before coding.** State assumptions out loud. Surface tradeoffs. Push back when a simpler approach exists. No silent guesses.
2. **Simplicity first.** Minimum code that solves the stated problem. No speculative features. No abstractions for single-use code.
3. **Surgical changes.** Touch only what the task requires. Don't "improve" adjacent code, comments, or formatting. Match existing style.
4. **Goal-driven execution.** Define success criteria up front, then loop until verified. Prefer stating the goal over dictating steps.
5. **Don't make the model do non-language work.** Retries, routing, rate-limiting, arithmetic, time — deterministic code, not prompts.
6. **Hard token budget.** Every loop gets a ceiling. If the same input has been re-chewed for 90 minutes, stop.
7. **Surface conflicts, don't average them.** Two codebase patterns disagreeing → pick one visibly and say why.
8. **Read before you write.** Understand adjacent code before adding new code.
9. **Tests are gated by correctness, not "pass."** Assertions must be tied to behavior, not shape.
10. **Long-running operations need checkpoints.** Commit between steps.
11. **Convention beats novelty.** Use the codebase's established pattern.
12. **Fail visibly, not silently.** Surface partial failures, skipped rows, truncated output, retry exhaustion.

## Project specifics

<!-- Add repo-specific rules here. Keep it under 50 lines. -->
