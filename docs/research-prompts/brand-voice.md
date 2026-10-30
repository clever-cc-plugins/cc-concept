# Research Prompt: brand-voice

**For:** `cc-concept:brand-voice` (planned skill, not yet built)
**Current knowledge base:** none in cc-concept. The only existing brand-voice support
is `cc-content:content-onboarding`'s five-question interview, which writes answers
into a file without analysis or examples, and `cc-content`'s
`_shared/readability-patterns.md`, which covers sentence-level readability (Clark,
Martin & Mahowald, 2026) but not voice itself.
**Why research helps:** the skill has to work in any output language and produce a
guideline that both people and LLMs/AI agents can apply. Most brand-voice advice is
practitioner lore written for English-speaking marketing teams; the research should
separate evidence from convention and cover multilingual and machine-readable use
explicitly.

**What the skill will do** (scope the research is meant to inform): derive a brand
voice from existing text samples, from an interview, or both; write it as a guideline
with checkable rules and examples; register it as a context file that every
`cc-content` drafting skill loads.

Paste the prompt below into a deep-research AI tool (Claude, ChatGPT, Gemini,
Perplexity, or similar). Running it in two or three tools and merging the results
gives better coverage than one run. Save the response as Markdown to
`docs/research/brand-voice.md`, then build the skill from it.

---

```
─────────────────────────────────────────────
Research prompt: creating brand voice guidelines for any language, usable by humans and AI
─────────────────────────────────────────────
You are a research analyst preparing the evidence base for an AI tool that helps
organizations and individuals create a brand voice guideline. The tool derives the
voice from existing text samples, from a structured interview, or both. The
guideline it produces must work in any language the user needs (not only English)
and must be equally usable by human writers and by large language models (LLMs)
and AI agents that generate text from it.

Cover, with headers separating each area:

1. Foundations: definitions and distinctions between brand voice, tone, style,
   register, and brand personality. What is the evidence on voice/tone effects on
   reader perception (trust, credibility, likability, purchase or action intent)?
   Include the Nielsen Norman Group tone-of-voice dimensions research and Aaker's
   brand personality scale, its later critiques and cross-cultural replications.
   State which models are empirically validated and which are practitioner
   conventions (e.g. brand archetypes).

2. Anatomy of an effective guideline: which components recur in well-regarded
   public voice and style guides (e.g. Mailchimp/Intuit, GOV.UK, Microsoft,
   Atlassian, Shopify Polaris, and non-English examples where available), such as
   voice attributes, "this, not that" pairs, tone maps by context or channel,
   vocabulary lists, do/don't examples, and grammar and punctuation rules. What
   does research or practitioner evidence say about which components make writers
   actually apply a guideline, and why guidelines fail (too vague, too long,
   adjectives without examples, no governance)?

3. Deriving a voice from existing texts: methods to extract a voice from a sample
   corpus, including stylometry, corpus linguistics (keywords, collocations,
   sentence-length distribution, pronoun use, formality markers), dictionary tools
   such as LIWC, and LLM-based style extraction. How many samples are needed, how
   to handle inconsistent samples, how reliable LLM-based style description is, and
   how to separate a deliberate voice from accidental habits or errors in the
   samples.

4. Deriving a voice through interviews or workshops: question sets and exercises
   used by brand strategists and UX writers (e.g. personality sliders, "we are X
   but not Y", reference brands, audience-relationship framing). Which have
   evidence behind them, how to connect voice to positioning and audience, and how
   to resolve conflicts between stakeholders' stated preferences and what their
   existing texts actually show.

5. Multilingual and cross-cultural voice: how global brands keep one voice across
   languages (translation vs. localization vs. transcreation) and which voice
   attributes transfer across languages and cultures versus which must be defined
   per language. Cover formality and address systems (T-V distinctions such as
   du/Sie, tu/vous, tú/usted; Japanese keigo; Korean speech levels), gender-
   inclusive language conventions in gendered languages (e.g. German, French,
   Spanish), typographic and punctuation conventions, culturally dependent
   directness, humor and politeness (e.g. Hofstede, Meyer's Culture Map, and their
   evidence status), and how to structure a guideline with a language-independent
   core plus per-language rule layers.

6. Readability and plain language across languages: ISO 24495-1:2023 (plain
   language), language-specific readability formulas (e.g. Flesch for English,
   Amstad and Wiener Sachtextformel for German, LIX, Fernández-Huerta for Spanish)
   and their validity, CEFR levels as a target, and German Einfache Sprache vs.
   Leichte Sprache. How should a voice guideline set a readability target that
   works in any language?

7. Writing the guideline for LLMs and AI agents: current evidence (prefer 2023
   onward) on how LLMs follow style instructions. Compare descriptions vs.
   examples (few-shot), positive vs. negative instructions ("avoid X"), concrete
   checkable rules vs. adjectives, persona prompting, structured formats (tables,
   rule lists, YAML or JSON) vs. prose, and the effect of guideline length and
   position in long contexts. Do LLMs over-apply or caricature stated voice traits?
   Do models follow style rules equally well in non-English output? Cover how to
   phrase rules so they work both as human guidance and as machine instructions.

8. Evaluating voice consistency: methods to check whether a text matches a
   guideline, including human rating rubrics, inter-rater agreement, LLM-as-judge
   scoring and its known biases, stylometric distance to a reference corpus, and
   A/B tests of tone variants. Which of these could an AI tool use to self-check a
   draft, and how reliable are they?

9. Variants and maintenance: multiple voices within one organization (e.g.
   recruiting vs. corporate vs. product UI), a personal brand voice for an
   individual vs. an organizational voice, how and when to revise a guideline,
   and governance practices that keep it in use.

For every recommendation, state the evidence level: peer-reviewed empirical
research, standards body, documented practitioner method, or opinion. Flag where
findings come only from English-language contexts. Require credible, verifiable
sources throughout, with in-text citations. Prioritize peer-reviewed research
(linguistics, psycholinguistics, marketing science, NLP/LLM evaluation), standards,
and published style guides over generic marketing-blog content. Close with a
synthesis section listing the concrete design implications for an AI tool that
builds brand voice guidelines. Provide a formatted source list in APA style at the
end. Respond in Markdown.
─────────────────────────────────────────────
```
