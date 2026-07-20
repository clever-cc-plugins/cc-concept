<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/clever-cc-plugins/.github/main/assets/logo-dark.svg" />
    <img src="https://raw.githubusercontent.com/clever-cc-plugins/.github/main/assets/logo.svg" width="220" alt="clever [cc] plugins" />
  </picture>
</p>

# cc-concept

A [Claude Code](https://claude.ai/code) plugin providing marketing-strategy skills — positioning, campaign concepting, channel strategy, content strategy, go-to-market planning, and open-ended strategic advice. cc-concept produces the strategic frame that `cc-content` skills then execute against.

cc-concept runs standalone — it never requires `cc-content` — but recognises and reuses context an existing `cc-content` project already provides.

---

## At a glance

| Skill                              | What it does                                                                                                                               |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `/cc-concept-audience`             | Develops one or more audience personas or ICPs from scratch via interview or synthesis from customer data                                  |
| `/cc-concept-competitive-research` | Runs a standalone competitive audit covering messaging, positioning, SWOT, market gaps, and content-strategy opportunities                 |
| `/cc-concept-onboarding`           | Collects any strategic context downstream skills need but the project lacks                                                                |
| `/cc-concept-orchestrator`         | Matches a stated business goal to an engagement type and sequences the right subset/order of cc-concept and cc-content skills to run       |
| `/cc-concept-positioning`          | Develops product/company positioning and registers it as project context                                                                   |
| `/cc-concept-campaign-concept`     | Builds a complete campaign concept — goals, audience, key messages, channel mix, creative brief — and hands it off as `brief.md`           |
| `/cc-concept-channel-advisor`      | Recommends a channel mix and tactics for a goal, audience, and budget                                                                      |
| `/cc-concept-content-strategy`     | Produces an editorial planning framework — content pillars, topic clusters, mix, cadence — and registers it as context                     |
| `/cc-concept-seo-research`         | Builds keyword-validated topic clusters using Ubersuggest MCP tools when connected, or fallback interview-driven research                  |
| `/cc-concept-gtm`                  | Structures a go-to-market launch plan — audience, positioning, channel sequence, messages, milestones                                      |
| `/cc-concept-marketing-advisor`    | Open-ended strategic advisor for questions that don't fit a templated skill, with deferral to the more specific ones above                 |
| `/cc-concept-performance-review`   | Reviews whether a positioning, channel-mix, content-strategy, GTM, or campaign bet actually played out, and recommends the next adjustment |
| `/cc-concept-learnings-promotion`  | Reviews accumulated `.claude/learnings.md` entries and promotes recurring patterns into durable guidance                                   |

Skills are invoked by bare name (e.g. `/cc-concept-positioning`), never namespaced with the plugin name.

---

## Installation

Open Claude Code in any project and run:

```
/plugin marketplace add clever-cc-plugins/marketplace
/plugin install cc-concept@clever-cc-plugins
```

### Keeping it current

Auto-update for third-party marketplaces is off by default. To enable it:

1. Run `/plugin` in Claude Code
2. Go to the **Marketplaces** tab
3. Toggle auto-update for `clever-cc-plugins/marketplace`

Once enabled, Claude Code updates the plugin on startup whenever a new version is available.

### Uninstalling

```
/plugin uninstall cc-concept@clever-cc-plugins
```

To remove the marketplace as well:

```
/plugin marketplace remove clever-cc-plugins
```

---

## Getting Started

**Step 1 — Onboard (optional but recommended)**

```
/cc-concept-onboarding
```

Collects business goals, target audience, and any other strategic context the skills below need — and picks up context an existing `cc-content` project already has. Every templated skill also asks for what it's missing on its own, once, the first time it needs it — onboarding just front-loads that.

**Step 2 — Set the strategic frame**

```
/cc-concept-positioning
/cc-concept-channel-advisor
/cc-concept-content-strategy
```

Run whichever of these apply to the work at hand. Each produces a document and registers it as project context, so later skills (including `cc-content`'s) pick it up automatically.

**Step 3 — Plan a campaign or launch**

```
/cc-concept-campaign-concept
/cc-concept-gtm
```

Both produce a full plan and offer to save a `brief.md`-compatible handoff file that `cc-content` skills can consume directly.

**Step 4 — Ask anything else**

```
/cc-concept-marketing-advisor
```

For strategic questions that don't fit a templated skill — it defers to the skill above that actually matches, when one does.

**Step 5 — Close the loop**

```
/cc-concept-learnings-promotion
```

Periodically, review the corrections and preferences the skills above have logged to `.claude/learnings.md`, and promote the recurring ones into `CLAUDE.md` so they don't need to be repeated.

---

## Context Architecture

cc-concept follows the same context model as `cc-content`: a `## Context files` table in `CLAUDE.md`, not `@`-imports.

**`@`-imports** (e.g. `@DESIGN.md`, `@AGENTS.md`) are parsed by Claude Code and pull the referenced file's full content into the context window unconditionally — every message, every session. Reserve them for the handful of files genuinely relevant to every task.

**The `## Context files` table** is plain Markdown. Only the table itself (label, path, one-line summary) loads every message via `CLAUDE.md` — cheap. The underlying files load conditionally: a skill reads the table, matches the current task against each row's Summary, and reads only the file(s) that are actually relevant.

```markdown
## Context files

Skills read all registered files and load what's relevant for each task.

| Label            | File                          | Summary                                                                                 |
| ---------------- | ----------------------------- | --------------------------------------------------------------------------------------- |
| Positioning      | `context/positioning.md`      | Product positioning: differentiation, target audience, competitive alternatives         |
| Content strategy | `context/content-strategy.md` | Content strategy: content pillars, topic clusters, content type mix, publishing cadence |
```

- **Label** — free-form, whatever you'd recognize at a glance. Skills never match on it.
- **File** — relative to the `CLAUDE.md` that contains the table, not the repository root.
- **Summary** — the field skills actually match against. One sentence, specific enough to act as a relevance signal.

`/cc-concept-onboarding` and each templated skill's own registration step (e.g. positioning, content strategy) build and extend this table. `cc-concept-campaign-concept` and `cc-concept-gtm` also hand off an optional `brief.md` at the working-directory root — this is a one-time handoff artifact for `cc-content`, never registered in the context table.

---

## Learnings

Every cc-concept skill can log a correction or a recurring preference to `.claude/learnings.md`, tagged `[cc-concept:<skill-name>]`. Nothing modifies `CLAUDE.md` directly in the moment — `/cc-concept-learnings-promotion` reviews the accumulated entries later, groups recurring ones (3 or more similar), and proposes promoting them into `CLAUDE.md` or dismissing one-offs. It never commits on your behalf and never touches other plugins' tags.

---

## License

[MIT](LICENSE) — Copyright (c) 2026 Michael van Laar

---

<p align="center">
  Part of the <a href="https://github.com/clever-cc-plugins">clever-cc-plugins</a> family · <a href="https://github.com/clever-cc-plugins/marketplace">marketplace</a> · <a href="https://github.com/clever-cc-plugins/cc-config">cc-config</a> · <a href="https://github.com/clever-cc-plugins/cc-content">cc-content</a> · <a href="https://github.com/clever-cc-plugins/cc-handoff">cc-handoff</a> · <a href="https://github.com/clever-cc-plugins/cc-chime">cc-chime</a>
</p>
