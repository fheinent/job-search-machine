---
name: work-product
description: Generate a company-specific work product (analysis, mini PRD, or problem exploration) that earns interviews by demonstrating real insight.
---

# /work-product - Work Product Generator

## When to Use

Run `/work-product [company + role + type]` when:
- You want to earn an interview at a target company by sending something that proves you already think like someone who works there
- You are in-process and want to impress the hiring manager with a mini PRD or product proposal
- You fumbled a specific interview question and want to send a follow-up that shows your real thinking process

**Three types:**
- `get-interview` -- an analysis showing unique insight, sent before or alongside your application to stand out. Best use: analysis for someone you want a referral from, specific to their charter.
- `in-process` -- a mini PRD or product proposal specific to the hiring manager's charter, sent while you are interviewing.
- `specific-interview` -- a problem exploration doc addressing a question you did not answer well, sent as a follow-up after an interview round. Shows you don't normally jump to solutions.

**Critical Warning (from a Meta HM):** "More of them have been a negative signal than a positive one." Most work products fail because they are generic framework exercises, not demonstrations of unique insight. The bar is: would a hiring manager forward this to their team because the analysis is genuinely useful?

Example triggers:
- `/work-product Notion + Senior PM Growth + get-interview`
- `/work-product Stripe + PM Payments Platform + in-process`
- `/work-product Anthropic + PM Claude Code + specific-interview`

## Role Type Detection

Before executing any step, read `career-plan.md` and detect the user's **target function** from their target role title:
- **Product Management (PM):** Product Manager, Group PM, Director of Product, VP Product, CPO
- **Software Engineering (SWE):** Software Engineer, Staff Engineer, Principal Engineer, Engineering Manager
- **Design:** Product Designer, UX Designer, Design Lead, Head of Design, VP Design
- **Data Science / Analytics:** Data Scientist, ML Engineer, Analytics Manager, Head of Data
- **Marketing:** Marketing Manager, Growth Marketing, Brand Manager, VP Marketing, CMO
- **Customer Success / Sales:** CSM, CS Manager, Director of CS, Account Executive, Sales Manager, CRO
- **Other:** Infer function from role description

All instructions below use PM as the default. When the detected function is NOT PM, substitute function-appropriate equivalents as marked with **[FUNCTION-ADAPTIVE]** notes throughout.

## Inputs

**Required arguments:**
- `[company]` -- the target company name
- `[role]` -- the specific role title
- `[type]` -- one of: `get-interview`, `in-process`, `specific-interview`

**Required files (read automatically):**
- `@context-library/experience-library.md` -- your real experience, metrics, stories. This is the differentiation. Without it, the work product is a generic framework exercise. With it, it reads like someone who brings real perspective.
- `@context-library/target-companies.md` -- company context, product focus, recent news
- `@context-library/career-plan.md` -- your positioning and how to frame your background

**Additional inputs by type:**
- `get-interview`: no additional input required (Claude runs research hooks)
- `in-process`: the user should provide the HM's name, their charter or team focus (from interview conversations), and any specific problems the HM mentioned
- `specific-interview`: the user must provide the specific question they fumbled and any context about what went wrong. Also reads `@context-library/interview-history.md` for the debrief notes from that round.

## Process

### CRITICAL FIRST STEP: Research Hooks

**This step runs before ANY drafting begins. A work product without research hooks is a framework exercise. With them, it reads like someone who already works at the company.**

**Step 0: Check local data first.** Before running any web searches, check `insider-data/company-intel/` for the target company. If a profile exists (e.g., `insider-data/company-intel/notion.md`), read it for product focus, interview style, recent changes, and competitive context. Also check `context-library/target-companies.md` for any notes on this company. Local data is curated and more reliable than ad-hoc web search. Use it as your foundation, then supplement with web research for recency.

For the target company, search for and document the following:

1. **Earnings call or funding announcement** -- What did the CEO or leadership say matters right now? What are the stated priorities? What metrics did they highlight? Search: "[company] earnings call transcript [recent quarter]" or "[company] funding announcement."

2. **Product reviews** -- What do real users complain about? Search: "[company] reviews G2" / "[product] App Store reviews" / "[product] Play Store reviews." Pull specific user quotes, not summaries.

3. **Product/engineering blog posts** -- What is the team publicly working on? What technical or product challenges have they written about? Search: "[company] engineering blog" / "[company] product blog."

4. **Public user complaints** -- What is broken that they know about? Search: "[company] complaints Reddit" / "[product] issues Twitter" / "[product] frustrating." Pull verbatim complaints.

5. **Recent product launches or changes** -- What direction are they moving? Search: "[company] launch [recent month]" / "[product] new feature" / "[company] product update."

**Pull 3-5 specific hooks.** Each hook should be a concrete data point, user quote, leadership statement, or observable product behavior -- not a vague summary. These hooks become the "unique insights" that make a hiring manager think "this person actually uses our product and understands our problems."

**If web search is unavailable:** Do NOT proceed with generic hooks. Instead, present the user with the exact search queries they should run manually, formatted as copy-pasteable strings:

```
I need research hooks but cannot search the web directly. Please run these searches and paste the most relevant results:

1. "[company] earnings call transcript Q[N] [year]" -- looking for CEO priorities and metrics
2. "[product] reviews site:g2.com" -- looking for specific user complaints with quotes
3. "[company] engineering blog OR product blog" -- looking for what the team is publicly building
4. "[product] complaints site:reddit.com" -- looking for verbatim user frustrations
5. "[company] product launch [recent month] [year]" -- looking for product direction signals

Paste the top 2-3 results from each search and I will extract hooks from them.
```

Do NOT draft the work product until you have at least 3 specific hooks from any combination of local data and web research. A work product without hooks will fail the quality checks.

**Present the hooks to the user before drafting.** Format:

```
## Research Hooks Found

1. [Source]: "[specific quote or data point]" -- Implication: [what this means for the product]
2. [Source]: "[specific quote or data point]" -- Implication: [what this means]
3. [Source]: "[specific quote or data point]" -- Implication: [what this means]
...

Proceed with drafting using these hooks? Or should I search for more?
```

Wait for user confirmation before proceeding to the draft.

---

### Type 1: get-interview

**Purpose:** An analysis that earns you an interview by proving you understand the company's product better than most applicants.

**Format:** 1-page analysis (Google Doc or Notion style). Max 2 pages.

**Structure:**

#### Executive Summary (2-3 sentences)
State the core insight. What did you notice about their product that is non-obvious? Lead with the research hook that is most compelling. Not "Company X has a great product but could improve." Instead: "Notion's enterprise activation drops 40% between workspace creation and first shared page. Based on my work on a similar problem at [Company], here's why -- and three approaches to fix it."

#### Why Listen to Me (3-5 sentences)
Connect your specific experience to this specific problem. Pull from `experience-library.md`. This is NOT a resume summary. It is a precise argument for why your perspective on THIS problem is informed. Structure: "I spent [time] doing [exactly this thing] at [Company]. We faced [similar challenge]. The result was [metric]. That experience is why I see [specific thing about their product] differently than most people would."

**No domain experience in the target industry?** If `experience-library.md` contains no experience in the target company's industry (e.g., you are a fintech PM targeting a healthcare company), do NOT fake domain expertise. Instead:
1. **Find the structural parallel.** Every product problem has an abstract shape that recurs across industries. Activation drop-off is activation drop-off whether it is in fintech or healthcare. Identify the underlying problem pattern (growth loops, marketplace dynamics, platform adoption, enterprise onboarding, compliance constraints) and match it to an experience where you solved a structurally similar problem.
2. **Lead with the problem pattern, not the domain.** Frame as: "I have never built healthcare software. But I have seen this exact adoption curve at [Company in different industry], where [specific parallel]. The dynamics are the same: [explain why]."
3. **Compensate with deeper research hooks.** If you cannot bring domain experience, you MUST bring deeper research. Add 2-3 additional research hooks (aim for 5-7 total instead of the standard 3-5). The extra research signals that you did the work to understand their world even if you have not lived in it.
4. **Be explicit about the trade-off in the "Why Listen to Me" section.** Honesty is more credible than bluffing: "My background is in fintech, not healthcare -- but the activation dynamics I see in [Company's] product mirror what we solved at [Company]. Here's why that cross-pollination perspective might be useful."

#### The Analysis (bulk of the doc)
Walk through your insight. Use research hooks as evidence. Structure varies by topic, but must include:
- What you observed (grounded in research hooks -- user complaints, product behavior, public data)
- Why it matters (connect to their stated priorities from earnings calls or leadership statements)
- What most people miss about this problem (your unique angle, informed by your experience)
- 2-3 non-obvious recommendations (not "improve onboarding" -- instead: "add a guided first-share flow triggered by workspace inactivity at hour 4, modeled on what worked at [Company] where similar timing-based nudges increased activation by 18%")

#### Next Steps (1-2 sentences)
Offer to discuss. Not "hire me." Instead: "Happy to walk through the data behind these recommendations or dig deeper into any of these areas."

---

### Type 2: in-process

**Purpose:** A mini PRD or product proposal that demonstrates you can do the job, targeted at the specific problem area the hiring manager owns.

**Format:** Product spec style. Max 2 pages.

**Structure:**

#### Problem Statement (3-5 sentences)
Define the problem using research hooks and what you learned in interviews. Reference what the HM told you about their team's priorities. "In our conversation, you mentioned [specific thing HM said]. Combined with [research hook -- user complaints, product data], I think the core problem is [definition]."

#### Why Listen to Me (2-3 sentences)
Same as above -- connect your specific experience to this specific problem. Shorter here because you are already in-process; they have some context on your background.

#### Proposed Solution
- User stories (3-5, specific and testable)
- Key design considerations (what are the hard trade-offs?)
- What you would NOT build (scope control signals product maturity)

#### Competitive Context (3-5 sentences)
How are competitors approaching this? What can be learned from their approach? What should be avoided? Use specific examples, not "competitors are also working on this."

#### Success Metrics
- Primary metric (what moves if this works?)
- Secondary metrics (what else changes?)
- Guardrail metrics (what should NOT move?)

#### Phased Roadmap
- Phase 1 (4-6 weeks): [specific deliverable]
- Phase 2 (next quarter): [specific deliverable]
- Future: [what you would explore next]

---

### Type 3: specific-interview

**Purpose:** A follow-up doc sent after you fumbled a specific interview question. It demonstrates that you do not jump to solutions and that your real process produces strong answers.

**Format:** Structured analysis. Max 2 pages.

**Structure:**

#### The Question
State the exact question you were asked. "In our conversation on [date], you asked: '[exact question]'."

#### What I Said vs. What I Would Say With Proper Process
Brief (2-3 sentence) honest acknowledgment: "I jumped to a solution too quickly. Here's how I would approach this with the process I normally follow."

#### Why Listen to Me (2-3 sentences)
Connect your experience to why your process for this type of problem is battle-tested. "I've navigated [similar problem type] at [Company], where [specific situation with metric]."

#### My Actual Process
Walk through the steps you would take, applying them to the specific question:

1. **Metrics analysis** -- What data would you pull first? What would you look at? Be specific to their product.
2. **User research** -- What would you want to learn? From whom? What questions would you ask?
3. **Competitive analysis** -- Who else has solved this? What can be learned from their approach?
4. **Stakeholder alignment** -- Who needs to be in the room? What are the competing priorities?
5. **Synthesis** -- Given the above, what would you recommend and why?

#### The Answer (What I Would Have Said)
The actual answer to the question, grounded in the process above. Specific, opinionated, with trade-offs acknowledged.

#### What This Shows
1-2 sentences on what you want the interviewer to take away. Not "I'm thorough." Instead: "I don't jump to solutions. When I do reach a recommendation, it's grounded in data and user insight, not instinct."

---

### Function-Specific Work Product Types [FUNCTION-ADAPTIVE]

**SWE work products:**
- get-interview: Technical architecture analysis (evaluate the company's public technical choices, identify optimization opportunities, propose alternative approaches with tradeoff analysis)
- in-process: Technical design document (requirements, API contracts, data model, failure modes, scalability considerations, monitoring strategy)
- specific-interview: System design follow-up (the full design you would have produced, with architecture diagrams, component deep-dives, and operational concerns)

**Design work products:**
- get-interview: UX audit of the company's product (heuristic evaluation, friction points, improvement proposals with wireframes)
- in-process: Design exploration (problem reframe, concept sketches, user flows, interactive prototype link)
- specific-interview: Design challenge follow-up (polished version of a design exercise with full process documentation)

**Data Science work products:**
- get-interview: Data analysis of a public dataset relevant to the company (methodology, findings, business recommendations)
- in-process: Analytical framework (metric definitions, experiment designs, model proposals with expected impact estimates)
- specific-interview: Case study follow-up (full analysis the candidate would have produced with statistical rigor)

**DS-to-MLE Transition work products (trigger: career-plan.md indicates Data Science background targeting MLE roles):**
Blend analytical depth with production engineering thinking. Do NOT produce pure DS deliverables (analysis-only) or pure SWE deliverables (code-only).
- get-interview: ML system proposal for a real company challenge (model selection + serving architecture + monitoring plan + data pipeline design)
- in-process: Production ML system design (model training pipeline, feature store integration, A/B testing framework, model performance monitoring)
- specific-interview: Case study follow-up with full production ML perspective (not just the model, but the system: latency targets, throughput, fallback behavior, retraining cadence)

**Marketing work products:**
- get-interview: GTM strategy or growth analysis for the company's market (audience insights, channel strategy, competitive positioning)
- in-process: Campaign proposal (audience segmentation, messaging framework, channel plan, measurement framework)
- specific-interview: Post-interview follow-up document: campaign or growth analysis directly relevant to the interviewer's stated challenge. Structure as: Opportunity → Proposed Approach (channel strategy + audience segmentation + messaging) → Expected Impact (projections with assumptions stated) → Measurement Framework. Keep under 3 pages.

**CS/Sales work products:**
- get-interview: CS program design proposal (health score framework, QBR redesign, onboarding playbook, or churn reduction framework)
- in-process: CS operations blueprint (org design, segmentation model, tech stack recommendation, playbook library, metric dashboard)

When generating work products, use the function-appropriate type, NOT PM deliverables (mini PRDs, user stories, product roadmaps) for non-PM roles.

---

### Final Step: Polish and Cut

**Claude runs these automated checks after drafting:**
1. **AI language scan:** Search the draft for banned phrases ("leverage," "robust," "streamline," "cutting-edge," "delve," "in today's landscape," "it's important to note," "stakeholder alignment is key," "synergy," "at the end of the day"). If any are found, rewrite those sentences in plain language before presenting the draft.
2. **Page length check:** Estimate the draft length in Google Doc equivalent (11pt, normal margins, ~500 words per page). If over 2 pages, cut the weakest paragraphs until it fits.
3. **Research hook integration check:** Verify every research hook from the pre-draft step appears naturally in the body text. If a hook was listed but never used, either integrate it or note it was dropped and why.
4. **Experience-library traceability check:** Verify the "Why Listen to Me" section references specific experience from `experience-library.md` with at least one metric. If it does not, flag: "The 'Why Listen to Me' section is missing a specific metric from your experience library. This weakens the credibility argument."
5. **Portability test:** Read the document and mentally replace the company name with a competitor. If the document still makes sense, flag the paragraphs that are too generic and suggest what company-specific detail to add.
6. **Research verification:** For every statistic, user quote, or data point in the work product, verify it came from a real web search result or insider-data file. If a data point cannot be traced to a specific source, either remove it, mark it as "[Estimate -- verify before sending]", or replace it with a directional statement (e.g., "users report frequent frustration with X" instead of a fabricated percentage). No unverifiable numbers should appear in the final output without a flag.

**Recommend to the user after output:**
- "Read this out loud before sending. If any sentence sounds like a framework or textbook, rewrite it in your own words."
- "Time-box your editing pass to 30 minutes. The draft is 80% there; over-polishing past 90 minutes signals poor time management."

**Key Principles:**
- Showcase document quality -- the work product IS the proof of your PM craft. Formatting, clarity, and structure matter as much as the ideas.
- Demonstrate unique insight -- draw on real work experience or personal observations, not framework regurgitation.
- Do not visit other websites or AI until you begin editing. Start from your own thinking first.
- Time-box: 60-90 minutes max. Over-polished work products signal poor time management, not thoroughness.
- The "Why Listen to Me" section is the single most critical differentiator. Without it, you are just another applicant who read the company blog.
- Must feel like it was written ONLY for that company. If you can swap in a competitor's name and it still works, throw it out.

**Up-leveling Tactics (ordered by impact):**
1. User research interviews (highest signal) -- even 3-5 informal conversations with users of the product
2. Direct quotes and data from real users (forums, reviews, support tickets)
3. Customer emails or public complaints with specific details
4. Public metrics or earnings data with your interpretation
5. Competitive analysis with non-obvious observations

## Output

```
## Work Product: [Type] -- [Role] at [Company]

**Type:** [get-interview / in-process / specific-interview]
**Research hooks used:** [list the 3-5 hooks with sources]
**Key experience referenced:** [which experience-library bullets you drew from]
**Page count:** [1-2 pages]

---

[Full work product text, formatted with headers and clean structure]

---

## Delivery Plan
- [ ] Export to Google Doc or Notion (clean formatting, no tracked changes)
- [ ] Share with view-only link (not edit access)
- [ ] Run `/hiring-manager-msg` to draft the outreach message that delivers this work product
- [ ] After sending, update connection-tracker.md and app-tracker with the outreach
- [ ] If no response in 5 days, follow up with a one-line ping referencing the specific insight (not the doc generically)
```

## Example

Input: `/work-product Notion + Senior PM Growth + get-interview`

Research hooks found:
1. G2 review: "Setting up Notion for my team was painful. Half the team never moved past their first page." -- Implication: enterprise activation is a real user pain point, not just a metric.
2. Notion blog post (Jan 2026): "We're investing heavily in making Notion the default workspace for teams of 500+." -- Implication: enterprise growth is a stated company priority.
3. App Store review: "I love Notion for personal use but my team gave up after a week. Too many options, no guidance." -- Implication: the blank canvas problem scales with team size.
4. Reddit r/Notion: "We switched from Notion to Coda because onboarding 50 people was impossible without a dedicated admin." -- Implication: competitors are winning on enterprise ease-of-use.

Sample "Why Listen to Me" section (PM):

> I spent two years owning activation at [Company], where new team workspaces had the same blank-canvas problem -- 60% of invited users never completed a single action in their first session. We redesigned the first-run experience around guided team templates and timing-based nudges, moving 7-day team activation from 23% to 41%. That work is why the pattern in Notion's enterprise reviews jumped out to me immediately.

Sample "Why Listen to Me" section (Marketing):

> At [Company], I rebuilt the demand-gen engine from scratch -- SEO, paid search, and content-led nurture -- growing inbound pipeline from $2M to $8M ARR in 18 months. That experience is why [target company]'s current channel mix stood out to me: the organic foundation is strong, but the paid-to-organic handoff is leaking conversion at exactly the stage where I've seen the biggest wins.

For Marketing, lead with channel mastery and pipeline metrics, not job title. Show you understand the funnel mechanics, not just that you held a marketing role.

## Quality Checks

- [ ] **Research hooks are present and specific.** At least 3 hooks, each with a source and a verbatim quote or concrete data point. If the hooks are vague summaries ("users want better onboarding"), the research step was not done properly. Redo it.
- [ ] **The "Why Listen to Me" section exists and is specific.** It must reference a concrete experience from `experience-library.md` with at least one metric. Not "I have relevant experience." Instead: "I moved X from Y to Z at [Company] by doing [specific thing]."
- [ ] **Max 2 pages.** Count the output. If it exceeds 2 pages in a standard Google Doc (11pt, normal margins), cut until it fits. Shorter is better. One page that is sharp beats two pages that are thorough.
- [ ] **No frameworks or AI-sounding language.** Ban: "leverage," "robust," "streamline," "cutting-edge," "delve," "in today's landscape," "it's important to note," "stakeholder alignment is key." If you see these, rewrite the sentence in plain language.
- [ ] **Company-specific, not portable.** Read the document and ask: could you change the company name and send this to a different company? If yes, it is too generic. Every paragraph should reference something specific to this company -- a product feature, a user complaint, a leadership quote, a competitive dynamic.
- [ ] **Experience-library integration is natural.** Your experience should appear as supporting evidence for your analysis, not as a credentials dump. "We saw this same pattern at [Company]" not "In my previous role at [Company], I was responsible for..."
- [ ] **Recommendations are non-obvious.** "Improve onboarding" is not a recommendation. "Add a guided first-share flow triggered by workspace inactivity at hour 4, based on timing patterns we observed at [Company]" is a recommendation. Each recommendation should make the HM think "that's specific enough that this person might actually be right."
- [ ] **The tone reads like a smart colleague sharing an insight, not a candidate trying to impress.** No superlatives. No exclamation points. No "I'm passionate about." Just clear thinking, grounded in evidence and experience.
- [ ] **[FUNCTION-ADAPTIVE] Function-authentic voice.** The work product should sound like a practitioner of the TARGET function, not like any other function. An SWE work product should read like an engineer wrote it (technical precision, architecture rationale, failure mode analysis). A Design work product should read like a designer wrote it (user-centered framing, visual thinking, iteration mindset). A CS work product should read like a CS leader wrote it (customer empathy, retention frameworks, operational rigor). A Data Science work product should read like a data scientist wrote it (statistical methodology, hypothesis-driven, quantitative rigor). The 'sounds like a PM not a consultant' check generalizes: the work product should sound like a practitioner, not a generalist.
- [ ] **For specific-interview type: honest acknowledgment of the fumble.** Do not pretend you crushed the answer. The honesty is the point. "I jumped to a solution too quickly" is strong. "I provided a solid initial answer but wanted to expand" is weak and dishonest.
- [ ] **Classified Experience Handling (military-to-PM career changers).** If career-plan.md shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.) and the user's most impressive work is classified, the work product must demonstrate the METHODOLOGY and THINKING, not the content. Structure: "I can't share the specific intelligence products, but here's how I would approach a similar analytical challenge in [company's domain]..." Then demonstrate the framework on a public-domain problem relevant to the target company. For defense tech work products: the work product CAN reference the military context more directly, since the audience understands it. The "Why Listen to Me" section should frame classified experience as scope and skill evidence: "I led a team of 12 analysts producing intelligence products consumed by senior military leaders. While I can't share the specific content, the analytical framework I built -- synthesizing data from 12+ sources into actionable recommendations under time pressure -- is directly applicable to [company's challenge]." For general tech work products: abstract the military context entirely and focus on the transferable methodology applied to the target company's domain.
- [ ] **Failed Founder Work Product Rule.** Conditional on `career-plan.md` showing founder/CEO at a shut-down company:
    - The work product is the founder's BEST weapon — it proves PM capability without the stigma of the company outcome. Treat it as the highest-priority deliverable.
    - SCOPE NARROWING: the work product MUST demonstrate ability to go DEEP on one area (like a Senior PM), NOT breadth across the whole business (like a CEO). If the draft reads like "here's how I'd rethink your entire product strategy," it triggers the "can't be managed" concern. Narrow it.
    - If referencing founder experience in "Why Listen to Me": frame as DOMAIN expertise, not company leadership. "I spent 4 years building health-tech products for underbanked consumers" not "I was CEO of a health-tech startup."
    - If the startup had impressive metrics despite shutting down (users, revenue, etc.): those metrics ARE valid "Why Listen to Me" material. Use them without naming the company outcome.
- [ ] **Agency-to-In-House Design Work Product Rule.** Conditional on `career-plan.md` showing agency/consulting design background (IDEO, Frog, Pentagram, AKQA, R/GA, or any agency/consultancy):
    - UX audits from agency designers risk confirming the "sprint-and-leave" bias. Counter by including an "Iteration Roadmap" section showing how audit findings would evolve over 6-12 months of in-house iteration.
    - Include a "Design Debt" section that demonstrates product-lifecycle thinking -- not just greenfield workshop output, but how you would triage and sequence existing design inconsistencies.
    - The "Why Listen to Me" section should lead with DEPTH on a single client engagement (outcomes over 6+ months, iteration cycles, measurable impact), not breadth across 30 clients. Breadth signals agency thinking; depth signals in-house readiness.
- [ ] **Early-Career Work Product Rule.** Conditional on `career-plan.md` showing < 3 years experience OR APM/Associate-level title:
    - **"Why Listen to Me" framing:** Lead with density of output, not years. "In 18 months at LearnPath, I shipped [X], ran [Y] experiments, and drove [Z] metric improvement" -- show compressed impact, not tenure.
    - **Scope the work product tightly:** 1-2 pages max. Early-career candidates overcompensate with volume. A tight, focused analysis demonstrates judgment better than a comprehensive audit.
    - **Focus on one insight, not many:** The work product should demonstrate depth of thinking on ONE thing, not breadth across many. This plays to the early-career candidate's strength (fresh perspective, deep-dive capability) and avoids their weakness (limited pattern recognition across contexts).
- [ ] **Career Returner Work Product Rule.** Conditional on `career-plan.md` showing a career gap:
    - **Avoid timeline-based language in "Why Listen to Me":** Do not write "In my 8 years at [Company] before my career break..." -- write "At [Company], I led [scope] and drove [metric]." The work should speak for itself without time-stamping.
    - **Lead with pre-gap achievements as current capability:** The work product demonstrates that the skills are intact, not that they existed in the past.
    - **PRIVACY GUARDRAIL:** No mention of why the gap occurred in any work product content.
    - **AI-Era Technology Currency (trigger: career gap overlapping 2022-2026).** If the returner's gap coincides with the AI revolution period: (1) Demonstrate how pre-gap methodology applies to new technology -- e.g., "growth PM experimentation design applies directly to AI feature adoption measurement." Frame existing skills as technology-agnostic, not outdated. (2) Include ONE concrete AI/modern-tech reference that signals current knowledge (a recent paper, tool, or framework -- e.g., referencing an evaluation methodology or a specific LLM capability). (3) Do NOT position as an AI expert. Position as a domain expert whose methods transfer. The goal is to neutralize the "world changed while you were away" concern without overcompensating.
- [ ] **Remote-Only Work Product Rule.** Conditional on `career-plan.md` showing remote-only preference:
    - The work product should subtly demonstrate async/distributed competence without explicitly mentioning remote preference.
    - Frame recommendations through the lens of distributed team execution where natural: "This rollout could follow a phased async approach — here's the sequencing..."
    - Do NOT make the work product ABOUT remote work. It's about the company's product/problem. Remote competence shows through the thinking, not the topic.
    - Privacy guardrail: no personal circumstances referenced.
- [ ] **Veteran (15+ Years) Work Product Rule.** Conditional on `career-plan.md` showing 15+ years of experience or legacy/enterprise employers:
    - TONE CHECK: the work product must NOT read like an enterprise strategy deck. It should be crisp, opinionated, and direct — more like a startup memo than an Oracle business case.
    - If the analysis references past experience: emphasize RECENT work (last 5 years). If using older examples, connect them to current trends.
    - Tech currency signal: reference at least one modern framework, tool, or methodology naturally. This combats the "not current" perception.
    - Legacy employer de-emphasis: "I led a $280M cloud migration" not "At Oracle, I led..."
    - Keep the format modern: use headers, bold, short paragraphs. No walls of text.
- [ ] **Executive-Level Work Product Rule.** Conditional on `career-plan.md` showing VP/Director/CPO/SVP level AND 12+ years experience:
    - Reframe the purpose: an executive work product is a strategic memo from a peer, not an analysis "proving" the candidate's insight. The reader should feel like they received a perspective from a fellow executive, not a homework assignment from a candidate.
    - "Why Listen to Me" becomes "Shared Context": instead of proving credentials, establish shared strategic context -- "Having led [X]-person product orgs through [Y] transitions, here's my perspective on the challenge you described..."
    - Format: executive memo (1-2 pages), not tactical analysis (3-5 pages). Lead with the strategic recommendation, then supporting rationale. No "Methodology" section -- executives don't explain their process, they share their judgment.
    - Tone: confident, direct, peer-level. No hedging ("I might suggest..."). Use "I would..." or "Here's what I'd recommend..."
    - get-interview mode: strategic perspective piece on a public company challenge (market positioning, platform strategy, competitive response).
    - in-process mode: follow-up memo extending a strategic conversation from the interview.
    - specific-interview mode: board-ready strategic analysis responding to a specific question from the executive interview.
    - org-design mode (4th type, executive-only): PM Org Blueprint. Lead with a diagnosis of the company's current product org maturity (based on research hooks: job postings, org signals, Glassdoor reviews of PM culture). Then prescribe a 12-month org evolution plan: PM levels and ladder, product process cadence, team topology, and scaling path from current state to target state. This is distinct from the three product/strategy-oriented types -- it demonstrates organizational leadership, not product thinking.
