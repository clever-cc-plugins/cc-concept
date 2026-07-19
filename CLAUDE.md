# cc-concept

Marketing-strategy skills for Claude Code — positioning, competitive analysis,
go-to-market planning, and campaign concepting. Distributed as a plugin via the
clever-cc-plugins marketplace. Sits upstream of `cc-content`: cc-concept sets the
strategic frame, cc-content produces the pieces that execute it.

## Key Config Files

| File                                                              | Purpose                                                                                              |
| ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `.claude/format-markdown.sh`                                      | PostToolUse hook: formats Markdown files with prettier after edits                                   |
| `.claude/guard-secret-files.sh`                                   | PreToolUse hook: blocks reads/edits/writes of secret .env files                                      |
| `.claudeignore`                                                   | Paths excluded from Claude Code indexing                                                             |
| `CLAUDE.md`                                                       | Project instructions, loaded every message                                                           |
| `.claude/settings.json`                                           | Permissions, hooks, environment variables                                                            |
| `.githooks/pre-commit`                                            | Secret scanning (gitleaks) + CLAUDE.md table sync                                                    |
| `.gitignore`                                                      | Git ignore patterns                                                                                  |
| `plugins/cc-concept/.claude-plugin/plugin.json`                   | Plugin manifest                                                                                      |
| `plugins/cc-concept/skills/cc-concept-campaign-concept/SKILL.md`  | Skill: Build a campaign concept and hand it off to cc-content as brief.md                            |
| `plugins/cc-concept/skills/cc-concept-channel-advisor/SKILL.md`   | Skill: Recommend a RACE-sequenced channel mix for a goal, audience, and budget                       |
| `plugins/cc-concept/skills/cc-concept-content-strategy/SKILL.md`  | Skill: Produce a content strategy (pillars, topic clusters, mix, cadence) and register it as context |
| `plugins/cc-concept/skills/cc-concept-gtm/SKILL.md`               | Skill: Structure a go-to-market launch plan with an optional brief.md by-product                     |
| `plugins/cc-concept/skills/cc-concept-marketing-advisor/SKILL.md` | Skill: Open-ended strategic advisor with cross-skill deferral and per-turn save-prompt               |
| `plugins/cc-concept/skills/cc-concept-onboarding/SKILL.md`        | Onboarding skill: registers context files and collects gated needs                                   |
| `plugins/cc-concept/skills/cc-concept-positioning/SKILL.md`       | Positioning skill: generates brand positioning from a selected framework                             |
| `scripts/sync-config-table.sh`                                    | Keeps the Key Config Files table in sync on each commit                                              |

## Setup

Install from the clever-cc-plugins marketplace:

```
/plugin marketplace add clever-cc-plugins/marketplace
/plugin install cc-concept@clever-cc-plugins
```

## Don't

- Don't commit secrets or credentials to git
- Don't use `--force` flags — fix the underlying issue instead
- Don't modify CLAUDE.md directly when logging a correction — append to `.claude/learnings.md`

## Learnings

When the user corrects a mistake or points out a recurring issue, append a one-line
summary to `.claude/learnings.md`. Don't modify CLAUDE.md directly.
