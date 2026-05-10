# Browser Skill Graduation

Use when you have a repeatable browser task on a non-trivial site (hidden JSON endpoint, JS-rendered content, multi-step login) and the first run costs more than the tenth. Converge on a reliable path once, then **graduate** that path into a reusable skill.

## When NOT to use

- Deterministic HTML parsing (static page, no JS) — write Python + `fetch` directly.
- One-shot task you'll never repeat — do it and move on.
- Site with explicit anti-automation ToS — stop.

## The loop

Keep a `strategy.md` scratchpad in your working dir. Write to it every iteration.

1. **Objective.** One concrete sentence with an unambiguous success condition (returned record count, URL reached, reservation confirmed). Vague objectives → unbounded iteration.
2. **Run.** Attempt end-to-end against the live browser. Log tool calls, network, token cost, wall time.
3. **Study the trace.**
   - Where did you stall, guess, or retry?
   - Any undocumented JSON endpoint visible in network traffic? *(This is usually the single biggest win.)*
   - Any step that was magic but isn't reproducible?
4. **Update `strategy.md`** with what worked, what broke, what to drop, what helper to lean on next time.
5. **Iterate.** Read `strategy.md` first each time so improvements compound. **Cap at 3–5 iterations.** Short-circuit when two consecutive runs don't meaningfully reduce cost or turn count.
6. **Graduate.** Write a `SKILL.md` plus any helper scripts (`helpers/<site>.py`, selectors, CLI snippets) into your skills tree.

## What the graduated skill must contain

Keep the final artifact small and readable. No transcript, no screenshot reel.

- **Objective + success criteria** (exact same wording as step 1).
- **Shortest reliable path** as numbered steps with actual commands, URLs, selectors.
- **Undocumented endpoints** you discovered — the single biggest value.
- **Helper scripts** that did real work (HTML parse, auth flow, pagination).
- **Known brittle points** (rate limits, captchas, Tuesday redesigns).
- **Stop conditions** — when to refuse auto-run (captcha wall, session expired, ToS signal).

## Heuristics

- **The network tab is the prize.** If you find the JSON endpoint the page renders from, fetch it directly. A 28-page scrape collapses to one `curl`.
- **Skip screenshots when the DOM didn't change.** Most graduated skills reuse the same DOM across runs; `screenshot` is the most over-called tool.
- **Deterministic beats clever.** Once the path is known, helper code beats a reasoning loop.
- **Name the skill after the task, not the site.** `book-opentable-reservation`, not `opentable`.

## Cost shape

- First run: baseline generic agent cost.
- Graduated skill: ~5–10× cheaper, far fewer turns.
- If it's not dramatically cheaper, the skill didn't encode anything new. Delete and revisit.

## Anti-patterns

- Running unbounded because "it might figure it out" — set a hard cap (3–5) and budget.
- Graduating on a single successful run. You need at least 2 consecutive runs agreeing on the path.
- Skill that's a full transcript / log. The artifact is a recipe, not a diary.
- Re-running to "improve" a mature skill without new failure data. Improve on evidence.
