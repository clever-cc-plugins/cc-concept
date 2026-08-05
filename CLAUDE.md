# cc-concept

Marketing-strategy skills for Claude Code — positioning, competitive analysis,
go-to-market planning, and campaign concepting. Distributed as a plugin via the
clever-cc-plugins marketplace. Sits upstream of `cc-content`: cc-concept sets the
strategic frame, cc-content produces the pieces that execute it.

## Key Config Files

| File                                                             | Purpose                                                                                                                    |
| ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `.claude/format-markdown.sh`                                     | PostToolUse hook: formats Markdown files with prettier after edits                                                         |
| `.claude/guard-secret-files.sh`                                  | PreToolUse hook: blocks reads/edits/writes of secret .env files                                                            |
| `.claudeignore`                                                  | Paths excluded from Claude Code indexing                                                                                   |
| `CLAUDE.md`                                                      | Project instructions, loaded every message                                                                                 |
| `.claude/settings.json`                                          | Permissions, hooks, environment variables                                                                                  |
| `.githooks/pre-commit`                                           | Secret scanning (gitleaks) + CLAUDE.md table sync                                                                          |
| `.gitignore`                                                     | Git ignore patterns                                                                                                        |
| `plugins/cc-concept/.claude-plugin/plugin.json`                  | Plugin manifest                                                                                                            |
| `plugins/cc-concept/skills/audience-personas/SKILL.md`           | Skill: Develop audience personas or ICPs via interview or synthesis from customer data                                     |
| `plugins/cc-concept/skills/campaign-concept/SKILL.md`            | Skill: Build a campaign concept with upfront success metrics and hand it off to cc-content as brief.md                     |
| `plugins/cc-concept/skills/channel-advisor/SKILL.md`             | Skill: Recommend a RACE-sequenced channel mix for a goal, audience, and budget                                             |
| `plugins/cc-concept/skills/competitive-research/SKILL.md`        | Skill: Run a standalone competitive audit covering messaging, positioning, SWOT, and market gaps                           |
| `plugins/cc-concept/skills/editorial-strategy/SKILL.md`          | Skill: Produce a content strategy (pillars, topic clusters, mix, cadence) and register it as context                       |
| `plugins/cc-concept/skills/gtm-plan/SKILL.md`                    | Skill: Structure a go-to-market launch plan with upfront success metrics and an optional brief.md by-product               |
| `plugins/cc-concept/skills/learnings-promotion/SKILL.md`         | Skill: Review .claude/learnings.md, promote recurring cc-concept patterns or dismiss one-offs                              |
| `plugins/cc-concept/skills/marketing-advisor/SKILL.md`           | Skill: Open-ended strategic advisor with cross-skill deferral and per-turn save-prompt                                     |
| `plugins/cc-concept/skills/positioning/SKILL.md`                 | Positioning skill: generates brand positioning from a selected framework; delegates to competitive-research if needed      |
| `plugins/cc-concept/skills/seo-research/SKILL.md`                | Skill: Build keyword-validated topic clusters using Ubersuggest MCP tools or fallback interview-based research             |
| `plugins/cc-concept/skills/strategy-onboarding/SKILL.md`         | Onboarding skill: registers context files and collects gated needs                                                         |
| `plugins/cc-concept/skills/strategy-orchestrator/SKILL.md`       | Skill: Match a business goal to an engagement type and sequence the right subset/order of cc-concept and cc-content skills |
| `plugins/cc-concept/skills/strategy-performance-review/SKILL.md` | Skill: Extract concept bets, verdict them against performance data, recommend re-runs                                      |
| `scripts/sync-config-table.sh`                                   | Keeps the Key Config Files table in sync on each commit                                                                    |

## Context files

Project-scope context files registered by cc-concept and cc-content skills. Register new context files by running `/register-context` or by adding them manually to this table.

| Label                     | Path                                  | Summary                                                                                 |
| ------------------------- | ------------------------------------- | --------------------------------------------------------------------------------------- |
| Organization background   | `context/organization-background.md`  | Mission, market position, business model, constraints — gates all downstream skill work |
| Audience personas         | `context/audience-personas.md`        | Buyer personas or ICPs from `audience-personas`; gates positioning, campaign, content   |
| Competitive landscape     | `context/competitive-landscape.md`    | Competitor audit and market gaps from `competitive-research`; gates positioning         |
| Brand positioning         | `context/positioning.md`              | Positioning statement and narrative from `positioning`; gates all downstream            |
| SEO & topic research      | `context/seo-research.md`             | Keyword-validated topic clusters from `seo-research`; feeds content strategy            |
| Content strategy          | `context/content-strategy.md`         | Editorial framework, pillars, cadence from `editorial-strategy`; gates cc-content       |
| Campaign brief / GTM plan | `context/brief.md` / `context/gtm.md` | Campaign concept or launch plan from `campaign-concept` or `gtm-plan`                   |

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
