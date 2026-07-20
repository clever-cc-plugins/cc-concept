# Measurement Framework


---

## ChatGPT (source: `measurement-framework-chatgpt.md`)

# Erfolgsmessung in Kampagnen und Launch-Projekten

## 1. Führungs- vs. nachgelagerte Kennzahlen nach Kampagnen- und Launch-Typ

Im Kampagnen- und Launch-Controlling unterscheidet man **führende (Leading)** und **nachgelagerte (Lagging)** Kennzahlen. Führende Indikatoren signalisieren frühzeitig, ob eine Aktion Wirkung zeigt (etwa Website-Traffic, Klickrate, Engagement), während nachgelagerte Indikatoren das tatsächliche Ergebnis abbilden (z.B. Umsatz, Abschlüsse, Retention). Praktische Beispiele – aufgeteilt nach Kampagnentyp – sind:

- **Produkt-Launch (Kampagne):** *Führend* z.B. Page-Visits oder Demo-Anfragen für das neue Produkt, *nachgelagert* die daraus resultierenden Verkäufe oder Umsatz. Smith & Jones beschreibt etwa, dass bei einer Krankenhaus-Werbung Seitenaufrufe und Anrufvolumen als Leading und tatsächlich gebuchte Termine als Lagging gemessen werden.  
- **Thought-Leadership:** *Führend* etwa Anzahl neuer Blogposts bzw. Social-Shares; *nachgelagert* die generierten Leads oder Marktbefragungen zur Markenwahrnehmung. (Konkrete Werte müssen vorab definiert werden.)  
- **Saisonale Promotion:** *Führend* typischerweise Öffnungs- und Klickraten von Aktions-E-Mails bzw. Einlösungen von Gutscheinen; *nachgelagert* die im Aktionszeitraum erzielte Absatzsteigerung oder der zusätzliche Umsatz.  
- **Retention/Kundenbindung:** *Führend* könnten Anmeldungen zu Reaktivierungs-E-Mails, Nutzungsfrequenz oder Feature-Adoption sein; *nachgelagert* die Änderung der Abwanderungsrate bzw. Kunden-Lifetime-Value. Im Improvado-Beispiel werden Nutzungs-Frequenz oder NPS als Leading und monatliche Churn-Rate bzw. CLV als Lagging-Kennzahlen genannt.  
- **Lead-Generierung:** *Führend* z.B. Anzahl qualifizierter neuer Leads oder Demo-Anfragen; *nachgelagert* die Conversion-Rate zu Sales-Opportunities oder CAC. Eine Empfehlung von Improvado listet etwa Engagement in Zielaccounts und Demo-Qualität gegen MQL→SQL-Konversion und CAC.  
- **Brand Awareness:** *Führend* z.B. Marken-Sichtbarkeit (Impressions, Share-of-Voice) oder organisches Suchvolumen; *nachgelagert* eine Markenbekanntheits-Umfrage oder Anteil an Neugeschäft. Im Improvado-Framework erscheint z.B. bei einer Markteinführung “Awareness”-Kampagne Website-Traffic und Share-of-Voice als Führungsindikatoren, gegenüber später gemessenen Lead-Zahlen und Lead-Kosten.

Analog lassen sich führende/nachgelagerte KPI-Paare auch nach **Launch-Typ** differenzieren:

- **Produktlaunch:** Siehe Kampagnentyp „Produkt-Launch“ oben (Websitebesuche, Testsignups vs. tatsächlicher Absatz).  
- **Feature-Release:** *Führend* häufig Nutzungsrate oder Aktivierungsquote neuer Feature (z.B. neue Anmeldungen auf Feature oder Öffnungsrate von Release-Emails); *nachgelagert* etwa erhöhte Produktnutzung, Upsell oder churn-senkende Effekte.  
- **Markterweiterung (Geografisch):** *Führend* z.B. Traffic und Anfragen aus Zielregionen; *nachgelagert* Umsatz/Anzahl Abschlüsse im neuen Markt. Im Beispiel einer EMEA-Markteinführung führt Improvado „Webseiten-Traffic aus EMEA“ und regionale Content-Engagement-Raten als Leading und EMEA-Leadvolumen sowie Kost per Lead als Lagging KPIs auf.  

Für alle Typen gilt: KPIs sollten immer klar definiert, quantitativ und auf ein Geschäftsziel bezogen sein. So liegt etwa im Shiny-Leitfaden ein KPI-Set „von Awareness bis Umsatz“ nahe (Engagement/CTR als Leading, Cost-per-Lead oder ROI als Lagging). 

## 2. Attribution ohne vollwertiges Analytics-Stack

**Last-Touch-Attribution** („Last Click“ etc.) ist simpel und oft für kleine Teams oder kurze Kampagnen ausreichend. Channel99 weist darauf hin, dass gerade Startups oder kleine Unternehmen ohne ausgefeilte Analytik meist mit Last-Touch arbeiten, weil es „ohne Doktortitel“ schnelle Antworten liefert. Sie zeigt, welcher Kanal zuletzt zum Abschluss geführt hat und beantwortet: *„Welches Angebot hat jemanden zum Handeln veranlasst?“*. Allerdings erfasst sie keine vorgelagerten Touchpoints; Channel99 warnt, sie nur „als Opportunitätsquelle“ zu nutzen und nicht allein für Budgetentscheidungen. 

**Multi-Touch-Attribution** erfordert dagegen umfangreiches Tracking (mehr Kanäle, Attributionstools). Sie verteilt die Erfolgs-Credits über mehrere Touchpoints. Sie ist besonders dann angebracht, wenn viele Berührungspunkte vorliegen und hohe Budgets ausgegeben werden. SegmentStream empfiehlt z.B. ab etwa \$100k/Monat Werbebudget mehrerer Kanäle den Einsatz von Multi-Touch, während bei kleineren Budgets auch First-Touch oder einfache Modelle ausreichen. Sprich: Bei geringem Budget kann ein erster Kontakt (“First Click”) Aufschluss geben, welchen Kanal neue Interessenten erzeugt, ohne komplexe MTA-Modelle. Ab einer gewissen Skalierung lohnt sich dann Behavioral-MTA.  

**Selbstberichtete Attribution** (z.B. im Leadformular „Wie haben Sie von uns erfahren?“) fängt vor allem Kanäle ab, die mit Tracking nicht erfassbar sind („Dark Funnel“). SegmentStream weist explizit darauf hin, dass eine Kombination mit dieser Methode sinnvoll ist, wenn nur Last- oder First-Touch genutzt wird: Ein klarer Nachteil einzelner Touch-Modelle ist, dass sie Offline- oder Brand-Marketing-Quellen nicht sehen können. Eine Selbstauskunft kann solche Lücken mindern. 

**Empfehlung bei fehlender Multi-Touch-Attribution:** Wenn ein Team keine komplexe Attribution durchführen kann, sollte es transparent kommunizieren, welches Modell genutzt wird (z.B. Last-Touch oder First-Touch) und dessen Grenzen anerkennen. Etwa: *„Wir verwenden Last-Touch-Reporting (wie alle Traffic-Quellen). Das zeigt uns, welcher Kanal Kunden zuletzt zum Abschluss führt, berücksichtigt aber nicht, welche früheren Interaktionen ebenfalls zum Lead beigetragen haben“*. In jedem Fall ist es klug, ergänzend qualitative Hinweise (z.B. Kundenbefragungen) einzuholen und intern klarzustellen, dass frühere Touchpoints möglicherweise übersehen werden.

## 3. Review-Taktiken: Häufigkeit der KPI-Prüfung

Während einer aktiven Kampagne oder Launch-Phase prüfen Teams Kennzahlen deutlich häufiger als in ruhigen Zeiten. Fachliteratur und Praxishandbücher schlagen vor, **während des Launch-„Fensters” mindestens wöchentliche, oft sogar tägliche Kontrollen** durchzuführen. So können bei „Early Signals“ (z.B. plötzlich sinkende Klick- oder Conversionraten) noch unmittelbar Anpassungen erfolgen. Shiny rät explizit: *„Review performance daily during launch: Early movement often shows whether to scale, revise, or stop.“*. 

Nach Abschluss des Launches bzw. in der **Steady-State-Phase** genügen dagegen lockerere Intervalle. Hier empfiehlt sich üblicherweise ein **monatlicher oder höchstens vierteljährlicher Report**. MightyRoar etwa warnt: „KPIs only work if you can measure them regelmäßig – monatlich mindestens“. Domo bestätigt, dass ein übliches Reporting-Dashboard etwa **monatlich oder vierteljährlich** aktualisiert wird. Diese geringere Frequenz hilft, langfristige Trends zu erkennen und vermeidet Überinterpretation kurzfristiger Schwankungen. Praktisch setzen viele Teams nach Ende der Launch-Phase einen **Monatsreport** als Standard – das schont Ressourcen und gibt gleichzeitig genug Sicht auf anhaltende Entwicklungen.

## 4. Falsifizierbare Erfolgsmetriken formulieren

Eine gut formulierte Erfolgsmetrik muss so präzise sein, dass man im Nachhinein eindeutig feststellen kann, ob das Ziel erreicht wurde. **Falsifizierbar** bedeutet hier: Ein messbares Ergebnis (Zahl, Prozentzahl o.Ä.) in einem bestimmten Zeitraum – statt einer vagen Floskel. Ein oft zitiertes Beispiel verdeutlicht den Unterschied: „*Markenbekanntheit erhöhen*“ ist vage und nicht prüfbar. Dagegen nennt Improvado als falsifizierbare Formulierung: „*Erreiche 15% ungestützte Markenbekanntheit in der Zielgruppe im nächsten Quartal*“ – hier sind Metrik (Awareness), Zielwert (15%) und Zeitraum (nächstes Quartal) klar definiert. Mit dieser Präzisierung kann man danach eindeutig sagen, ob das Ziel *getroffen oder verfehlt* wurde. 

Wichtige Kriterien solcher Metrik-Formulierungen sind **Spezifität und Messbarkeit** (z.B. in absoluten Zahlen oder Prozent und mit Zeitrahmen) – SMART-Kriterien (Spezifisch, Messbar, Erreichbar, Relevant, Terminiert) helfen dabei. Beispielsweise ist statt „Umsatz steigern“ ein Ziel wie „+10% Umsatz im Launch-Monat“ falsifizierbar. Je klarer das Ziel quantifiziert ist, desto eindeutiger fällt die Bewertung aus.

## 5. Häufige Fallen und deren Vermeidung

Beim Festlegen von Erfolgsmessungen treten oft folgende Fehler auf – erfahrene Teams verhindern sie so:

- **Vanity-Metriken**: Das sind Zahlen, die gut aussehen, aber kein wirkliches Geschäftsergebnis anzeigen (z.B. Follower-Zahlen, reine Seitenaufrufe, Likes). Tableau definiert Vanity-KPIs als „Kennzahlen, die zwar gut aussehen, aber keine verwertbaren Erkenntnisse liefern und nichts informieren, was an der Strategie angepasst werden könnte“. Solche Metriken verstellen die Sicht aufs Wesentliche. Erfahrene Teams hinterfragen daher jede Kennzahl mit der Frage: „Führt diese Zahl zu einer konkreten Entscheidung? Wenn nicht, ist sie wahrscheinlich nur Schall und Rauch“. Stattdessen konzentriert man sich auf *actionable metrics*, die mit dem Geschäftsziel verknüpft sind.  

- **Unmögliche Messgrößen**: Ziele, für die man keine Daten hat, bleiben Luftschlösser. Ein klassisches Beispiel ist ein jährlicher Marken-Tracker, der erst nach Kampagnenende ausgewertet wird – da ist es zu spät zum Handeln. MightyRoar mahnt: *„Wenn du die nötigen Daten für einen KPI nicht hast, musst du in die Datenerfassung investieren, statt einfach eine leicht messbare, aber irrelevante Größe zu wählen.“*. Kurz: Wähle nur Kennzahlen, die mittels vorhandener Tools oder angemessener Messverfahren zuverlässig erfasst werden können. Gelingt das nicht, sollte die Messinfrastruktur aufgebaut werden, bevor die Kampagne startet.  

- **Nicht verknüpft mit Geschäftszielen**: Ein KPI muss direkt zum übergeordneten Business-Goal passen. Ein häufiger Fehler ist, z.B. Traffic oder Impressionen zu fokussieren, obwohl das eigentliche Ziel Umsatzsteigerung oder Lead-Qualität ist. MightyRoar empfiehlt deshalb, beim Audit der bestehenden KPIs stets zu prüfen, ob sie „Fortschritt am Geschäftsziel messen“. Ist das nicht der Fall, wird der KPI durch einen relevanteren ersetzt (bspw. Konversionsrate statt Traffic, wenn es um Sales geht). Verknüpfe jeden KPI mit einer konkreten Aktivität oder einem Ergebnis, das dein Team kontrolliert. 

Teams vermeiden diese Fallen, indem sie sich strikt an SMART-Kriterien halten und die Team- und Geschäftsziele vorab klären. Gute Praxis ist auch, nur wenige (zwei bis drei) KPIs pro Ziel zu setzen, damit Fokus und Übersichtlichkeit gewahrt bleiben. Zudem sollten KPIs transparent definiert und dokumentiert sein (wie Improvado zeigt), damit jeder versteht, wie sie berechnet werden und was sie bedeuten. Regelmäßige Reviews (siehe Punkt 3) helfen schließlich, rechtzeitig zu erkennen, wenn ein KPI nutzlos oder fehlgeleitet ist, und ihn zu korrigieren.

**Quellen:** Autoren und Branchenexperten weisen auf die oben genannten Prinzipien hin. Die vollständigen Literaturhinweise findest du im Quellenverzeichnis. 

**Quellenverzeichnis (APA):**

- Beberwyck, A. (2025). *Analytics: Leading indicators provide early warning*. Smith & Jones. URL: https://smithandjones.com/resources/blog/analytics-leading-indicators-provide-early-warning  
- Sheldon, J. (2026). *Campaign Management: A Startup’s Guide to Driving Growth*. Shiny. URL: https://useshiny.com/blog/campaign-management/  
- Channel99. (2025). *The Pros and Cons of Last-Touch Attribution*. Channel99 Blog. URL: https://www.channel99.com/articles/the-pros-and-cons-of-last-touch-attribution  
- SegmentStream. (2026). *What Is Multi-Touch Attribution? Models, Benefits & Limitations*. SegmentStream. URL: https://segmentstream.com/glossary/multi-touch-attribution  
- Improvado. (2026). *How to Measure Marketing Performance: 7 Steps*. Improvado Blog. URL: https://improvado.io/blog/steps-to-measure-marketing-performance  
- Tableau Software. (o.D.). *Vanity Metrics: Definition, How To Identify Them, and Examples*. URL: https://www.tableau.com/learn/articles/vanity-metrics  
- MightyRoar. (2023). *How to Develop Marketing KPIs That Actually Matter*. URL: https://www.mightyroar.com/blog/develop-marketing-kpis  



---

## Claude (source: `measurement-framework-claude.md`)

# The Success-Metrics Step: A Repeatable KPI-Commitment Framework for Campaign and Launch Planning

## TL;DR
- **Commit to paired metrics before you spend a dollar:** every campaign and launch should name one *leading* indicator (an early, controllable signal you can move weekly) and one *lagging* outcome (the business result you'll be judged on), plus a numeric target, a baseline, a deadline, an owner, and a named measurement source. This single discipline is what converts a vague aspiration ("increase awareness") into a falsifiable commitment ("lift aided awareness among 25–44s from 18% to 30% by December, measured by quarterly survey").
- **Match your attribution honesty to your analytics maturity:** teams without a full multi-touch stack should default to last-touch for demand-capture channels plus a mandatory "How did you hear about us?" self-reported field for demand-creation channels — and must document the caveats (dark-social blind spots, recency bias, no incrementality proof) rather than pretend the numbers are causal.
- **Review on two clocks:** weekly during the active launch/campaign window (to catch and fix problems while they're cheap), then monthly/quarterly in steady state (to judge trends and outcomes). The failure modes to design against are vanity metrics, metrics you can't measure with the tools you own, and metrics disconnected from the business goal.

---

## 1. Leading vs. Lagging Metric Pairing by Campaign and Launch Type

**The core principle.** A leading indicator is an *input* — an early, controllable signal that predicts an outcome and can be influenced within the current cycle (qualified traffic, trial activation, stage conversion). A lagging indicator is an *output* — the end result, which is accurate but slow and no longer changeable once measured (revenue, churn, market share). The framework guidance is blunt: relying on lagging metrics alone creates a "reactive culture" where problems are discovered too late (CleverTap, 2023), while leading metrics allow earlier detection and course-correction (Umbrex, n.d.). The practitioner rule of thumb is to keep 3–8 metrics per level, pair every lagging KPI with 1–3 leading inputs, give each an owner, and document the "lead time" — the gap between a leading indicator moving and the lagging outcome responding (days for paid search, quarters for brand advertising) (Umbrex, n.d.; The Pedowitz Group, n.d.).

Below, each type gets a concrete leading/lagging pair that practitioners actually use.

### Campaign types

| Campaign type | Leading indicator (early, controllable) | Lagging outcome (business result) |
|---|---|---|
| **Product-launch campaign** | Trial sign-ups / demo requests per week; landing-page conversion rate | New-customer revenue / paid conversions; competitive win rate |
| **Thought-leadership** | Content engagement (scroll depth, time on page), branded search volume, backlinks earned | Marketing-influenced pipeline / qualified inbound leads attributed to the content; share of voice |
| **Seasonal promotion** | Redemption/click rate on the offer, add-to-cart rate, daily ROAS during the window | Incremental revenue (iROAS vs. a holdout), margin after discount |
| **Retention** | Product/feature adoption rate, weekly active users, time-to-first-value, NPS | Churn rate / renewal rate; net revenue retention (NRR) |
| **Lead-generation** | MQL volume, cost per lead, MQL→SQL conversion rate | SQL→opportunity and opportunity→close rates; marketing-sourced pipeline and CAC |
| **Brand-awareness** | Reach/impressions to *new* audiences, branded search growth, direct-traffic trend | Aided/unaided brand recall (survey); share of voice vs. competitors |

Notes practitioners rely on: For **thought leadership**, gains compound over time and traditional attribution works poorly — content often doesn't rank well and high social engagement rarely produces a clean traffic spike — so the leading indicators carry most of the in-flight signal (Ten Speed, n.d.). For **retention**, churn is the classic slow lagging metric — by the time an account shows as churned, the leading indicators (declining usage frequency, dropping feature-adoption breadth, zero new activations) had been warning you for weeks; fix the leading indicators, not the lagging number (Userpilot, 2026). For **seasonal promotion**, be careful: a campaign running alongside a discount captures promotion-driven lift and reports it as media ROAS, so the honest lagging metric is *incremental* revenue measured against a control, not blended ROAS (LiftLab, n.d.; Circana, n.d.).

### Launch types

| Launch type | Leading indicator | Lagging outcome |
|---|---|---|
| **Product-launch (new product / GTM)** | Trials started, visitor-to-trial sign-up rate, demos requested, leads generated | Monthly product revenue, retention at 7/30/90 days, market share, competitive win rate |
| **Feature-release** | Feature-adoption funnel (exposed → activated → used → used-again), time-to-adopt, activation rate | 30-/90-day feature retention; impact on overall churn/expansion (NRR); expansion revenue |
| **Market-expansion** | New-customer acquisition in the new segment/geography, CAC in-market, brand awareness/website traffic from the new market | Market penetration/share captured, revenue growth and profitability in-market, LTV:CAC, NRR of the new cohort |

For **feature-releases**, the four-stage adoption funnel (Exposed → Activated → Used → Used Again) is the practitioner-standard diagnostic: each stage has its own drop-off, and a healthy product tends to see 50–70% conversion at each step, with anything below ~30% at a single stage flagging where to intervene (Feeqd, n.d.; Appcues, n.d.). Feature adoption is itself one of the strongest leading indicators of net revenue retention (Appcues, n.d.). For **market-expansion**, NRR of the newly-acquired cohort is the single most predictive lagging metric of whether the entry actually "stuck," and CAC-versus-LTV tells you if you acquired profitably (Brand Quarterly, n.d.; Factors.ai, n.d.).

A useful mental model for laddering these signals is Dave McClure's **Pirate Metrics (AARRR)** — Acquisition, Activation, Retention, Referral, Revenue — which maps naturally onto the leading-to-lagging chain: acquisition and activation are your leading signals, retention and revenue your lagging outcomes (McClure, 2007).

---

## 2. Attribution Model Tradeoffs for Teams Without a Full Analytics Stack

Attribution is not a reporting preference; it is a decision system that controls where budget goes (Symphonic Digital, n.d.). The three approaches a lean team will realistically choose among:

### Last-touch (last-click)
- **What it does:** assigns 100% of credit to the final touchpoint before conversion.
- **When appropriate:** short, simple, demand-*capture* journeys; e-commerce and direct-response where the final click is genuinely decisive; and any team needing fast, tactical feedback ("yesterday's email performance this morning") (Prescient AI, n.d.). It is the default for most organizations because of its clarity and simplicity (ACM, n.d.).
- **Weakness:** it systematically undervalues awareness-building and top-of-funnel channels and over-credits end-of-funnel tactics, which distorts strategy toward demand capture (ACM, n.d.). B2B buyer journeys are long and multi-touch — Dreamdata's analysis found a B2B customer averages roughly 62 touchpoints over about six months before purchase (Upvise, n.d.) — so a single-touch model ignores almost the entire journey.

### Multi-touch (MTA)
- **What it does:** distributes credit across multiple touchpoints (linear, time-decay, position-based/U-shaped ≈ 40/40/20, W-shaped, or data-driven).
- **When appropriate:** longer, multi-channel B2B journeys where you need to defend budget for mid-funnel tactics — *if* you have the stack to support it. It requires unified cross-channel tracking, consistent identifiers (increasingly hard under privacy regulation), and models that handle incomplete data (Prescient AI, n.d.).
- **Reality check for lean teams:** the common practitioner guidance is that if your average deal size is under ~$15k and your team is under ~10 people, you should skip multi-touch attribution software entirely — a self-reported field plus basic UTM tracking gives most of the insight at a fraction of the cost (Prospeo, n.d.). Multi-touch also "breaks down when buyers research offline or in private channels," and marketing-mix modeling needs years of clean data and volumes B2B rarely has (Prospeo, n.d.).

### Self-reported attribution (SRA / "How did you hear about us?")
- **What it does:** asks the buyer directly, usually via a mandatory open-text field on a high-intent form (demo request, contact sales, checkout).
- **When appropriate:** to capture "dark social" and demand-*creation* channels (word of mouth, podcasts, communities, Slack, referrals) that software attribution is structurally blind to. It is near-zero cost to implement and, per Refine Labs' widely-cited framework, best used *alongside* software attribution as a "hybrid" model rather than as a replacement (Refine Labs, 2024; Blend B2B, n.d.).
- **Best practices:** make it a mandatory, open-text field — not a drop-down, which anchors answers to channels you already know; phrase it "How did you *originally* hear about us?" to anchor on first awareness; and put it only on high-intent forms, not newsletter sign-ups (A88 Lab, n.d.; Prospeo, n.d.).

### What a lean team should DOCUMENT when it can't run proper multi-touch

Write these caveats directly into the campaign/launch plan and every readout:

1. **State the model in use and its known bias.** e.g., "We report last-touch; this over-credits demand-capture channels (branded search, retargeting) and under-credits demand-creation channels (content, podcast, word of mouth)."
2. **Flag the dark-social blind spot.** Software attribution mislabels dark-social traffic as "direct." A 2023 SparkToro study (1,113 visits, 11 networks) found "100% of all visits from TikTok, Slack, Discord, Mastodon, and WhatsApp were marked as 'direct,' and contained no other referral information" (Fishkin, 2023). Refine Labs' 12-month "Attribution Mirage" study of 620 declared-intent conversions and $21.5M closed-won ARR found a 90% measurement gap: software attributed 78% of conversions to web search, while customers self-reported web search only 12% of the time; podcasts drove a self-reported 53% of revenue ($11.4M closed-won) but 0% by software attribution (Refine Labs, 2024).
3. **Disclose self-reported data's limits.** Recency bias (buyers recall the most recent or memorable touch, not the first); difficulty tying answers to a specific campaign/ad; skew toward emotional/memorable channels. Basing strategy *solely* on SRA is as dangerous as relying solely on last-touch (Recast, n.d.; Blend B2B, n.d.).
4. **Distinguish correlation from causation.** State plainly that attribution assigns *credit*; it does not prove *incrementality*. Where a decision is high-stakes, note that only a holdout/geo test or MMM can establish causal lift — platform-reported ROAS routinely overstates true iROAS (Measured, n.d.; Prescient AI, n.d.).
5. **Document definitions and windows.** Attribution window (e.g., 28-day click / 1-day view), what counts as a "conversion," time-zone, and dedup rules — because each platform counts differently (Fairing, n.d.; Fluence Flow, n.d.).

---

## 3. Review-Cadence Conventions: Active Window vs. Steady State

The consensus practitioner rhythm is a **three-tiered cadence**, and the reason the frequency differs is decision latency: the faster money can be wasted or a problem can compound, the more frequently you must inspect (Nine, n.d.; Startups.com, n.d.).

- **Daily** — only during high-spend paid launches, for anomaly-catching (a broken link, a sudden traffic drop, runaway CPA). These live as real-time dashboards, not formal meetings (NetSuite, n.d.).
- **Weekly (the active launch/campaign window)** — the core operating cadence. Review *leading* indicators and exceptions, and commit actions (budget shifts, creative swaps, audience changes). The rationale: monthly reviews are too slow — paid media can waste budget in days, and email/engagement declines precede conversion problems (FineReport, n.d.). A weekly review should output a decision, not a data dump; every KPI needs a trigger threshold, a decision owner, and a playbook for green/yellow/red states (Nine, n.d.).
- **Monthly (steady state / post-launch)** — evaluate trends and channel-mix decisions, and reconcile *lagging* metrics (revenue, CAC, retention) with Finance. This is where you judge "what's working" rather than "what's on fire" (Nine, n.d.; The Pedowitz Group, n.d.).
- **Quarterly** — strategic resets, bigger bets, guardrails, and board-level lagging metrics (NRR, Rule of 40, market share) (Morning Report, n.d.; Factors.ai, n.d.).

The general convention practitioners state: **weekly for leading KPIs, monthly for lagging KPIs, quarterly for strategy** (The Pedowitz Group, n.d.). During a launch you compress toward weekly (even daily) because the window is short, the spend is concentrated, and early feedback can still change the outcome; in steady state you widen to monthly/quarterly because you are measuring slow-moving outcomes and over-frequent inspection of strategic metrics just creates noise (Startups.com, n.d.). Survey-based brand metrics (aided/unaided awareness) are the exception — measure them quarterly or biannually, since they don't move meaningfully week to week and re-surveying too often wastes budget (ALM Corp, n.d.). Gartner has found that marketing leaders who met regularly with analytics teams were far more likely to prove marketing's value than those who didn't — the underlying case for holding the cadence (Fluence Flow, n.d.).

**A caution seen in practice:** the two failure modes of cadence are (a) waiting for monthly decks to discuss performance (you're behind before you begin) and (b) weekly meetings that rehash data but produce no changes (you're just busy) (Nine, n.d.). Set the rhythm, attach an action to every exception, and hold it consistently.

---

## 4. What Makes a Success Metric "Falsifiable" Before the Fact

A success metric is falsifiable when, before the campaign runs, you can describe exactly what result would count as hit, missed, or inconclusive — so the post-campaign review is a lookup, not a debate. Peter Drucker's management-by-objectives principle underpins it: if you cannot measure it, you cannot manage it (Advergize, n.d.). The operational test combines the SMART framework — originated in George T. Doran's 1981 paper and now standard in marketing planning (Smart Insights, n.d.) — with practitioner criteria for a "good metric."

### Criteria for a falsifiable, well-formed metric

1. **Specific and singular** — one clearly defined variable, not a bundle. Specify *what* is being measured and for *whom* (segment) (Agile Sherpas, n.d.).
2. **Has a baseline and a target** — "every objective needs a baseline (where you are now) and a target (where you need to be)" (Advergize, n.d.). Without a baseline, "improved" is unfalsifiable.
3. **Time-bound** — a deadline. "An objective without a deadline is a dream" (Advergize, n.d.).
4. **Measurable with a named source** — you can put a specific dashboard, report, or survey behind it. If you can't, rewrite it (Advergize, n.d.).
5. **Relevant / laddered to a business goal** — it must pass the "so-what test": if we hit this, does the company make more money or gain share? A metric can be specific and measurable yet still be the *wrong* metric (e.g., "gain 10,000 TikTok followers" when your buyers are procurement managers who don't use TikTok) (Media Monkey Marketing, n.d.).
6. **Comparative, understandable, and preferably a ratio/rate** — Croll and Yoskovitz's criteria for a "good metric": it should let you compare across time/segments/competitors, be simple enough to remember and discuss, and ideally be a rate or ratio (which are more actionable than raw counts). Their capstone criterion: *"a good metric changes the way you behave"* (Croll & Yoskovitz, 2013).
7. **Actionable, accessible, and auditable** — Eric Ries's "three A's": the metric must show clear cause and effect (actionable), be understandable by the people who use it (accessible), and be traceable back to credible source data (auditable) (Ries, 2011).

### Well-formed vs. poorly-formed statements

| Poorly-formed (not falsifiable) | Well-formed (falsifiable) |
|---|---|
| "Increase awareness." | "Increase unaided brand awareness among US adults 25–44 from 18% to 30% by December 2026, measured by our quarterly brand-tracking survey." |
| "Get more leads." | "Increase SQLs by 15% in 90 days." |
| "Improve landing-page performance." | "Increase landing-page form-completion rate from 2.8% to 3.6% by June 30." |
| "Grow social engagement." | "Increase Instagram saves by 25% by end of Q2." |
| "Improve conversion rate." | "Improve conversion rate by 0.6% by end of Q2." |
| "Make the launch successful." | "Achieve 28% feature-adoption (used-at-least-once) among eligible users within 30 days of release." |

The tell for a poorly-formed metric: it lacks a number, a date, or both — "if your objective could appear on a motivational poster, it is a goal, not an objective. Rewrite it with a number and a date" (Advergize, n.d.). A subtler failure is being falsifiable but disconnected: "improve CTR by 15% across all landing pages" is measurable, but if the business problem is retention, you're just pushing more people into a leaking bucket (Agile Sherpas, n.d.).

Set the pass/fail threshold *in advance*, and pre-define what "inconclusive" looks like — e.g., a result inside the noise band of your measurement method (for incrementality tests, a lift estimate whose confidence interval crosses zero is inconclusive, not a miss) (Measured, n.d.).

---

## 5. Common Failure Modes When Setting Success Metrics Upfront

### Failure mode 1: Vanity metrics
Numbers that look impressive but don't inform a decision or connect to the bottom line — page views, impressions, total followers, total registered users, total downloads. The diagnostic question, rooted in Eric Ries's actionable-versus-vanity distinction in *The Lean Startup*, is *"Can this metric lead to a course of action or inform a decision?"* If the answer is no, it's a vanity metric (Ries, 2011; Tableau, n.d.). The classic tell: "10,000 registered accounts" is hollow if only 100 are monthly actives (Tableau, n.d.). **How experienced teams avoid it:** replace the count with a rate or ratio tied to behavior — page views → conversion/download rate; total sign-ups → activation rate and CAC; total customers → retention rate and CLTV (Userpilot, n.d.; Mailchimp, n.d.). Remember that *any* metric can become a vanity metric if it isn't tied to a decision, and even revenue can be a vanity metric on launch day if it isn't decomposed into *why* (Tableau, n.d.; Viral Loops, n.d.).

### Failure mode 2: Metrics you can't measure with the tools you have
Committing to a KPI the team has no instrument to capture — e.g., promising "multi-touch pipeline attribution" with only Google Analytics and a spreadsheet, or a thought-leadership KPI that assumes clean content attribution the stack can't produce. **How experienced teams avoid it:** during the planning step, require a named data source for every metric before it's approved; if the source doesn't exist, either instrument it first ("set up tracking" becomes the first goal) or pick a measurable proxy (Metricool, n.d.). Confirm the measurement method and cadence *before* launch, because "after-the-fact analysis is almost impossible" without it (UserVoice, n.d.). Store more raw data than you report so you can reconstruct metrics later, but don't over-invest in dashboards before you know what's worth tracking (UserVoice, n.d.).

### Failure mode 3: Metrics disconnected from the business goal
The metric moves but the business doesn't — the "activity for its own sake" trap. A HubSpot *State of Marketing* report found that only 36% of marketers set measurable objectives tied to specific business outcomes; the rest chase activity (Advergize, n.d.). This is also where misaligned cross-functional metrics create friction — marketing celebrates impressions while the CFO counts closed deals (B2B Drum, n.d.). **How experienced teams avoid it:** build an explicit KPI *tree* — Business outcome → Primary KPIs → Leading indicators/diagnostics → Guardrails — so every tracked number ladders to revenue, pipeline, retention, or share (Morning Report, n.d.). Run each proposed metric through the "so-what test." Assign one owner per metric. Cap the set at 3–5 KPIs per goal or channel — a report with 40 metrics "signals a lack of strategic clarity" (Fluence Flow, n.d.). And set **guardrail metrics** — limits you won't cross (CAC ceiling, minimum ROAS, frequency cap) — so optimizing one KPI doesn't quietly damage another (the "squeeze-toy effect" Croll and Yoskovitz warn about with a single dominant metric) (Croll & Yoskovitz, 2013).

### Cross-cutting discipline: the "One Metric That Matters"
To combat metric overload, Croll and Yoskovitz recommend identifying the **One Metric That Matters (OMTM)** for the current stage — "a single metric that's incredibly important for the step you're currently working through" (Croll & Yoskovitz, 2013). For a launch that's often activation or adoption; for a retention campaign it's churn/NRR; for lead-gen it's MQL→SQL conversion. The OMTM focuses the weekly review while the paired leading/lagging set and guardrails keep the wider picture honest.

---

## Recommendations: A Staged "Success-Metrics" Step to Bolt Onto Both Processes

**Stage 1 — At plan kickoff (before any creative or spend):**
1. Write the **business goal** the campaign/launch ladders to, in one sentence.
2. Name the **OMTM** for this effort's stage.
3. Define **one leading + one lagging pair** using the type-specific tables above.
4. For each metric, record: **baseline, target, deadline, data source, owner.** If any cell is blank, the metric isn't ready.
5. Run every metric through the **falsifiability checklist** (§4) and the **so-what test.** Kill or rewrite anything that fails.
6. Set **guardrail metrics** (CAC ceiling, minimum iROAS, frequency cap).

**Stage 2 — Lock the measurement method:**
7. Declare the **attribution model** and write its **caveats** (§2) into the plan. Add a mandatory open-text "How did you *originally* hear about us?" field to high-intent forms.
8. Confirm each **data source actually exists**; if not, instrumenting it is the first task.
9. Set the **review cadence**: weekly (leading, in-window) → monthly (lagging, steady state) → quarterly (strategy); attach a trigger, owner, and playbook to each KPI.

**Stage 3 — In-flight and post-mortem:**
10. Hold the weekly review; every exception produces a logged decision (date, options, decision, owner, review date).
11. At close, judge each metric **hit / missed / inconclusive** against the pre-committed thresholds, and feed the read-back into the next planning cycle.

**Benchmarks that should change your approach:**
- If deal size < ~$15k and team < ~10 people → **do not** buy multi-touch attribution software; use last-touch + SRA + UTMs.
- If a single-stage adoption-funnel conversion drops below ~30% → treat as a red flag and diagnose that stage.
- If leading indicators look strong but the lagging outcome misses → revisit driver quality (ICP fit, pricing, product readiness, stage definitions) and validate with a holdout/incrementality test rather than assuming the leading metric was wrong.
- If your report exceeds ~5 KPIs per goal → cut it; metric overload signals missing strategic choices.

---

## Caveats
- **Benchmarks are directional, not laws.** Figures such as "24.5% average core-feature adoption," "~31% average lead-to-MQL," or "28% feature engagement" come from vendor/agency datasets and vary widely by industry, motion, and deal size; use your own historical baselines to set targets.
- **Attribution is credit, not causation.** Every model in §2 assigns credit; none proves incremental lift. Treat all attributed ROAS as an upper bound and validate high-stakes decisions with holdout/geo tests or MMM where feasible.
- **Some sources are vendor content.** Much practitioner writing on these topics is published by tool vendors and agencies with a commercial interest (attribution platforms, survey tools, dashboards). The frameworks cited (SMART, Lean Analytics, Lean Startup, AARRR, leading/lagging) are well-established, but specific statistics from vendor blogs should be corroborated before they anchor a target.
- **The Refine Labs "90% gap" study** is a single 12-month dataset (620 conversions, one agency's client base, B2B SaaS); its magnitude is context-specific and should not be treated as a universal constant, even though the *direction* (software under-counts dark social) is broadly corroborated by independent work such as SparkToro's dark-social study.
- **This framework assumes a lean stack by design.** Teams with mature identity resolution and data-science capacity can and should layer in data-driven attribution and continuous incrementality/MMM; the guidance here is calibrated to teams that cannot.

---

## Sources (APA)

A88 Lab. (n.d.). *Self-reported attribution for B2B SaaS: How to capture what software can't track.* https://www.a88lab.com/blog/self-reported-attribution-b2b-saas

Advergize. (n.d.). *Marketing objectives: 10 SMART examples that actually drive results.* https://www.advergize.com/marketing-objectives-examples/

Agile Sherpas. (n.d.). *Are your marketing objectives setting you up to fail?* https://www.agilesherpas.com/blog/marketing-objectives-examples

ALM Corp. (n.d.). *How to measure brand awareness: 12 metrics, survey questions, and a practical dashboard.* https://almcorp.com/blog/how-to-measure-brand-awareness/

Appcues. (n.d.). *A guide to feature adoption: Metrics, funnel & how to improve.* https://www.appcues.com/blog/a-guide-to-feature-adoption

Association for Computing Machinery. (n.d.). *A practical guide to last-touch and multi-touch attribution.* Communications of the ACM. https://cacm.acm.org/blogcacm/a-practical-guide-to-last-touch-and-multi-touch-attribution/

B2B Drum. (n.d.). *Vanity metrics vs. actionable metrics.* https://www.b2bdrum.com/blog/why-vanity-metrics-are-killing-b2b-growth

Blend B2B. (n.d.). *Self-reported attribution: What it is & why you need it.* https://www.blendb2b.com/blog/self-reported-attribution

Brand Quarterly. (n.d.). *GTM KPIs: How to measure market entry success.* https://brandquarterly.com/gtm-kpis-how-to-measure-market-entry-success/

Circana. (n.d.). *How to measure advertising effectiveness: Sales lift & ROAS.* https://www.circana.com/post/how-to-measure-advertising-effectiveness-sales-lift-roas

CleverTap. (2023). *Leading vs. lagging indicators: Explained with examples.* https://clevertap.com/blog/leading-vs-lagging-indicators/

Croll, A., & Yoskovitz, B. (2013). *Lean analytics: Use data to build a better startup faster.* O'Reilly Media.

Factors.ai. (n.d.). *GTM metrics: 10 go-to-market KPIs B2B teams track in 2026.* https://www.factors.ai/blog/gtm-metrics

Fairing. (n.d.). *What is marketing attribution?* https://fairing.co/resources/measurement-faqs/what-is-marketing-attribution

Feeqd. (n.d.). *Feature adoption: Metrics, benchmarks, and how to improve it.* https://feeqd.com/blog/feature-adoption

Fishkin, R. (2023). *We finally have proof that "dark traffic" is real and large* [SparkToro study]. SparkToro. https://sparktoro.com/

Fluence Flow. (n.d.). *Digital marketing reporting: The ultimate guide.* https://feeds.fluenceflow.io/blog/digital-marketing-reporting

FineReport. (n.d.). *Marketing weekly report guide: Structure, KPIs, and best practices.* https://www.fanruan.com/en/blog/marketing-weekly-report

LiftLab. (n.d.). *Trade promotion ROAS: Why promotions inflate media performance.* https://liftlab.com/blog/trade-promotion-media-roas-attribution/

Mailchimp. (n.d.). *What are vanity metrics?* https://mailchimp.com/resources/vanity-metrics/

McClure, D. (2007). *Startup metrics for pirates (AARRR!)* [Presentation]. 500 Startups / Master of 500 Hats.

Measured. (n.d.). *Incremental lift analysis: A practical guide to lift, iROAS, and confidence intervals.* https://www.measured.com/faq/incremental-lift-analysis-practical-guide-iroas-confidence-intervals/

Media Monkey Marketing. (n.d.). *Stop guessing: A guide to setting SMART marketing goals.* https://mediamonkeymarketing.com/stop-wasting-budget-the-marketers-guide-to-smart-goals/

Metricool. (n.d.). *SMART goals for digital marketing: Examples and templates.* https://www.womenconquerbiz.com/examples-of-smart-goals-in-digital-marketing/

Morning Report. (n.d.). *Marketing KPI framework: Metrics that actually drive revenue.* https://morningreport.io/blog-posts/marketing-kpi-framework

NetSuite. (n.d.). *Marketing reporting: A comprehensive guide for building stellar reports.* https://www.netsuite.com/portal/resource/articles/erp/marketing-reporting.shtml

Nine. (n.d.). *Weekly marketing cadence: Streamlining marketing decisions.* https://www.nine.am/insights/building-a-weekly-marketing-cadence

The Pedowitz Group. (n.d.). *What are leading vs lagging indicators in marketing?* https://www.pedowitzgroup.com/what-are-leading-vs-lagging-indicators-in-marketing

Prescient AI. (n.d.). *Last-touch vs multi-touch attribution.* https://prescientai.com/blog/last-touch-vs-multi-touch-attribution

Prospeo. (n.d.). *Self-reported attribution: 2026 guide.* https://prospeo.io/s/self-reported-attribution

Recast. (n.d.). *"How did you hear about us?" survey and the limitations of self-reported attribution.* https://getrecast.com/hdyhau/

Refine Labs. (2024). *The attribution mirage.* https://www.refinelabs.com/article/attribution-mirage

Ries, E. (2011). *The lean startup: How today's entrepreneurs use continuous innovation to create radically successful businesses.* Crown Business.

Smart Insights. (n.d.). *How to define SMART marketing objectives (with example RACE KPIs).* https://www.smartinsights.com/goal-setting-evaluation/goals-kpis/define-smart-marketing-objectives/

Startups.com. (n.d.). *Reporting cadence: The operational rhythm of metric review.* https://www.startups.com/lexicon/reporting-cadence

Symphonic Digital. (n.d.). *Marketing attribution models: Single-touch vs multi-touch.* https://www.symphonicdigital.com/blog/single-touch-vs-multi-touch-attribution

Tableau. (n.d.). *Vanity metrics: Definition, how to identify them, and examples.* https://www.tableau.com/learn/articles/vanity-metrics

Ten Speed. (n.d.). *How to measure thought leadership: 9 metrics to gauge success.* https://www.tenspeed.io/blog/how-to-measure-thought-leadership

Umbrex. (n.d.). *Leading vs lagging indicators framework.* https://umbrex.com/resources/frameworks/marketing-frameworks/leading-vs-lagging-indicators-framework/

Upvise. (n.d.). *How many touchpoints does a B2B customer make before a purchase?* https://www.upvise.com/

UserVoice. (n.d.). *How to measure product launch success.* https://www.uservoice.com/blog/measure-product-launch-success

Userpilot. (n.d.). *Vanity metrics vs actionable metrics: What's the difference and what to track in SaaS?* https://userpilot.com/blog/vanity-metrics-vs-actionable-metrics-saas/

Userpilot. (2026). *User adoption metrics in 2026: Humans vs. AI agents.* https://userpilot.com/blog/user-adoption-metrics/

Viral Loops. (n.d.). *How to measure product launch success: 10 KPIs beyond revenue.* https://viral-loops.com/blog/how-to-measure-product-launch-success/

---

## Consensus (source: `measurement-framework-consensus.md`)

# Umfassender **KPI-** und **Attributions**-Rahmen

Die Literatur stützt einen wiederholbaren **Pre-Launch-Messrahmen**, der KPIs an Geschäftsziele koppelt, wenige strategisch relevante Kennzahlen priorisiert und Leading- mit Lagging-Indikatoren verbindet (Kufile et al., 2022; Rădulică, 2024). Für Ihre fünf Teilfragen zeigt die Evidenz vor allem Muster zu KPI-Paaren, Attributionsgrenzen bei geringer Datenreife, häufigerer Prüfung in aktiven Launch-Fenstern sowie typische Fehler bei unscharfen oder nicht messbaren Erfolgsdefinitionen (Kufile et al., 2022; Rădulică, 2024; Bucko et al., 2025).

## 1. Leading- und Lagging-Metriken

Leading- und Lagging-KPIs sollten **funnel-stufig** gepaart werden, weil Marketingmetriken entlang Awareness, Consideration, Conversion und Loyalty unterschiedlich früh oder spät auf Zielerreichung reagieren (Kufile et al., 2022; Sangwa & Sangwan, 2018). Die Quellen nennen keine universelle Standardliste je Kampagnentyp, aber sie zeigen konsistent, dass KPI-Auswahl vom Kampagnenziel, Kanal, Zielgruppe und Entscheidungskontext abhängt (Rădulică, 2024; Khimich, 2021; Mintz et al., 2020).

**KPI-Paare nach Kampagnentyp**

| Typ                | Führender Indikator                        | Nachlaufender Indikator                     | Begründung                                                                                                                           |
| ------------------ | ------------------------------------------ | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Produkt-Launch     | **Wiederholte Besuche** / Session Duration | **Umsatzproduktivität** / Sales             | Frühere Intent-Signale gehen späteren Performance-Outcomes voraus (Kufile et al., 2022; Nathan & Rosso, 2021)                        |
| Thought Leadership | **Engagement** mit Inhalten                | **Empfehlungsbereitschaft** / Markenwirkung | Customer-mindset-Metriken sind für Entscheidungen oft wirksamer als rein finanzielle Ziele (Kufile et al., 2022; Mintz et al., 2020) |
| Seasonal Promotion | **Display- plus Search-Interaktion**       | **Conversion-Uplift** / ROI                 | Saisonale Verzerrung macht frühe Kanalinteraktion wichtig, weil Last-Click Bottom-Funnel übergewichtet (Verma, 2025)                 |
| Retention          | **Repeat Visits**                          | **CLV** / langfristige Profitabilität       | Loyalitätsnahe Verhaltenssignale sind frühe Proxys für spätere Wertrealisierung (Kufile et al., 2022)                                |
| Lead Generation    | **Conversion Rate** auf Formulare          | **Anzahl Kontakte** / CPL-Effizienz         | Die Kampagnenliteratur nennt CR, CPL und Kontaktzahl als Standardmetriken für Leadziele (Khimich, 2021)                              |
| Brand Awareness    | **Reach / Coverage** / CPM                 | **Brand Recognition** / Awareness           | Awareness-Kampagnen werden mit Reichweite und Recognition-nahen Outcomes verknüpft (Khimich, 2021)                                   |

**Figure 1:** Beispielhafte Leading-/Lagging-Paare nach Kampagnentyp.

**KPI-Paare nach Launch-Typ**

| Typ             | Führender Indikator                      | Nachlaufender Indikator                          | Begründung                                                                                                              |
| --------------- | ---------------------------------------- | ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| Produkt-Launch  | **Launch-Aktivität** / frühe Interaktion | **Leistung des Launches** / Revenue Productivity | Launches hängen mit späterer Performance zusammen, besonders bei hochwertigen Einführungen (Nathan & Rosso, 2021)       |
| Feature-Release | **Nutzungssignale** / Seiten pro Besuch  | **Conversion** / Adoption-Effekt                 | Web-Interaktionen dienen als frühe Proxys für spätere Verhaltensänderung (Kufile et al., 2022; Gubela & Lessmann, 2021) |
| Markt-Expansion | **Target Coverage** / Geography-Reach    | **Neukunden** / Sales                            | Frühe Reichweite in Zielregionen wird gegen spätere Kunden- und Verkaufsziele gespiegelt (Khimich, 2021)                |

**Figure 2:** Beispielhafte Leading-/Lagging-Paare nach Launch-Typ.

## 2. Attributionsmodelle

Für Teams ohne vollständigen Analytics-Stack ist der zentrale Trade-off **Einfachheit gegen Genauigkeit** (Verma, 2025; Bucko et al., 2025). Last-Touch ist leicht umsetzbar, verzerrt aber oft kanalübergreifende Wirkung, besonders wenn Display, Search, Nurture und saisonale Effekte zusammenspielen (Berman, 2018; Verma, 2025).

| Modell                        | Wann passend                          | Hauptvorteil                                                                                             | Hauptnachteil                                                                       | Was explizit gesagt werden sollte                                                          |
| ----------------------------- | ------------------------------------- | -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Last-Touch**                | Einfache Journeys, geringe Tool-Reife | Niedrige Implementierungskomplexität (Verma, 2025)                                                       | Unterbewertet frühe und mittlere Touchpoints (Duggirala, 2026; Verma, 2025)         | „Berichtet **Conversion Credit**, nicht kausalen Inkrementaleffekt.“                       |
| **Multi-Touch**               | Mehrkanalige, längere Journeys        | Erfasst Interaktionen und Synergien besser (Kufile et al., 2022; Verma, 2025; Seth & Ramakrishnan, 2025) | Höhere technische und organisatorische Hürde (Kufile et al., 2022; Duggirala, 2026) | „Zeigt **Marketing-Einfluss** entlang der Journey, mit modellbasierten Annahmen.“          |
| **Self-Reported Attribution** | Wenn Tracking unvollständig ist       | Fängt nicht getrackte Quellen und Offline-Einflüsse ein                                                  | Stark von Selbstauskunft und Erinnerung abhängig (Akbar et al., 2023)               | „Beruht auf **Selbstauskunft** und ergänzt, ersetzt aber keine kanalbasierte Attribution.“ |

**Figure 3:** Trade-offs der Attributionsmodelle für Teams mit begrenzter Analytics-Infrastruktur.

Wenn kein belastbares Multi-Touch möglich ist, sollte ein Team die **Messgrenzen vorab** dokumentieren: verwendetes Modell, erfasste Kanäle, ausgeschlossene Touchpoints, Identitäts- und Offline-Lücken sowie dass die Kennzahlen Budgetentscheidungen unterstützen, aber keine vollständige kausale Wahrheit darstellen (Kufile et al., 2022; Duggirala, 2026).

## 3. Review-Kadenz

Die Evidenz beschreibt keine starre universelle Marketing-Taktung, aber sie unterstützt **häufigere Reviews in dynamischen Phasen** und periodische Überprüfung der Relevanz von SMART-Zielen (Rădulică, 2024; Umoren et al., 2021). Während aktiver Launches ist engmaschiges Prüfen sinnvoll, weil traditionelle Lagging-KPIs zu spät reagieren und frühe Verhaltenssignale reale Kurskorrekturen erlauben (Umoren et al., 2021; Trigos & Aldana, 2023).

- **Während Launch/Kampagne:** wöchentlich, bei bezahlten Digital-Kanälen oft zusätzlich täglich für Auslieferung, Spend und Conversion-Signale (Redwan et al., 2025; Umoren et al., 2021).
- **Direkt nach Launch:** zwei- bis vierwöchentlich für Stabilisierung, weil erste Steady-State-Muster erst nach initialer Volatilität erkennbar werden (Trigos & Aldana, 2023).
- **Steady State:** monatlich oder quartalsweise für strategische KPIs, weil dann Relevanz, Alignment und Langfristwirkung wichtiger werden als Tagessteuerung (Saura et al., 2017; Rădulică, 2024).

## 4. Falsifizierbare Erfolgsmetriken

Eine Erfolgsmetrik ist vorab **falsifizierbar**, wenn sie spezifisch definiert, messbar, zeitgebunden und direkt mit dem beabsichtigten Geschäftsergebnis verknüpft ist (Kufile et al., 2022; Katsikeas et al., 2016). Vage Formulierungen scheitern oft daran, dass Performance-Konstrukte in der Marketingliteratur häufig schlecht definiert oder zwischen Studien nicht vergleichbar sind (Katsikeas et al., 2016).

| Schwach formuliert     | Falsifizierbar formuliert                                                                           | Warum besser                                                                           |
| ---------------------- | --------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| „Awareness steigern“   | „Unaided awareness in Zielsegment X steigt bis Ende Q3 von A auf B“                                 | Klares Konstrukt, Population und Zeitfenster (Kufile et al., 2022; Mintz et al., 2020) |
| „Mehr Leads erzeugen“  | „Landingpage-CR erreicht ≥X% und erzeugt Y marketingqualifizierte Leads bei CPL ≤Z im Launch-Monat“ | Verknüpft Früh- und Endergebnis mit Schwellenwerten (Khimich, 2021; Rădulică, 2024)    |
| „Retention verbessern“ | „Repeat-visit-Rate steigt in 60 Tagen auf X%, CLV/CAC-Ratio erreicht Y nach 2 Quartalen“            | Trennt frühe Verhaltensänderung von späterem Geschäftswert (Kufile et al., 2022)       |

**Figure 4:** Von vagen zu falsifizierbaren Erfolgsmetriken.

Ein guter Vorab-Scorecard-Eintrag braucht mindestens **Definition, Datenquelle, Baseline, Zielwert, Zeitfenster, Besitzer und Entscheidungsregel**; sonst bleibt ein Review leicht „inkonklusiv“, weil nicht klar ist, ob ein Proxy, ein Messfehler oder ein Zielkonflikt vorliegt (Kufile et al., 2022).

## 5. Häufige Fehlermodi

Häufige Fehlermodi sind **Vanity Metrics**, KPI-Überladung, schlechte Ziel-Metrik-Passung, Proxy-Fehler und Messdesigns, die mit vorhandenen Tools nicht tragfähig sind (Rădulică, 2024; Kufile et al., 2022; Bucko et al., 2025). Erfahrene Teams vermeiden das, indem sie wenige priorisierte KPIs definieren, diese an Geschäftsziele rückbinden und nur Metriken zusagen, die mit vorhandener Infrastruktur konsistent erhoben werden können (Rădulică, 2024; Bucko et al., 2025; Kufile et al., 2022).

- **Vanity statt Wert:** Likes oder isolierte CTRs wirken attraktiv, bilden Geschäftswirkung aber oft schlecht ab (Rădulică, 2024; Umoren et al., 2021).
- **Messbarkeit überschätzt:** Attributions- und Datensilos verhindern saubere Aggregation über Kanäle und CRM hinweg (Kufile et al., 2022).
- **Proxy-Verwechslung:** Teams behandeln den Proxy als Ziel selbst und verlieren den eigentlichen Geschäftswert aus dem Blick (Gubela & Lessmann, 2021).
- **Failure washing:** Verfehlungen werden als „Lessons Learned“ umetikettiert, statt Zielerreichung klar zu prüfen (Akbar et al., 2023).

Für Ihren wiederholbaren Success-Metrics-Schritt spricht die Literatur am stärksten für ein knappes Template: **Geschäftsziel → Leading KPI → Lagging KPI → Zielwert → Zeitfenster → Datenquelle → Attributionshinweis → Review-Kadenz → Go/No-Go-Regel** (Kufile et al., 2022; Umoren et al., 2021).

## APA-Quellenverzeichnis

Akbar, M., Foote, L., & Lawson, A. (2023). Conceptualizing, embracing, and measuring failure in social marketing practice. _Social Marketing Quarterly_.

Berman, R. (2018). Beyond the last touch: Attribution in online advertising. _Marketing Science_.

Bucko, J., Pavlov, B., & Pitka, T. (2025). Evaluating the effectiveness of customer behavior analysis in online sales through financial composite metrics. _Journal of Marketing Analytics_.

Duggirala, S. (2026). Beyond the last touch: A framework for implementing multi-touch attribution in high-touch enterprise marketing. _Applied Marketing Analytics: The Peer-Reviewed Journal_.

Gubela, R., & Lessmann, S. (2021). Uplift modeling with value-driven evaluation metrics. _Decision Support Systems_.

John, Y. J., Caldwell, L., McCoy, D. E., & Braganza, O. (2023). Dead rats, dopamine, performance metrics, and peacock tails: Proxy failure is an inherent risk in goal-oriented systems. _Behavioral and Brain Sciences_.

Katsikeas, C., Morgan, N. A., Leonidou, L. C., & Hult, G. T. M. (2016). Assessing performance outcomes in marketing. _Journal of Marketing_.

Khimich, E. V. (2021). Key metrics for assessing efficiency of online marketing communication.

Kufile, O. T., Otokiti, B., Onifade, A. Y., Ogunwale, B., & Okolo, C. H. (2022). Constructing KPI-driven reporting systems for high-growth marketing campaigns. _Journal of Frontiers in Multidisciplinary Research_.

Mintz, O., Gilbride, T. J., Lenk, P., & Currim, I. S. (2020). The right metrics for marketing-mix decisions. _International Journal of Research in Marketing_.

Nathan, M., & Rosso, A. (2021). Innovative events: Product launches, innovation and firm performance. _Research Policy_.

Rădulică, M. (2024). Methods and tools for measuring marketing performance. _Social Economic Debates_.

Saura, J. R., Palos-Sánchez, P., & Suárez, L. M. C. (2017). Understanding the digital marketing environment with KPIs and web analytics. _Future Internet_.

Sangwa, N. R., & Sangwan, K. S. (2018). Development of an integrated performance measurement framework for lean organizations. _Journal of Manufacturing Technology Management_.

Seth, S., & Ramakrishnan, S. (2025). Innovations in multi-touch attribution models: Beyond traditional marketing analytics in the pharmaceutical sector. In _2025 International Conference on Emerging Smart Computing and Informatics (ESCI)_.

Taylor, T., & Ahmed-Kristensen, S. (2016). Global product development: KPI selection support.

Trigos, F., & Aldana, C. (n.d.). A transdisciplinary approach for predicting and tuning to optimise initial business performance steady state in a changing and connected environment.

Umoren, O., Didi, P. U., Balogun, O., Abass, O. S., & Akinrinoye, O. V. (2021). Developing multidimensional KPIs for marketing strategy success using cross-functional insights and behavioral feedback loops. _International Journal of Multidisciplinary Futuristic Development_.

Verma, A. (2025). A comparative study of ad attribution models: Evaluating the impact on ROI measurement. _European Journal of Computer Science and Information Technology_.

Redwan, R., Niraula, S., & Swamy, A. S. (2025). KPI tracking and performance metrics for brand growth optimization. _Research Journal in Business and Economics_.

_These search results were found and analyzed using Consensus, an AI-powered search engine for research. Try it at https://consensus.app. © 2026 Consensus NLP, Inc. Personal, non-commercial use only; redistribution requires copyright holders’ consent._

## References

Akbar, M., Foote, L., & Lawson, A. (2023). Conceptualizing, Embracing, and Measuring Failure in Social Marketing Practice. _Social Marketing Quarterly, 29_, 241 - 256. https://doi.org/10.1177/15245004231187134

Berman, R. (2018). Beyond the Last Touch: Attribution in Online Advertising. _Mark. Sci., 37_, 771-792. https://doi.org/10.1287/mksc.2018.1104

Bucko, J., Pavlov, B., & Pitka, T. (2025). Evaluating the effectiveness of customer behavior analysis in online sales through financial composite metrics. _Journal of Marketing Analytics_. https://doi.org/10.1057/s41270-025-00430-6

Duggirala, S. (2026). Beyond the last touch: A framework for implementing multi-touch attribution in hightouch enterprise marketing. _Applied Marketing Analytics: The Peer-Reviewed Journal_. https://doi.org/10.69554/deag9699

Gubela, R., & Lessmann, S. (2021). Uplift modeling with value-driven evaluation metrics. _Decis. Support Syst., 150_, 113648. https://doi.org/10.1016/j.dss.2021.113648

Katsikeas, C., Morgan, N. A., Leonidou, L. C., & Hult, T. (2016). Assessing Performance Outcomes in Marketing. _Journal of Marketing, 80_, 1 - 20. https://doi.org/10.1509/jm.15.0287

Khimich, E. V. (2021). Key Metrics For Assessing Efficiency Of Online Marketing Communication. https://doi.org/10.15405/epsbs.2021.07.74

Kufile, O. T., Otokiti, B., Onifade, A. Y., Ogunwale, B., & Okolo, C. H. (2022). Constructing KPI-Driven Reporting Systems for High-Growth Marketing Campaigns. _Journal of Frontiers in Multidisciplinary Research_. https://doi.org/10.54660/.jfmr.2022.3.1.403-413

Mintz, O., Gilbride, T. J., Lenk, P., & Currim, I. S. (2020). The right metrics for marketing-mix decisions. _International Journal of Research in Marketing_. https://doi.org/10.1016/j.ijresmar.2020.08.003

Nathan, M., & Rosso, A. (2021). Innovative Events: Product launches, innovation and firm performance. _Research Policy_. https://doi.org/10.2139/ssrn.3085935

Rădulică, M. (2024). Methods and Tools for Measuring Marketing Performance. _Social Economic Debates_. https://doi.org/10.58679/sed48149

Redwan, R., Niraula, S., & Swamy, A. S. (2025). KPI Tracking and Performance Metrics for Brand Growth Optimization. _Research Journal in Business and Economics_. https://doi.org/10.61424/rjbe.v3i2.452

Sangwa, N. R., & Sangwan, K. S. (2018). Development of an integrated performance measurement framework for lean organizations. _Journal of Manufacturing Technology Management, 29_, 41-84. https://doi.org/10.1108/jmtm-06-2017-0098

Saura, J. R., Palos-Sánchez, P., & Suárez, L. M. C. (2017). Understanding the Digital Marketing Environment with KPIs and Web Analytics. _Future Internet, 9_, 76. https://doi.org/10.3390/fi9040076

Seth, S., & Ramakrishnan, S. (2025). Innovations in Multi-Touch Attribution Models: Beyond Traditional Marketing Analytics in the Pharmaceutical Sector. _2025 International Conference on Emerging Smart Computing and Informatics (ESCI)_, 1-5. https://doi.org/10.1109/esci63694.2025.10988316

Trigos, F., & Aldana, C. (2023). A Transdisciplinary Approach for Predicting and Tuning to Optimise Initial Business Performance Steady State in a Changing and Connected Environment. 541-550. https://doi.org/10.3233/atde230649

Umoren, O., Didi, P. U., Balogun, O., Abass, O. S., & Akinrinoye, O. V. (2021). Developing Multidimensional KPIs for Marketing Strategy Success Using Cross-Functional Insights and Behavioral Feedback Loops. _International Journal of Multidisciplinary Futuristic Development_. https://doi.org/10.54660/ijmfd.2021.2.2.07-15

Verma, A. (2025). A Comparative Study of Ad Attribution Models: Evaluating the Impact on ROI Measurement. _European Journal of Computer Science and Information Technology_. https://doi.org/10.37745/ejcsit.2013/vol13n355675


---

## DeepSeek (source: `measurement-framework-deepseek.md`)

# Building a Repeatable Success-Metrics Framework for Campaign and Launch Planning

## 1. Leading vs. Lagging Metric Pairing by Campaign and Launch Type

A leading indicator measures an early signal you can act on while there is still time to change a campaign's outcome. A lagging indicator measures the return on investment (ROI) of your work after a campaign or sales cycle ends. You need both: **leading to steer, lagging to confirm impact**. Over-indexing on lagging indicators means you are always looking in the rear-view mirror; over-indexing on leading indicators means you might be optimizing activities that do not drive business outcomes.

### By Campaign Type

**Product-Launch Campaign**

- **Leading indicator:** Demo request volume among target accounts / percentage of target account executives attending launch webinar and requesting follow-up
- **Lagging indicator:** Customer acquisition cost (CAC) of new contracts / closed-won revenue from launch cohort
- **Practitioner note:** For enterprise B2B launches, lagging metrics can take eight months to materialize; leading indicators let you scale or pivot mid-quarter

**Thought-Leadership Campaign**

- **Leading indicator:** Content engagement (time on page, scroll depth, share rate); decision-maker engagement signals (downloads of gated research, webinar attendance)
- **Lagging indicator:** Pipeline influenced from thought-leadership assets; market influence / share of voice; inbound inquiries citing the content
- **Practitioner note:** The best measurement models include both leading indicators (resonance) and lagging indicators (pipeline impact). Leading indicators can move in weeks; pipeline impact typically follows your sales cycle

**Seasonal-Promotion Campaign**

- **Leading indicator:** Early traffic-to-cart conversion rates; promotional email open and click-through rates in the 48 hours post-send
- **Lagging indicator:** Incremental sales lift (vs. baseline); promotion-attributed revenue; average order value during promotion period
- **Practitioner note:** Treating seasonal demand as purely a revenue event misses the strategic opportunity; measure incrementality, not just revenue spikes

**Retention Campaign**

- **Leading indicator:** Engagement with retention communications (email open rates, flow conversion rates, opt-in rates); product feature adoption by existing customers
- **Lagging indicator:** Customer churn rate; customer lifetime value (LTV); net promoter score (NPS); expansion revenue
- **Practitioner note:** Retention is no longer a "nice to have"—it is the only way to sustain a business. Retention-adjusted CPA includes projected 12-month revenue contribution

**Lead-Generation Campaign**

- **Leading indicator:** Engagement rate; ICP traffic percentage; dwell time; frequency / audience penetration trends
- **Lagging indicator:** Cost per lead; sales-qualified leads (SQLs); pipeline generated; cost per SQL
- **Practitioner note:** Lead volume is only a leading indicator—pipeline revenue should be the primary KPI. Cheap leads often lead to wasted sales time and poor conversion rates

**Brand-Awareness Campaign**

- **Leading indicator:** Branded search volume; direct website traffic; share of voice; aided / unaided brand recall in tracking surveys
- **Lagging indicator:** Brand lift (measured via brand tracking studies); brand preference scores; market share movement
- **Practitioner note:** Brand awareness does not cause sales the way a promotional email does. But brand metrics are leading indicators of commercial performance—rising brand preference precedes market share growth

### By Launch Type

**Product Launch (Full Go-to-Market)**

- **Leading indicator:** Pre-launch waitlist / signup volume; launch-day traffic to product page; early adoption velocity (Day 1, Day 7, Day 30 activation rates)
- **Lagging indicator:** Launch-attributed revenue (first 90 days); CAC; payback period; market share in category
- **Practitioner note:** Lagging indicators are unresponsive and hard to change—they are results of the past. Leading indicators are often hidden, qualitative, and hard to track, but critical for mid-launch correction

**Feature Release**

- **Leading indicator:** Feature discovery rate (users reaching the feature); in-product engagement with the new feature; feature adoption velocity among existing users
- **Lagging indicator:** Net retention impact; new business previously blocked by lack of feature; feature-attributed revenue
- **Practitioner note:** Joint success metrics matter—both marketing and product teams should be measured on feature adoption rates, not just marketing on leads and product on shipping velocity

**Market Expansion**

- **Leading indicator:** Brand awareness in the new market; website traffic from the new geographic region; pipeline-creation velocity in new market
- **Lagging indicator:** Revenue from new market; market share in new geography; customer acquisition rates by region
- **Practitioner note:** As an early-stage KPI, brand performance offers something revenue and reach alone cannot—perspective. It reveals whether awareness is building at real scale and not just spiking around a launch moment

## 2. Attribution Model Tradeoffs for Teams Without a Full Analytics Stack

For marketing teams without a full analytics stack, attribution is a **triangulation problem**—algorithmic multi-touch tells you the trend, self-reported attribution tells you the truth buyers remember, and marketing mix modeling tells you what budget to defend. None of those signals is right alone.

### Model Comparison

| Model                        | How It Works                                                                     | When Appropriate                                                | Key Limitation                                                                    |
| ---------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **Last-Touch**               | 100% credit to final interaction before conversion                               | Low-complexity, short sales cycles; default in most platforms   | Under-credits brand, content, and dark social; over-credits direct/branded search |
| **Multi-Touch (Rule-Based)** | Fractional credit across identifiable touchpoints (linear, time-decay, U-shaped) | When you have clean UTM/CRM linkage and want journey visibility | Requires data integration; can only track what's trackable                        |
| **Self-Reported**            | Prospects answer "How did you hear about us?" on forms                           | When you have tracking gaps; as a check against model bias      | Recall bias; conflicts with dashboard data                                        |

### When Each Is Appropriate

**Last-touch is appropriate when:**

- You have short, simple sales cycles (<30 days)
- You lack the data infrastructure for multi-touch
- You need a simple, universally understood model for finance stakeholders
- You're optimizing bottom-of-funnel tactics

**Multi-touch (rule-based) is appropriate when:**

- You have clean UTM tagging and CRM integration
- You need visibility into long, multi-touch B2B journeys
- You can invest in getting all marketing data into one ecosystem
- **Start with:** Apply a simple weighting rule (30% first-touch, 20% assists, 50% last-touch) before investing in algorithmic models

**Self-reported attribution is appropriate when:**

- You have tracking gaps (organic search, direct visits, dark social)
- You need a reality check against dashboard data
- You want to understand what buyers _remember_ influenced them
- **Implementation:** Add a dropdown on demo or booking forms with clear options (LinkedIn ad, organic search, referral, etc.)

### What to State Explicitly When You Can't Run Proper Multi-Touch Attribution

When a team cannot run proper multi-touch attribution, the success-metrics framework should include a **clear disclosure statement** covering:

1. **"We are using [last-touch / self-reported] attribution as our primary model, which means [specific touchpoints] are systematically under- or over-credited."**
   - Example: _"We use last-touch attribution, which means top-of-funnel channels (display, podcast ads, organic social) receive zero credit for conversions they may have influenced."_

2. **"We reconcile [model A] with [model B] monthly to identify systematic bias."**
   - Run last-touch plus self-reported, reconcile monthly, and revisit the question once pipeline volume justifies the build

3. **"We use this model for [specific decision type] only—not for [other decision type]."**
   - Example: _"We use last-touch for tactical campaign optimization but do not use it for annual budget allocation decisions."_

4. **"Our reported numbers represent [metric definition], not causal impact."**
   - Attribution is signal allocation, not causal proof

5. **"Incrementality testing (where feasible) is our standard for validating attribution conclusions."**
   - Incrementality testing provides the only truly causal measure of marketing effectiveness

## 3. Standard Review-Cadence Conventions

The cadence should match the **speed at which the underlying metric can meaningfully change**. A reporting cadence is a scheduled rhythm for reviewing marketing performance data with specific audiences at specific intervals. It determines whether problems get caught early or discovered late.

### Active Launch / Campaign Window

| Cadence                  | Purpose                                     | What to Review                                                                                                                                                                   | Who                          |
| ------------------------ | ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| **Daily (5-min scan)**   | Catch outliers before they run for a week   | Total paid spend pacing; key conversion volume vs. same day last week; cost per conversion by major channel (flag >20% above normal); anomalies (traffic drops, tracking breaks) | Campaign manager             |
| **Weekly**               | Decision-making analysis; course correction | Channel-level performance (spend, conversions, CPL/CPA); funnel conversion rates; campaign-level summary (up/down/changes); week-over-week trends                                | Marketing lead + team        |
| **Bi-weekly** (optional) | Mid-sprint health check                     | Creative performance; audience segment performance; early leading-indicator signals                                                                                              | Campaign lead + stakeholders |

**Weekly reports should end with one to three actions:** a budget shift, a campaign to pause, or a test to run. If it produces no actions, the report is too high-level.

**Campaign launch window example:** For an 8-week product launch campaign:

- Weeks 1-2: Daily scans + weekly team reviews
- Weeks 3-6: Weekly reviews with bi-weekly stakeholder check-ins
- Week 7-8: Weekly reviews + pre-close analysis

### Steady State (Post-Launch / Always-On)

| Cadence       | Purpose                            | What to Review                                                                                                                 | Who                             |
| ------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------- |
| **Monthly**   | Strategic layer; unit economics    | CAC by channel (month vs. prior months); LTV cohort updates; payback period trend; channel-level ROI; budget allocation review | Marketing leadership + founders |
| **Quarterly** | Strategic planning; budget defense | Annual KPI progress; brand health metrics; market share; marketing mix modeling outputs; next-quarter budget allocation        | CMO + executive team            |
| **Annual**    | Full-funnel effectiveness          | YoY revenue impact; marketing contribution to business outcomes; measurement framework refinement                              | Full leadership team            |

### Reasoning Behind the Difference

1. **Campaign windows are time-boxed and irreversible.** If you wait until month-end to discover a creative is underperforming, you've wasted budget you can't recover.
2. **Leading indicators change faster than lagging ones.** Engagement rates can shift daily; CAC and LTV move slowly.
3. **Steady-state metrics have longer feedback loops.** Cohort analysis requires enough data to be statistically meaningful.
4. **Decision velocity differs.** Active campaigns require tactical actions (pause, shift, scale). Steady state requires strategic actions (budget reallocation, channel mix changes).

## 4. What Makes a Stated Success Metric "Falsifiable" Before the Fact

A falsifiable success metric is one **specific enough that a post-campaign review could clearly say it was hit, missed, or inconclusive**—versus a vague goal like "increase awareness."

### The Falsifiability Test

A metric is falsifiable if it passes these five questions **before the campaign runs**:

1. **Specific:** Does it name a precise number, percentage, or threshold?
2. **Measurable:** Can we actually measure this with our current tools?
3. **Time-bound:** Does it specify _when_ we will measure it?
4. **Comparative:** Does it compare against a baseline (historical, industry benchmark, or control group)?
5. **Unambiguous:** Would two independent reviewers agree on whether it was met?

### Falsifiable vs. Non-Falsifiable Examples

| ❌ Non-Falsifiable (Vague) | ✅ Falsifiable (Specific)                                                                                                                                                                                                    |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Increase awareness"       | "Increase unaided brand awareness among our target segment from 22% to 28% within 90 days of campaign launch, measured via brand tracking survey (n=400, ±5% MoE)"                                                           |
| "Drive engagement"         | "Achieve a 4.5% average engagement rate (likes+comments+shares / impressions) on LinkedIn campaign posts over the 6-week campaign period, vs. 2.8% 6-week pre-campaign baseline"                                             |
| "Generate leads"           | "Generate 120 marketing-qualified leads (MQLs) with an average CPL below $85 in Q3, measured via HubSpot form submissions meeting lead-scoring threshold of ≥50 points"                                                      |
| "Improve retention"        | "Reduce monthly logo churn from 4.2% to 3.0% within 6 months of the retention campaign launch, measured via CRM cohort analysis"                                                                                             |
| "Grow revenue"             | "Generate $450,000 in attributed pipeline value within 90 days of launch, with at least $120,000 in closed-won revenue by Day 120, measured via multi-touch attribution (or, if unavailable, self-reported source tracking)" |

### Using Benchmarks and Proxy KPIs

- **Benchmarks** make it easier to spot if a campaign is underperforming, based on selected metrics. Benchmarks are averages based on the performance of past campaigns from the brand or from the industry.
- **If the ideal KPI is not measurable, choose one metric to be your 'Proxy KPI'**.
- **Example:** If you cannot directly measure brand lift due to budget constraints, use branded search volume + direct traffic as proxy leading indicators.

### The "So What?" Test

Every proposed metric should pass the "so what?" test: it must guide strategy, inform decisions, or connect to repeatable actions that drive pipeline and revenue. If a metric fails this test, it's not falsifiable in any meaningful sense—it's just a number.

## 5. Common Failure Modes When Teams Set Success Metrics Upfront

### Failure Mode 1: Vanity Metrics

**The problem:** Numbers that look impressive but don't translate into business success in any meaningful way. They can lead to poor business decisions if misused.

**Common vanity metrics to avoid:**

- Total social media followers
- Unqualified leads
- Email open rates without click-through data
- Website traffic without considering bounce rate
- App download numbers without active user data

**The trap:** "There's no shame in being small and profitable. Ignore the ego side of it". Having 10,000 social media followers might feel like a win, but if engagement metrics are low, those followers aren't driving real value.

**How experienced teams avoid it:**

- Ask: "Does this metric correlate to revenue?"
- Pair every vanity-prone metric with an action metric (e.g., "social followers" → "engagement rate among followers"; "page views" → "conversion rate")
- Focus on **growth levers that help you bring more value to your market**

### Failure Mode 2: Metrics That Can't Be Measured With Available Tools

**The problem:** Teams commit to KPIs they have no way to actually track, leading to post-campaign guesswork or fabricated reports.

**Common examples:**

- Brand lift without a brand tracking survey budget
- Multi-touch attribution without data integration
- Incrementality without experimental design capability
- "Offline sales influenced" without a measurement mechanism

**How experienced teams avoid it:**

- **Audit tool capabilities before committing to metrics.** If the ideal KPI is not measurable, choose a proxy KPI
- **Define the measurement method explicitly in the success metrics document:** "We will measure [metric] using [tool + method] on [cadence]"
- **Build measurement capability into the campaign budget** before launch, not after

### Failure Mode 3: Metrics Disconnected From the Stated Business Goal

**The problem:** Teams measure what's easy rather than what matters. A 2010 study with Deloitte found that 56% of companies rate their marketing measurement capability as non-existent or basic. Less than 10% always set clear KPIs for marketing initiatives.

**The trap:** "Target cost per lead is not your marketing goal. It's a lagging indicator of marketing performance. Your marketing goal should be something like increase new customers by 10% while retaining 90% of existing customers".

**How experienced teams avoid it:**

- **Start with the business objective, then derive metrics**—not the reverse
- **Use a "metric ladder":** Business goal → Marketing objective → Leading indicator → Lagging indicator
- **Align marketing, sales, and finance** to prove business impact clearly

### Failure Mode 4: Too Many KPIs

**The problem:** Both Pepsi and Sky admitted they had too many KPIs that made measuring marketing effectiveness almost impossible. Pepsi's analytics function comprised more than 900 people and 2,000 KPIs.

**How experienced teams avoid it:**

- **Limit to 3-5 core KPIs per campaign/launch** (ideally 1-2 leading + 1-2 lagging)
- **Differentiate between "tracking metrics" (for monitoring) and "success metrics" (for evaluation)**
- **Use the "one-pager" rule:** If you can't fit your success metrics on one page, you have too many

### Failure Mode 5: Confusing Leading and Lagging Indicators

**The problem:** Teams mix leading indicators and lagging metrics together, treating early signals as outcomes and vice versa.

**The trap:** A team celebrates high lead volume (leading indicator) as if it were revenue (lagging indicator), then misses revenue targets by 40%.

**How experienced teams avoid it:**

- **Explicitly label every metric as "Leading" or "Lagging" in the success metrics document**
- **Set separate targets for each:** "We will track [leading metric] for mid-campaign steering and [lagging metric] for post-campaign evaluation"
- **Educate stakeholders** on the difference and the expected time lag between leading and lagging movement

### Failure Mode 6: No Falsifiability / No Clear "Win" Condition

**The problem:** Teams set vague goals that can be interpreted as "success" no matter what happens, creating post-campaign rationalization rather than genuine learning.

**How experienced teams avoid it:**

- **Use the SMART framework:** Specific, Measurable, Achievable, Relevant, Time-bound
- **Write success criteria as "if-then" statements:** "If [metric] reaches [threshold] by [date], the campaign is a success. If not, it is not."
- **Pre-commit to the evaluation criteria** in writing before the campaign launches

## Source List

Buck, D. (2025). _Vanity Metrics 101: How to identify (and avoid) vanity metrics (2026)_. Shopify. https://www.shopify.com/blog/vanity-metrics

Childers, D. (2025, September 24). Why B2B marketers are measuring the wrong things [LinkedIn post]. LinkedIn. https://www.linkedin.com

Dane, J. (2025, December 17). Here's the problem with B2B LinkedIn Ads [LinkedIn post]. LinkedIn. https://www.linkedin.com

Digital Marketing Institute. (2026, June 8). _Agile marketing metrics that matter: Leading vs. lagging_. https://digitalmarketinginstitute.com/blog/agile-marketing-metrics-leading-vs-lagging

Location3 Media. (2025, July 28). _From metrics to meaning: Building a smarter marketing measurement plan_. https://location3.com/blog/from-metrics-to-meaning-building-a-smarter-marketing-measurement-plan/

Marketing Agency Singapore. (2026, March 31). _Product marketing metrics: KPIs that actually matter_. https://marketingagency.sg/product-marketing-metrics-guide/

Onclusive. (2025, October 16). _4 essential campaign KPIs to measure the success of your communication_. https://onclusive.com/en-gb/resources/blog/4-powerful-ways-to-measure-communication-campaign-kpis/

Shopify. (2025, August 5). _Leading indicators: Guide for ecommerce businesses (with examples)_. https://www.shopify.com/nz/enterprise/blog/leading-indicators-ecommerce

Stackmatix. (2026, April 6). _Marketing reporting: How often and what to include_. https://www.stackmatix.com/blog/marketing-reporting-frequency

The Pedowitz Group. (n.d.). _Measure the effectiveness of thought leadership initiatives_. https://www.pedowitzgroup.com

Uplift GTM. (2026, March 30). _GTM metrics & KPIs: What to measure at every stage [2026]_. https://www.upliftgtm.com


---

## Gemini (source: `measurement-framework-gemini.md`)

# **Comprehensive Pre-Campaign Measurement Frameworks: A Strategic GTM Playbook**

## **1\. Leading vs. Lagging Metric Pairing by Campaign and Launch Type**

In corporate performance management, establishing a pre-campaign measurement framework requires a rigorous understanding of the relationship between leading and lagging indicators1. Lagging indicators serve as the retrospective "report card" of a marketing strategy, confirming past performance such as revenue generated, customers acquired, or contract value1. However, because lagging metrics are backward-looking, managing a campaign solely through them leaves marketing teams unable to course-correct in real time2. Leading indicators act as predictive inputs that signal future performance trends, allowing teams to adjust strategies before budget is fully expended1.  
These indicators are relative positions in a causal chain, best visualized as a metric tree where the ultimate lagging business outcome sits at the top and decomposes downward into increasingly controllable leading inputs5. This causal relationship can be understood through fundamental marketing mathematics, such as the site-wide revenue formula:  
![][image1]  
In this equation, total revenue is a lagging outcome, while sessions, conversion rates, and average order values function as leading levers that teams can directly influence6. Which metric is treated as the primary lever depends heavily on the business phase: launch teams require sessions, growth teams optimize CVR, scale teams focus on return on ad spend (ROAS) or revenue per session (RPS), and mature teams drive overall AOV6.  
To operationalize this framework, practitioners construct explicit, testable chains from day-to-day activities to final outcomes2. The tables below outline concrete, paired metrics used by marketing practitioners, broken out by campaign type and launch type.

### **Campaign Types: Leading and Lagging Metric Pairings**

| Campaign Type | Leading Indicator (Predictive Input) | Lagging Outcome (Confirmed Result) | Causal Linkage & Operational Rationale |
| :---- | :---- | :---- | :---- |
| **Product Launch** | Trial activation rate or high-intent demo requests3 | Customer Acquisition Cost (CAC) payback period or new recurring revenue9 | Early product usage and demo intent predict conversion efficiency and subsequent financial payback speed1. |
| **Thought Leadership** | Gated resource downloads or content completion rates within the Ideal Customer Profile (ICP)8 | Lift in organic brand search volume or share of voice (SOV)13 | High-quality content engagement from target accounts precedes a shift in organic brand equity and market visibility2. |
| **Seasonal Promotion** | Add-to-cart rate or checkout initiation rate2 | Return on Ad Spend (ROAS) or gross promotional revenue3 | Micro-conversions at the bottom of the e-commerce funnel directly predict transactional revenue velocity2. |
| **Retention** | Feature adoption rate or product usage frequency8 | Customer churn rate or Net Revenue Retention (NRR)1 | Sustained product adoption and high feature utility serve as an early warning system against contract cancellation9. |
| **Lead Generation** | Lead-to-opportunity conversion rate or sales-accepted lead velocity3 | Marketing-attributed pipeline value generated3 | The efficiency of converting top-of-funnel leads to accepted sales opportunities determines the volume of pipeline created3. |
| **Brand Awareness** | Aided brand recall lift or target segment impressions2 | Lift in direct and organic website sessions12 | Initial ad exposure and brand memory lift drive future non-paid navigational search and direct site entries15. |

### **Launch Types: Leading and Lagging Metric Pairings**

| Launch Type | Leading Indicator (Predictive Input) | Lagging Outcome (Confirmed Result) | Causal Linkage & Operational Rationale |
| :---- | :---- | :---- | :---- |
| **Product Launch** | Target account sign-up conversion rate or trial-to-paid velocity8 | Customer count acquired or initial Monthly Recurring Revenue (MRR)1 | Early conversion rates from high-intent cohorts determine the baseline run-rate of the newly launched product1. |
| **Feature Release** | Feature adoption rate or usage frequency of key release workflows7 | Retention rate lift or expansion revenue per customer1 | Direct engagement with new features increases overall product stickiness and unlocks expansion opportunities within current accounts5. |
| **Market Expansion** | Localized search volume index or qualified traffic from expansion region2 | Market share growth or regional annual recurring revenue2 | Top-of-funnel demand indicators in a new market precede sales opportunities and long-term geographic revenue capture2. |

## **2\. Attribution Model Tradeoffs for Lean Analytics Stacks**

Marketing teams operating without a fully integrated, modern analytics stack (such as a centralized data warehouse, reverse ETL pipelines, and specialized analytics engineers) must make strategic tradeoffs when measuring campaign impact16. Adopting an attribution model is essentially setting a credit-assignment policy rather than discovering scientific truth10. However, as industry experts note, teams do not need a complex data stack of Snowflake and dbt to extract directional value from multi-touch models24.  
Each model has inherent assumptions, best use cases, and distinct structural vulnerabilities:

### **Standard Last-Touch Attribution**

This model assigns 100% of conversion credit to the final marketing interaction immediately preceding the purchase10.

* **When Appropriate:** Last-touch is useful for highly transactional consumer businesses with short sales cycles (typically under 30 days) and a limited channel mix (two to three channels)25. It is also the simplest and most accessible model to deploy using basic, standard out-of-the-box setups10.  
* **Vulnerabilities:** In complex, multi-touch journeys—such as B2B SaaS—last-touch completely oversimplifies reality10. According to extensive customer journey benchmark analysis, a typical B2B SaaS deal requires an average of **266 touchpoints** (representing a 19.8% YoY increase from 222 touchpoints) and **2,879 impressions** over a **211-day cycle**10. Stage-by-stage touchpoint requirements are highly complex10:  
  * *First visit to MQL:* 71 touchpoints10.  
  * *MQL to SQL/Pipeline:* 96 touchpoints10.  
  * *SQL to Closed-Won:* 99 touchpoints10.  
  * *Enterprise Deals (Above $100K ACV):* 417 touchpoints10.

Because B2B buyers require repeated exposure across such an extended cycle, standard last-touch models over-credit bottom-funnel "demand capture" channels (such as branded paid search or retargeting) while starving budget from upper-funnel "demand generation" channels (such as content marketing and social media)10.

* **Refinement:** To improve accuracy, teams utilize **Last Non-Organic Touch**10. This variation ignores direct type-ins and untagged organic traffic, passing credit back to the last paid or active marketing touchpoint, which prevents owned channels from stealing conversion credit from paid campaigns10.

### **Multi-Touch Attribution (MTA)**

MTA models attempt to spread credit across several digital interactions using rule-based formulas (such as Linear, Time-Decay, or U-Shaped)10. Over 52% of marketers adopted MTA in 2024, with 57% calling it critical for measurement28.

* **When Appropriate:** Rule-based multi-touch models (like the U-shaped model, which assigns 40% to the first touch, 40% to the last touch, and splits 20% across middle touches) are valuable when analyzing multi-channel digital campaigns with medium-length consideration cycles10. They are useful when teams seek to understand how top-of-funnel brand discovery and bottom-funnel conversion efforts work together25.  
* **Vulnerabilities:** Advanced, data-driven algorithmic models function as an opaque "black box" that requires statistical software and high conversion volumes (typically hundreds of conversions per channel, per month) to achieve mathematical stability10. For a lean team with low-to-medium conversion volumes, the outputs of data-driven models are highly volatile and carry a false sense of analytical authority10. Additionally, observational data-driven approaches historically overestimate ad effectiveness by around 3x compared to randomized, controlled incrementality experiments10.

### **Self-Reported Attribution**

This method utilizes an always-on, open-ended, free-text field on high-intent lead capture forms (e.g., asking "How did you hear about us?")10.

* **When Appropriate:** SRA is highly effective for lean teams with low conversion volumes, especially in B2B setups10. It is unique in its ability to capture the "dark funnel"—such as word-of-mouth recommendations, peer-to-peer Slack communities, podcast listenership, and offline event interactions—which digital tracking cookies are completely blind to10.  
* **Vulnerabilities:** SRA is highly subjective, relies entirely on human memory, and cannot be programmatically integrated to calculate automated cost-per-acquisition (CPA) or return-on-ad-spend (ROAS) dashboards10.

### **Multi-Touch Alternative Disclosures**

When multi-touch attribution cannot be reliably executed due to stack limitations, marketing teams must protect themselves from boardroom scrutiny by explicitly defining their measurement limits17. The following disclosures should be formally documented in pre-campaign planning materials to align expectations across marketing, finance, and GTM leadership:  
**Disclosure 1: Operational Boundary Disclosure (Bottom-Funnel Bias)** "The success metrics for Campaign \[Campaign Name\] will be tracked using a Last Non-Organic Touch attribution model due to current analytical stack constraints10. Stakeholders should note that this model carries a structural bias toward bottom-funnel demand capture channels (such as paid search and retargeting)10. Upper-funnel demand generation activities (such as content production and social brand building) will likely appear under-credited in standard dashboards10. Budget decisions and performance evaluations will therefore be adjusted to account for this bias, rather than optimizing strictly to last-click CPA10."  
**Disclosure 2: Measurement System Exclusion (Dark Funnel Gap)** "Our digital tracking infrastructure relies on cookie-based click data, which cannot capture peer-to-peer recommendations, dark social channels, podcasts, or community influence10. To prevent the systematic underfunding of these high-influence channels, we are implementing a self-reported attribution model alongside standard UTM tracking10. Any discrepancy between digital dashboard data and self-reported user surveys will be treated as an indicator of dark funnel influence, not tracking error, and will be reviewed monthly to guide strategic spend reallocation10."  
**Disclosure 3: Directional Measurement Framework (Operational Decisioning Policy)** "In the absence of programmatic multi-touch attribution, marketing performance will not be judged on single-metric outputs10. Decision-making will be guided by directional triangulation10: daily optimizations will leverage rule-based channel click metrics10; monthly strategic steering will align standard digital tracking against qualitative customer feedback10; and campaign-level ROI will be validated by cross-referencing total blended spend directly against bank-reconciled revenue records in collaboration with Finance22."

## **3\. Standard Review-Cadence Conventions**

Setting upfront success metrics requires defining the operational rhythm at which those metrics will be reviewed15. A common analytical failure is reviewing every KPI on the same timeline, which collapses the distinction between day-to-day operations and strategic steering33.  
To prevent this, practitioners design a tiered review cadence with a functional separation between active launch windows and steady-state operations32. This design is grounded in the structural difference between **Key Performance Indicators (KPIs)** and **Objectives and Key Results (OKRs)**: KPIs evaluate whether the business is operating within healthy limits (capacity, efficiency, reliability), while OKRs describe whether a focused set of active bets is producing meaningful improvement relative to a strategic objective33. Reviewing both on the same cadence collapses this distinction, leading to reactive firefighting instead of proactive strategic execution33.  
The standard four-tier operating rhythm details these cadence conventions and the reasoning behind them34:

### **1\. Weekly Operating Review (Active Launch Window)**

* **Operational Cadence:** 30–45 minutes, occurring weekly (or daily during the initial launch window)34.  
* **Target Metrics Focus:** Fast-moving operational indicators: click-through rates (CTR), cost-per-click (CPC), landing page bounce rates, daily conversion sign-ups, and sales SLA response times11.  
* **Primary Decision Outcomes:** Immediate ad budget reallocation, creative changes to combat ad fatigue, and fixing technical landing page friction16.  
* **Operational Reasoning:** Preserves operational agility by surfacing execution risks, technical bugs, or targeting anomalies before campaign budgets are wasted33. Weekly updates ensure that deviations are caught before they damage the business or cause OKRs to slip33.

### **2\. Monthly Business Review (Steady-State Operations)**

* **Operational Cadence:** 60–90 minutes, conducted monthly34.  
* **Target Metrics Focus:** Medium-to-slow-moving commercial drivers: customer acquisition cost (CAC) payback, customer lifetime value (LTV), pipeline velocity, channel-specific ROI, and monthly churn trends16.  
* **Primary Decision Outcomes:** Month-ahead resource reallocation, channel budget adjustments, and performance trend identification16.  
* **Operational Reasoning:** Slower-moving indicators do not need weekly tracking, but regular monthly check-ins provide the long-term trend data required to support better strategic decisions33. This timeline allows teams to distinguish between temporary fluctuations and sustained trends that demand action33.

### **3\. Quarterly Strategic / Board Review (Steady-State Operations)**

* **Operational Cadence:** 2–3 hours, conducted quarterly34.  
* **Target Metrics Focus:** High-level strategic and financial metrics: annual recurring revenue (ARR) growth, Net Revenue Retention (NRR), macro market share, and long-term customer cohorts4.  
* **Primary Decision Outcomes:** Strategic reforecasting, target adjustment, and metric retirement32.  
* **Operational Reasoning:** A company's operational realities change as it scales33. Quarterly reviews ensure the KPI system grows and adapts alongside the organization instead of falling behind33.

### **4\. Annual Strategic Planning**

* **Operational Cadence:** 1–2 days, conducted annually34.  
* **Target Metrics Focus:** Market trends, macro capacity, long-term forecasts, and broad-market benchmarks34.  
* **Primary Decision Outcomes:** Locking budgets, setting annual targets, and defining corporate capacity plans34.  
* **Operational Reasoning:** Aligns annual targets and budgets with the broader corporate strategy, establishing a stable foundation that cascades into the 4 quarters34.

## **4\. Pre-Facto Falsifiability Standards for Success Metrics**

For a pre-stated success metric to hold analytical validity, it must be inherently falsifiable39. Falsifiability, a standard of scientific evaluation introduced by Karl Popper, states that for a hypothesis to have empirical credibility, it must make risky, formal predictions that can be logically disproven by empirical observation40. In marketing analytics, a success metric that cannot be failed is not a metric; it is merely an ungrounded goal or a corporate vision39.  
Vague targets like "increase brand awareness" or "improve customer engagement" are unfalsifiable because they do not exclude any empirical observations8. If brand awareness is subsequently measured by any positive movement in impressions, page views, or social media mentions, the goal is structured to always confirm success, thereby evading any true test of effectiveness41.  
To make a stated success metric falsifiable before campaign execution begins, practitioners use the "don't talk, only point" methodology—replacing subjective claims with a specific, objective chain of evidence45. A falsifiable metric must satisfy five key components:

> 1. **A Specific, Standardized Metric Name** with an explicit mathematical formula8.  
> 2. **An Explicit Target Number** (not a range or directional statement)8.  
> 3. **A Named Data Source** or measurement platform to establish a single source of truth8.  
> 4. **A Strict Timeframe** or deadline12.  
> 5. **A Defined Qualification Cohort** to eliminate calculation errors and segment manipulation8.

To enforce these standard definitions, the table below provides the exact mathematical formulas, required data sources, and common calculation errors for key GTM metrics:

| Metric Name | Formula | Required Data Sources | Common Calculation Errors |
| :---- | :---- | :---- | :---- |
| **Customer Acquisition Cost (CAC)** \[cite: 8\] | ![][image2] | CRM, Payroll system, Ad platforms, Agency invoices, Software subscriptions8 | Excluding sales salaries, counting MQLs instead of closed customers, utilizing the wrong time window8. |
| **Customer Lifetime Value (LTV)** \[cite: 8\] | ![][image3] | Billing system, Churn database, Cost of Goods Sold (COGS)8 | Using top-line revenue instead of gross profit, neglecting expansion revenue, ignoring churn cohorts8. |
| **Marketing Qualified Lead (MQL)** \[cite: 8\] | ![][image4] | Marketing automation platform, CRM, Lead scoring models8 | Inconsistent scoring thresholds, not validating with sales, counting duplicate leads8. |
| **Sales Qualified Lead (SQL)** \[cite: 8\] | ![][image5] | CRM, Sales SLA tracking system8 | No formal SLA acceptance process, different sales reps using different definitions8. |
| **Return on Ad Spend (ROAS)** \[cite: 8\] | ![][image6] | Ad networks, Attribution model, Billing system8 | Relying on inflated platform-reported revenue, using the wrong lookback window, ignoring customer returns/refunds8. |
| **CAC Payback Period** \[cite: 8\] | ![][image7] | CAC calculations, Billing platform, Gross margin database8 | Using average lifetime value instead of monthly revenue, neglecting the time value of money8. |
| **Lead Velocity Rate (LVR)** \[cite: 8\] | ![][image8] | CRM, Standardized lead tracking database8 | Inconsistent qualification over time, neglecting seasonal impacts, including recycled leads8. |

### **Falsification Examples**

* *Vague / Unfalsifiable Goal:* "Increase organic visibility to demonstrate SEO authority."38  
* *Falsifiable Pre-Campaign Success Metric:* "Achieve a ![][image9] month-over-month increase in direct sign-ups originating from organic search traffic landing on transactional product pages, measured via Google Analytics 4 over Q3, using Stripe-verified checkout records6."  
* *Falsifiability Rationale:* Specifies the exact traffic source, the landing page type, the numerical target, the tracking platform, the verification financial database, and the timeframe, leaving no room for subjective interpretation8.  
* *Vague / Unfalsifiable Goal:* "Boost top-of-funnel brand awareness through our display campaigns."17  
* *Falsifiable Pre-Campaign Success Metric:* "Secure a ![][image10] lift in aided brand recall among our defined target accounts (US-based tech companies with ![][image11] employees), measured via an independent post-campaign survey (![][image12]) completed by October 312."  
* *Falsifiability Rationale:* Establishes a clear, independent measurement method, sample size, strict timeline, and target audience, making it possible to definitively prove the campaign failed if the recall lift is under ![][image13]2.

## **5\. Upfront Success Metric Failure Modes and Pre-Launch Audits**

Setting success metrics upfront is critical, yet many teams establish frameworks that are fundamentally flawed21. Data shows a significant gap between measurement and effectiveness: according to the Data & Marketing Association (DMA), **41% of marketing metrics in use today fail to reflect actual effectiveness**47. This challenge is compounded by a deep confidence gap; research from TransUnion and EMARKETER reveals that **62% of marketers question the validity of their metrics** at least some of the time29.  
Experienced analytics teams systematically identify and mitigate three primary failure modes:

### **1\. Vanity Metrics**

Vanity metrics are superficial numbers that look impressive in dashboard reports but lack actionable commercial utility or statistical correlation with business outcomes13. Common examples include ad impressions, social media follower counts, page views, and raw email opens17.

* *Operational Danger:* Optimizing for vanity metrics creates a false sense of security while wasting budget on empty reach3. For instance, a campaign may drive millions of ad impressions or a significant increase in page views, but if none of those visitors convert, the efforts have no impact on the company's bottom line3. As author Seth Godin notes, optimizing any number is pointless if that number is not aligned with why you went to work44.

### **2\. Unmeasurable Metrics with Current Tooling**

Teams often commit to metrics that their current analytics infrastructure is technically incapable of capturing26.

* *Operational Danger:* Committing to tracking complex consumer journeys (such as cross-device, cross-domain paths or multi-touch attribution) without having server-side tagging, integrated Customer Data Platforms (CDPs), or database reconciliations leads to massive data gaps28. When the campaign ends, the resulting performance reports are either highly contested or inconclusive29.

### **3\. Disconnected Metrics**

This failure mode occurs when the chosen marketing metrics have no logical or mathematical linkage to the ultimate business objectives6.

* *Operational Danger:* A marketing team may celebrate hitting its lead-generation volume targets while the sales organization experiences a stagnating pipeline7. Marketing Sherpa notes that while 60% of B2B marketers send their leads directly to sales, **less than 30% of those leads are actually qualified**, which wastes valuable sales resources and dilutes conversion rates7.

### **The Solution: The Pre-Launch Measurement Feasibility Audit**

To prevent these failure modes, experienced teams run a mandatory Pre-Launch Measurement Feasibility Audit before campaign execution begins31. This audit serves as a due diligence process that validates both the technical tracking implementation and financial reporting alignment31.  
The matrix below outlines the systematic checklist of the feasibility audit31:

| Feasibility Focus | Key Validation Questions & Action Steps | Prevention Mechanics |
| :---- | :---- | :---- |
| **Technical Tracking Validation** \[cite: 31, 46\] | 1\. Are custom UTM parameters standardized and enforced with a lowercase filter to prevent URL-casing duplication in GA410? 2\. Have conversion-tracking event configurations been tested in a raw data view to confirm they align with back-end database entries31? 3\. Is server-side tagging implemented to prevent data loss from browser privacy settings and ad blockers28? | Eliminates "unmeasurable metrics" by identifying tracking gaps, broken tags, and browser restrictions *before* capital is deployed28. |
| **Financial & Database Alignment** \[cite: 22, 31, 34\] | 1\. Is there a locked, cross-functional metric dictionary shared across marketing, sales, and finance13? 2\. Does the calculated Customer Acquisition Cost (CAC) formula include sales payroll, software licenses, and agency overhead, or only media spend8? 3\. Are marketing dashboards tied directly to CRM data or transactional databases16? | Mitigates "disconnected metrics" and "vanity measures" by ensuring marketing outcomes reconcile directly with company financial records16. |
| **Operational Feasibility Verification** \[cite: 31, 50, 51\] | 1\. Is there a single, designated owner accountable for tracking and reporting each active KPI6? 2\. Are baseline numbers established using historical performance data before targets are set11? 3\. Does the team have the technical tools and staff resources needed to monitor metrics at the chosen review cadence37? | Prevents setting unrealistic expectations or tracking metrics that the team lacks the resources or tools to act upon37. |

## **APA-Formatted Source List**

> 1. Statsig. (n.d.). *Leading vs. lagging indicators*. Retrieved from https://www.statsig.com/perspectives/leading-vs-lagging-indicators1  
> 2. Umbrex. (n.d.). *Marketing dashboard design framework*. Retrieved from https://umbrex.com/resources/frameworks/marketing-frameworks/marketing-dashboard-design-framework/13  
> 3. 23HubLab. (n.d.). *Marketing KPIs that actually predict revenue*. Retrieved from https://23hublab.com/marketing-kpis-that-actually-predict-revenue/3  
> 4. Invoca. (n.d.). *What is marketing attribution? Basics and benefits*. Retrieved from https://www.invoca.com/blog/what-is-marketing-attribution-basics-benefits25  
> 5. Winston Francois. (n.d.). *What is marketing attribution and why it breaks*. Retrieved from https://winstonfrancois.com/blog/what-is-marketing-attribution/26  
> 6. GrowthOptix. (n.d.). *Marketing attribution models*. Retrieved from https://www.growthoptix.com/blog/marketing-attribution-models10  
> 7. AttributionApp. (n.d.). *Attribution smackdown: 10 takeaways*. Retrieved from https://www.attributionapp.com/blog/attribution-smackdown-10-takeaways/24  
> 8. RevenueScope. (n.d.). *Marketing KPI design: 5 metrics that drive decisions*. Retrieved from https://www.revenuescope.jp/en/news/marketing-kpi-design6  
> 9. Pedowitz Group. (n.d.). *Best cadence for business reviews: Weekly, monthly, quarterly*. Retrieved from https://www.pedowitzgroup.com/best-cadence-for-business-reviews-weekly-monthly-quarterly34  
> 10. OKRs Tool. (n.d.). *Reviewing KPIs and OKRs*. Retrieved from https://www.okrstool.com/blog/review-kpis-okrs33  
> 11. HockeyStack. (2025). *B2B customer journey touchpoints benchmark report*. Retrieved from https://www.hockeystack.com/lab-blog-posts/b2b-customer-journey-touchpoints10  
> 12. Gordon, B. R., Zettelmeyer, F., Bhargava, N., & Chapsky, D. (2018). *A comparison of approaches to advertising measurement: Evidence from RCTs and observational methods*. Northwestern University. Retrieved from https://www.kellogg.northwestern.edu/faculty/gordon\_b/files/fb\_comparison.pdf10  
> 13. Improvado. (n.d.). *Steps to measure marketing performance*. Retrieved from https://improvado.io/blog/steps-to-measure-marketing-performance8  
> 14. StoryFlow. (2026). *The complete guide to marketing plans*. Retrieved from https://storyflow.so/blog/what-is-a-marketing-plan-complete-guide39  
> 15. UniFida. (n.d.). *How to measure the success of a marketing campaign when you don't trust the data*. Retrieved from https://unifida.co.uk/uncategorized/how-to-measure-the-success-of-a-marketing-campaign-when-you-dont-trust-the-data/29

#### **Referenzen**

> 1. Leading vs. lagging indicators: Experimenting to find the best predictors \- Statsig, [https://www.statsig.com/perspectives/leading-vs-lagging-indicators](https://www.statsig.com/perspectives/leading-vs-lagging-indicators)  
> 2. Leading vs Lagging Indicators Framework \- Umbrex Consulting, [https://umbrex.com/resources/frameworks/marketing-frameworks/leading-vs-lagging-indicators-framework/](https://umbrex.com/resources/frameworks/marketing-frameworks/leading-vs-lagging-indicators-framework/)  
> 3. Marketing KPIs That Actually Predict Revenue \- 23HubLab, [https://23hublab.com/marketing-kpis-that-actually-predict-revenue/](https://23hublab.com/marketing-kpis-that-actually-predict-revenue/)  
> 4. KPIs Explained: What Are Key Performance Indicators in Business?, [https://www.europeanbusinessreview.com/kpi-explained-what-are-key-performance-indicators-in-business/](https://www.europeanbusinessreview.com/kpi-explained-what-are-key-performance-indicators-in-business/)  
> 5. Leading vs Lagging Indicators Explained \+ Examples \- KPI Tree, [https://kpitree.co/guides/core-concepts/leading-vs-lagging-indicators](https://kpitree.co/guides/core-concepts/leading-vs-lagging-indicators)  
> 6. Marketing KPI design: 5 metrics that drive decisions \- RevenueScope, [https://www.revenuescope.jp/en/news/marketing-kpi-design](https://www.revenuescope.jp/en/news/marketing-kpi-design)  
> 7. 6 Misleading Digital Marketing KPIs & What to Track Instead \- Funk/Levis, [https://funklevis.com/6-misleading-digital-marketing-kpis-what-to-track-instead/](https://funklevis.com/6-misleading-digital-marketing-kpis-what-to-track-instead/)  
> 8. 7 Steps to Measure Marketing Performance in 2026 \- Improvado, [https://improvado.io/blog/steps-to-measure-marketing-performance](https://improvado.io/blog/steps-to-measure-marketing-performance)  
> 9. The difference between leading and lagging indicators \- Mercury, [https://mercury.com/blog/leading-versus-lagging-indicators](https://mercury.com/blog/leading-versus-lagging-indicators)  
> 10. Marketing Attribution Models That Actually Work for B2B SaaS and Why Most Don't, [https://www.growthoptix.com/blog/marketing-attribution-models](https://www.growthoptix.com/blog/marketing-attribution-models)  
> 11. 27 Marketing Communications Performance Indicators, [https://www.emercury.net/blog/email-marketing-tips/marketing-communications-performance-indicators/](https://www.emercury.net/blog/email-marketing-tips/marketing-communications-performance-indicators/)  
> 12. 23 Marketing KPIs to Measure Campaign Success | ActiveCampaign, [https://www.activecampaign.com/blog/marketing-campaign-kpis](https://www.activecampaign.com/blog/marketing-campaign-kpis)  
> 13. Marketing Dashboard Design Framework \- Umbrex, [https://umbrex.com/resources/frameworks/marketing-frameworks/marketing-dashboard-design-framework/](https://umbrex.com/resources/frameworks/marketing-frameworks/marketing-dashboard-design-framework/)  
> 14. Stop Tracking Vanity Metrics: The 7 Numbers That Prove Marketing Works (2026), [https://humblytics.com/blog/how-to-measure-marketing-effectiveness-proven-strategies](https://humblytics.com/blog/how-to-measure-marketing-effectiveness-proven-strategies)  
> 15. KPI Examples for Marketing Teams \- Talstack, [https://www.talstack.com/blog/kpi-examples-marketing-teams](https://www.talstack.com/blog/kpi-examples-marketing-teams)  
> 16. You Need a Marketing Measurement Framework \- Kard, [https://www.getkard.com/blog/you-need-a-marketing-measurement-framework](https://www.getkard.com/blog/you-need-a-marketing-measurement-framework)  
> 17. Vanity Metrics Are Killing Marketing ROI: What to Measure Instead \- Trade Press Services, [https://www.tradepressservices.com/vanity-metrics-are-killing-marketing-roi-what-to-measure-instead/](https://www.tradepressservices.com/vanity-metrics-are-killing-marketing-roi-what-to-measure-instead/)  
> 18. How To Measure Success of a Marketing Campaign With Metrics | Indeed.com, [https://www.indeed.com/career-advice/career-development/how-to-measure-success-of-marketing-campaign](https://www.indeed.com/career-advice/career-development/how-to-measure-success-of-marketing-campaign)  
> 19. Leveraging Data Metrics to Optimize Decision-Making in Agile Product Management \- DiVA Portal, [https://www.diva-portal.org/smash/get/diva2:1970878/FULLTEXT01.pdf](https://www.diva-portal.org/smash/get/diva2:1970878/FULLTEXT01.pdf)  
> 20. Leading vs. Lagging KPIs: Understanding the Metrics That Drive Success \- KPI Zone, [https://www.kpi.zone/leading-vs-lagging-kpis/](https://www.kpi.zone/leading-vs-lagging-kpis/)  
> 21. Beware of Misleading Marketing KPIs: Measure Success Wisely \- Borenstein Group, [https://www.borensteingroup.com/latest-insights/measuring-marketing-success-heres-some-kpis-that-might-fool-you/](https://www.borensteingroup.com/latest-insights/measuring-marketing-success-heres-some-kpis-that-might-fool-you/)  
> 22. What are the leading vs lagging indicators in marketing? \- The Pedowitz Group, [https://www.pedowitzgroup.com/what-are-the-leading-vs-lagging-indicators-in-marketing](https://www.pedowitzgroup.com/what-are-the-leading-vs-lagging-indicators-in-marketing)  
> 23. 13 Critical Marketing Goals to Achieve Your Objectives \- American Marketing Association, [https://www.ama.org/marketing-news/13-critical-marketing-goals-to-achieve-your-objectives/](https://www.ama.org/marketing-news/13-critical-marketing-goals-to-achieve-your-objectives/)  
> 24. What the Attribution Smackdown Revealed About the Future of Growth: 10 Takeaways That Are Redefining MTA, [https://www.attributionapp.com/blog/attribution-smackdown-10-takeaways/](https://www.attributionapp.com/blog/attribution-smackdown-10-takeaways/)  
> 25. What Is Marketing Attribution? How to Get Started \- Invoca, [https://www.invoca.com/blog/what-is-marketing-attribution-basics-benefits](https://www.invoca.com/blog/what-is-marketing-attribution-basics-benefits)  
> 26. What Is Marketing Attribution and Why It Breaks | Winston Francois, [https://winstonfrancois.com/blog/what-is-marketing-attribution/](https://winstonfrancois.com/blog/what-is-marketing-attribution/)  
> 27. Attribution Deep Dive Series Part Two: The Pros and Cons of First-Touch Attribution, [https://www.channel99.com/articles/the-pros-and-cons-of-first-touch-attribution](https://www.channel99.com/articles/the-pros-and-cons-of-first-touch-attribution)  
> 28. Performance Marketing Report: Attribution, AI, and Ad Spend \- Trackier, [https://trackier.com/industry-report-on-performance-marketing-reset-today/](https://trackier.com/industry-report-on-performance-marketing-reset-today/)  
> 29. How to Measure the Success of a Marketing Campaign When You Don't Trust the Data, [https://unifida.co.uk/uncategorized/how-to-measure-the-success-of-a-marketing-campaign-when-you-dont-trust-the-data/](https://unifida.co.uk/uncategorized/how-to-measure-the-success-of-a-marketing-campaign-when-you-dont-trust-the-data/)  
> 30. Attributing AI Authorship: Towards a System of Icons for Legal and Ethical Disclosure \- Scholarly Commons, [https://scholarlycommons.law.northwestern.edu/cgi/viewcontent.cgi?article=1386\&context=njtip](https://scholarlycommons.law.northwestern.edu/cgi/viewcontent.cgi?article=1386&context=njtip)  
> 31. How to Conduct a Marketing Measurement Data Audit (And Why Most Companies Fail), [https://unifida.co.uk/uncategorized/marketing-data-audit/](https://unifida.co.uk/uncategorized/marketing-data-audit/)  
> 32. Email Marketing Agency Report Cadence | CFO Guide \- Sidekick Accounting, [https://www.sidekickaccounting.co.uk/post/email-marketing-agency-report-cadence](https://www.sidekickaccounting.co.uk/post/email-marketing-agency-report-cadence)  
> 33. When to Review KPIs vs OKRs (Weekly, Monthly, Quarterly), [https://www.okrstool.com/blog/review-kpis-okrs](https://www.okrstool.com/blog/review-kpis-okrs)  
> 34. Best cadence for business reviews | Weekly, monthly, quarterly \- The Pedowitz Group, [https://www.pedowitzgroup.com/best-cadence-for-business-reviews-weekly-monthly-quarterly](https://www.pedowitzgroup.com/best-cadence-for-business-reviews-weekly-monthly-quarterly)  
> 35. 4 Essential campaign KPIs to Measure the Success of Your Communication \- Onclusive, [https://onclusive.com/en-gb/resources/blog/4-powerful-ways-to-measure-communication-campaign-kpis/](https://onclusive.com/en-gb/resources/blog/4-powerful-ways-to-measure-communication-campaign-kpis/)  
> 36. 6 KPI Red Flags That Signal Your Marketing Campaigns Are Failing, [https://blog.hurree.co/kpi-red-flags-marketing-campaign-failure/](https://blog.hurree.co/kpi-red-flags-marketing-campaign-failure/)  
> 37. Marketing Automation KPIs & How To Measure Them \- Braze, [https://www.braze.com/resources/articles/marketing-automation-kpi](https://www.braze.com/resources/articles/marketing-automation-kpi)  
> 38. 5 Common Mistakes in Setting Marketing Goals and How To Avoid Them, [https://thriveagency.com/news/5-common-mistakes-in-setting-marketing-goals-and-how-to-avoid-them/](https://thriveagency.com/news/5-common-mistakes-in-setting-marketing-goals-and-how-to-avoid-them/)  
> 39. What Is a Marketing Plan? The Complete Guide (2026) \- Storyflow, [https://storyflow.so/blog/what-is-a-marketing-plan-complete-guide](https://storyflow.so/blog/what-is-a-marketing-plan-complete-guide)  
> 40. Falsifiability \- Wikipedia, [https://en.wikipedia.org/wiki/Falsifiability](https://en.wikipedia.org/wiki/Falsifiability)  
> 41. Falsifiability rule | Religion and Philosophy | Research Starters \- EBSCO, [https://www.ebsco.com/research-starters/religion-and-philosophy/falsifiability-rule](https://www.ebsco.com/research-starters/religion-and-philosophy/falsifiability-rule)  
> 42. Three Focus Failures and How to Avoid Them \- \- Taylor Pearson, [https://taylorpearson.me/three-focus-failures/](https://taylorpearson.me/three-focus-failures/)  
> 43. Vanity Metrics Defined: 3 Examples of Vanity Metrics \- 2026 \- MasterClass, [https://www.masterclass.com/articles/vanity-metrics](https://www.masterclass.com/articles/vanity-metrics)  
> 44. False Marketing Metrics \- Smart Insights, [https://www.smartinsights.com/goal-setting-evaluation/goals-kpis/beware-of-false-metrics/](https://www.smartinsights.com/goal-setting-evaluation/goals-kpis/beware-of-false-metrics/)  
> 45. The Art of Copywriting: 3 Rules From Harry Dry That Make Copy Stick \- Sproutworth, [https://www.sproutworth.com/art-of-copywriting/](https://www.sproutworth.com/art-of-copywriting/)  
> 46. Measurement Marketing Audit Checklist – 10 Steps to Take When Starting a New Project, [https://measureu.com/measurement-marketing-audit-checklist-10-steps/](https://measureu.com/measurement-marketing-audit-checklist-10-steps/)  
> 47. Vanity Metrics in Marketing: What CMOs Should Measure Instead \- Objective Platform, [https://www.objectiveplatform.com/blog/the-measurement-mess-why-cmos-struggle-to-show-marketings-true-value](https://www.objectiveplatform.com/blog/the-measurement-mess-why-cmos-struggle-to-show-marketings-true-value)  
> 48. What Is Vanity Metric? | Business Performance Glossary \- Enji.ai, [https://enji.ai/glossary/vanity-metric/](https://enji.ai/glossary/vanity-metric/)  
> 49. Vanity Metrics vs. Actionable Metrics \- B2B Drum, [https://www.b2bdrum.com/blog/why-vanity-metrics-are-killing-b2b-growth](https://www.b2bdrum.com/blog/why-vanity-metrics-are-killing-b2b-growth)  
> 50. How to Conduct a Market Feasibility Study (2026 Guide) | August Brown, [https://augustbrown.com/news-item/market-feasibility-study-a-complete-guide-for-2025-and-beyond/](https://augustbrown.com/news-item/market-feasibility-study-a-complete-guide-for-2025-and-beyond/)  
> 51. What makes a good Marketing Audit in 2025?, [https://www.consortiumbiz.co.uk/what-is-a-marketing-audit/](https://www.consortiumbiz.co.uk/what-is-a-marketing-audit/)  
> 52. Setting Marketing Goals: Crafting Strategic Objectives for Digital Campaigns \- IDEAS/RePEc, [https://ideas.repec.org/h/spr/sprchp/979-8-8688-0546-2\_27.html](https://ideas.repec.org/h/spr/sprchp/979-8-8688-0546-2_27.html)

[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAmwAAABhCAYAAABrlP3SAAAZ1ElEQVR4Xu2dBZRtR5WGN2Eg2OAw2CBBgrtbmgTX4BpeICFBZoJrkEeQBHcdJMMgwd3lPSC4BddMsnBb6AIWsFgz9b06+9261ef2uy2vux/5vrX26nuq6lhVnVv/2bXrdoSIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiInKLYq9i+xU7fZ4isIxfoE0RE1ppTF/u/Oe1Fwz7rweOKvarYFfuMhrfH9PW9Yjp7iu0xXZbjr5ZbRj3OS4vdqMtbK/612NeLfarP2I3QJx5Q7KNR6+3Nxa4Z9X7vPym24Xw7Ju15sS5vd/DhWPxMjBnttV7sF7UPPrvYPbq8nktFfaayXY8sdqZi72zK7IrlnG+13KzYu4ptK/aRqOf7t2KvbgttMC+LSbuLiOxWzlXsiGJnHLavGvXL58s7S1TR8LZixzVp83C5YlfvE+fkG1GvY6FL7zlVVDFzUrHfxLin5ULFPhf1eC/v8lbDbaOem+Nu6fKWC3V8xz6xcP5iv496b3iT1oP/KfbeqNcEVyr2vWK/js0l2M5Q7CWxfoLtK1EFz/mGbfoe5z7nsI3QfUyxnw/by2Gs7edh/5gIyaVeQmjD3xa76bDNc/LUYr8o9rMsNAfznm+13KfYD4pddNg+T7H3R73eN2ShTQDP5L1DwSYi68Aluu3LRv3y+XSXzhc+b7nLgTf4lQ7wt475BBswgBwTtfzYwPeoYg+Nmv/cLm+1XCHWRrBdP2YPRFeOOlCuBynY6Qct+xT7U6y8PXcXh8bKBNuxfcIcICDO2qVxbrxUyWmiCiDE23KY1fbzcJbYtYDCGz12jhfH8gQbzHO+1bB3VNHb9zVE5hdi/D42Er5DFWwistu5drc9S7BB63Wbh0/G4i/debl5LE+wXSVq+bd2efCOqMfZHYLtMrE2gu3JsTkGovtFvZ/z9hmFt8TK23N3cUisTLB9oE+Yg2/2CbFYsAGeoHN3abtiNW2Pd3xXAuqnMR7SwIvYcgXbPOdbDflM3aXPKDwwVldXu4OLh4JNRNYB4kRaLh2zBRvCaF4OinqclQ7wN4nlCTY8H8cX+3uxs09nx9bYfYLtkrF6wUZsEd6rWQMR3ho8eesBcULcz+F9RlRxdFifuMHkdNRyBduH+oRdwPQr8VQ9Y4INYUS/mBfaf1bbz8PpYtcCini/78d4yMDn+4RdMM/5VsO/Rz3+a/uMqOKIKfvNBH1PwSYi685Sgq3ltMWeFNXrti1qIDPTacAXKsdoDUGSsKKKmDjOwTQr8VK9sFuJYHtQjIsNBs+FGBds+0Xd/+NR74EA+wOafOKTyP9EsQ9GvV68M2cb8nvBduywnXbdIZ14J6ZmiYPiOBnojQDq6wojyB+YGsq0hEUOfxzSLl/sYVFj/o5qyiR4UF8fVaBQ59Tz1mInDnk954gaL4fwpR0RcGPig3shpo1rwOvxjGJvKvarqHXYrpqjbbjmE6LWJXFnObXIlOYvox6HazswquBBYLyuKQfE1BFDRjzd+6IGnyMa2He5gm05Lx9Lwbl7wdaD0CXWEY8zfZ6XmWSs/bPtgb7MfvRN+iD3z/R0yzwC6olRy3w3atvdIOp+Pf9S7AXFPhO1rz89Fou8WeejLyJquddtUfslMV5A/6fPk0cdYEytzmJ71HN8LKrXl++WPBbcMGrcKmXoByySIcaW++PaCTFoGXv+6NeEGyBkOQ6imXug/302ah8jv4fj4G3dHnWqOV9yRETWlRQgSwk24nS2R12VmbE6xFgRHJ/k1GovxOCxUfPuNGwz/fbnmB7IViLYCAZnHwa3hC9qWIia1ws2hAziJAPJEQx/ifomDwxOC1G/wJk6enTU49xmyO8FG2KP4z0ypqfFqCuEKZ4aYAo0F3oAxx7zspy52BtjekBgEGEgJW171IUdtxi2GXCSO0e9FjwWuU2ZK0YVcbTZGAzmKcbSEGL3bMpw3/855LEqMgXaRYqdXOxbwzb1h1BLMbl3VMHLQAeIjxzwvhQTsY1Qpk9wDqCf0Se3xaRe+cu52XezCrajoy54QQgD9UQsHGKmZaztec7oi19t0p4dtW4RVsksAdVCvXOOtk2xd8e0R3q/IR3RBtR5v1Bn7HwsMELoZ586f7EfFXvIsL0w/IVLRH0RycUaY9BnEVfttf6t2LOiPtMsQrhR1Pr5XUzOi7hEaP0hpsXW2PP346j3Tn/nenhJeGHUegfunZeQlmdGnV7OY9Mvs15FRNaVeQQbIowyLLFv4Ysrv+yWEmwMWkfGtPdk22DJSgRbfma/FCn5Rb4wpPeC7XoxEQXA9VMuBUaSXkOEHaItB+msr3tHrY9PxOJp5gzkZ4BJGHDYJ5kl2ADvVT8g3G5I41qAc7fbgChiZWDC4EQZBv1dceGo3kIGMvbB/hHTXrls4yOaNMBrltfLYg8G2lacpnC86LCNmGGb2K8WhEqm3TdqmfTiJggC0jejYEM8k3/7Lp1nAjHaXvOstkfM3qrZxrPEMfmbjAmoWVCPx0cV8tmuiLaE/s/LRgp/noO/xrSXbex874j68tCC+Dlx+PycmBaZxJq2z/8YiCsE79dicq1YK3Z5bvDotiAIKfeeYXvW80dawssCwo97SxCt9N0EUco+KUKTPL6IyLoyj2DjCz+/iFseH5M3z6UEG+wbVbAcE3WlGtMS7aKG5Qq2nKI8LOp+KVzSO7AwpPeCDZi2RHQ8Lyaeq74cgq31ICZZXw+POi3J7zL1PC2mB5y0pzZllhJsuX8LHj7S8KwB3gq220GUa0YYJNQRZbjH5XDpqCKPfRmYkwwO7wUbYjmvl37U33faTYcyDNxsc58t9IcUVgzwlNlrkr2DeQTb82PxuWfZ9rrL3LDPLMGG2CA/hWmCR4f0BzVps9oez9jNo4oonpN8cWhF4JiA2hWIIfoOU4jse7UmD88lAf9PiOqtJr/1hvXny0UIs+y0UT3QnAsRxX1zX8vhXFGfbUIr8OQleLt6wQZ4yyiLN27W84cln4/F33l8B7RluG6225AJULCJyIYwj2DD64LA6mFQudvweSnBdo2oeQzGvA0Dn5kCSVYq2PjLWzExJngL0kOzEPV4vRDLn/vAi4UHKn9bC/HWwkB5UpcGWV94svCu4Y0grYUBhTL9wN2ylGB7SiweEG45pFFPkIIN0ZwsDGmUhcOjtt1S14GIGottA+6P+LEk770XbEwT5fUylTom7luITaM899nSCrYTYlp8JvMItjHWw8N2XNR8polbrjWkv6RJm9X2xFrRnw+KKpRS7N2hKdMLqDG29gkD+ZxtGbaJK2Mq84dR+wH9iXwEU9Kf74rD9qt3llgMQpv2oxyGQOI4YzCdSl8do38WuNYxwUbsG+V4LuZ5/j4TtX+3pGDLsIoU/rRfi4JNRDaEeQTbF2P8pwCYPslph16wPSKqpwD4YuQNOH+YFXiTZ+qDwY/Bd7mCDbGV4AVi38dEDUaGhSGtFWx8mf8hanB7kmKD6RymbtOzgGDDQ9CT9cXbN9OSHI+g5hY8I5RpvRg9rWAj6PyYJg9PXD8gZMxaL9i2ZoGoP3VCkDr18YuocWspkGdBO2FjcB/ETyWzBNs+QzrgdfxdTAa9MWhzyo8JNvoF5FR3HwC/mQVbeiV5FlpyWvNJTdpY2+czcN9hG/Yf0phW5rhMM/YCagzafwym+Nn37sN2CiKm/2DrsM0UIsIM+vPlMVrva0++NOB95Vn5R7F7TbKnoA7aadqWu8akb8EswUacIEJ375jv+eP7bpZg4zsBuF+2ealpUbCJyIYwj2DLwPv2rRteG3X6A/aNWuY/hm3EE94B3uBJRwC14F1DsPG7UEzZIe4ot9CUmUXrYQMGH/ZFPDG9AwtDWivYDhzS7tOkcU+kIdhY/ZgDDffWepeSnBbMKSrEC9s5AEIOsv1U5IObz3g0WFwA14tpTxkDeD8g5JRoL9ieuLNEvf723uYBsYZ3csz7sb3Ya5rt7CtMB7cwdZXXu3X4nPWY0B9y+vysUcuMCTY8JcBKQcpcfJK9g4cN6ZtRsDHVTv4du3S8R6S3nsyxtk/Bx7OU4FkjDcH2lqgvPTkluZRgY3rw4D4xJuKRtoQvRO2LCZ5m8hFsWWdj50NY87ydt0kD7gtRSdB/Cy81rLYcA8H2l1jsqQZeCk9uthFs72q2gSl8ri8Xtsx6/mifBI/fLMHG9UO+hB6ys0Tl6kO6iMi6koHSeNFmwRf2x6N6bxLeMhkUEr7kmCZ8ZdTpEL7Q+TLH08KXI+InPWy3jhofxkCBAOENnEGO60iv3Cw4xneieiHyePz9Y0yCjgHPH8dDiCVcD9d8XJPGIMm1INCeHBNRwdTUj7NQQ35Z5wpK7vXEqNOneBMSPCiUQ2gBAhOPXIJHAe8V07ictx3kCX5m33zTh4OGtJwau/Cw/cwsEPUYCGEGVgQSHo1Z050Jgu2XUVfHtdd/ZFQv4IWatBRstDODLNB/mAZlZSTQFtwXbZtiizJvGz7DBaMep52Gpp/g0czj0J8Qb22fwwNK22f9U/fzshaCLafPW+9uD/3phJgsukD40CbtfcBY2+cLRXqJiTtD6JCG6KPPcM+8lJDWemV76Oe8EG2JibeTtqT+js5CUa/37zFZdEBf5tg83whEGDsf3jfOQQhCvjzx0pLiE8GW3mruE48f4nQM+hLHp42u06QfEFUUtuIfwUbZQ6PeF21xfNTjt4Jv7PlLLx774fFvQzKAa2YfXjITXiq+GpP2xINHX6Zc7/0VEdkt5BffmPXB4MBAzBso++EJ4QvvtlMlqqggpovpiXYlJkKAL0NEH9MVxL7x5c2XMeKJgYk3bM7955g9EPEG3V9rwhf0vYfPfRksvQPXj3ocBkLE3N2iDoZcy9aYCKG0dqoGccN0H+nc50ujTpdkWa49PV54rIhZ4rgMnFxfC57Fn0QdIPFKMBAj0PB05vHIwyvwoqjnI416ek5MfssMo16BNkJ89vf+9Vgch5NwT7QjnkMEb/YL6qef2kvB9rKoXjkGvJ9HFR3tdDftzf4IgY9Evf4c1BloEXh5bdwv15ZCDGNaFc4cdV8WIHBOBNzLm3LU/7ysRrDhHe7rNK99DLzMCNbPRg2Sf3QsFpd92yf0YV52EEuIKeqGl4mTogo68hHSeQ2UHWNbVEHBuREciKu8lhRwQBn6LMchVADvHm3xmag/8LvU+faL2gfom0yP8lznsXm2SPtQ1J/dyBeNMRBs3Ct9hO+J70btOzw33HML/ZO2xMvGSyB96dgY/626/vnDE8cLF99deT/0Y+qYtso02obVukDbPDjqT4Tw3FFu61AO0S0iIrIs8GIwgDGo4NlKEYBXj4Hz+zGZvl4pKdiO6DPWkfPHtCdwXlYj2GTzMCuGbT3h5aT15omIiCwLPEF4NlphdoWoYiWnt1ZDTgfjpRFZb5gm/3Ws7P/CioiIbBoY0J4RdUoakYYxvXNUrN671k4H/yOWXiEostYQ65rxdRhTscRCioiIiIiIiIiIiIiIiIiIiIiIiIiIyCrJIF1N0zRt95uIiIiIiIiIiIiIiIiIiIiIiIisnAtE/ZdmIiIim5ZPxOwAYn5tvQ8wvv9UifWD/6d5ZLEvR70O/sH3XYe8xxS7xfBZVse7i92tT9xA+PdjJ0f9f7G7g+zX/NN3ERGRTc8Xi/0mFv+j8fMUO7bYR4pdYjprXfl7sWcVu3yx00f9t1T3K/bfUf911O0nRdcE/uH1HfvEf3LOF1W8rMX/YV0rPh/1mq7aZ6wRCDUFm4iI7DEwMD6k2Jv6jKhiCC/WRvG0Yof2iQOPjzrgrrVgu36xN/SJ/+Q8IGpd/jmqKN4MnKvYlj5xDeElRMEmIiJ7DAi200QdvPrpxY0UbAgnrulUfcYAnjD+SftaC7YnxylPsH242Buj1vedu7x/VphqVbCJiMgew+eGv38t9oOY9rAghogf2wjeEXVAXYp3xdoKtksV+1OcsgQbnqxPFrtxbL5p0YsUO2ufuEZcLBRsIiKyB4GHDZ4QdQB7TpM3y8N222Ifj+qZYfHCzYb0WxX7adTjPDzq4E8MGtvfGMpsG7aJm5s13UmcGt6zXQm2Q4pdp9iNopbFuB44U5OWx8FbR/zbO4t9qtinBztLscO68mnX3LFn5bTFnhT1Hj4a0/FV3Msvo+7DAo0Di72o2DeLvSDqvvtHPTdxg28rdukde1a4tkcV+0qxDw7lLjnkHRC1rmmro6KK6K8Xe96Qf45iW4t9KeriAfadl/sUe3TU6/tDsb/EbJF09agi+WvFjiv29qh1l7Af18S1va/Yg2LS7vO0Ee0OHDvTFoY0pu2/G9UDSB/9UbGDhzzg3C8tdkLUunrJkNZC/dIe24vdI+rxFWwiIrJHkIJt76geNgax6w5pCDYG85Z7FvvfYhcathEh7HOVYZtBGO9YgsDBa3W6YRthwnlasdJzmZgM2POyEFUwpRiAsxX7UEyOsxCT+wXimH5e7JxN2s9i3MPGtPH2Yq8Ytrnv3xe73rC9T0xEAMLp8CGdYxMbhghDUHAc6oAyrxnKAMd9b7EzDNtMzf642BmjLgBB8HAchMo1ogoizoVgelyxZ9bddiyYYEXtvHCcbAuuh2MevDN3wm2iLvJAhAF9g7IsCAF+IgNxtq3YXkPa7aL2lWQhlm6jFGyIRwR/K9gQr2zTftwzdZFtSd9CqCFmgb78gaiCMqF+eJm48rBNGyvYRERkj6EVMLeMOoh9O+og2As2xMNPooqwFjwur262fxVVmAAeOo6JJwwQdHhAlmIlgg0QQa0YgOfG5Dh4Zj4WE2EAb41pT8wswYbXjOO0v9tFOeoq7xVPF2Xev7NEhZ8iwaOIkEjwACFkAU8d+yHKEkRaLygQawgToD5TFHLfCLyElb3zcPaoHr0k2x/vXwv1dXJUz2DClCKi6CbD9uui7tsL8VawwVJt1LYL3tpWsAHbzx8+8xMkee6HFvtb1P6Z4Imj/EWLXW74jJcuyTpXsImIyB7BF7rtDD5/bCwWbCxKSCHVG3FQCdt4VwDxgqh5xrB9l2JHDJ9nwcCNwOE4S4F4IgYr+WzMFgOwZfjM1Np7onqLWhEFswTb8cVO7NJypWp6bRB+bLO6tQWP1/Yu7YVRRQZQvq/PtKcOZQDBhsDswTtH2TcXu1OXtxSIlfRKQU6L4r1qYVqY4zO1OwbtxVQqYqynF2xLtVEr2LKvLTRpbKeHr4Vp7b7e0m4adR8+M7WcKNhERGSPovWaJMR5MZgxXdgKNn6wlnQ8GkvBj54y9YUww1PCFB777R819mserhV1n6XAU8dq0QQh0ApHQGTkcfAg4QUDfneOgZxpvnsNadAKNoTKMcNn6om8FsQOx07PWMZkPWVniQqCDc9eC4Itr+vFw+erTbJHQbD9V58Yk5+/wJNEPsfCA7YU1Nv3YvEq3DvE4npn2pe0FN09CC3EZy/+oRdsS7VRK9gQWqQtNGlsMyXfw1Ts72LxvSRMGbMvx0wUbCIiskcx5hVh4GNgZUBrBRsepN9G9Wjs1aSzspQfsk1YlMC+34/qweJ4J0UdvNtpqV2Bd+nGfeIAU2K9MNoedTFBCx6+FCB4og5q8oDYMoLRkx9G9TICQgUvGlAPHKf16L02qicQzxSkh62/rl0JNoQsn58+yd4BsYQPbraJacsYuhaE1wWHz0zPsuL32pPsUe4ek7i3FtqLNs6YQ6D98Eq206eAwEoRR7wY93DuSfYOesG2PWa3UU4tw82HtIUmje0tzXayNWoegryF6Xi8n5eNmn9Ik8cCCgWbiIjsERAQT0wa05Q9+0ad5uoXHRwWE1GCUEG44SFCdCQIOKbW2qlFVg+yXwqLeWF67pExWY24T1QRRQxYO8ADgod4uoRFBb+OacFGfi4yYP9fxGThALDK8ltDHnFh+V8PiI9iZeyrhm08NMSgHTxsA/fGuXL1JqTYyZ9PSY6NyXUBdcU2wf1AMD7XkjFziCPuBZHYg2DLuua6KHfmSfYiaFvi6qjXMZguPrBLw9uIOE0BCwhdPHJA3CGLMF4TEzFPXi/Ylmqjtg8xtdunsX14s53gLaTNENsXH9L4zxhtLB79lXvOODfyOB7evc3yY8EiIiKLSA9a2hhMB/aCDZhKZMUd0554o4g36kEc4WlLmBYlSH25IC5eH/Ua/xjVI5bB5j0M3K+M6pljYQSxYXxmX+4Dr9YDo65iZWUiKyRTcCRXiipiiVfj3lpPIscn3gqPGXF57f0dGnWxRdYnXkimdb/TpDF1RxpxXJnGNDPg0UKEInQRNAiwDODfEtNthT1iyAPqhOln/nLNGVM3RsbdpbFyNWEaFeFDOm3LlDPXmzDlynUx9Xl0sRs0eYBHkHpBGB0X1aPVC7al2gijnVhYwMsC23j7WPCRcXppCMgWpri5f35GhkUX/KQKojehHfFWshKXxSdbY3Is7llEREQ2ELxe5+sTZd3oBdsYG9FGCEd+KuTUfYaIiIjIKY15BJuIiIiIbCBMnevFEhEREdmE8H9AiWUjRozVwjeczhYRERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERER2Vj+Hx2WNQ4pOgPXAAAAAElFTkSuQmCC>

[image3]: <data:image/png;base64,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5Z1k+7dEvS/2kmVXc/ICbh3zE4QW+v3mqCs+9P/C+WqR/eVoVGdFBi5nL/wX540R9DPOgwizZGbEq4IDPqMv3Af22r+DwtHYPB1nMkF/CDYOMhmwifQcjZ12ezJsFp08pS9seETUye7TYn4rj8i+c1WRb+0LB5hdszQiq0OWhSyEXPeo45sLWScDNhljym7322b3mkkV2XdIK5Puz30PQJqcdDkGw3KArA57ZhYtUcnJQx3fXNgfxvLbQc80yk7G7FablQPPeVF/QcR+AfYqvD1qOtpltr1zSdQfBMhmoI5vFuy/IwOd+4oYhO8/10Jkp90eDW1WRNYMP54QERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERER+eji/wHHrjm4y4SZPgAAAABJRU5ErkJggg==>

[image4]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAmwAAABJCAYAAACAa3qJAAAT5klEQVR4Xu2dCbBnR1WHj0FcUBZRAgjKaCRgQAiiomKYRyKiiGIAo1LghMWIghBxARFxiAurG4IgqHkGkB0liMSVIQQBRVFBIBKclMoqhSAlFFKU3m/6ntx+/fr+l8l7k1m+r6or7/bt27e7b/fpX5/u/yRCRERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERERA5x8yHcuI2Uo5rrDeGUNvIY4Fgtt4iInKDcfQj/1wlfWCfaZX47pvc+qLmXPCq2lu/dW29v4xdia/rd5rpDeNsQ3tDe2EX+N7Z/N8LHh/DnQ7jzlHTHuX9M79vcemspJw3hZ4bwN1Ha7JFDeN4QrhzCLadku0aWfbOJr/ml2N6uvXDffECOeS6N7d+3F/46Hxh4+BA+OIRzqjiJOBBTe33j1ltb+KYhvG8IT2tvXA2+YQhPH8K/R3n/nw7h66LYnVcN4fpT0lmOpD2yD8na0LFf0kYeIRhICDXKMCfYkicP4WCUtIsEyYujpHlnlPx3ku9tIwZuNoSPDeEjsfPvW8RNotTzs6u4L45iMD8Tuysobj+ET8Ri4dPj8UP41yje1H8cwiejiDfqgWE9Eqxa7t+JUq4faeL53vTVH2vi5fC45xBObiOvARi72Ay+eTtZf1mUifw9VdyvREn7E1WcRHxOTIueRYLtXlHS/FF74zD4/ChjmgUr45Xvh138oiH8epT5jXd9yZh+EXP26GuiCMKdxD4ka0OHuaiNPIKcGqsJtp8bwpOipGUV1eObo3R+0vx9c28neGEbMfK1Qzizjdxl8IRSz5YvjxL//iF8VnNvJ7kyVhM+CWX5UBQPG3zXEB4whBsNYV8mOgJcGauVG0NPO+KV6/HENkIOC7wgt20jV+SnhnC7NvJqgM3gmyPQWpj8WZTlmEIQPDSKWJCt3CeWCzY4O67+8QS+w2VD+NQQbtPcA4Q4uw6rCrY5e/SzQ/jRNvJqYh+StaEjb7aRRxBWQ6sKtu8ZwhVRJv5rb719iN+MYmyPtGC7JpgTbPDhKPd2ekVYczDW6zd8L8r0iPbGEWbVcqdgQ1T2eH4bIWuDRxjv9OEKtgtiuShYh0WCDS6Jo8MbeLRz71hNsO0Ej43yrkVbqxuxumCb4/Wx84JNZG3oyBe2kUeQr4rVBRtudDwbpGcrpeZaQ3jZ+PduCLavjnnBxrvZJjySzAk2PABsNXLvLs29nYStzc02cgGfF/OC7SuGcIM2cpdYtdwp2PZVcacN4dnj339Zxcv60E+fG6WND1ew/WLsrChIwXaLKm5jCHvGv1kQ1h49vG5z4u5EJrc7l30bPEu3aiPXBK8n71r0HbDPLAxWFWytPWLRxjt2Q7DZh2Qt6Ii/10bOgAv7dVFczJcO4Tuqe7h33ziEvxjvPyX6rt7HDOGfo5y1+sOYDoKvKtjYfiR96+G4RxT3MvQEGwOQyfYfopTvWWNcwgRC2d4aZZvmlUO49XjvvCh51iGN0QequIT3cJ6COAz8T0Zp47dH8QrUsI37B0P4syG8IopR2B/lvAz35pgTbIgK4v8jynmSs6LUl7MZvBvXPgf+fyMfiKnubb0TfqDC87Qp3+wHoy986jau23dfbG8/zrm8qLreGNM+JIoHlTjaAq8qZ4teENtF3bJvCm3Ze+Xu0RNsj4tJsCW98j4z5sv8pVF+bPOaIfxJlC18xlKeidsbpS6MM0ThS6N8w5ZePrRp5rOoPzOG+PEOZWYRQh+lzIzfl0cRKIQDUcYz465lzhbM5U0ZuZfkwfA6cDB8HajvMlGwDinY9lRxvxZT39wT5Xs+LKYyY5dg0Ribswec40wRwEKG+mMbW7vJOObHVJTvtVH6RXvGCs6NYkMoy2aUvvCuKIvbReWDH47iRSJvvifl+8rq/sEo5b8wSv0Zu5dH6TPtwvA7o6TlhwXnR+kHb47pOATnwbL9KFcNdSUdtpI+c0nMH0sA8vjvWH78g7p+QSy2hz17xNnFjMvwP+O9hG96cZQfnvF9TooiDnNsMP6+P8pYoj6ItF4fAv7FBL4hP3Ah/W6IRDmGocNwwHoZOUnfYrw+M8qzdxyv90ZZgQLbX3S454zXCW5rfhmUhpuVD4OZfFYVbMBgxgAiWpILowwEIL9asOHdYVJPsfS5UQYOE3hCG7x6CNcZr1m9I3oY5EnPw3a9mH7okFC/p4xxB2LamkxDxgCH7xvCp2NaYXHN/dOjiDjaeI5WsGGw8PJhJPgV6beP8TcZwt2iHLZnkrxTFEPIs9cf02Tdoa03AoQy1kaTiYDnN6u4to3b9k0PW22cMM6cQyJ+Y4xjkkgR/3dRJhKMH+WvD/q37+t9017Z23LPkYKtDa1g65UXemXGm8x2dZaH84Z4Q5mgfnyMQ7hTZgQZUAfS3HK8hrl8eFfms6g/33AId42y2EBYPiOmIwaM27fEdBicdmDxwIIsWWQL5vIm35eM6RMmI547XA/bbgs2xja2ZmO8Thhr3xJb+/OiMbbMHvxxTPbvplEWAQltdyDK98ReAu39sSGcMV4DgoOy5nei3Q9GsQcI9UXl4x30HwRk8qtDeEdM+fE8aT4ak11CWJIPgqkW41kvvnnWFdFI3GnjNf0bYV8LNuqHaES03niM45swHtg+70Geta1fxiJ72LNHQP8krieeEJ8fialNbhblXzbAPm0M4U1RzhMzLhnn5MM81utD8Lgx7pzxmnLi4RM5BJ1jmWDDyL83yiqv5p9i2k5l0KcQASZSDoLmajFXVXTmGlaKxKfBmqMWbI+P8sy+8Rrxktuh0A5ivA+ImFp8pTg6JaYyMJATBnZbrp5gg6dGSVtz7zEuV5WAEarjEBf/Nd0+NNlxH2O5jBRsGfg+rGIvir5nDuOEwIE7xyQs2rrX9caAMVnXIijBcG9W120b1+0LPcEG/PiA+I0qDuNM3GuqOCaT+rp9H9TvnCt7W+45UrDtq+JYcLSCDXrlhbbM9H3S5SIHEEc1TMK1yGNc8UwKU5jLJ/Nqvyn0+jMCk/bg2yQsukiXQuh+zfUqtgDavMmX71VztAq2NmxUaRLEHPfq/jw3xmCRPXhVFQf1dbZRCpgEW/TOmIQ2Ag7PTHJ2lOdqFpUP8c9YTL41yvP8N0F4vLS6hlOjpEN0JinYenWt4xAztWB7aJQ0tFWCrf/92LpgqCE9Xr51mWuLnj1aJNhY2Bxo4rA7yfOiPHtyFJFK/bHd0OtDN4/i9bvBeP3aMYgcgg4zJ9gw+HSgHIC9wIoowe3780P4rSiude7jaYDzx+uzxutkHcGGtwGYkHmGlRFgbFj1J9yrBRsrvbbcGfBEPbkTn+GXY2JOsOXzNYhL4mi7hLYgLgcog5kVVIKHkPusxpeRgm1VMFAvbyNjvu7Um1Uzfz/hqtQTrfCZa+P09M0JtuxbG1Ucxoo4ypbwPWvjPve+fOdc2dtyz9ETbPTVFGz0udPHv3vlhbbM50VJx1ZR8rfV3wkr70dE8ZqkZ4byJHP55MQ1900JdX9mW4h2rMl6I3ghRTBlglVtQZt35luzjmDjn9Rp3zcXEIY5Ka5DCrY94zXeLoTnxnhdk+OvFWy9MQaL7EErfmuRf1lsFQBJLlrTs/W+2CqasJXcr1lUPjzU9xjCo6PY7xQa96nS8I5WsAHCkW3C3JbMPtKra91e9I96fCBUSdOK00WQHk/dMm4VW3+oNtcWPXs0J9hYvNT9rg45fmhHxHSPXh8Cysp8+KQodVvHgyjHOXSYOcH2rigesh+Ikg6vxhysdvGiJfujPMPKnomNTsl1TuDJOoKNVWNCWbKzt0KK+LqTs1XARD13zgEDxTNf395oyPewqmcwJUyCPF+TA//uVVwarf3jNR4SzoqwSvtglG3QU8d7yzgcwfbcNjIW130jyr16kk9a4bOsjelHPeNEfyB+o4rLutGnEr4ni4Bk2fs2ol/2ttxz9ARbDYIkV/298kJbZtqASYI253tztqXtH2wvvaCKu1aUvJ8RZfFEmmX5LPqmNUyYlzZxWe+sWwq2veP1KrYA2rwzX+qTtIKNCZtJcFV2y8O2p4nv0evPc2MMFtmDdlHBtniC1xTPVgseV55NLypbbsTR7gejeOlb0TpXPspEXni4kjPHOL5/fh+e7wm2K6KIZEQffHfM13V/FYfArwXbJVHS4HlaldzCTA9Zj+vG9rNyc23Rs0etYPvpKOIWjxnx2O85EGyXt5EjvT7EmEEAU2bAfuC95ltyFEJOcOgwPcHGgP3w+DceBLbuMAYnXZWidDjc1dB6CvAOkDeCjcGSnf7BdaIoZxyIX0WwsWpMmLx4Dg9VvQoE4mvBtn+Mu2cVB4+N6d9Q437r2cKrkGeC4MXjf8+IssJNEG88X5Mr6p7RSgP9yCH80HR7LdYVbJxfmvvObd2z3kyubH/lN675eGwVPvtjextn+0KuRlvBhuEjfqOKo78R1wq2v6qu98f290G+c67sbbnnWCbYmKSSXnmhLfMdohjwOejf5FP3iRuNcQg2+gv1XZZP75tC258RnasKto3xehVbAG3ebb5APYm73XjNhF0LumXslmA7pb3Rodef58YYrGIPklpc5Lkn+kHN86OcnUpPzsti+S8u58qHuOMd9fP3HeP4/uQNiJyLr0pROC1KuvroQW7/LqvrG2JrXfdFSdPa8wfE/D9RRH85EMX7x5zQ4zmxtSww1xY9e0S7EPfw8Robc9fxbwQViyy8sQnzRPZzvtO/VPdq2j7EeUKu67H91iiCjTHfjmc5AaGDXNTEnRVlsntHFXdelLQYSYwExpqVPJMDMOjT8GLw3hMlPR60HPA8y7meXEWzInvFmI4zLhj9HnhRXhhl4CEAEwYLorI+g0PZyI9OnrBaoS7/FtPhbcrKuxPy57k8J8f2JCv+2j1PHteOcoCbLZqEsvNsPdlgZIjD8CV7xrinjdfkwYBkwGIEHhj982c9bhglr7k2q8F40E4Yjx5Zd2jrzYqT7Y5bj9fwmCjpL4tpy7tt47Z9T47yzAVVHJwzxmc/Ag7RE4foB74/q9Q3X5Vi+/ugfWev7G2550gv1UPaG1F+aFBPNG15oVdm+i7bI4h9vjkejbtV9zH6lPdFVRzjimf4dvQ7xOhcPunhgGX9mfKxkqf/1TCJ8RyTBzxovGYiS5bZgl7ebb6A2CLu3CjnAN9U3VuFnRZsHHanPIiQZeSZrP3j9bIxtoo9ANoOMZxgK18XW3/Jj02ln5xbxT09iqeH/oAHCE9oLcAWlS8XCg8br68TxWtLHJ4r+g0g2HJMUE5sEGMJL289xrKutfDaM8ZlXXmeuQAbnlBGxMqVMf0QizFBmWsb34INvDCKaKPe5IMtPj2Kt/rBU9JDLGqLnj0iPYuU343S1ylzCjTewbdgG5sxBvVi/pVRxGGPtg/RJix0EHjpYWOcY+MQnOePcXICQgegsywKtXcA6DAMig9FWUXUZxQYNHRkBsgToxgLtlTfGOXfMAM6Oyv8V0f5uTwGen9M76sFYvKo2F6ujfEeLurN8W/4aGxPm2AAMEKfjvJz6WfGNMAAg/CsKKslxB4TXmu4EbEIUepOXTAKGNd8F/fwYpD3p8a4T0apK4aPdqvLxaBkQLZlfltsPZ/UwvZDnb7Xbsm+2J4/Br0m6z5X72+L4v1APLw+yqHYuq1zZVu3cd2+TPrvj5L2M1GM0t4okwztQzwGke/JZPCfYxyB9qUf5fXbY9p6X/ZNoS17r9w1vJ93ZBqM8YEoB3/5ZSTlJx6PV6Zvy8u3mysz5cz4DLRPcpco3grqxTvuF6Xv0C/3T8m6+Xygur+oP+OtQFDlcwgVysx4zDj6OiIr+/EnYusZvTlbMJd3ne/9x7Tw7CjvoA+fUcWvwk4Jtktje1sS6vrW1P2ZvoeYap+tx9gq9gBRhu24fLzGBuT3wk7goUQw4QWkfc8e7yV4fNoyEFgo7evEtzaAOmG/WVwzVvhmCJqDMe1s8H4WKhdHERX0+83Y+s9/rFLXO0b53nn9lpi2bxEtj47yTehXLA5XWZQCixYEJHkiIhF/Ofcki9qiZ48SRCj1uiK2/2/p9kZZnHAf0Uwd9sT296TwhV4fAmwa447+wCKIMcEYZhGHkBa5RsEYsTqrvVMnAnjqMHoYNDxECEBg1cWgf3dM2x1HI6wsF616j1auyXJvRpkU7xCTN4z/YrBvO16vwmb083lCrJfPsc5OCbZjHUQJi7gHRvlnJZLbx+Kt83VBsPXOsImIHNcg0lhd3bS9EdMvHBFvcvxwMMovqVtYzbMVsypz+cA6+Rzr3CZW974cz7Dlh0euB9uOOwUeVQWbiJyQsPpl26v2pLEqZtshz/3J8QPbIGzZ1OfnEOUIsNwSWoW5fNiOWicfOT7gmyPY2LaruVeUH6rsBHnui+MFIiInHBjBp0Y5F4FII3DG54I4urdD5fDBG8L5Ns6g8b05F8c/D7AuvXw26wRyQsFWKOecOK9If0DQLzrbui6cz82zWJzX4oc2IiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIiIictzx/3XTMG2mwPYwAAAAAElFTkSuQmCC>

[image5]: <data:image/png;base64,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>

[image6]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAmwAAABhCAYAAABrlP3SAAAOk0lEQVR4Xu3dBaxkVx3H8T9aXItDkFKKOyVYeMWlxQNBWyju7pBStMWdYl3cpVBcWqBQKO4ODW5BAwQIgfPtOX/mzOnMvHm7+3an7PeT/JN3z71z5+6d18yvR+6LkCRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJ0i7n/KXOOTauEK7vXGPjScTJS+1V6rTjDkmSdrR/lvrPnPpjqUNKnfp/R+sMpY4vtefQvtleF9Pve1hMPqf9W9sq6a/vbsO+HW1rP7O8/ouOOyRJ2hnOHfWL6Ydtm4B24VJrpb5a6oul9mj7dnW3i3qvHjTuGCwKKZcptffYuI7jor7vlds2vT+8x/YObFtzbbP017foXmDf2NxewmU/s9FLw8AmSVoh9EDwxfTtcUdMvuzeMO7YRb056v342Lhj8JOxofO4UvcdG9dxjjhxMLt0bP/AtjXXNs/FYrnA9qGo/5bNsuxnNrp7GNgkSSskA9u3xh3F1aLu++u4Yxd0ulJfLvWlqPfkvNO7p/xybOh8KrZPKNqMwLa9rg0MQS4T2P4UmxfYNvKZjQ4MA5skaYUsCmwMV7HvI+OOXdCtSj2j1FOi3pN5Q2xnjPmB7c5RX7s1oYhh6rN029s7sG3Ltc1C0FkvsJ0s6jGbFdiW/cxmySFdA5skaSXMC2z0TtDjwuKDnDuVCA4vK/WVqGGO+T4ZJrZEPV/WU1s7x2Ub+LJ+dNQeEIbFjih18bbviqW+H/XYN5W6bKkXl/psqfe3/SnPecO2zUKJbHtSHtRwnveU+nSpo0o9POp8q2Uw8f8apa4e9dycY8T19/926pFtH68f92XP5XWj3h/mqh0cdWjy66WeH5MhPWqtHY9LtLaHlnpBqbdG/Qw5nnmJYD5i/374TLfN+2LRtaXx3o33jc/ym6WOLvWuUneKep5Fge2nMf2e753eHecr9ZqoPWT8LvJv28iq02U+s0TQfnWp70X9HXtC1Nf0ge1Gpd4Y9VqY38lxN+32S5K0aTKw/SVqaPh8qd+2tnfHiXsYThM1qBEssFupD0b9kk4EBlagbonJFztfvpz31m37laXeFzUYgl6Qn5U6famzldqn1K+izq17UalTteMIHISTlCsSM7ARBG/R2vrAxoT635e6TtvmeggMBJ71EHx+FPXcFHPUOP+FumN683rYslds7MXifl2/1N+iXtNVo4YBjuW9H9F+XmvHI8Ph8aUu0NpOGfUz+1rU+wiGJo+Jeiw439PbdgY2zLs2zLp3/X17VqlfxCRInyJq0OZ8iwIbOGZWD9tFov4+HNC1EaL4HPj9WM9GPjOul9+ro2KyAILAzPH5+8/9/E3U+YTgf1CYF5e/z5IkbapZPWxnito7QY/E2bt2PCxqGMtAgFycsEfX9oGovRV8WYIv4OxBoceO4wkpKVer9l/wrFClh4+QmF4Y9f0Tw168LgMbdm9tfWAjyBzdbYMgmKtjF9kvai9WOjTq+R/StfU2GtgSYY0wDHqG7tV+5v153VrbRga2B3ZtuHZrf1TX9tzWlggZbC8b2Gbdu7xvhDleNwbf/Iy3NrAR+OhZ6xFIubeE/fVs5DO7d9R9fU8y/x7aMrDxe0ZozcAGhlhv3m1LkrRpZgU2nLW182Xd64fUxmLIKPFFTdta235M1GCHfthyrKe1Y8AQIe/Xe17U41KGmUWBjXA5vk9f9MYscnip63XbOcR2dNfW25bA9o6xMeqwG69b69rmBbYzt/Yju7Zntra0kcC26N5x3x7cfu7PhW0JbPmehw/toBf4D2PjDLx22c+Me86+7A3GGNj4n5F/R+1l+3DUoX56GiVJ2iHmBTYwJMk+wltiWHOZXinO+/eoQ5ZgqDV7yt4W9bx9j9wsx5b65NCWgS177m7cthcFtsu37VkBYD0Ml/ElzetnFU/zH21LYGPO1oh/G69b69rmBTbQ3vdO5RBo2khgW+/e0YvFflYU97YlsGWv3auGdhBE2bcoLG30M6NXk+Ho3hjYsG9Mz7v7dalLdvslSdo0iwLb8VH3Xalr+0bUYcoMTIu8PuoXJ3ObXtG1vyTqea/Stc1C79q8wMaXMjLM9L17TEynLQMbj3Nge+wtXAbn3TI2Rl0QwDnvP+6I6cDWP/9rDEUsSLjJZPcJYaC/T4lr4HVrXdu8wMZwNu3MK0z0BtGWbtu2FwW2vLb17l1Ozu/vP7YmsDFknnMYaWdYdHRUqX/FZO7jLBv9zOi1o73/M1RjYCNE5n8HLFDgHjLHjoUKkiRtukWBjcnr7GPFH3PM+CI9qLXR29B7bEyv3gRf+Bz72ZhMWAc/035o14ZrxvQco+NifmBjPhOYB8d2H3w4D20Hd20Epz+XOk/XhrfE5FyzsBr2ZmNjTJ5Rx/DYiJ4XEGpZAZv2iunAwD3bZ7L7hAAwa35W3se1ri0D2zgni7lvtPc9ZU9ubYnhabb7IcNF1zbr3uV9y6B3YLcPe7f2ZQIbK1BByMwgzn3L+XwpFw+wIGORjX5m92ntLNBIrCCmLQPb/qVePtl9AlbzsnBGkqRNl70ZPxh3xOThoQxN0ZPClzC9C4Q7vjjzC44v3He2n3t8+RJe6HEae+ToPeHcOWmbYVd6WPKxDRzPClEe+9Ej0PA65mqBSeA8giLnx4GFCRzDNeVxDO1xHIshcoj3jqWe2H6ehaBEb+I43AfCCg99ZQFEPxEdvPdFSt0gpie+8xrmX3E/mS9FEMoQxL7fRe2VHGWPWB96M7AdE5MHwvLZfDzqYo1+Xh7hmmNBQOc1bBM4cvXtomubde/6+0YPHo+5yIUou0W997wHn8WiP6DOMQdEXdxCsE8EyJ9HfT5cul/Ue36prm20NZ8Z7dy3vrfsO1Gv7S5R7weBjdf252VlNMFWkqRNxRcXX0p90auVCE3Mf2K1KF9OfHHhAlF7QBia+mjUZ6T189x6z4n6yI4R89l4fhs9N/TkEeByPhDBkLCW18Tzvfii5As92/gyp+cPt4y6qpWeI65lrTuOf2O6dtQA+I+oQ3yspByDZMphMorj79rtu01M5vdR3416fAaTY9t+rjefiZYIIJyPgPyA1kYYGD8HhiRB4GMuIG0Equw5I7B9IWrQIWgQdrmPrHwlhI8eHzV00/uUz0ijCGFp1rWl8d71943fC3r66G1iRSr/7oNi8h6zem8T18M5OeZawz56tzgnPW08ooN7nL1xs2zLZ8ZQMr87LEA4LGpvWh7LNe4fdfEG/8PA67hvhLXsEZQkSRtEmLhCrL/6c1dFuKZ3dF5Y3R7o7SNUnlQDDYsa+B8TSZIkSZIkSZIkSZIkSZIkSZIkSZIkSZKkJfXP+rIsa/uWJEmSJEmSJEmSJEmSJK2C88fkD9n/v+Dvbe4xNkqSJO1s/FH1O4yN68gJ6Hcbd8xwiah/vP1jpY4u9bhSZyh1RHfMztb/sfgt07skSZJ2rvNGDSlvH3esg6C2TGDjD9T/odSN2vZpSz2t1K9L/TIPWhGXK/W3MLBJkqQVc7+owYugQpha1sViucD2rlJvGhuLl8TqBTYcHwY2SZK0Yj5S6i1Rw9fthn2L7BnLBbZflHrx2Bi1520VA9uPw8AmSZJWyDlKfarUDWLjw6IXjeUC27dLfT9m994dNzasgB+FgU2SJK2Qe5R6TKlTl/pzqb+XOsvUEdMeXeqbURcO5CT99QLbk6Ie992or9+n1Gmmjoj4Rql/RQ12hEd6/D4dNTxxjaNblvpE1N7BT5a6cWs/RdTz0HN31lKHlHpPqWNL3b4d07th1ND4pahDt3cJA5skSVox7y91yfbza6MGqwP+t3fas6IOb16xbTMvbZnAtltMju2Llalna8eslfpca394a8PBre2eXVuGqgu27etEPeZKpU5e6oNRw+dbS527HUNw+3nUYJpuETXcETzTA6Kea0vXJkmStNMQlr7cbe8bNay8s2tLl4m676Fd25Vb23qBLd271DFRQ1If2hKh7rfdNk4WNZz9qtTpWxG8ntwfVHyt1OHt5+dGPfc1J7vjtkMbwe2HUXvVRn8MA5skSVoRBC16sFIOi7Ja9IxdOx4cNfBct2vbaGBLpyt106hDpLz+Kq39jXHiwIbDoh53taivy7A3FnPx8Oy2zXPe0q1b21rbppeQbYZrRwY2SZK0Eghk34vag9W7TdQgwxyy3hNaez5LDcsGNp63Nks+/+2Obft1MTuw8cDdDFvMQ+Pnh/UHDBj+5Jh+nlwGNoZPsda2eR7cyMAmSZJWAiGJOWkj5pvxkNu/xHTguXTUgHNg17Z3a1svsP01Zs+Lu17U11+8bRPYCEssHEhcAwsRWETAtbEgguv7TNT5aokVqK9pP2cP26zAlj2EvAdDq/maHv/2LWOjJEnSjrRXqa+WetS4ozkyarhhUn7vqVFfxzwyMNeN414Ysx/ZkQhszDHbPyY9ehcs9Z1ST8+DogY2zveKqOcjVPH8tn/H9PPhWIDAcVwPw7gENx7Cm71nL2/7eWRJ4r1pu1nXRm8h15aBEaxi5Tjm2u3etUuSJO0wT4waSLJe1u3juWrf6vb9JupjM5g7BoLRQ0q9L+rE/oO6Y3ndPEdFDWA8PoTAR0hitSnb/ZBsDokSxH4X9QG2vP9ad0xiTh3n4BoZvmVuGwhweU3sJ6gxB47HldDG/Ly+Z5FHiLCq9DlR58DxN07p5ctzSJIknaQxD47eqX4Ic1vMm8O2o10+TvycOEmSJMX8VaKSJElaEUdEHY7sH24rSZKkFcGfh8p5Y8xd2296tyRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRJkiRpM/wXbdCoQ0iN0+cAAAAASUVORK5CYII=>

[image7]: <data:image/png;base64,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>

[image8]: <data:image/png;base64,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>

[image9]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADsAAAAZCAYAAACPQVaOAAAC2UlEQVR4Xu2XWahNYRTHl1mGjJEyhGQoSRkzD8WDsYQ8KDJFPChDEbcoPCCZp5AxSSkuIRkTiVIeiBLygELyQuL/b+19ztrrnrPPuecc5yb7V78631rfPXevvfe3vu+IJCTUJO3gXrgT9nI5y1rYwwfLTUdYxwdBN7gQNjGx4XCbGTP3Ao6FXeE7uCKIE37vaHgOng9iZac+7Asr4CfYL5JVeJG/nR/gMDNnHnxixuvhZngAnoQP4BnRm9DezMvKYLgJdvKJIngLK+E10SIyFTtGdN57+BQehN0jM0T2i35HyCTRJ2tZAhe7WCyd4Q7RtRG3LqrLSsleLJ/sIR907ILXzXgyXG7GXAp3YS0Ty5u2cAs8JXoxxRJX7EjJXewC+NiMK+D44DMLvAF7p7IF0kz0Qi/AGbB2NJ03uYo9DbfCy/Aj3C7Rp9QcvoRDYRt4T9LNjut5Q/C5JDQQvbuX4BxYN5rOSVyx7BVvYJdgzG77Ba5KzVDY6K6KNqKwr7QSLbxhOKmUsMizog2lscvFEVdsU6naFE/Ar7C1i3t2i74ZIYtE38JpJlZtWORs+AzegeOi6ZyExfb3iSxwW+H8mT5hGCC69YRshPtgS3gEjjK5vOA+ybv1HB4TfeUKIVuxXJc34X2J9gOegjh/qYlZ6sErsEUwZm/5Junr4wGGzTUvuPjnw0dwjWhTKIawWD4NC2/mL/gdNjJxNivOn2BiltWiDTOEJy7O72li3Ipi4frh5syuOFe0MZWCsNiBPgEewj4uxv//WfSV9PAs4I+Eg0S/354NuB1lZQS8CKdKgZtzDOtEL4anJc9EuEfST5ZP6afolpIJFtrBxfi3fEOGBGM2PHbtsnIUvhYtlP6At6TqsY6NiE/ituhWMiWaTjEdLvPBAP5wOC76oA5LaQ5DNQa3Om4rmX45ETYtHitfwVku90/CrlsSuGb5yyIfK+UvnVoSEhIS/lv+ANCNjCNsYIyRAAAAAElFTkSuQmCC>

[image10]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADEAAAAZCAYAAACYY8ZHAAACiUlEQVR4Xu2WS0gWURTHTw97afQkc1O6LCLoQREIQQW1rAgToqCihwYRLdr0IigiLCiKWrTKIqpFJPnKUoLAgqKiqHCVUC5s40Jc5//vmXHOHL7J+fxSXMwPfvDde+abmTv3nnOvSEZGyFr4BJ6BC10spATehlN8YKw5DFebNl/kClxv+tbA73AJ3A5/wZ0SvSz/swt+hCeCvnGlHf511sNp5hq2b5j2K1gL78On8B18DDslxSxsgJfhUh8ogA74CfbBF/B4PDzED3jWtK9KfKbIQ7jS9SVSIfpV7sDlLjYa+FXLfafjCzxv2tdEcyTkoOjHzZtS0bXLL7DJxfLhpYw8CC6b66bdBucEvxfD93BmFM4f3uwUbIC74eR4eEQ4iP3wGfwsmpxcthYunZ9wAdwM75oYB7jFtAtiumilaRJ9qanxcCKN8KJp34TdcL7pI9XwNbwFZwR9G+G98IL/CV+e9ZxlsNjFcuGTcZlohbrk+j18DotCuGfMhnXwEVwVXpQvvOk++A2+gVvj4dRw4BzEVx9wnIR7g9+TRGfpgGiu8vnzglgqWM+Pwi7RqfXr+V9ww+qFVaaPL8RB/DF9HlZI7g8hzIl+ifKRg6uJwslwUzkEP8DTcFE8nIoLoi9sy+fcoO+t6fM8l/hexef/Nu0VormVCNfeMdgiOn1M6NGyAz6ARaavUnQQ50yfZY/oUrKwOvaYNgfBApATVgNWEz6c014ovEerRLsvlwPvzx06V93nLPHj+aPFNjhg+pmb/NDjRplo3ecZipsWz0lJScklwsOghzPJc9MROEs0sX2JnhCsEz0hJMETLnOF57BcA50QcIMrJP+GYU7wmJDGZol21oyMjIyxYRBaVnA1IVTgqgAAAABJRU5ErkJggg==>

[image11]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADUAAAAZCAYAAACRiGY9AAACpUlEQVR4Xu2WSchOURjH/2QmmRJFvp0IZUqKDGWBhWFhIRsyLyyUITNRZFpgYR5LFoZkYbaQkJmFkEhkSGFjJ/7/9zn33nPPe7/3e++rvqT7q1+9z3POve+ZzwUKCv5L5tJBXtyObqHDvJzoRg/SG/QunZMuLtGMbqDX6QO6jbZO1WgkrtHfgcdoC69OF/qULnRxT/qKrosqOE7SE7DOtaLnYR1sdPSnj+g3eokuSheX2A7rlM98+pU2d/Ek2IB0jWsAfV0unPUUE+lNOios+Auu0rowGfCWngpyY2ENHunio/RzUlxCM/aLrgjyZYyGrWu9pC5VUhtXUPk92ktq/N4gP9jlV7lYM/k8KY7RCrgcJutjOr1Dt9LOQVke1KmZ9Bx9TB/S4V75EFjjd3s50d/lD7v4O8qXqPhEX4fJhhhBD8FOmh5BWTVcoBu9eBdsuXVysZZ6Vqei/aKDQeh3Vqc+0PdhsloG0tP0OB0QlFUirNsH1sBNLtasZXUqqqdtIH4iu1Pq0JswmZfe9Aw9CztW89IW1thnLtb7FO+Jaxj9XH6ni98hecbnI+zOqpmOdDP9AhvpJuniMqbCTqxpXk7PqLF6h9AdpVgXr89Ql1/tYu1F3V0hP2D7Nje6tZfANvoyJPuhIdbDGrbWy3Vwudte7iVsafuMh9Wb4OIDsJPOpw2sjga6anTxLaBP6GLk/ySZAtvo0QUqdPCoIWu8nA6SF0jPvAZRSyt6dhzsuV5xDbt0lfM/w+qlJZ1N79OVtH26uGrUyItIbvymsNNQ940/QNqbt+hkF6tMszcjrmHoBN7hxTq0wvstk1mwP9UtXWtnfLrT/bBvwHuw7z7tzRAt6eX0CN0Hm+UQDco82Emp5bjU5SoyBrb+te4LCgoKCgr+Ff4Ah2WN0dwsZEoAAAAASUVORK5CYII=>

[image12]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEcAAAAaCAYAAADloEE2AAADPklEQVR4Xu2XaahNURTHl6kMGTN+kCFzSMYo3ktJpJAPEiJliJAyh0yJzCJDhmcoCYmUUHyQD4RMJSQSoRQSH5T4/62179l339Nz7nPfjZxf/Xtv//e++569z95rrSuSkpLyn1EXKoOeQOehPVAXf4DRHDoAXYVuQFOzu39RHVoNXYFuQ5ugWlkj/jGOQxO9Nhf2BWrjeY2h+9BMa7eEnkIr3QCDcx0T3aSa0DnR+YrCZGiu6NsuBDwNP6CHnrfAPJ4Ax2bRzfGZAb2Halh7pOjnmmZG6Amk18/zKpVB0GFoFdQk6MsXbs476JbnLRFd0AbPewGd8NpksOi4gdbmM3EuH56g79DSwK90ukMHod1Qh6AvH7jBvAKOk6KLLrW2O1173QCjl/nLrM2T9SjqzvABuhSaxYKxYTt0FOod9OXLCOgbNN3zOCc3YafnkW7mH7L2R8m9euQt9Cw0Q+aI7izfTANokehRvSn69utHQysET8Aa6JTokc8HLpSf4wIZVOt4fSUSvzkunjAAE/4ftzmvoVeh6dMJ2ga1kygADrC+FuYxwBUCXoN70JmwIwEM9EzBXCRfIOkv8ZvT2XzGGvJV4jeHG/M8NH0Y+ftCY0QnHO/18Y0XYnMaQSugN6JvP65WScIo0ecps3ZHa+9yA4yu5m+19kvoQdSdgc/DDf8tjA2fJUp/ZJLol/BUVQSmznWib4cZhjVIUphNethfR1vR52GW4fVijcM2C0CfPuYvt/Yd0don5BN0OTTj4ARnA+8CdC3wklBPNMawWp0i2RknKbzqXOBGz2tvHtXQPFbPpzMjlGGiY4Zbe79oZvKpLTpmfeDn0Ex04CzPa23eNKiaRMGtPFpBO0QD6NCgL1+4IH4/T56Dc9JjonCshR5DVTyPxSKvjLsFQ0Q/x+dzsPij19PzYhknuddnrHm8Cnz73KTyYHV8RBJ8WUJYqzDVuvkY/1gQMriWuEGip/K6aDwi/L3E0zQhM0Lhb6ktXpvlRVgfxTJf9LeGD7MDU/tFaB5UNbu7KJSKZre7ogGVsYVBOIQBf7FooN4Hjc7qVfj8rJGY2XgqF5qXkvIXM1s0LSaRqz9SUlJSUlJS/oifYYa08dskKEUAAAAASUVORK5CYII=>

[image13]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABsAAAAZCAYAAADAHFVeAAAB/0lEQVR4Xu2UOWgVURSGjzsERdFoAgqC4hIELVKIiPLQQgQVu6QQbMQNUrvgUiXaqIVoo4WiURsXEBQXYnBBEGzU0spACi2MhRYG0e9/986bM/fNey6d8D744J1zz7wzc+fMNWsRmIKHcRA3JWuebdiTJjOW4B6c7nLr8bSLhZocwTn4CC/jAre+Ek/ie5zh8gU24M/Ej7jO1SyN+bkx1jW38ARewud4D9/h1lhTykYcwVF8gxdwWaHCbIeFZhkz8a6LRbeFp22K7vJimkzQO1CziTHWlt/Ol20qvsYOlyulYr9vttxCs/YY6wYH8mXrx90ubkgFr+MpvI+f8AxOcDXiJh7CyRbqNFhiBT62+vpS1uAHXBTjxTiGB2oVgVl4DR9YeLIMNe5ycVM0pguT3FX8Yvm2NULv8qiLdRN3LOzAHz2p0Peid9SbLjh0kw9xWow340uch/vxWMzXUPdhC0XZpAl9vGrW53IpZ3Gti59YcetfuN9VNLI/8Cu2ubyGRc22uJxnNZ5z8ST8buEkytDQ1X0Kr3BVktNL/4yzk7zQNOq48sebduUb7nU5Net0cRUdL+ctfzKdi+O4q1ZR5CBuT5PwzMJgZGgbS4dEgzCETy0Ulf2Z0NTeSJMRXfPWwieyE48Xl/+eKzg/TTr2WTj1dUD7gfsndAC3aPGf8wuc91ZVI39gnQAAAABJRU5ErkJggg==>

---

## Perplexity (source: `measurement-framework-perplexity.md`)

# Pre-Campaign Success Metrics Framework: A Repeatable KPI-Commitment Step for Campaign and Launch Planning

## 1. Leading vs. Lagging Metric Pairing

Leading indicators are early, influenceable signals that predict future outcomes; lagging indicators confirm results after the fact and cannot be changed once observed. A repeatable planning step should require every campaign or launch brief to name at least one leading/lagging pair per objective, mapped to the funnel stage it sits in, with an owner and a target value committed before execution. Umbrex's funnel-stage framework recommends pairing one to three leading inputs with each lagging outcome and assigning weekly cadences to leading metrics and monthly/quarterly cadences to lagging ones.[^1][^2][^3][^4]

### By Campaign Type

| Campaign type | Leading indicator (pre-outcome signal) | Lagging indicator (confirmed outcome) |
|---|---|---|
| Product launch (marketing campaign) | Pre-launch waitlist signups, teaser content engagement rate, press/analyst briefing pickups [^2][^5] | Units/sign-ups in first 30-90 days, launch-period revenue, market share shift [^5] |
| Thought leadership | Content downloads/completions, share-of-voice, speaking/podcast invitations, dwell time on long-form content [^6][^7] | Inbound inquiries attributed to content, brand search volume lift, analyst/media citations over a quarter [^6] |
| Seasonal promotion | Early email open/click rate, ad impressions and CTR in first days of the window, promo-code activation rate [^8] | Total promotional-period revenue, redemption rate, year-over-year sales lift [^4] |
| Retention | Product adoption/engagement trend, NPS/CSAT trend, expansion-intent signals, support-ticket sentiment [^3] | Gross/net revenue retention, churn rate, expansion ARR [^3] |
| Lead generation | MQL volume and quality, speed-to-first-touch, landing-page conversion rate, cost per qualified lead [^3][^6] | SQL creation, qualified pipeline added, win rate, cost per acquired customer [^3] |
| Brand awareness | Impressions, branded search volume, social share of voice, unaided-recall survey trend [^8][^6] | Aided/unaided brand awareness lift (survey), direct-traffic growth, assisted-conversion share [^6] |

### By Launch Type

| Launch type | Leading indicator | Lagging indicator |
|---|---|---|
| Product launch | Beta/early-access signups, demo requests, sales-enablement asset usage by reps [^5][^9] | Revenue/units in first quarter, customer acquisition cost, launch KPI attainment rate [^5] |
| Feature release | In-app announcement click-through, opt-in/activation rate in first week, support-doc views [^10] | Feature adoption rate at 30/60/90 days, retention lift among adopters, reduction in related support tickets [^10] |
| Market expansion | Local-market qualified pipeline, localized content engagement, regional partner sign-ons [^9] | Market share in new region, revenue from new market at two quarters, customer count vs. plan [^9] |

Practitioners emphasize that a lagging KPI without a paired leading KPI leaves teams "reacting too late," while leading metrics without a lagging tie-in risk becoming vanity signals disconnected from business impact.[^3][^4]

## 2. Attribution Model Tradeoffs for Teams Without a Full Analytics Stack

Three attribution approaches dominate practical use, each with distinct tradeoffs for a resource-constrained team.

**Last-touch attribution** assigns 100% of conversion credit to the final touchpoint before conversion. It is simple to implement, requires minimal tooling, and works reasonably well for short sales cycles or a single dominant channel, but it systematically overallocates credit to lower-funnel channels and undervalues upper-funnel and awareness work — one simulation found last-touch and time-decay models overcredit near-conversion channels by roughly one-third relative to causal estimates. It is appropriate when budget and analytics resources are limited and the buying journey is short.[^11][^12][^13]

**Multi-touch attribution (MTA)** distributes credit across all touchpoints using models such as linear, time-decay, U-shaped, or algorithmic/Shapley-value approaches, giving a fuller picture of upper-, mid-, and lower-funnel contribution. It is best suited to long sales cycles, omnichannel programs, and teams that want to justify budget across the funnel — but it requires unified tracking across channels, sufficient volume, and more sophisticated tooling and cost to implement well, which is often unrealistic for a small marketing team without a dedicated analytics stack.[^12][^14][^15]

**Self-reported attribution** ("How did you hear about us?") asks converting or signing-up customers directly to name their discovery channel, typically via a form field at signup, checkout, or in onboarding. It captures "dark social" and offline influence — word of mouth, podcasts, conferences — that pixel-based tracking misses; one study found a 90% measurement gap between last-touch software attribution and self-reported data on dark-social channels. It is well suited to teams without engineering resources to build MTA pipelines, but its answers are biased toward recent and memorable touchpoints (recency and salience bias) and depend on question design — free text outperforms dropdowns for discovering unexpected channels, and required fields reduce response quality.[^16][^17][^18][^19]

Because no small-team method is unbiased, the framework should require teams to explicitly document, alongside every KPI commitment, which attribution model was used, its known bias direction (e.g., "last-touch overweights bottom-funnel paid channels; upper-funnel content contribution is likely underrepresented"), and any correction applied (e.g., blending with self-reported data). This turns an attribution limitation into a stated assumption that can be revisited rather than an invisible distortion of the review.[^13][^19][^16]

## 3. Standard Review-Cadence Conventions

Cadence conventions differ meaningfully between an active launch/campaign window and steady-state operation, driven by the need to catch and correct course quickly while spend and attention are concentrated.

- **Active launch/campaign window**: Leading indicators — impressions, CTR, signup pace, early activation — are reviewed weekly, sometimes daily in the first days, because early corrective action (creative swaps, budget reallocation, messaging tweaks) is only useful if caught before spend and attention move on.[^8][^3]
- **Post-launch/steady state**: Lagging and outcome-level KPIs (retention, revenue, pipeline, expansion) shift to monthly or quarterly review cycles, reconciled with finance, because these metrics mature slowly and over-frequent review generates noise rather than signal.[^3]
- **Funnel-stage variance**: Practitioner frameworks explicitly assign weekly cadence to awareness/engagement/qualification-stage metrics and monthly cadence to opportunity, retention, and unit-economics metrics, with a quarterly audit of the framework's predictive power itself.[^3]

The underlying logic: leading indicators are actionable in the moment (a team can still change a channel mix or creative this week), while lagging indicators require enough data accumulation to be statistically meaningful and are typically tied to budget or planning cycles owned by finance or leadership. A repeatable planning template should therefore commit to two cadences up front — e.g., "weekly during the 6-week launch window; monthly thereafter" — rather than a single blanket review schedule.[^4][^3]

## 4. What Makes a Success Metric Falsifiable

A falsifiable metric is one specific enough that a post-campaign reviewer can unambiguously classify the result as hit, missed, or inconclusive without new interpretive debate. This requires four properties, consistent with SMART-goal literature and lean-metrics practice: a named metric with a defined measurement source, a numeric target, a time window, and a comparison baseline.[^20][^21]

- Vague: "Increase awareness." Falsifiable: "Increase aided brand awareness among the target segment from X% to Y% (survey, n≥300) within the 8-week campaign window, measured against a pre-campaign baseline wave".[^6][^21]
- Vague: "Drive engagement." Falsifiable: "Achieve a 25% completion rate on the launch video among paid-reach viewers, tracked in [platform], reviewed at day 14".[^8]
- Vague: "Grow the pipeline." Falsifiable: "Generate 150 marketing-sourced SQLs at a cost per qualified lead under €X by [date], per CRM stage-change data".[^3]

The test practitioners apply, drawn from Eric Ries's actionable-vs-vanity-metrics distinction, is whether the metric would let the team say clearly what to do differently if the target were missed — if a number can only go up regardless of the team's actions, or if hitting it wouldn't change a decision, it isn't a real commitment. Inconclusive should be an allowed verdict when instrumentation gaps or external shocks (e.g., a platform outage) make the recorded number untrustworthy — but the plan should say in advance what would trigger that verdict, rather than letting it become a post-hoc excuse.[^21][^20]

## 5. Common Failure Modes and How Experienced Teams Avoid Them

**Vanity metrics.** Metrics like total followers, page views, or cumulative user counts tend to move in one direction regardless of effort and create false confidence without informing a decision. Experienced teams replace them with cohort-based, ratio, or per-user metrics — e.g., activation rate, retention by cohort, or conversion rate by channel — that can move down as well as up and reflect real behavior change. B2B marketing teams are increasingly told to audit reporting decks specifically to strip out metrics that "look good but miss pipeline," such as raw impressions or pageviews disconnected from revenue.[^22][^23][^20][^21]

**Metrics that can't be measured with available tools.** A common failure is committing to a KPI (e.g., true incremental lift or full multi-touch attribution) that the team's tooling cannot actually produce, discovered only at the review stage. The self-reported/last-touch discussion above illustrates the fix: state the measurement method and its limitations in the KPI commitment itself, so the target is scoped to what is actually measurable rather than an idealized number. Teams without engineering resources for MTA should default to last-touch plus a self-reported layer and say so explicitly rather than quoting an MTA-style number they cannot substantiate.[^18][^13][^16]

**Metrics disconnected from the business goal.** A metric can be specific and measurable yet still fail if it doesn't causally relate to the objective the campaign was meant to serve — e.g., optimizing for social shares on a campaign meant to drive sales pipeline. The corrective practice is to work backward from the stated business goal to the metric (value/growth hypothesis framing) rather than starting from what's easy to track, and to name the intended causal link between leading and lagging metrics explicitly in the plan (e.g., "we believe demo-intent clicks predict SQL creation because...") so the link itself can be falsified in review, not just the numbers.[^21][^3]

Across all three failure modes, the safeguard experienced teams use is the same discipline applied in items 1 and 4: pair every metric with its counterpart (leading/lagging), name the measurement source and its known limitation, and set the numeric target and window before execution begins — turning "we'll know it when we see it" into a testable, falsifiable commitment.[^4][^21][^3]

---

## References

1. [Leading vs. Lagging Indicators: 20 Examples](https://whatfix.com/blog/leading-vs-lagging-indicators/) - Leading indicators can predict what is likely to happen, while lagging metrics measure outcomes and ...

2. [Leading vs. Lagging Indicators (With Real-World Examples)](https://amplitude.com/blog/leading-lagging-indicators) - Leading indicators predict future performance outcomes. Lagging indicators measure past outcomes—for...

3. [What are the leading vs lagging indicators in marketing?](https://www.pedowitzgroup.com/what-are-the-leading-vs-lagging-indicators-in-marketing) - Discover how to effectively use leading and lagging indicators in marketing to predict outcomes, man...

4. [Leading and Lagging KPIs: What They Are and Why ...](https://www.thealternativeboard.co.uk/insights/leading-and-lagging-kpis) - Lagging KPIs measure performance after the fact. They tell you what has already happened, such as yo...

5. [Launch KPI Attainment Rate Guide | Product Management - Umbrex](https://umbrex.com/resources/company-analysis/product-management/launch-kpi-attainment-rate/) - Shows how to analyze company with Launch KPI Attainment Rate analysis for Product Management to asse...

6. [B2B Marketing KPI Guide: Leading vs. Lagging Indicators](https://www.innovaxisinc.com/b2b-marketing-strategy-blog/b2b-marketing-kpi-guide-leading-vs-lagging-indicators) - Learn why leading indicators can tell you exactly where you need to improve your B2B marketing strat...

7. [10 Best Leading and Lagging Marketing Performance Indicators](https://webbiquity.com/marketing-strategy/10-best-leading-and-lagging-marketing-performance-indicators-to-increase-roi/) - Here are the 10 best leading and lagging marketing performance indicators to help increase ROI, plus...

8. [Marketing Leading Indicators vs. Lagging Indicators](https://www.youtube.com/watch?v=dMtdXgVDpxU) - ... lagging indicators show results after the fact. Understanding both can help you optimize your ma...

9. [Go-to-Market KPIs That Measure Execution Success](https://themarketingjuice.com/kpis-for-go-to-market-execution-success/) - Most GTM measurement tracks the wrong things. This framework connects launch KPIs directly to plan a...

10. [16 product management KPIs and how to track them](https://www.atlassian.com/agile/product-management/product-management-kpis) - Discover key product management KPIs and how to track them to reach your product development goals.

11. [Toward sustainable ROI governance in marketing: Integrating multi-touch attribution and incrementality testing for evidence-based budget decisions](https://jems.sciview.net/index.php/jems/article/view/281) - Purpose. This paper addresses the methodological misalignment between descriptive multi-touch attrib...

12. [Understanding Attribution Models: Last Touch vs Multi-Touch ...](https://lifesight.io/blog/last-touch-vs-multi-touch-attribution/) - The goal of multi-touch attribution is to accurately distribute credit to each marketing touchpoint ...

13. [The Pros & Cons of 4 Single & Multi-Touch Attribution ...](https://www.newbreedrevenue.com/blog/single-multi-touch-attribution-model) - Companies that use last touch attribution believe that the interaction that converted a lead into an...

14. [Understanding Multi-Touch vs. Last-Touch Attribution](https://ingestlabs.com/touch-attribution-models-methods/) - Ever wonder which of your marketing efforts truly drives conversions? Learn how multi-touch and last...

15. [Single-Touch vs. Multi-Touch Attribution: Which Model Fits ...](https://www.martechcube.com/single-touch-vs-multi-touch-attribution/) - Single touch is simpler; multi-touch models offer greater insight but take much effort and managemen...

16. ['How did you hear about us?' survey and the limitations of ...](https://getrecast.com/hdyhau/) - 'How did you hear about us?' survey and the limitations of current measurement techniques · Why you ...

17. [Does "How Did You Hear About Us" Actually Work? · Attri](https://attri.io/blog/self-reported-attribution/) - Self-reported attribution catches what UTMs miss and lies in ways UTMs don't. How to design the fiel...

18. [Marketing Attribution in 2026 | Free Template for ...](https://formbricks.com/survey-templates/marketing-attribution) - A self-reported attribution survey asks new customers one simple question: "How did you hear about u...

19. [Matt Bahr - How reliable is self-reported attribution data?](https://www.linkedin.com/posts/matthewbahr_if-youre-using-an-attribution-survey-hdyhau-activity-7340420992080506882-ZWBq) - If you're using an attribution survey (hdyhau) to measure marketing performance, how reliable is tha...

20. [Vanity Metrics vs. Actionable Metrics - Guest Post by Eric Ries - The Blog of Author Tim Ferriss](https://tim.blog/2009/05/19/vanity-metrics-vs-actionable-metrics/) - Vanity metrics: good for feeling awesome, bad for action. (photo source: UK Guardian) This is a gues...

21. [The 7 Vanity Metrics You MUST Avoid](https://www.shortform.com/blog/vanity-metrics/) - What are vanity metrics according to Lean Startup, and why are they so bad? Learn the key vanity met...

22. [Vanity Metrics Examples: How to Replace Them in 2026](https://pipeline.zoominfo.com/marketing/marketing-vanity-metrics) - Vanity metrics examples like pageviews and follower counts look good but miss pipeline. Here's how B...

23. [Vanity Metrics vs Actionable Metrics: Eric Ries on What Matters](https://www.linkedin.com/posts/jing-xu-b5927143_vanity-metrics-vs-actionable-metrics-the-activity-7444856849822134272-jybz) - Vanity Metrics vs Actionable Metrics: The Difference Between Looking Good and Getting Better Most te...


