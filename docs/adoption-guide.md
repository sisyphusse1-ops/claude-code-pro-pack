# 10-Minute Adoption Guide

## 1. Pick the right filename

| Agent | Filename |
|-------|----------|
| Claude Code | `CLAUDE.md` |
| Codex / OpenCode | `AGENTS.md` |
| Cursor | `.cursorrules` (copy `CLAUDE.md` content) |
| Hermes Agent | works with either, prefers skill format |
| Copilot | `.github/copilot-instructions.md` |

## 2. Drop the file at the project root

Copy `CLAUDE.md` or `AGENTS.md` from the pack into your repo root. Commit it. The agent picks it up on the next run.

## 3. Add project specifics

Uncomment the `## Project specifics` section and add your stack, test runner, and any "don't touch X" rules. **Keep it under 50 lines.** Every line past that drags compliance down.

Example:

```markdown
## Project specifics

- Stack: TypeScript + Next.js 15 + Prisma + Postgres
- Test: `pnpm test` (Vitest, needs `--run` for CI)
- Lint: `pnpm lint:fix` before commit
- Never touch `migrations/` (Prisma-managed)
- Secrets in `.env.local`, never log them
```

## 4. Add skills (optional but high-leverage)

Copy any of the `examples/skill-*.md` files into `.claude/skills/` or `skills/`. They're optional — only load the ones that match your actual workflow.

Recommended starter set:
- `skill-plan-first.md` — for any multi-file change
- `skill-systematic-debugging.md` — when stuck
- `skill-github-pr-workflow.md` — for any repo with PRs

## 5. Test the adoption

Give the agent one realistic task. Check:

- Did it state assumptions before editing? (Rule 1)
- Did it avoid "improving" unrelated code? (Rule 3)
- Did it surface partial failures? (Rule 12)

If any flip negative, drop a note next to the rule with the actual failure and keep iterating.

## 6. When to update

New failure mode → new rule, not new preference. Each rule must cite a real event. Don't turn CLAUDE.md into a wishlist.

## FAQ

**Does this work with multiple agents in one repo?** Yes — `CLAUDE.md` and `AGENTS.md` can coexist. Same content, different filenames.

**Will this slow the agent down?** No. Rules are read once per session and referenced implicitly. Token cost is ~700 tokens for the full pack.

**What if a rule conflicts with my current workflow?** Delete that rule from your copy. The pack is a starting point, not a contract.

**How do I know it's working?** After two weeks, count the correction-to-completion ratio on your tasks. If it hasn't dropped visibly, something is wrong with how you're applying the rules.
