---
name: cover-letter
description: Map top 3 matching experiences to a JD's top 3 requirements in a concise, under-300-word cover letter.
---

# /cover-letter - Targeted Cover Letter Generator

## When to Use

- User pastes a JD and asks for a cover letter
- User runs `/cover-letter` with a job description
- After `/resume-tailor` flags gaps that need cover letter language, user wants the full letter
- User is applying to a role where the application requires or accepts a cover letter

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

- **Required:** Job description text (pasted or referenced)
- **Auto-loaded:** `context-library/experience-library.md` (source of truth for matching experiences)
- **Auto-loaded:** `context-library/career-plan.md` (addressing-weaknesses strategy for the opening)
- **Optional:** Output from a prior `/resume-tailor` run (uses the gap analysis to inform the letter)

If `experience-library.md` is empty or contains only template placeholders, STOP and tell the user: "Your experience library is empty. I need real experience to write a cover letter that isn't generic. Run `Help me build my experience library` first."

## Process

### Step 1: Identify the 3 Most Important JD Requirements
Read the full job description and rank requirements by importance:
- Weight REQUIRED qualifications over PREFERRED
- Weight responsibilities mentioned first or repeatedly
- Weight skills that appear in both the title and the description
- Ignore boilerplate (equal opportunity statements, benefits, generic company descriptions)

**[FUNCTION-ADAPTIVE]** For non-PM roles, weight requirements by the function's priorities. SWE: technical depth, system scale, architecture experience. Design: portfolio quality, design process, user research. Data Science: modeling experience, business impact, technical tools. CS: NRR ownership, churn reduction, team building.

**Joint optimization rule:** Do NOT just pick the 3 most important JD requirements in isolation. Optimize for **(JD importance) x (match quality)**. A JD's #1 requirement where you have a weak match is less valuable in a cover letter than the #2 requirement where you have a killer story with metrics. The goal is to present the 3 strongest pairings, not the 3 most important requirements with mediocre matches.

Specifically: after identifying the top 5 JD requirements by importance, scan `experience-library.md` for match quality on each. Score each as Strong (direct experience + metric), Moderate (adjacent experience or metric but not both), or Weak (no direct experience). Select the 3 highest-scoring pairs. If a #1-priority JD requirement only has a Weak match, drop it to the "Gaps not addressed" section and replace it with a lower-priority requirement that has a Strong match.

Output the 3 requirements you selected and why, including the match quality assessment, so the user can override if needed.

### Step 2: Find the 3 Strongest Matching Experiences
For each of the 3 top requirements, search `experience-library.md` for the single best matching bullet or story:
- Prefer entries with specific metrics over vague descriptions
- Prefer entries from the Story Bank (STAR format) when available -- these make better narratives
- Prefer recent experience over older experience
- Each experience must be different (no reusing the same bullet for two requirements)
- **For career changers (no PM title on resume):** Adjacent experience counts. Consulting deliverables (market sizing, due diligence, ops transformation) map to PM skills. Match the UNDERLYING SKILL the JD requirement demands (analytical rigor, cross-functional leadership, customer discovery, roadmap prioritization), not the literal PM title. A McKinsey engagement lead managing a 6-person team on a $200M digital transformation maps to "cross-functional leadership" even though the title was "Engagement Manager," not "Product Manager."

**CRITICAL: Only use experiences that exist in experience-library.md. If no strong match exists for a requirement, use the addressing-weaknesses strategy from career-plan.md to frame the gap honestly.**

**DECLINING PRODUCT / EMPLOYER STIGMA RULE:** If experience-library.md shows the user's primary experience is at a company or product that has publicly declined, been deprioritized, or faced significant negative press (e.g., Alexa at Amazon, Google Stadia, Meta's Reality Labs, a shut-down startup), the cover letter must proactively reframe this in the body paragraphs -- not the opening. When referencing that experience: (1) Lead with the transferable outcome, not the product name. "I grew activation 4x for a smart home platform with 50M+ users" is stronger than "I grew Alexa activation 4x." (2) Frame constrained-environment wins: "Shipping growth in a product facing headwinds taught me to prioritize ruthlessly -- I delivered $40M in cost savings while the broader org was contracting." (3) Never be defensive about the product trajectory. Interviewers respect candidates who did strong work in tough environments.

**SINGLE-EMPLOYER CONCENTRATION RULE:** If experience-library.md shows 5+ years at a single company, avoid referencing that company name more than twice in the letter. Use "at my current role" or "in my previous team" for additional references. The letter should read as "a PM who solved interesting problems" not "an [Company] PM looking for an exit." This prevents the "company PM" perception.

**CAREER CHANGER RULE: If the user has zero PM-titled roles in experience-library.md, do NOT panic or produce a generic letter. Instead: (1) Map consulting/adjacent experience to PM skills using the translations above. Engineering experience maps to: technical feasibility judgment, experiment design, metric definition, cross-functional coordination, and build-vs-buy decisions. UXR/Design experience maps to: customer discovery, experimentation design, data-driven prioritization, insight-to-roadmap translation. (2) In the opening, frame the non-traditional path as a strength. Examples by background:**
- **Consulting:** "I bring the analytical rigor of 6 years at McKinsey to product -- which means I pair customer instinct with the kind of business-case discipline most PMs learn on the job."
- **Engineering:** "After 5 years building the systems PMs spec, I bring something most product hires lack -- the technical judgment to know what's feasible before the sprint starts, and the experimentation instinct to prove what's valuable after it ships."
- **UXR/Design:** "6 years of turning user research into product decisions taught me that the best PMs don't just listen to users -- they synthesize conflicting signals into a clear direction. That's what I've been doing under a different title."
**(3) If a JD requires "X years PM experience" and the user has zero, address this ONCE in the opening framing, then never mention it again -- the body paragraphs prove capability through results, not titles.**

**DUAL-THREAD (Engineering + Consulting) Cover Letter Guidance:** When a candidate has BOTH engineering AND consulting experience before transitioning to PM, weave both threads together -- do NOT treat the candidate as purely a consultant or purely an engineer. The combination is the differentiator. Example framing: "I bring the technical depth of [X years] building software AND the strategic rigor of [Y years] at [Consulting firm] -- which means I can go deep on architecture decisions AND build the business case to get them funded." Each body paragraph should draw from whichever thread is the stronger match for that specific JD requirement.

**INTRA-FUNCTION TRANSITION HANDLING:** When `career-plan.md` shows the user is pivoting within their function (not changing to PM), apply the appropriate transition template:

- **Agency-to-In-House (Design):** Lead with scale and systems thinking: "At [Agency], I designed for 15+ clients across [industries]. At [Company], I want to go deep — building a design system that scales across [product lines] and compounding user research insights over years, not weeks." Do NOT lead with "I want to stop doing client work" — frame as what you're moving TOWARD, not away from.

- **Sales-to-CS (CS/Sales):** Lead with relationship depth: "In [X] years of enterprise sales, I've seen firsthand what happens after the deal closes — the gap between what was sold and what was delivered. I want to own that relationship long-term, driving NRR and expansion rather than just closing." Position as a strategic evolution, not a retreat from quota.

- **DS-to-MLE (Data Science):** Lead with production impact: "My recommendation models at [Company] drove $[X]M in revenue, but I want to own the full ML lifecycle — from model development through production deployment, monitoring, and iteration. That's why I'm targeting MLE roles where I can build systems that scale." Emphasize engineering skills (deployment, monitoring, infrastructure) alongside statistical skills.

- **IC-to-EM (SWE/Design/DS):** Lead with force multiplication: "As a Staff [IC role], I've realized my biggest impact comes through others — mentoring [X] engineers, driving architecture decisions across [Y] teams, and building the technical culture that ships reliable software. I want to formalize that into a management role where I can build and grow engineering teams." Do NOT lead with "I'm tired of coding" — frame as amplifying impact.

- **Brand-to-Growth Marketing (Marketing):** Lead with data-driven rigor: "My brand marketing foundation gives me deep audience understanding, and I've been building my growth toolkit — running [X] experiments, building attribution models, and optimizing funnels that drove [Y]% conversion improvement. I want to bring brand intuition to a data-driven growth role."

- **Startup-to-Enterprise or Enterprise-to-Startup (any function):** The cover letter must address the environment change directly. Startup-to-Enterprise: "After scaling [Product] from 0 to [X] users, I want to operate at a different magnitude — where my decisions affect millions of users and the infrastructure challenges require systematic, not scrappy, solutions." Enterprise-to-Startup: "After [X] years building products used by [Y] enterprises, I want to apply that systems thinking to a stage where I can move faster, own more surface area, and directly see the impact of every decision."
  - **Fintech-specific startup-to-enterprise example (founder-to-fintech):** "After building [Product]'s payments infrastructure from zero to [X] transactions/month, I understand the merchant/payment experience from the builder's side -- I've been on the other side of the API that your customers integrate with." Use this framing for founder-to-fintech transitions targeting companies like Stripe, Brex, or Adyen where API-side experience is a differentiator.

**EXECUTIVE-LEVEL LETTER RULE:** If career-plan.md shows the user is at Director level or above (Director, VP, SVP, CPO, Head of Product), the cover letter must read as one executive proposing to join another executive's team -- not as a candidate pleading for consideration. Apply these adjustments:
- **Opening paragraph:** Do NOT lead with enthusiasm about the company or the role. Instead, lead with a strategic insight about the company's product challenge -- something that demonstrates you have already been thinking about their business at a senior level. Example: "Notion's expansion into enterprise is a classic PLG inflection point -- the product-led motion that drove adoption now needs to coexist with a sales-assisted motion without destroying what made Notion sticky. That's the exact problem I spent three years solving at [Company]." The opening should read as a peer offering a perspective, not a candidate expressing interest. **[FUNCTION-ADAPTIVE]** The strategic opening should reference the function-specific challenge. SWE: a technical architecture challenge (e.g., "Stripe's migration to a multi-region payment processing architecture is exactly the distributed systems problem I solved at [Company]"). Design: a design systems or UX consistency challenge. CS: a retention or expansion challenge. Marketing: a growth or brand positioning challenge. Do NOT default to "product challenge" for non-PM roles.
- **Body paragraphs:** Invert the standard structure. Instead of "JD requirement -> my matching experience," lead with a strategic observation about the company's challenge, then connect your experience as evidence of your ability to solve it. Each paragraph should demonstrate executive-level pattern recognition: you see the problem, you have solved a version of it before, and you have a point of view on how to approach it here.
- **Tone:** Peer-to-peer. No deference. No "I would be excited to contribute." Instead: "I'd welcome a conversation about how I'd approach this." The letter should feel like a senior hire writing to a future peer, not an applicant writing to a gatekeeper.
- **Qualification framing:** At Director+ level, the qualification sentence is shorter -- background speaks for itself. One line with scope metrics (revenue owned, team size, user base) is sufficient. Do not over-explain or list multiple achievements. Executives summarize; they do not enumerate.
- **Weakness handling:** Executives do not preemptively address weaknesses in the opening. If there is a gap (e.g., industry change), address it with confidence in one sentence in the relevant body paragraph, not in the opening. Frame it as a deliberate strategic choice, not a gap to explain away.

**REMOTE-ONLY PERSONA CHECK:** If `career-plan.md` shows the user has a remote-only preference or caregiver/family constraints, apply these adjustments:
- **Never mention WHY the candidate prefers remote.** Only that they thrive in distributed environments. The letter sells capability, not logistics.
- **Opening paragraph leads with impact, not "as a remote worker."** Remote is a work arrangement, not an identity. The opening must demonstrate what the candidate DOES, not WHERE they do it. Good: "I've shipped 3 major product launches across distributed teams spanning 4 time zones." Bad: "As a remote worker with 6 years of experience..."
- **Hybrid/onsite JD mismatch handling:** If the JD says "hybrid" or "onsite" but career-plan.md says remote-only, output a WARNING before the letter: "WARNING: This role specifies [hybrid/onsite]. Your career plan indicates remote-only. This may be a dealbreaker -- confirm before investing application time." Still generate the letter focusing on the work, not the location. Do not mention the mismatch in the letter itself.
- **PRIVACY GUARDRAIL:** Never reference caregiving, children, family obligations, health conditions, or any personal reason for remote preference. This information, even if shared in career-plan.md, is NEVER included in any external-facing document. This applies to the cover letter, the gap suggestions, and any supplementary notes.

**CAREER RETURNER PERSONA CHECK:** If `career-plan.md` shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), apply these adjustments:
- **Opening paragraph:** Lead with the strongest pre-gap achievement + what excites them about THIS role. Do NOT lead with "After a career break..." or "Returning to the workforce..." The opening must establish credibility before any hint of a gap.
- **Gap acknowledgment (2+ years):** If the gap is 2+ years, include ONE sentence max that signals awareness without dwelling: "Eager to bring [X years of experience] back to [domain] -- I've stayed current through [specific activity]." Then move on immediately. This sentence goes in the bridge between the opening and the first body paragraph, not as a standalone paragraph.
- **Banned language:** Never use: "gap," "break," "hiatus," "returning," "back to work," "re-entering." Reframe as forward momentum: "focused on," "building on," "bringing [X] to [Y]."
- **During-gap professional activity:** Reference any during-gap professional activity naturally (certification, advisory role, freelance project) as supporting evidence in the body paragraphs. Do not create a separate paragraph about what you did during the gap.
- **PRIVACY GUARDRAIL:** Never reference the REASON for the gap. External documents present the work history and professional trajectory only.

### Re-Application Framing

If the user previously applied to this company and was rejected (check interview-history.md):
- Acknowledge the prior application positively: "I interviewed with [Company] last year and the experience confirmed this is where I want to build my career. Since then, I've [specific new qualifications]."
- Lead with what's NEW since the rejection, not rehashed old content.

### Step 3: Write the Opening Paragraph (2-3 sentences)
The opening must do two things:
1. **Express genuine enthusiasm** for the specific role and company. Reference something concrete: a product feature, a recent launch, a company value. Not "I'm excited about this opportunity" -- instead, "Notion's recent AI blocks launch is the kind of product bet I want to work on."
2. **Preemptively address your biggest weakness** using the addressing-weaknesses framework from career-plan.md. If your biggest gap is years of experience, frame your trajectory. If it's domain expertise, frame adjacent experience. This goes in the opening because recruiters form impressions in the first 10 seconds.

**For career changers:** The opening is where you reframe the narrative. Do NOT be defensive ("Although I lack PM experience..."). Instead, frame the transition as intentional and additive: "After six years solving growth strategy problems at McKinsey -- including [specific relevant engagement] -- I'm moving to product because I want to own the solution, not just the recommendation." The framing should make the reader think "this person chose PM deliberately" not "this person is trying to break in."

### Step 4: Write 3 Body Paragraphs (2-4 sentences each)
Each paragraph follows this structure:
1. **Lead with the JD requirement** (show you read the posting)
2. **Connect to your specific experience** (the match from Step 2)
3. **Include the metric or outcome** (proof, not just claim)
4. **Bridge to why this matters for the role** (show you understand their context)

Keep each paragraph tight. No filler sentences. No "I believe I would be a great fit because..." -- show, don't tell.

### Step 5: Write the Closing (2-3 sentences)
The closing must include a **soft ask**, not a hard close:
- Good: "I'd welcome the chance to discuss how my experience with [X] could contribute to [team/product]. I'm available for a conversation whenever it's convenient."
- Bad: "I am confident I am the ideal candidate. Please contact me at your earliest convenience."
- Never beg. Never grovel. Never use "I would be honored." Sound like a peer, not a supplicant.

### Regional Variants

**UK:** Slightly longer acceptable (350 words). Use UK spelling. More conversational tone common in UK tech.

**Germany (Motivationsschreiben):** 500-600 words. Formal salutation ("Sehr geehrte Damen und Herren" if no name). More structured argumentation. Explain career logic and motivation more explicitly than US format.

**India:** More formal tone. Can reference specific company values/mission more extensively. 300-400 words.

**Middle East:** More formal, respectful-of-hierarchy tone. Address seniority of reader. 300-400 words.

Default to US format (under 300 words, direct) unless career-plan.md specifies a non-US target market or the JD is clearly from a non-US company.

### Step 6: Word Count Check
Count the total words. **LLMs estimate word counts imprecisely -- aim for 270 words as the target, not 300.** This leaves a buffer so the actual count stays under the hard limit. If over 300, cut. If between 280-300, attempt to trim further. Priorities for cutting:
1. Remove any sentence that restates something already said
2. Shorten metric descriptions (keep the number, cut the setup)
3. Trim the opening if it's more than 3 sentences
4. Never cut the metrics or specific details -- those are the substance

### Step 7: Final Polish
- Read the full letter for tone: it should sound like a smart colleague writing to a peer, not a form letter
- Check that no sentence starts with "I" more than twice consecutively
- Verify every claim traces back to experience-library.md
- Confirm the letter is specific enough that it could NOT be sent to any other company without edits
- Apply the same "pointy profile" principle from resume tailoring: the cover letter should reinforce a single through-line identity, not present a generic "I can do everything" pitch
- If a `/resume-tailor` run preceded this, the cover letter should specifically address the gaps flagged in that run -- this is the cover letter's primary purpose beyond the resume

## Output

```markdown
## Cover Letter - [Company Name] [Role Title]
**Word count:** [N]/300
**Top 3 JD requirements addressed:**
1. [Requirement] --> matched with [Experience bullet source]
2. [Requirement] --> matched with [Experience bullet source]
3. [Requirement] --> matched with [Experience bullet source]

---

Dear [Hiring Team / specific name if known],

[Opening paragraph: enthusiasm + weakness preempt]

[Body paragraph 1: JD requirement 1 --> experience match with metric]

[Body paragraph 2: JD requirement 2 --> experience match with metric]

[Body paragraph 3: JD requirement 3 --> experience match with metric]

[Closing paragraph: soft ask]

Best,
[Name]

---

**Gaps not addressed in this letter:**
- [Any remaining JD requirements not covered, with brief notes on how to address via referral or interview]
```

## Example

**Input:**
```
/cover-letter

Product Manager, Growth - Stripe
Requirements: 5+ years PM experience, growth/experimentation expertise,
payments or fintech domain, SQL/data fluency, cross-functional leadership
```

**Output:**
```markdown
## Cover Letter - Stripe Product Manager, Growth
**Word count:** 247/300
**Top 3 JD requirements addressed:**
1. Growth/experimentation expertise --> "Built A/B testing framework, ran 40+ experiments, activation 23% to 41%"
2. Payments/fintech domain --> "Deep fintech domain: built lending product, payments infrastructure"
3. Cross-functional leadership --> "Led 8-person cross-functional team across eng, design, data"

---

Dear Stripe Growth Team,

Stripe's recent embedded finance push -- particularly Connect's expansion into platforms -- is the intersection of fintech infrastructure and growth experimentation where I've spent the last four years building. I come from a non-traditional PM path through consulting, which means I pair product instincts with the analytical rigor of someone who spent two years building business cases before building products.

Your growth team needs someone who can run high-velocity experiments on conversion and activation. At [Company A], I built the experimentation framework from scratch and personally designed 40+ A/B tests that moved our activation rate from 23% to 41% over eight months. I also own the SQL dashboards the team still uses to monitor funnel health daily.

Fintech is not new territory for me. At [Company B], I shipped a lending product end-to-end -- from regulatory scoping through KYC/AML flows to launch -- processing $12M in the first quarter. I understand the compliance constraints that make fintech growth harder than typical SaaS.

Shipping experiments that move metrics requires alignment across eng, design, and data. I led an 8-person cross-functional team at [Company A] that shipped a recommendation engine in 6 weeks, which taught me that growth PMs succeed by removing blockers, not by writing longer specs.

I'd welcome a conversation about how my experimentation and fintech experience could accelerate Stripe's growth initiatives. Available anytime that works for your team.

Best,
[Name]

---

**Gaps not addressed in this letter:**
- "5+ years PM experience" - Have 4 years PM + 2 years adjacent. Addressed in opening framing. If asked directly, use addressing-weaknesses script from career-plan.md.
```

**[FUNCTION-ADAPTIVE] SWE Example (abbreviated):**
```
/cover-letter

Staff Software Engineer, Platform - Stripe
Requirements: 8+ years engineering experience, distributed systems, payments or fintech,
technical leadership, system design at scale
```
Opening: "Stripe's migration to multi-region payment processing is a distributed systems challenge I know well -- I spent three years at [Company] rebuilding our payment retry system to handle 12K TPS across 4 regions with 99.99% uptime. That kind of reliability-at-scale engineering is what drew me to this role."
Body paragraph 1 maps "distributed systems" to a specific architecture decision with latency and throughput metrics. Body paragraph 2 maps "technical leadership" to mentoring 6 engineers and driving an RFC process. The tone is peer-to-peer among engineers, emphasizing technical depth over management scope.

## Quality Checks

**Good output looks like:**
- Under 300 words, no exceptions. Every word earns its place.
- The 3 body paragraphs each connect ONE specific experience to ONE specific JD requirement
- Opening mentions something specific about the company that could not apply to any competitor
- The addressing-weaknesses framing sounds confident, not defensive
- Metrics are present in at least 2 of the 3 body paragraphs
- The closing is a soft ask, not a desperate plea or an arrogant demand
- Every claim traces back to experience-library.md -- nothing fabricated
- The letter sounds human. Read it aloud: does it sound like an actual person wrote it?

RULE: Never address termination or involuntary departure in the cover letter. The cover letter sells strengths. Departure framing belongs in interview prep only.

For candidates with significant classified experience: lead with unclassified work. Use classified work as secondary evidence described at the methodology/approach level only.

**Bad output looks like:**
- Over 300 words (the whole point is conciseness)
- Generic opening: "I am writing to express my interest in the Product Manager position"
- Body paragraphs that describe skills without specific examples or metrics
- All 3 paragraphs pull from the same role or same project (lack of range)
- Closing: "I am confident I would be a great addition to your team" (cliche, no soft ask)
- Claims not in the experience library (fabricated experience)
- Could be sent to three other companies without changing a word (too generic)
- Defensive tone around weaknesses: "Although I lack..." instead of framing strength

**Persona-specific checks (verify these when applicable):**
- **Single employer (5+ years):** Company name appears no more than 2x. Body paragraphs use "in my current role" for additional references.
- **Declining product:** At least one body paragraph frames constrained-environment wins positively. Product name is secondary to user outcomes.
- **Career changer:** Opening frames transition as intentional, not defensive. "X years PM experience" gap addressed once in opening, never again.
- **International/unknown employers:** Every non-US-famous employer is contextualized with a brief parenthetical (scale + market position) on first mention.
- **Manager-to-IC transition:** If career-plan.md indicates the user managed a team but is now targeting IC roles, body paragraphs must lead with hands-on IC contributions (shipped, designed, analyzed, defined, tested), not management achievements (managed team, drove OKR process, hired). Include at most one brief management reference to show leadership range, and frame IC pursuit as a deliberate choice toward product depth -- never as a retreat from management.
- **Pay-cut / downleveling:** If the user is targeting below their current level, no language implies "I'm settling" -- frame as intentional pursuit of IC craft, product area, or mission alignment.
- **Early-career / thin experience (fewer than 3 years):** (a) Opening reframes thin tenure as concentrated output -- e.g., "In 18 months I shipped X, Y, and Z" rather than leading with years. (b) Body paragraphs lead with metrics, not role descriptions. Every paragraph opens with a number or outcome, not "In my role as..." (c) No apologetic language anywhere. Ban: "despite my limited experience," "although I'm early in my career," "I may not have X years but..." These phrases prime the reader to see a gap instead of a candidate.
- **Domain-locked (out-of-domain application):** Body paragraphs lead with the transferable skill label, and domain context is supporting detail. Good: "I've run 40+ pricing experiments across 4M users -- in a healthcare context, but the experimentation rigor transfers directly." Bad: "At my healthcare company, I ran pricing experiments." The reader should see the skill first and the domain second.
- **Remote-only candidate:** If career-plan.md indicates remote-only preference: (a) Opening paragraph leads with impact, not "as a remote worker." (b) No mention of WHY the candidate prefers remote -- only that they thrive in distributed environments. (c) If the JD says "hybrid" or "onsite" but career-plan.md says remote-only, a WARNING was generated. The letter still focuses on the work, not the location. (d) PRIVACY GUARDRAIL: No reference to personal circumstances (caregiving, family, health) anywhere in the letter.
- **Career gap / returner:** If career-plan.md shows a career gap: (a) Opening paragraph leads with strongest pre-gap achievement + excitement for THIS role. Does NOT lead with "After a career break..." (b) No use of "gap," "break," "hiatus," "returning," or "back to work" -- language is reframed as forward momentum. (c) During-gap professional activity is referenced naturally. (d) If gap is 2+ years, at most ONE sentence signals awareness: "Eager to bring [X years of experience] back to [domain]." Then moves on immediately.
- **Failed founder / shut-down company (founder-to-employee persona):** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value: (a) Opening leads with the SCALE of problems solved, not the company outcome. Good: "I spent 4 years building a health-tech product from zero to 12K users." Bad: "After my startup didn't work out..." (b) The letter proactively addresses the "can you take direction?" concern by including a line about collaboration: "I'm energized by joining a team where I can focus deeply on [area] rather than spreading across every function." (c) Never uses: "failed," "shut down," "pivoted away from," "didn't work out." (d) The transition is framed positively: "After building [X] from scratch, I'm excited to bring that builder mindset to [Company] where I can focus on [specific area] at scale."
- **Compound failure narrative (two+ consecutive non-successes):** If career-plan.md shows two+ companies that shut down or underperformed: (a) Frame Company B as a DELIBERATE APPLICATION of Company A lessons. "After building [Company A] and learning [specific lesson], I applied that insight at [Company B] where I [specific achievement]." (b) The letter must present the two stints as a COHERENT LEARNING ARC, not two independent failures. (c) One sentence max on the arc -- then pivot to the target role immediately.
- **Stronger employer brand identity rule (founder with well-known prior employer):** If career-plan.md shows the user has a well-known prior employer (Google, Meta, Amazon, Nubank, etc.) IN ADDITION to their founder experience: (a) The cover letter opening should lead with the known employer achievement, not the founder stint. "At [Strong Brand], I [big achievement]" is a stronger opening than "I co-founded [Shut-Down Startup]." (b) The founder experience appears as supporting context in the middle of the letter. (c) Exception: if applying to a founder-friendly company or the founder experience is directly more relevant to the target role.
- **Military-to-PM career changer:** If career-plan.md shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), apply these adjustments: (a) Opening paragraph: lead with the TRANSFERABLE SKILL, not the military title. Good: "I've spent 6 years leading complex, high-stakes operations where incomplete data and fast decisions are the norm -- the same muscle that drives great product management." Bad: "As a former Army Captain..." (b) Bridge sentence: explicitly connect military experience to PM competencies. "In the military, I managed ambiguity daily -- coordinating 30-person teams across time zones with imperfect information, making trade-offs that affected mission success. That's what product management is." (c) For defense tech applications: lean INTO the military identity. "My 6 years in military intelligence give me a native understanding of the end-user problem space that most PMs would need years to develop." (d) For general tech applications: lead with the SKILL, mention military as context. The ratio should be 70% transferable skill, 30% military context. (e) All military jargon in the letter must be fully translated to civilian business language.
