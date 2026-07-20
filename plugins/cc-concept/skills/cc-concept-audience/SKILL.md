---
name: cc-concept-audience
description: >
  Use this skill to develop one or more audience personas or ICPs from scratch —
  interviewing the owner or synthesizing from pasted customer data (support tickets,
  sales call notes, survey results). Invoke when the user asks to "build a persona",
  "define our ICP", "who is our target audience", "develop buyer personas", or when
  another cc-concept skill reports that its "target audience" need is missing.
  Produces `context/audience-personas.md` for every other skill's existing audience
  gate to consume — this skill is the producer other skills already assumed existed.
allowed-tools: Read, Write, Edit, Bash
argument-hint: "[optional: path to customer data to synthesize personas from]"
---

# Audience Persona Development Skill

Every other `cc-concept` and `cc-content` skill gates on "target audience" as
something already known. This skill is where it gets built, so gated skills upstream
of it stop asking the owner to describe an audience from memory.

Adapts `../_shared/skill-contract.md`'s 8-step sequence. Step 1 differs: this skill
has no required gate of its own (it is a discoverer, like `cc-concept-onboarding`),
but it still loads organization background if registered, since persona work grounded
in a known mission/offer beats personas built in isolation.

## Step 0: Recall learnings

If `.claude/learnings.md` exists, read it silently, all plugin tags. Apply relevant
entries (e.g., a prior run's preferred persona count or template). Never announce.

## Step 1: Load context and choose a mode

Read the `## Context files` table in `CLAUDE.md`. If `context/organization-background.md`
(or equivalent Summary match: organization, company, business model, background,
profile, mission, values, size, market position, customer, constraints) exists,
load it — persona work references the org's actual offer and constraints rather than
generic language.

Ask once: "Do you have existing customer data (support tickets, sales notes, survey
results, interview transcripts) to synthesize personas from, or should I interview
you to build one from scratch?" Branch on the answer:

- **Synthesize mode:** read the supplied file(s)/pasted text; extract patterns across
  the source data (research recommends minimum 5 corroborating cases per segment
  before drawing conclusions, saturation typically by ~12 interviews). Apply the
  thematic coding + affinity mapping pipeline from `docs/research/cc-concept-audience.md`
  § _Synthesizing a Defensible Persona from Raw Qualitative Inputs_.
- **Interview mode:** run the JTBD question set from `docs/research/cc-concept-audience.md`
  § _Jobs-to-be-Done (JTBD) Style Interview Question Set_, one question at a time,
  same one-at-a-time interview rhythm as `cc-concept-onboarding`.

## Step 2: Detect B2B vs. B2C

Ask once: "Are you building personas for a B2B product/service, or B2C/consumer?"
If unclear from the answer, ask the owner for one clarifying detail: "Are your
customers organizations buying for their teams/operations, or individuals buying
for personal use?"

This determines the persona template (field structure) in Step 4. Save this choice
for downstream quality checks.

## Step 3: Calibrate persona count

Default: **3–5 personas** per research consensus (Jansen et al., 2022; Salminen et
al., 2022). This is the practical ceiling where most organizations can operationalize
messaging and sales without sprawl.

Ask once: "How many distinct audience segments are you trying to reach with different
messaging or positioning? (Usually 3–5 is the sweet spot; I'll help you avoid creating
too many.)"

- **User says 2–3** → proceed with 2–3.
- **User says 5–7** → warn once: "5–7 is getting toward the threshold where diminishing
  returns kick in. I recommend keeping it to 5 max unless each segment truly has
  different decision logic. Shall I keep it to 5?"
- **User says 8+** → warn: "Beyond 7–8 personas, you risk persona sprawl — too many
  to operationalize well. Let's stick to 5 and note the others as variants of your
  primary personas. Agreed?"

Record the final count for Step 4 scoping.

## Step 4: Generate

Apply the appropriate persona template from the research file:

**For B2B** (research: Jansen et al., 2022; Rebets, 2026):

For each persona, produce a structured profile including:

- **Identity & role:** name/archetype, job title, seniority, function/department
- **Organization context:** company size, industry, geographic market
- **Position in buying committee:** economic buyer, champion, influencer, end user,
  technical evaluator, blocker — **and** budget authority (approval threshold)
- **Jobs & success metrics:** the functional, emotional, and social jobs they're
  trying to make progress on; how their success is measured (KPIs)
- **Pain points & objections:** business obstacles, feared risks (integration,
  compliance, procurement, career risk)
- **Decision criteria & information sources:** what they weigh when evaluating;
  where they research (analyst reports, peer reviews, case studies, webinars)
- **Verbatim quote** from an interview or customer data illustrating a key insight

**For B2C** (research: Christensen et al., 2016; Rebets, 2026):

For each persona, produce:

- **Identity & demography:** name/archetype, age range, household type, lifestyle,
  location
- **Goals & motivation:** functional job (task to accomplish), emotional job (feeling
  sought), aspirational motivation
- **Purchase trigger:** the event or moment that prompts search (life event, frustration,
  seasonal, social influence)
- **Pain points & objections:** friction with current solutions, barriers to purchase
  (price, trust, effort, prior bad experience)
- **Decision journey:** how they become aware, consider, and choose (typically quick,
  often influenced by social proof and reviews)
- **Channel & content preferences:** where they discover products (social, review sites,
  word-of-mouth), media formats preferred
- **Verbatim quote** illustrating a key motivation or objection

Structure each persona as a **markdown block** with clear section headers, not a table.
Aim for 200–300 words per persona (specific enough to guide messaging, not so detailed
it becomes unwieldy).

## Step 5: Internal quality check

Before presenting personas, gate each against **falsifiability** (research: Pedowitz,
2026; Dewi et al., 2026): A persona must make testable claims about behavior,
decision criteria, and triggers — not just demographics.

For each persona, check:

1. **Jobs (functional/emotional/social)** — Does it describe the actual work being
   done, not just who the person is? ✓ (Vague: "Alex is a data-driven executive"
   ✗ Better: "Alex reviews analytics dashboards weekly and needs 5-minute decision
   summaries to flag action items for her team".)
2. **Triggers** — Does it name the event or moment that starts a search? ✓
3. **Decision criteria** — Does it describe what they actually weigh when choosing,
   not just adjectives? ✓ (Vague: "Values quality" ✗ Better: "Requires integration
   with existing CRM and pricing ROI breakdown before commit".)
4. **Supported by data** — Is each claim backed by at least one interview/ticket/quote?
   (Interview mode: yes, by definition. Synthesize mode: flag claims appearing in
   only 1 source as "potential outlier" or "single anecdote", don't surface as core
   persona traits.)

If a persona fails the check, revise it before presenting. Do not pass vague
demographic sketches downstream — they will mislead downstream skills' messaging work.

## Step 6: Delimited output

Present all personas in a delimited block before writing anything:

```
========== PERSONAS — FOR YOUR REVIEW ==========
[persona blocks with clear section headers]
========== END PERSONAS ==========
```

Ask: "Do these personas match your sense of your audience, or should I adjust?
Anything to add or merge?"

Wait for feedback before proceeding to Step 7.

## Step 7: Feedback + registration

**Write** the validated personas to a collision-checked file:

1. Check if `context/audience-personas.md` already exists.
2. If it does, generate a distinct filename by appending `-N` (e.g.,
   `context/audience-personas-2.md`). Keep incrementing N until a filename that does
   NOT exist is found.
3. Write the final file with the format:

```markdown
# Audience Personas

[Preamble: 1–2 sentences on the segments these personas represent and the methodology
(interview/synthesize) used to develop them.]

## [Persona Name]

[Persona block: sections as per Step 4 template. Include at least one verbatim quote
per persona.]

## [Next Persona]

[...]
```

**Register** in the `## Context files` table of `CLAUDE.md`:

```markdown
| Audience personas | `context/audience-personas.md` | Target audience segments, roles, jobs, pain points, and decision criteria (ICP, personas, audience segmentation) |
```

The Summary keyword set (ICP, personas, audience, segmentation, jobs, decision) must
match what other skills' existing "target audience" gates already search for semantically.

**Store learnings** tagged `[cc-concept:cc-concept-audience]` in `.claude/learnings.md`:

Examples:

```
[cc-concept:cc-concept-audience] client prefers "buyer personas" over "audience segments" — 2026-07-20
[cc-concept:cc-concept-audience] org's B2B buying committee has 6 distinct roles; 5 personas covers the critical path — 2026-07-20
[cc-concept:cc-concept-audience] synthesize mode: 22 support tickets across 4 themes sufficient for 3-persona set, saturation ~15 — 2026-07-20
```

Do not announce this step.
