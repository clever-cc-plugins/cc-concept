<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/clever-cc-plugins/.github/main/assets/logo-dark.svg" />
    <img src="https://raw.githubusercontent.com/clever-cc-plugins/.github/main/assets/logo.svg" width="220" alt="clever [cc] plugins" />
  </picture>
</p>

# <img src="assets/icon.svg" width="40" height="40" align="top" alt="" />&nbsp;cc-concept

A [Claude Code](https://claude.ai/code) plugin with marketing-strategy skills for positioning, campaign concepting, channel strategy, content strategy, go-to-market planning, and open-ended strategic advice. `cc-concept` produces the strategic frame that the `cc-content` skills then execute against. Positioning after the posts is like writing tests after the release: possible, but you find out late what's broken.

`cc-concept` runs standalone and never requires `cc-content`, but it recognizes and reuses context that an existing `cc-content` project already provides.

> **Breaking change (v1.0.0):** Skill names dropped the `cc-concept-` prefix (for example `cc-concept-positioning` became `positioning`). Claude Code already namespaces plugin skills as `cc-concept:<skill-name>`, so the prefix was redundant. A few names also changed wording to stay specific and to avoid collisions with `cc-content` skills: `cc-concept-onboarding` became `strategy-onboarding`, `cc-concept-performance-review` became `strategy-performance-review`, `cc-concept-orchestrator` became `strategy-orchestrator`, `cc-concept-content-strategy` became `editorial-strategy`, and `cc-concept-gtm` became `gtm-plan`. Update any saved `/cc-concept-...` invocations to the new names.

---

## At a Glance

| Skill                                     | What it does                                                                                                                           |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `/cc-concept:strategy-onboarding`         | Collects any strategic context that downstream skills need and the project lacks                                                       |
| `/cc-concept:audience-personas`           | Develops one or more audience personas or ICPs from scratch via interview, or from customer data                                       |
| `/cc-concept:positioning`                 | Develops product or company positioning and registers it as project context                                                            |
| `/cc-concept:competitive-research`        | Runs a standalone competitive audit covering messaging, positioning, SWOT, market gaps, and content-strategy opportunities             |
| `/cc-concept:seo-research`                | Builds keyword-validated topic clusters with Ubersuggest MCP tools when they're connected, or with interview-driven research otherwise |
| `/cc-concept:campaign-concept`            | Builds a complete campaign concept (goals, audience, key messages, channel mix, creative brief) and hands it off as `brief.md`         |
| `/cc-concept:channel-advisor`             | Recommends a channel mix and tactics for a goal, audience, and budget                                                                  |
| `/cc-concept:editorial-strategy`          | Produces an editorial planning framework (content pillars, topic clusters, mix, cadence) and registers it as context                   |
| `/cc-concept:gtm-plan`                    | Structures a go-to-market launch plan: audience, positioning, channel sequence, messages, milestones                                   |
| `/cc-concept:strategy-orchestrator`       | Matches a stated business goal to an engagement type and sequences the right `cc-concept` and `cc-content` skills, in the right order  |
| `/cc-concept:marketing-advisor`           | Gives open-ended strategic advice for questions that don't fit a templated skill, and defers to the more specific skills above         |
| `/cc-concept:strategy-performance-review` | Reviews whether a positioning, channel-mix, content-strategy, GTM, or campaign bet played out, and recommends the next adjustment      |
| `/cc-concept:learnings-promotion`         | Reviews accumulated `.claude/learnings.md` entries and promotes recurring patterns into durable guidance                               |

Claude Code namespaces every plugin skill, so you invoke each one as `/cc-concept:<skill-name>`, for example `/cc-concept:positioning`.

---

## Installation

Open Claude Code in any project and run:

```
/plugin marketplace add clever-cc-plugins/marketplace
/plugin install cc-concept@clever-cc-plugins
```

All skills are available immediately.

### Keeping Skills Current

Auto-update is off by default for third-party marketplaces. To switch it on:

1. Run `/plugin` in Claude Code
2. Open the **Marketplaces** tab
3. Toggle auto-update for `clever-cc-plugins/marketplace`

Once it's on, Claude Code updates the skills on startup whenever a new version is available.

### Uninstalling

```
/plugin uninstall cc-concept@clever-cc-plugins
```

To remove the marketplace as well (this uninstalls every plugin you installed from it):

```
/plugin marketplace remove clever-cc-plugins
```

---

## Getting Started

**Step 1: Onboard (optional but recommended)**

```
/cc-concept:strategy-onboarding
```

Onboarding collects business goals, target audience, and any other strategic context that the skills below need. It also picks up context that an existing `cc-content` project already has. Every templated skill asks for what it's missing the first time it needs it, so onboarding just front-loads those questions.

**Step 2: Set the strategic frame**

```
/cc-concept:positioning
/cc-concept:channel-advisor
/cc-concept:editorial-strategy
```

Run whichever of these apply to the work at hand. Each one produces a document and registers it as project context, so later skills (including the `cc-content` skills) pick it up automatically.

If your plan includes content production, build the brand voice guide with `/cc-content:brand-voice` once positioning is set. That skill belongs to the [`cc-content`](https://github.com/clever-cc-plugins/cc-content) plugin, which you need to install separately. It turns positioning, values, and personas into writing rules that the `cc-content` drafting skills load. Voice is the bridge from strategy to content, so it lives with the skills that use it.

**Step 3: Plan a campaign or launch**

```
/cc-concept:campaign-concept
/cc-concept:gtm-plan
```

Both skills produce a full plan and offer to save a `brief.md`-compatible handoff file that `cc-content` skills can consume directly.

**Step 4: Ask anything else**

```
/cc-concept:marketing-advisor
```

Use it for strategic questions that don't fit a templated skill. When a more specific skill matches, the advisor defers to it.

**Step 5: Close the loop**

```
/cc-concept:learnings-promotion
```

Every so often, review the corrections and preferences that the skills above logged to `.claude/learnings.md`, and promote the recurring ones into `CLAUDE.md` so you don't have to repeat them.

---

## Context Architecture

`cc-concept` follows the same context model as `cc-content`: a `## Context files` table in `CLAUDE.md` instead of `@`-imports.

**`@`-imports** (for example `@DESIGN.md` or `@AGENTS.md`) are parsed by Claude Code, and they pull the referenced file's full content into the context window on every message of every session. Reserve them for the handful of files that every task needs.

**The `## Context files` table** is plain Markdown. Only the table itself (label, path, one-line summary) loads with `CLAUDE.md` on every message, which is cheap. The underlying files load on demand: a skill reads the table, matches the current task against each row's summary, and reads only the files that are relevant.

```markdown
## Context files

Skills read all registered files and load what's relevant for each task.

| Label            | File                          | Summary                                                                                 |
| ---------------- | ----------------------------- | --------------------------------------------------------------------------------------- |
| Positioning      | `context/positioning.md`      | Product positioning: differentiation, target audience, competitive alternatives         |
| Content strategy | `context/content-strategy.md` | Content strategy: content pillars, topic clusters, content type mix, publishing cadence |
```

- **Label:** free-form, whatever you recognize at a glance. Skills never match on it.
- **File:** a path relative to the `CLAUDE.md` that contains the table, not relative to the repository root.
- **Summary:** the field that skills match against. Write one sentence, specific enough to work as a relevance signal.

`/cc-concept:strategy-onboarding` and each templated skill's own registration step (for example positioning or content strategy) build and extend this table. `campaign-concept` and `gtm-plan` also hand off an optional `brief.md` at the working-directory root. It's a one-time handoff artifact for `cc-content` and never gets registered in the context table.

---

## Learnings

Every `cc-concept` skill can log a correction or a recurring preference to `.claude/learnings.md`, tagged `[cc-concept:<skill-name>]`. Nothing modifies `CLAUDE.md` directly in the moment. Later, `/cc-concept:learnings-promotion` reviews the accumulated entries, groups the recurring ones (three or more similar entries), and proposes either promoting them into `CLAUDE.md` or dismissing them as one-offs. It never commits on your behalf and never touches the tags of other plugins.

---

## Contributing

Issues and pull requests are welcome. If you've spotted a gap or a rough edge, please open an issue first so we can agree on the approach.

---

## License

[MIT](LICENSE), Copyright (c) 2026 Michael van Laar

---

<p align="center">
  Part of the <a href="https://github.com/clever-cc-plugins">clever-cc-plugins</a> family · <a href="https://github.com/clever-cc-plugins/marketplace">marketplace</a> · <a href="https://github.com/clever-cc-plugins/cc-config">cc-config</a> · <a href="https://github.com/clever-cc-plugins/cc-content">cc-content</a> · <a href="https://github.com/clever-cc-plugins/cc-career">cc-career</a> · <a href="https://github.com/clever-cc-plugins/cc-coach">cc-coach</a> · <a href="https://github.com/clever-cc-plugins/cc-handoff">cc-handoff</a> · <a href="https://github.com/clever-cc-plugins/cc-chime">cc-chime</a> · <a href="https://github.com/clever-cc-plugins/cc-chef">cc-chef</a>
</p>
