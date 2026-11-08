# Research Prompts

Ready-to-paste deep-research prompts that strengthen this plugin's skills with scientific background and best practices beyond the general knowledge that was available when each skill was built.

## Scope

Five skills apply a named framework from general knowledge, with no dedicated `docs/research/` doc behind it yet, and they get a prompt here. Skills that already have a research doc, or that are pure process or orchestration skills with no framework of their own, don't.

| Skill                         | Research prompt                                | Why / why not                                                                                                                                                                                                                          |
| ----------------------------- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `campaign-concept`            | [campaign-concept.md](campaign-concept.md)     | Composes SOSTAC + RACE + Message House from general knowledge; covers the three shared frameworks generally                                                                                                                            |
| `channel-advisor`             | [channel-advisor.md](channel-advisor.md)       | Uses RACE specifically for channel-mix decisions; scoped to that facet, doesn't duplicate campaign-concept's prompt                                                                                                                    |
| `editorial-strategy`          | [editorial-strategy.md](editorial-strategy.md) | Uses Message House specifically for content pillars and cadence; scoped to that facet                                                                                                                                                  |
| `gtm-plan`                    | [gtm-plan.md](gtm-plan.md)                     | Composes all three frameworks plus a launch-type taxonomy; scoped to what's GTM-specific, since the other prompts cover the shared frameworks and the Success Metrics table already traces to `docs/research/measurement-framework.md` |
| `positioning`                 | [positioning.md](positioning.md)               | Uses four positioning frameworks (Obviously Awesome, Geoffrey Moore, Value Proposition Canvas, Perceptual Map) from general knowledge                                                                                                  |
| `audience-personas`           | None                                           | Already has `docs/research/audience-personas.md`                                                                                                                                                                                       |
| `competitive-research`        | None                                           | Already has `docs/research/competitive-research.md`                                                                                                                                                                                    |
| `seo-research`                | None                                           | Already has `docs/research/seo-research.md`                                                                                                                                                                                            |
| `strategy-orchestrator`       | None                                           | Already has `docs/research/strategy-orchestrator.md`                                                                                                                                                                                   |
| `learnings-promotion`         | None                                           | Process skill (reviews `.claude/learnings.md`); no framework to research                                                                                                                                                               |
| `marketing-advisor`           | None                                           | Open-ended advisor that defers to other skills; no framework of its own                                                                                                                                                                |
| `strategy-onboarding`         | None                                           | Interview and setup process skill; no framework to research                                                                                                                                                                            |
| `strategy-performance-review` | None                                           | Bet-verdict process skill; no framework to research                                                                                                                                                                                    |

## Using a Prompt

1. Open the prompt file for the skill you want to strengthen.
2. Paste the delimited prompt block into a "deep research" AI tool (Claude, ChatGPT, Gemini, Perplexity, or similar).
3. Save the response as Markdown under `docs/research/<skill-name>.md`, following the existing convention (see `docs/research/audience-personas.md` and its siblings).
4. Use the research to refine the relevant `_shared/*-frameworks.md` file (or the skill file itself for `gtm-plan`'s launch-type logic). Validate the frameworks already in use, add any well-evidenced ones that the research surfaces, and correct anything the current version got wrong.
