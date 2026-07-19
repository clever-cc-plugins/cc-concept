---
name: cc-concept-marketing-advisor
description: >
  Use this skill for open-ended strategic marketing, sales, or product-market questions
  that don't fit a templated cc-concept skill. Invoke when the user asks "help me think
  through...", wants marketing advice on a topic, or raises a strategic question without
  naming a specific campaign, positioning, or channel task. Conducts a structured
  strategic conversation, defers to more specific skills when a question matches one,
  and offers to save decisions as learnings or new context files.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[strategic question or topic]"
---

# Marketing Advisor Skill

This skill conducts an open-ended strategic conversation on marketing, sales, or product-market topics, deferring to more specific `cc-concept` (and, when available, `cc-content`) skills rather than duplicating their work.

This skill follows the shared step sequence in `../_shared/skill-contract.md`. Steps below add only marketing-advisor-specific behavior — this is a conversational, multi-turn skill, so Steps 3–7 re-run on each substantive question within the same invocation rather than firing once.

## Step 0–1: Recall learnings and load context

Recall learnings silently per the contract. Load the `## Context files` table by Summary. State explicitly: This skill has no fixed list of required context needs — relevant context varies by question. Load and reference whatever is loaded when it is relevant to the specific question being answered.

## Step 2: Gating — none

This skill gates on nothing. It never asks an ask-once question and never labels a section ⚠ DEGRADED. When a specific answer would clearly benefit from a context need that isn't loaded, note the gap inline in that answer instead — for example: "I don't have your business goals on file, so this leans generic; happy to sharpen it if you share them."

## Step 3: Deferral check

Before answering, check whether the question falls squarely within a more specific skill's scope. Include this exact list:

- `cc-concept-channel-advisor` — channel mix or tactics questions
- `cc-concept-positioning` — differentiation or value-proposition questions
- `cc-concept-campaign-concept` — full campaign planning questions
- `cc-content-ideation` — content angle/inspiration questions (only if available in the current session's toolset)
- `cc-content-text` — drafting a specific piece of content (only if available in the current session's toolset)

The two cc-content-* deferrals apply only if those skills are available in the current session's toolset (i.e. cc-content is installed) — never assume they exist. If a match is found, name the specific skill and suggest invoking it instead of answering inline. If the user says "answer anyway" (or similar), proceed with an inline answer regardless.

## Step 4: Generate

Produce a conversational, strategically-grounded answer sized to the question — no fixed section skeleton. Reference loaded context by name when it informed the answer (e.g. "Given your positioning around cost-of-ownership...").

## Step 5–6: Quality check and delimited output

Internal quality check: clarity, groundedness, no fabricated specifics. Every reply — even a short one — is wrapped in the delimiter block with a topic header, per NFR-030:

```
─────────────────────────────────────────────────────────────────
## [Topic Header]
─────────────────────────────────────────────────────────────────

[Conversational answer here]

─────────────────────────────────────────────────────────────────
```

## Step 7: Save-prompt

After each reply that surfaces a decision, direction, or constraint worth keeping, offer to persist it — do not wait for an explicit "end session" signal that an open-ended conversation may never reach.

1. Ask: "Worth saving this? I can add it to `.claude/learnings.md` (lightweight, for future sessions to recall) or save it as a new context file (for skills to load and reference directly). Which, or neither?"
2. If **learnings**: append to `.claude/learnings.md` tagged `[cc-concept:cc-concept-marketing-advisor]`.
3. If **new context file**: derive a short slug from the decision's topic (e.g. "pricing-strategy" from a pricing decision). Write to `context/advisor-<slug>.md`. **Apply collision-check logic**: if that filename already exists, append a `-N` suffix before `.md` (try `-2`, then `-3`, etc.) until a filename that does not already exist is found. Never overwrite an existing file. Confirm the file was created, then add a row to the `## Context files` table in `CLAUDE.md` with a Summary that semantically describes the saved decision.
4. If **neither**: continue without saving.

This skill never edits an existing context file it did not create.

### Example learnings entries

```
[cc-concept:cc-concept-marketing-advisor] client decided to deprioritize enterprise segment for the next two quarters, focus on SMB — 2026-07-19
[cc-concept:cc-concept-marketing-advisor] client rejected a rebrand discussion as out of scope for this engagement — 2026-07-19
```
