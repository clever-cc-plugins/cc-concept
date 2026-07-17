# cc-concept

Marketing-strategy skills for Claude Code — positioning, competitive analysis,
go-to-market planning, and campaign concepting. Distributed as a plugin via the
clever-cc-plugins marketplace. Sits upstream of `cc-content`: cc-concept sets the
strategic frame, cc-content produces the pieces that execute it.

## Key Config Files

| File                                            | Purpose                                    |
| ----------------------------------------------- | ------------------------------------------ |
| `.claude/format-markdown.sh`                    | TODO: add description                      |
| `.claude/guard-secret-files.sh`                 | TODO: add description                      |
| `.claudeignore`                                 | TODO: add description                      |
| `CLAUDE.md`                                     | Project instructions, loaded every message |
| `.claude/settings.json`                         | TODO: add description                      |
| `.githooks/pre-commit`                          | TODO: add description                      |
| `.gitignore`                                    | TODO: add description                      |
| `plugins/cc-concept/.claude-plugin/plugin.json` | TODO: add description                      |
| `scripts/sync-config-table.sh`                  | TODO: add description                      |

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
