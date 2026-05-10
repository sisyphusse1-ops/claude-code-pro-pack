# Why 12 Rules

Each rule earned its place from a concrete failure mode. If you skip a rule, here's what you're re-introducing.

## Rule 1 — Think before coding
Closes: **silent wrong assumptions.** Claude implements your guess instead of asking. You discover the mismatch three commits later.

## Rule 2 — Simplicity first
Closes: **over-engineering.** A 12-line fix becomes 300 lines of abstraction because the model felt generous.

## Rule 3 — Surgical changes
Closes: **orthogonal damage.** The model reformats a file, renames a variable, "cleans up" an import while fixing an unrelated bug.

## Rule 4 — Goal-driven execution
Closes: **step-following without verification.** The model does exactly what you said and the feature still doesn't work.

## Rule 5 — Don't make the model do non-language work
Closes: **flaky logic.** A prompt that "decides whether to retry on 503" reads the request body as context and the retry policy becomes random.

## Rule 6 — Hard token budget
Closes: **debugging spirals.** A 90-minute session iterates on the same 8KB error message and suggests fixes you already rejected 40 messages earlier.

## Rule 7 — Surface conflicts, don't average them
Closes: **pattern pollution.** Codebase uses async/await with try/catch. Also has a global error boundary. Model writes new code that does both. Errors get swallowed twice.

## Rule 8 — Read before you write
Closes: **duplicate functions.** Model adds a new function next to an identical existing one it didn't read. Import order decides which one wins.

## Rule 9 — Tests are gated by correctness
Closes: **shape-only tests.** Function returns a constant. Test checks that the function returns something. All green. Auth is broken in production.

## Rule 10 — Long-running operations need checkpoints
Closes: **cascading breakage.** Step 4 of a 6-step refactor goes wrong. By the time you notice, steps 5 and 6 are stacked on top of the broken state.

## Rule 11 — Convention beats novelty
Closes: **mixed-paradigm drift.** Model introduces React hooks into a class-component codebase. They work. The test infrastructure assumed `componentDidMount` and silently breaks.

## Rule 12 — Fail visibly, not silently
Closes: **lying successes.** Database migration "completes successfully" while silently skipping 14% of records on constraint violations. You find out 11 days later when reports start looking wrong.

## Why this list ends at 12

Past 200 lines of CLAUDE.md, compliance drops sharply. Rules get buried. 12 is about where the curve bends for us. If you add more, delete a less-valuable one first.
