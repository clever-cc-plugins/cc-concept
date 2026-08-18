# Research Prompt: gtm-plan

**For:** `cc-concept:gtm-plan`
**Current knowledge base:** composes SOSTAC + RACE + Message House (see
`campaign-concept.md` and `channel-advisor.md` in this folder for those),
plus a launch-type taxonomy (product-launch / feature-release /
market-expansion) and a Success Metrics table of leading/lagging indicators
per launch type. The Success Metrics table already appears to be grounded in
`docs/research/measurement-framework.md`; the launch-type taxonomy itself and
GTM-specific best practices beyond the shared frameworks are not
research-backed yet.
**Relationship to other prompts:** don't duplicate `campaign-concept.md`'s
SOSTAC/RACE/Message House research — this prompt is scoped to what's specific
to go-to-market planning.

Paste the prompt below into a deep-research AI tool (Claude, ChatGPT, Gemini,
Perplexity, or similar). Save the response as Markdown, e.g. to
`docs/research/gtm-plan.md`, then use it to refine `gtm-plan/SKILL.md`
directly (the launch-type and calibration logic lives in the skill file
itself, not in the shared `campaign-frameworks.md`).

---

```
─────────────────────────────────────────────
Research prompt: go-to-market planning — launch types and best practices
─────────────────────────────────────────────
You are a research analyst investigating evidence-based practice for
go-to-market (GTM) planning, for use in an AI marketing-strategy tool that
already covers overall campaign structure (SOSTAC), channel sequencing
(RACE), and message architecture (Message House) — do not re-research those;
focus on what's specific to GTM planning itself.

Cover, with headers separating each area:

1. Whether "product-launch," "feature-release," and "market-expansion" is a
   well-recognized taxonomy of GTM engagement types in current practitioner
   or academic literature, or whether a different/finer-grained taxonomy is
   more commonly used and better supported (e.g. distinguishing net-new
   category creation from launching into an existing category).
2. Research or well-evidenced practitioner guidance on how launch depth
   should actually scale by type — is "feature-release gets lighter
   treatment than product-launch" a defensible simplification, or does
   research suggest other factors (e.g. existing customer base size,
   competitive intensity) matter more than launch type for calibrating
   depth?
3. What's known about GTM launch failure modes specifically (distinct from
   general campaign failure) — e.g. research or case-study patterns on why
   product launches underperform their plan (positioning misalignment,
   channel readiness gaps, premature scaling).
4. Best practices for sequencing a GTM plan's milestones against the Control
   facet of SOSTAC — what does current practice recommend for how far out
   milestones should be set and reviewed for a launch, as distinct from an
   ongoing campaign.
5. How positioning should factor into a GTM plan when no dedicated
   positioning work has been done yet (i.e., what's a defensible fallback
   process for generating "good enough" launch positioning under time
   pressure, versus skipping it or bolting on generic claims).

Require credible, verifiable sources throughout, with in-text citations —
prioritize peer-reviewed marketing/product-management research and
recognized practitioner sources (e.g. published GTM playbooks from
recognized firms, case studies with real outcomes) over generic
launch-checklist blog content. Provide a formatted source list in APA style
at the end. Respond in Markdown.
─────────────────────────────────────────────
```
