# Claude Code / Codex Pro Pack

A battle-tested set of behavior rules, prompts, and reusable skill templates for AI coding agents — Claude Code, Codex, Cursor, Hermes Agent.

Built from real-world agent failure modes across 30+ codebases. Drop-in files, no fluff.

## What's inside

```
cc-pro-pack/
├── CLAUDE.md                          # The 12-rule behavior file (drop in project root)
├── AGENTS.md                          # Same rules, Codex/OpenCode variant
├── templates/
│   ├── prd-generator.md               # Senior PM prompt → agent-ready PRDs
│   ├── browser-skill-graduation.md    # Turn browser workflows into reusable skills
│   └── skill-template.md              # SKILL.md frontmatter + structure
├── examples/
│   ├── skill-github-pr-workflow.md
│   ├── skill-systematic-debugging.md
│   ├── skill-tdd-loop.md
│   ├── skill-code-review.md
│   └── skill-plan-first.md
└── docs/
    ├── why-12-rules.md                # The failure modes each rule closes
    └── adoption-guide.md              # 10-minute setup for any project
```

## Quick start

1. Copy `CLAUDE.md` (or `AGENTS.md`) into your project root
2. Add any 2-3 example skills under `.claude/skills/` or `skills/`
3. Use `templates/prd-generator.md` when starting a new feature
4. Use `templates/browser-skill-graduation.md` when automating a non-trivial site

## Why it works

Karpathy's original 4-rule CLAUDE.md went viral in early 2026 and cut Claude coding mistakes from ~40% to ~11%. It didn't cover agent-orchestration failure modes — token spirals, silent partial failure, mid-session convention drift.

This pack adds 8 more rules and three working skill templates that close those gaps. Each rule cites the real failure mode it fixes.

## License

MIT. Do whatever you want with it — fork, modify, redistribute.

## Support / updates

New failure modes → new rules. Follow updates on X (link in purchase receipt).
