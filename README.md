# Claude Code / Codex Pro Pack

Battle-tested behavior rules, prompts, and reusable skill templates for AI coding agents — Claude Code, Codex, Cursor, Hermes Agent.

Built from real-world agent failure modes across 30+ codebases. Drop-in files. No framework. ~700 tokens total.

> **Karpathy's original 4-rule CLAUDE.md cut Claude coding mistakes from ~40% to ~11%.** This pack adds 8 more rules covering the agent-orchestration failures the original didn't — token spirals, silent partial failures, two-pattern pollution, duplicate-function drift.

## What's inside

```
cc-pro-pack/
├── CLAUDE.md                          # 12-rule behavior file — drop in project root
├── AGENTS.md                          # Same rules, Codex/OpenCode variant
├── templates/
│   ├── prd-generator.md               # Senior PM prompt → agent-ready PRDs
│   ├── browser-skill-graduation.md    # Turn browser workflows into reusable skills
│   └── skill-template.md              # SKILL.md frontmatter + structure
├── examples/
│   ├── skill-plan-first.md
│   ├── skill-systematic-debugging.md
│   ├── skill-tdd-loop.md
│   ├── skill-github-pr-workflow.md
│   └── skill-code-review.md
└── docs/
    ├── why-12-rules.md                # The failure mode each rule closes
    └── adoption-guide.md              # 10-minute setup for any project
```

## Quick start

1. Copy `CLAUDE.md` (or `AGENTS.md` for Codex) into your project root.
2. Uncomment the `## Project specifics` block and add your stack, test runner, and any "don't touch X" rules. Keep it under 50 lines.
3. Commit. The agent picks it up on the next run.
4. (Optional) Copy 2–3 skills from `examples/` into `.claude/skills/` or `skills/`.

## The 12 rules — short version

1. Think before coding — state assumptions, push back on needless complexity.
2. Simplicity first.
3. Surgical changes — don't touch adjacent code.
4. Goal-driven execution — state success criteria, loop until verified.
5. Don't make the model do non-language work — retries/routing are code.
6. Hard token budget — stop the debugging spiral.
7. Surface conflicts, don't average two codebase patterns.
8. Read before you write.
9. Tests gated by correctness, not "pass."
10. Long-running operations need checkpoints.
11. Convention beats novelty.
12. Fail visibly, not silently.

Full rationale for each rule → [`docs/why-12-rules.md`](docs/why-12-rules.md).

## Why this works

Past ~200 lines of CLAUDE.md, compliance drops sharply — rules get buried. The pack holds at 12 rules + minimal boilerplate so the agent actually reads and follows the file. Every rule cites a real failure it closes, not a preference.

## License

MIT. Fork it, modify it, redistribute it, ship it in your company guide.

## Related

- **[cc-audit](https://github.com/sisyphusse1-ops/cc-audit)** — one-file Python linter that scores any `CLAUDE.md` / `AGENTS.md` against this 12-rule baseline. Use in CI.
- **Karpathy's original CLAUDE.md** — the 4-rule floor this pack builds on.
- **[anthropic/skills](https://github.com/anthropics/skills)** — Anthropic's official Agent Skills repo. Use our pack as the behavioral baseline (`CLAUDE.md`), then layer their skills on top.
- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** — lifecycle slash commands (`/spec`, `/plan`, `/build`, `/test`, `/review`, `/ship`). Complements the pack — our 12 rules tell the agent *how to behave*, their skills tell it *what workflow to follow*.
- **Browserbase Autobrowse** — inspiration for the `browser-skill-graduation` template.
- **Hermes Agent** — reference implementation for the skill format.

## How this differs

| | This pack | anthropic/skills | addyosmani/agent-skills |
|---|---|---|---|
| Shape | Drop-in CLAUDE.md + 5 example skills | Plugin marketplace | Plugin with slash commands |
| Install | Copy one file | `/plugin install` | `/plugin install` |
| Focus | Agent behavior baseline | Domain skills catalog | Dev lifecycle workflow |
| Token cost | ~700 total | Per-skill | Per-skill + hook |
| Works with | Claude Code, Codex, Cursor, Hermes, Copilot | Claude Code | Claude Code, Cursor, Gemini CLI |

Use all three — pack for behavior, anthropic/skills for domain tasks, addyosmani for lifecycle flow.

---

Pull requests welcome. New rules must cite the failure mode they close.
