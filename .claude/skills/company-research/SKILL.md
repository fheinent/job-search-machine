---
name: company-research
description: Deep research on a target company to inform applications, work products, interview prep, and hiring manager outreach.
---

# /company-research - Company Research Brief

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In company research contexts, this means: research briefs may use private information to filter or prioritize companies internally (e.g., filtering for sponsorship-friendly companies) but must never state the private reason in the output (e.g., write "H-1B sponsorship confirmed" not "needs sponsorship because of immigration status").

## When to Use

Run `/company-research [company name]` when:
- You are about to apply to a company and want to tailor your resume, cover letter, and outreach
- You need research hooks for a `/work-product` (this skill feeds directly into work-product research)
- You are preparing for an interview and need to understand the company's strategy, product, and culture
- You are adding a new company to `target-companies.md` and want a thorough brief
- You want to identify the hiring manager, team structure, or recent product moves before reaching out

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
- `[company name]` -- the company to research

**Optional arguments:**
- `[role title]` -- if researching for a specific role, narrows the focus to the relevant team/product area
- `[depth]` -- `quick` (5-min brief) or `deep` (full research). Default: `deep`

**Required files (read automatically):**
- `@context-library/target-companies.md` -- to check if this company already has notes and to update it
- `@context-library/connection-tracker.md` -- to surface any existing connections at this company
- `@context-library/career-plan.md` -- to focus research on areas that matter for the user's targeting strategy

## Process

### Step 1: Company Fundamentals

Research and document:

1. **Stage and funding:** Series A/B/C/D, public, etc. Last funding round, amount, valuation if available. Key investors.
2. **Size:** Employee count (approximate), growth rate (hiring velocity as a signal).
3. **Revenue model:** How do they make money? Subscription, transaction fees, marketplace, enterprise contracts?
4. **Core product(s):** What do they actually build? Who uses it? What problem does it solve?
5. **Recent trajectory:** Growing, flat, struggling? Any layoffs, pivots, or major wins in the last 6 months?
6. **Visa sponsorship history (if user needs sponsorship):** If `career-plan.md` or `qa-master.md` indicates the user needs work visa sponsorship, research and document: (a) H-1B petition count from USCIS data (search: "[company] h1b data" or check h1bdata.info, myvisajobs.com), (b) Whether the company has international offices that could enable L-1 intracompany transfer (a faster, non-lottery visa path), (c) Any public statements or Glassdoor reviews about the company's immigration support quality, (d) Recent changes to sponsorship policy (some companies reduced sponsorship after layoffs). Present as: "H-1B Sponsorship: [Confirmed / Limited / No Data]. [N] petitions filed in last 3 years. International offices: [list if relevant for L-1 path]."

### Step 2: Product Deep Dive

Focus on the product area relevant to the target role (or the flagship product if no role specified):

1. **Product experience:** Sign up for the product if free/freemium. Note the onboarding flow, core UX, and any friction points. If not free, use reviews and demos.
2. **Recent launches:** What have they shipped in the last 3-6 months? Search: "[company] product update," "[company] launch," "[company] changelog."
3. **User sentiment:** What do users love? What do they hate? Search: G2 reviews, App Store reviews, Reddit threads, Twitter/X complaints. Pull 3-5 verbatim quotes.
4. **Competitive positioning:** Who are the main competitors? How does this company differentiate? Where are they winning and losing?
5. **Technical architecture (if relevant):** Any public engineering blog posts about their stack, scale challenges, or technical bets?

### Step 3: Strategy and Leadership

1. **CEO/founder vision:** Recent interviews, podcast appearances, or blog posts from leadership. What do they say matters? Search: "[CEO name] interview," "[company] strategy."
2. **Earnings/board updates:** For public companies or late-stage startups, search for earnings call transcripts or investor updates. What metrics do they highlight?
3. **Stated priorities:** What is the company publicly betting on for the next 1-2 years?
4. **Culture signals:** Glassdoor reviews (focus on PM-specific reviews), engineering blog tone, job posting language. Is it bureaucratic or scrappy? Data-driven or intuition-driven?

### Step 4: Team and Hiring Intelligence

1. **Product org structure:** Who leads product? VP Product, CPO, Head of Product? Search LinkedIn.
2. **Hiring manager identification:** For the target role, who is the most likely HM? Look at LinkedIn for the team lead one level above the role.
3. **Team size and composition:** How many PMs? How are they organized (by product area, by function, by customer segment)?
4. **Recent PM hires:** Search LinkedIn for people who recently joined as PMs. What backgrounds do they have? This reveals what the company actually values, not just what the JD says.
5. **Open roles:** How many PM roles are open? A company hiring 5 PMs is in a different mode than one hiring 1.

**[FUNCTION-ADAPTIVE]** Replace PM-specific research with function-appropriate research. SWE: "Engineering org structure, engineering ladder (IC levels vs management), how many Staff+ engineers, recent SWE hires and their backgrounds, engineering blog quality, tech stack." Design: "Design org, Head of Design, design team size, recent design hires, design tools and process." Data Science: "Data org, Head of Data/ML, data team composition, recent DS hires, data stack." Marketing: "Marketing org, CMO/VP Marketing, marketing team structure, recent marketing hires, martech stack." CS: "CS org structure, VP/Director CS, CS team size, CS tech stack (Gainsight/Totango/Vitally), whether CS reports to CRO or CEO (critical culture signal), CS-as-revenue-center vs cost-center signal."

### Step 5: Career Changer Angle

**[FUNCTION-ADAPTIVE]** If the user is NOT a career changer (staying in their function), skip the career changer section. Instead, add function-specific org intelligence research appropriate to the target function.

**If `career-plan.md` indicates the user is a career changer (no PM title in experience):**

1. **Non-traditional PM precedent:** Search LinkedIn for people at this company who came from non-PM backgrounds. Check for:
   - **Consulting-to-PM:** People from McKinsey, BCG, Bain, Deloitte, or similar firms who are now PMs at this company. If they exist, note their names and paths -- this is proof the company hires non-traditional PMs.
   - **Engineering-to-PM:** Engineers who transitioned into PM roles at this company. Search for people whose LinkedIn shows SWE/engineering titles followed by PM titles at the same company or who joined as PMs from engineering roles elsewhere. This signals the company values technical depth in its PMs.
   - **UXR/Design-to-PM:** Researchers or designers who moved into PM roles. Search for people with UXR, design, or research titles that transitioned to product. This signals the company values user-centricity and research-driven product thinking.
   If any exist, note their names, previous titles, and current PM roles -- this is proof the company hires from the user's specific background and is the strongest signal for a career changer.
2. **MBA-to-PM pipeline:** Does this company recruit from MBA programs? Do they have an APM or rotational program? Even if the user is too senior for APM, it signals openness to non-traditional backgrounds.
3. **Domain match:** Does the user's industry expertise (from consulting, engineering, UXR, or any other domain) align with this company's domain? A McKinsey consultant who did 3 years of banking engagements has domain expertise for a fintech PM role. An engineer who built ML systems has domain expertise for an AI PM role. A UXR who studied healthcare user behavior has domain expertise for a health-tech PM role. Flag these domain overlaps.
4. **Culture fit for career changers:** Some companies strongly prefer "internal promotion" or "5+ years PM experience." Others value diverse backgrounds. Glassdoor reviews and recent hire profiles reveal which camp this company falls into.
5. **Domain Transition Precedent:** Search LinkedIn for PMs at this company who came from a DIFFERENT vertical than the company's primary domain. If the user is from healthcare applying to a fintech PM role, finding a PM at the target company who came from healthcare (or any other non-fintech vertical) is powerful evidence that domain-switching is possible there. Search: "[company] product manager" + filter by past companies in the user's domain. If found, note: "[Name] joined [Company] as PM from [different vertical]. Path: [brief description]." If none found, note: "No cross-domain PM hires found. This company may strongly prefer domain experience. Consider building a domain bridge through a work product."
6. **Non-PM Career Changer Precedent Search:** For NON-PM career changers, adapt the precedent search to the relevant function transition:
   - **Agency-to-in-house Design:** Search for designers at [Company] who came from agencies (IDEO, Frog, Pentagram, R/GA). Check LinkedIn for "agency" or "consultancy" in prior experience.
   - **DS-to-MLE:** Search for ML engineers who previously held Data Scientist titles. Filter LinkedIn by current title "ML Engineer" or "Machine Learning Engineer" + past title containing "Data Scientist."
   - **IC-to-Manager:** Search for first-time managers at [Company] -- look for promotions from Senior IC to Manager/Lead within the company. Internal promotions signal the company grows its own managers rather than only hiring externally.
   - **Military-to-civilian:** Search for employees with military background on LinkedIn. Filter by "Army," "Navy," "Air Force," "Marines," "Coast Guard," "veteran," or military titles in prior experience.
   - If precedent is found for the user's specific transition type, note it as strong evidence. If not, flag: "No [transition type] precedent found at [Company]. This may require a stronger work product or referral to get past the initial screen."

### Step 6: Connection Mapping

Cross-reference `connection-tracker.md` and suggest networking paths:

1. **Direct connections:** Anyone already at this company?
2. **Second-degree connections:** Anyone who used to work there? Anyone who knows someone there?
3. **Alumni connections:** Wharton, McKinsey, or other institutional alumni at the company? For career changers from elite institutions, alumni networks are the highest-conversion referral path.
4. **Recommended approach:** Based on the connections found, suggest the optimal path: direct referral, alumni warm intro, cold outreach with work product, or build-the-connection-first.

## Output

```markdown
## Company Research Brief: [Company Name]

**Research date:** [YYYY-MM-DD]
**Depth:** [quick / deep]
**Target role:** [role title, or "general"]

---

### Company Snapshot
- **Stage:** [Series X / Public / etc.]
- **Size:** [employee count]
- **Revenue model:** [how they make money]
- **Recent trajectory:** [growing/flat/struggling + key signal]
- **Core product:** [one-sentence description]

### Product Intelligence
- **Recent launches:** [bullet list of last 3-6 months]
- **User sentiment:** [3-5 verbatim quotes from real users, with source]
- **Competitive position:** [who they compete with, where they win/lose]
- **Biggest product opportunity:** [your assessment based on research]

### Strategy and Priorities
- **Leadership says:** [key quotes from CEO/leadership with source]
- **Stated bets:** [what the company is prioritizing for next 1-2 years]
- **Culture signals:** [scrappy vs bureaucratic, data-driven vs intuition, etc.]

### Team and Hiring
- **Product org lead:** [name, title]
- **Likely hiring manager:** [name, title, LinkedIn URL]
- **Team size:** [N PMs, organized by X]
- **Recent PM hires:** [backgrounds of last 2-3 PM hires -- what the company actually values]
- **Open [FUNCTION-ADAPTIVE] roles:** [count and titles]

### Career Changer Intel
- **Non-traditional PM precedent:** [names of people who transitioned from consulting/engineering/UXR/design/other to PM at this company, or "none found" per background type]
- **MBA pipeline:** [APM program, MBA recruiting, or neither]
- **Domain match:** [how the user's industry expertise maps]
- **Culture fit assessment:** [open to non-traditional vs. prefers PM pedigree]

### Your Connection Map
- **Direct connections:** [names from connection-tracker]
- **Alumni connections:** [names from LinkedIn search]
- **Recommended approach:** [direct referral / alumni intro / cold + work product / build connection first]

### Research Hooks for Work Product
These are ready to feed into `/work-product`:
1. [Source]: "[specific quote or data point]" -- Implication: [what this means]
2. [Source]: "[specific quote or data point]" -- Implication: [what this means]
3. [Source]: "[specific quote or data point]" -- Implication: [what this means]

---

## Recommended Next Steps
- [ ] Add/update this company in `target-companies.md`
- [ ] If connections exist: run `/referral-request`
- [ ] If no connections: run `/connection-request` targeting [suggested people]
- [ ] Run `/work-product` using the research hooks above
- [ ] Run `/job-fit-scorer` on the target role
```

## Mode 2: Target List Generation

### Trigger
`/company-research generate target list` -- generates ~100 target companies from career plan preferences.

### Inputs

- **Required:** User describes ideal companies in 2-3 sentences OR `career-plan.md` has target companies preference filled in
- **Auto-loaded:** `context-library/career-plan.md` (industry, stage, level, location preferences)
- **Auto-loaded:** `context-library/experience-library.md` (to match industry experience)

If career-plan.md is empty, STOP and tell the user: "I need your career plan filled in to generate a relevant target list. Run `Help me fill out my career plan` first."

### Process

#### Step 1: Parse Preferences
From career-plan.md and user input, extract:
- Target industries (ranked)
- Preferred company stage (startup, growth, enterprise, mix)
- Location / remote requirements
- Target level
- Comp expectations
- Any specific companies mentioned as dream targets
- Any dealbreakers (e.g., "no defense companies," "no pre-revenue startups")

#### Step 2: Generate ~100 Companies
Organize into tiers:

**Tier 1: Dream Companies (10-15)**
Companies that match every preference. Well-known, competitive, aspirational.

**Tier 2: Strong Fit (20-30)**
Match 4 of 5 preferences. Mix of well-known and respected mid-size companies.

**Tier 3: Good Fit (25-35)**
Match 3 of 5 preferences. Solid companies the user may not have considered.

**Tier 4: Worth Watching (20-25)**
Match 2-3 preferences. Earlier stage, less well-known, but interesting trajectory.

For each company, include:
- Company name
- What they do (1 line)
- Stage / size
- HQ + remote policy
- Why included (which preferences it matches)
- Estimated PM headcount (rough)

#### Step 3: Cross-Reference
- Check `insider-data/company-intel/` -- mark companies that have pre-loaded intel with **[INTEL AVAILABLE]**
- Check `connection-tracker.md` -- mark companies where user has connections with **[CONNECTED: N contacts]**

#### Step 4: Output
Write the full list to `context-library/target-companies.md`. Tell the user to review, edit, and reorder by priority.

### Output (Target List)

```markdown
# Target Companies
Generated: [date]
Last updated: [date]

Preferences: [1-line summary of what drove this list]

## Tier 1: Dream Companies (N companies)

### [Company Name] [INTEL AVAILABLE] [CONNECTED: 2 contacts]
- **What:** [1-line description]
- **Stage/Size:** [e.g., "Public, 15K employees, ~200 PMs"]
- **Location:** [HQ + remote policy]
- **Why:** [which preferences it matches]
- **Open PM roles:** [count or "check"]
- **Priority:** [1-10 user ranking -- leave blank for user to fill]

## Tier 2: Strong Fit (N companies)
[same format per company]

## Tier 3: Good Fit (N companies)
[same format per company]

## Tier 4: Worth Watching (N companies)
[same format per company]
```

## Quality Checks

**Single Company Research:**
- [ ] **User sentiment includes verbatim quotes, not summaries.** "Users say onboarding is hard" is useless. "Setting up Notion for my team was painful. Half the team never moved past their first page" (G2, 2-star review) is useful.
- [ ] **Hiring manager identification is specific.** Not "probably a Director of Product." Instead: "Jane Smith, Director of Product, Growth -- she has been at [Company] for 2 years and her team owns [area]. LinkedIn: [URL]."
- [ ] **Recent PM hires section reveals actual hiring patterns.** If the last 3 PM hires all came from FAANG with 5+ years PM experience, that is important context for a career changer. If one came from consulting, that is a green light.
- [ ] **Research hooks are concrete enough to use in a work product.** Each hook must have a source, a specific quote or data point, and an implication. Vague hooks like "users want better features" are worthless.
- [ ] **Career changer section is honest.** If no consulting-to-PM precedent exists at this company and the culture leans toward PM-pedigree hires, say so. Do not sugarcoat. The user needs to know where to spend their energy.
- [ ] **Connection map is actionable.** Not "you might know someone." Instead: "Sarah Kim (Wharton '18) is a PM at [Company]. She's in your connection-tracker -- last contact was 2 weeks ago. Recommend running /referral-request."

**Target List Generation:**
- [ ] Companies are genuinely relevant to career-plan.md preferences, not a generic "top tech" list
- [ ] Each company has a specific reason for inclusion tied to user preferences
- [ ] Insider data cross-reference done -- companies with intel flagged
- [ ] Connection tracker cross-reference done -- existing contacts surfaced
- [ ] Tier assignment reflects actual fit quality, not brand name recognition
- [ ] At least 20% of companies are lesser-known names the user likely hasn't considered

**Persona-specific checks (verify these when applicable):**
- **Visa sponsorship research required.** If career-plan.md indicates the user needs work visa sponsorship, the Company Snapshot section must ALWAYS include "H-1B Sponsorship" with petition count, confidence level, and L-1 transfer availability. This is not optional context -- it is a gating criterion. If sponsorship data cannot be found, flag: "VISA RISK: No H-1B sponsorship data found for [Company]. Verify before investing application time. Check h1bdata.info or myvisajobs.com." For the target list generation mode, EVERY company in Tiers 1-3 must have confirmed sponsorship history. Companies without confirmed sponsorship belong in Tier 4 at most, with a "Sponsorship unconfirmed" flag.
- **L-1 transfer path detection.** If the user has international work experience and is targeting US roles, check whether the target company has offices in the user's current country. If yes, flag the L-1 intracompany transfer as an alternative visa path: "[Company] has a [city] office. L-1 transfer may be possible: start at the [city] office and transfer to US, bypassing the H-1B lottery." This is high-value strategic intel for visa-requiring candidates.
- **International candidate connection mapping.** In the Connection Mapping section, specifically search for: (a) alumni of the user's universities at the target company, (b) people at the target company who previously worked in the user's home market or at their former employers, (c) people from the user's nationality/diaspora at the target company. These are the highest-conversion cold outreach paths for international candidates with zero US network.
- **Founder-friendly culture assessment (failed founder / shut-down company):** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, add a "Founder-Friendly Culture Assessment" section to the research output. Search for: "entrepreneurial hires," "startup background welcome," or evidence the company has hired founders before. Red flags: companies with rigid hierarchies, long tenure requirements, or "years in role" requirements above 3 for the level. Positive signals: intrapreneurship programs, venture arms, "move fast" culture, or leaders with founder backgrounds.
- **Career returner company intelligence.** If career-plan.md shows a career gap > 1 year, apply these adjustments:
  - Add a "Return-to-Work Program Scan" step: search for "[company] returnship program," "[company] Path Forward," "[company] iRelaunch," "[company] return to work program," "[company] career returner."
  - If a program is found: document program name, duration, conversion rate (if available), application timeline, and typical conversion level.
  - Search for "returner-friendly culture signals": has the company hired people with career gaps? Are there blog posts or employee stories about returning to work?
  - Add to output template: "Return-to-work program: [Found: name, details / Not found / Unknown]"
- **Veteran (15+ years) company intelligence.** If career-plan.md shows 15+ years of experience or legacy/enterprise employers, apply these adjustments:
  - Add an "Enterprise-to-Growth Transition Precedent" step: search for "[company] hired from Oracle," "[company] hired from IBM," or equivalent for the user's specific employer. Check LinkedIn for PMs at the target company with enterprise backgrounds.
  - Assess "veteran-friendliness": does leadership team include 15+ year veterans? Is the median PM tenure 5+ years? Are job descriptions experience-inclusive (no "digital native" language)?
  - Red flags for veterans: "fast-paced startup culture" with no experienced leaders, all-junior PM team, explicit "recent graduates" preference.
  - Add to output template: "Enterprise hire precedent: [Found: names/roles / Not found]"
- **Military-to-PM company intelligence.** If career-plan.md shows military background, apply these adjustments:
  - Add a "Defense/Military Connection Scan" step: does the company have defense contracts or government work? Do they have a veteran ERG? Have they hired military transitioners into PM roles? Do they require or prefer security clearances?
  - For defense tech companies: document specific military relationships, DoD contracts, clearance requirements, military advisory board members.
  - For general tech companies: search for military-to-tech success stories at the company.
  - Add to output template: "Military/veteran connection: [Defense contracts: Y/N | Veteran ERG: Y/N | Military PM hires: names if found | Clearance relevant: Y/N]"
