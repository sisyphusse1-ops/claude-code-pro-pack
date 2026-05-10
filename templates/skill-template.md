# SKILL.md template

Use this structure for any skill you author. Keep it under ~150 lines so the agent actually loads and follows it.

```markdown
---
name: <lowercase-hyphen-name>
description: "One sentence describing when and why to use this skill. Agent reads this first to decide if the skill is relevant."
tags: [area, pattern, tool]
version: 1.0.0
author: <you>
license: MIT
---

# <Human-readable title>

One paragraph: when a user's task matches this, load this skill.

## When NOT to use
- Scenario A → use <other skill> instead
- Scenario B → don't automate at all

## Steps

1. **Step name.** What to do, what command to run, what input to collect.
2. **Next step.** …

Include **exact commands** — not pseudocode. Agents copy these verbatim.

## Pitfalls

- Failure mode observed in the wild → the specific fix.
- Thing that looks right but isn't → the sign.

## Verification

How you know the skill succeeded:
- [ ] Tangible artifact exists at <path>
- [ ] Command X returns <expected>
- [ ] No partial-failure markers in the log

## References

Links to upstream docs, RFCs, or prior conversations where this pattern was validated.
```

## Frontmatter rules

- `name` — lowercase, hyphens/underscores only, max 64 chars.
- `description` — one sentence, present tense, states trigger condition. Shows in `skills_list`. Get this right or the agent skips the skill.
- `tags` — 3–6 tags. First tag is the area (`github`, `browser`, `web3`).
- `version` — semver. Bump when behavior changes, not when you tweak prose.

## Content rules

- **Exact commands over prose.** The skill is a runbook, not an essay.
- **Numbered steps, not bullets** for anything ordered.
- **"When NOT to use" comes before "Steps"** so the agent bails fast if the skill is wrong for the task.
- **Cite the failure** each pitfall fixes. "Do X" is forgettable. "If you skip X, you get Y error" sticks.
- **Verification section is mandatory.** If you can't write verification steps, you don't know when the skill succeeded.
