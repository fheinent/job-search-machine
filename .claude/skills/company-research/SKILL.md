---
name: company-research
description: Deep research on a target company to inform applications, work products, interview prep, and hiring manager outreach.
---

# /company-research - Company Research Brief

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In company research contexts, this means: research briefs may use private information to filter or prioritize companies internally (e.g., filtering for sponsorship-friendly companies) but must never state the private reason in the output (e.g., write "H-1B sponsorship confirmed" not "needs sponsorship because of immigration status").

## Understanding Confidence Levels

All research output includes confidence scores that indicate how recent and reliable data is. Use them to decide whether to act on the research:

| Level | Meaning | When to Use | When to Refresh |
|-------|---------|------------|-----------------|
| **HIGH** | Data verified within recency window (14-30 days for most data) | Safe to include in conversations, presentations, apply decisions | No immediate refresh needed |
| **MEDIUM** | Data is 30-90+ days old but considered still relevant | Safe to reference but mention the date | Consider refresh before major decisions |
| **LOW** | Data is 90+ days old or based on older sources | Use with caution; mention the age | Refresh before interviews or major decisions |
| **STALE** | Data is >180 days old or source is explicitly archived | Do not rely on for decision-making | **Must refresh before using** |
| **HIGH CONFIDENCE ABSENCE** | We actively searched and found NO data | Safe to say "no data available" | Only refresh if strategy changes |

**Example interpretations:**
- "Company raised $30M Series B in Nov 2022 [CONFIDENCE: HIGH - funding announcement dated Nov 15, 2022]" → Safe to cite in interview
- "ADR growth trailed inflation in 2025 (1.6% vs. 2.7%) [CONFIDENCE: MEDIUM - Lodgify 2026 Industry Report published May 2026]" → Cite but mention source/date
- "VP of Data departed 1 month ago [CONFIDENCE: HIGH - confirmed via LinkedIn search on 2026-05-10]" → Current, trustworthy
- "Most recent PM hire: Jane Smith, 18 months ago [CONFIDENCE: LOW - hire date >12 months]" → Refresh LinkedIn to check if still representative
- "No H-1B sponsorship data found [CONFIDENCE: HIGH CONFIDENCE ABSENCE - searched h1bdata.info and USCIS records, 2025 data]" → Safe to say company doesn't sponsor

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

## Data Freshness Reference

Every claim in company research includes a confidence level based on data recency. Use these thresholds to assign confidence when conducting research:

### Confidence Thresholds by Data Type

**COMPANY FUNDAMENTALS** (Stage, Size, Revenue, Trajectory)
- **HIGH:** Verified within 30 days (funding announcement, latest financial disclosure, recent news)
- **MEDIUM:** 30-90 days old (recent press release, analyst report, company blog post)
- **LOW:** 90+ days old (older financial data, archived blog posts, year-old news)
- **STALE:** >180 days old (requires refresh before acting)

**PRODUCT INTELLIGENCE** (Recent Launches, User Sentiment, Competitive Positioning)
- **HIGH:** Verified within 14 days (latest G2/Trustpilot reviews, recent changelog, fresh demo)
- **MEDIUM:** 14-60 days old (moderately recent user reviews, product updates from 1-2 months ago)
- **LOW:** 60-90 days old (user feedback from quarter ago)
- **STALE:** >90 days old (product landscape may have shifted)

**LEADERSHIP & STRATEGY** (CEO Vision, Stated Priorities, Culture Signals)
- **HIGH:** From past 30 days (recent interview, podcast appearance, blog post)
- **MEDIUM:** 30-120 days old (recent earnings call, company announcement, board update)
- **LOW:** 120+ days old (older strategic statements, archived interviews)
- **STALE:** >180 days old (strategy may have pivoted)

**TEAM & HIRING** (Org Structure, Hiring Manager Identity, Recent Hires, Open Roles)
- **HIGH:** Verified within 7 days (LinkedIn search just performed, current job board, recent hire announcement)
- **MEDIUM:** 7-30 days old (LinkedIn data 1 month old, recent hire from weeks ago)
- **LOW:** 30-60 days old (org chart from 1-2 months back)
- **STALE:** >60 days old (requires re-check before relying)

**H-1B SPONSORSHIP DATA**
- **HIGH:** Current year petition data from USCIS or h1bdata.info (updated 2025)
- **MEDIUM:** Previous year data (2024 confirmed, 2025 estimated)
- **LOW:** 2+ year old data
- **STALE:** >2 years old (sponsorship policy may have changed)

**CAREER CHANGER PRECEDENT** (Non-traditional hires, transitions, domain switches)
- **HIGH:** Hire within past 6 months (confirmed via LinkedIn recent activity)
- **MEDIUM:** Hire within past 12 months
- **LOW:** Hire 12-18 months ago (may have left company)
- **STALE:** >18 months old (person may have churned, not representative of current hiring)

### Confidence Assignment Rules

- If exact research date is known → assign based on days elapsed
- If source includes implied date (e.g., "latest earnings call" or "recent announcement") → estimate conservatively
- If source has no date but is inherently current (e.g., "current job board") → HIGH
- If source is archived/cached → assign based on archive date, flag as "archive source"
- If data point is stated as "no data available" or "none found" → this is **HIGH CONFIDENCE ABSENCE** (actively searched, found nothing). Mark as such.
- If data point was researched months ago and not re-verified → LOW or STALE, not HIGH

### Warning Thresholds

Automatically flag:
- ANY data point >6 months old → "[VERIFY - researched [date]. Details may have changed.]"
- MAJOR data point (funding, headcount, strategy) >3 months old → "[CAUTION - data from [date]. Recommend refresh.]"
- Career changer precedent >12 months old → "[NOTE - hire from [date]. May no longer reflect current hiring patterns.]"

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

Research and document. **For each data point, note the SOURCE and DATE of the information you find.** Assign confidence levels using the Data Freshness Reference above.

1. **Stage and funding:** Series A/B/C/D, public, etc. Last funding round, amount, valuation if available. Key investors. [Note: Funding announcements have dates; cite them. Example: "Series B, $30M, November 2022 [CONFIDENCE: HIGH - funding announcement]"]
2. **Size:** Employee count (approximate), growth rate (hiring velocity as a signal). [Note: If from company About page or Crunchbase, cite the data age. If estimated, flag as "~[number] estimated from [source] [date]"]
3. **Revenue model:** How do they make money? Subscription, transaction fees, marketplace, enterprise contracts?
4. **Core product(s):** What do they actually build? Who uses it? What problem does it solve?
5. **Recent trajectory:** Growing, flat, struggling? Any layoffs, pivots, or major wins in the last 6 months? [Note: Cite the news source and date. Flag 6+ month old data as potentially stale.]
6. **Visa sponsorship history (if user needs sponsorship):** If `career-plan.md` or `qa-master.md` indicates the user needs work visa sponsorship, research and document: (a) H-1B petition count from USCIS data (search: "[company] h1b data" or check h1bdata.info, myvisajobs.com) — **Note the data year** (2024, 2025, etc.), (b) Whether the company has international offices that could enable L-1 intracompany transfer (a faster, non-lottery visa path), (c) Any public statements or Glassdoor reviews about the company's immigration support quality, (d) Recent changes to sponsorship policy (some companies reduced sponsorship after layoffs). Present as: "H-1B Sponsorship: [Confirmed / Limited / No Data] [CONFIDENCE: HIGH/MEDIUM/LOW]. [N] petitions filed in [year] ([data age]). International offices: [list if relevant for L-1 path]. [If >2 years old: [CAUTION - verify current sponsorship status]]"

### Step 2: Product Deep Dive

Focus on the product area relevant to the target role (or the flagship product if no role specified). **For reviews and sentiment, note the REVIEW DATE and platform. For launches, cite the announcement date.**

1. **Product experience:** Sign up for the product if free/freemium. Note the onboarding flow, core UX, and any friction points. If not free, use reviews and demos. [Date of your review: today's date]
2. **Recent launches:** What have they shipped in the last 3-6 months? Search: "[company] product update," "[company] launch," "[company] changelog." [For each launch, cite the announcement date. If 'recent' means >3 months, flag it: "[CAUTION - 'recent' launch is [date], now older than 3 months]"]
3. **User sentiment:** What do users love? What do they hate? Search: G2 reviews, App Store reviews, Reddit threads, Twitter/X complaints. Pull 3-5 verbatim quotes. [For each quote, include: Source (G2/Trustpilot/etc.), rating (if available), and review date. Example: "Setting up Notion for my team was painful" (G2, 2-star, 2026-04-15) [CONFIDENCE: HIGH if <14 days, MEDIUM if <60 days, LOW if older]]
4. **Competitive positioning:** Who are the main competitors? How does this company differentiate? Where are they winning and losing? [CONFIDENCE: MEDIUM if 30-90 days old, LOW if >90 days old]
5. **Technical architecture (if relevant):** Any public engineering blog posts about their stack, scale challenges, or technical bets? [Note the blog post date; flag >6 month old posts as potentially outdated]

### Step 3: Strategy and Leadership

**When citing leadership quotes, note the INTERVIEW/PUBLICATION DATE. Old strategic statements may be outdated.**

1. **CEO/founder vision:** Recent interviews, podcast appearances, or blog posts from leadership. What do they say matters? Search: "[CEO name] interview," "[company] strategy." [For each quote, cite: source, publication name, date. Example: "We're betting on AI-first infrastructure" (CEO interview, [publication], [date]) [CONFIDENCE: HIGH if <30 days, MEDIUM if <120 days, LOW if older]]
2. **Earnings/board updates:** For public companies or late-stage startups, search for earnings call transcripts or investor updates. What metrics do they highlight? [Note: earnings calls have dates; cite them. Flag Q2 2025 calls as potentially stale in 2026]
3. **Stated priorities:** What is the company publicly betting on for the next 1-2 years? [If no recent strategic communication found, flag explicitly: "[LOW] No recent strategy updates found. Last confirmed: [date]. Consider refreshing before interviews."]
4. **Culture signals:** Glassdoor reviews (focus on PM-specific reviews), engineering blog tone, job posting language. Is it bureaucratic or scrappy? Data-driven or intuition-driven? [CONFIDENCE: MEDIUM-HIGH if based on recent job postings/reviews from past 60 days, MEDIUM if older]

### Step 4: Team and Hiring Intelligence

**LinkedIn searches are time-stamped by when you perform them. Note this date. For 'recent' hires, explicitly state hire date or when they joined.**

1. **Product org structure:** Who leads product? VP Product, CPO, Head of Product? Search LinkedIn. [Note: LinkedIn data you found today is [today's date]; if you're reading old research, re-check LinkedIn]
2. **Hiring manager identification:** For the target role, who is the most likely HM? Look at LinkedIn for the team lead one level above the role. [CONFIDENCE: HIGH if found on current job board, MEDIUM if inferred from org chart dated within 30 days, LOW if org data is >60 days old]
3. **Team size and composition:** How many PMs? How are they organized (by product area, by function, by customer segment)? [Note data date: "[N] PMs as of [date]"]
4. **Recent PM hires:** Search LinkedIn for people who recently joined as PMs. What backgrounds do they have? This reveals what the company actually values, not just what the JD says. [For each hire, note: name, join date (if visible or estimated), previous background. Example: "Jane Smith joined 2 months ago from McKinsey" [CONFIDENCE: HIGH if <6 months, MEDIUM if 6-12 months, LOW if >12 months]]
5. **Open roles:** How many PM roles are open? A company hiring 5 PMs is in a different mode than one hiring 1. [As of [date], pulled from job board]

**[FUNCTION-ADAPTIVE]** Replace PM-specific research with function-appropriate research. SWE: "Engineering org structure, engineering ladder (IC levels vs management), how many Staff+ engineers, recent SWE hires and their backgrounds, engineering blog quality, tech stack." Design: "Design org, Head of Design, design team size, recent design hires, design tools and process." Data Science: "Data org, Head of Data/ML, data team composition, recent DS hires, data stack." Marketing: "Marketing org, CMO/VP Marketing, marketing team structure, recent marketing hires, martech stack." CS: "CS org structure, VP/Director CS, CS team size, CS tech stack (Gainsight/Totango/Vitally), whether CS reports to CRO or CEO (critical culture signal), CS-as-revenue-center vs cost-center signal."

### Step 5: Career Changer Angle

**[FUNCTION-ADAPTIVE]** If the user is NOT a career changer (staying in their function), skip the career changer section. Instead, add function-specific org intelligence research appropriate to the target function.

**If `career-plan.md` indicates the user is a career changer (no PM title in experience):**

1. **Non-traditional PM precedent:** Search LinkedIn for people at this company who came from non-PM backgrounds. Check for:
   - **Consulting-to-PM:** People from McKinsey, BCG, Bain, Deloitte, or similar firms who are now PMs at this company. If they exist, note their names and paths -- this is proof the company hires non-traditional PMs. [For each person found: name, previous company, current PM title, join date (if visible) [CONFIDENCE: HIGH if <6 months, MEDIUM if 6-12 months, LOW if >12 months]]
   - **Engineering-to-PM:** Engineers who transitioned into PM roles at this company. Search for people whose LinkedIn shows SWE/engineering titles followed by PM titles at the same company or who joined as PMs from engineering roles elsewhere. This signals the company values technical depth in its PMs. [Include: transition date or hire date [CONFIDENCE: HIGH if <6 months, MEDIUM if 6-12 months, LOW if >12 months]]
   - **UXR/Design-to-PM:** Researchers or designers who moved into PM roles. Search for people with UXR, design, or research titles that transitioned to product. This signals the company values user-centricity and research-driven product thinking. [Include: transition date [CONFIDENCE: HIGH if <6 months, MEDIUM if 6-12 months]]
   If any exist, note their names, previous titles, current PM roles, and **hire dates** -- this is proof the company hires from the user's specific background. If precedent is found but >12 months old, flag: "[PRECEDENT FOUND but >12 months old. Verify if still representative of current hiring.]"
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
**Data Confidence Summary:** [HIGH / MEDIUM / LOW / MIXED - brief summary]
**[CAUTION]** if any major data point is >3 months old

---

### Company Snapshot
- **Stage:** [Series X / Public / etc.] [CONFIDENCE: HIGH/MEDIUM/LOW] [Source/Date if needed]
- **Size:** [employee count] [CONFIDENCE: HIGH/MEDIUM/LOW] [Last verified: date]
- **Revenue model:** [description]
- **Recent trajectory:** [growing/flat/struggling] [CONFIDENCE: HIGH/MEDIUM/LOW] [Data from [date]]
- **Core product:** [description]

### Product Intelligence
- **Recent launches:** [bullet list with DATES]
  - [Launch name] - [date] [CONFIDENCE: HIGH if <14 days, MEDIUM if <60 days, LOW if older]
- **User sentiment:** [3-5 verbatim quotes with SOURCE and DATE]
  - "[Quote]" (G2, [rating], [date]) [CONFIDENCE: HIGH if <14 days, MEDIUM if <60 days, LOW if older]
- **Competitive position:** [description] [CONFIDENCE: MEDIUM if 30-90 days old, LOW if >90 days]
- **Biggest product opportunity:** [assessment] [NOTE: Confidence depends on product data recency]

### Strategy and Priorities
- **Leadership says:** [key quotes] [SOURCE: name, title, [publication], [date]] [CONFIDENCE: HIGH if <30 days, MEDIUM if <120 days, LOW if older]
- **Stated bets:** [what the company is prioritizing] [Data from [date]]
- **Culture signals:** [assessment based on artifacts] [CONFIDENCE: MEDIUM-HIGH if based on recent job postings/reviews <60 days, MEDIUM if older]

### Team and Hiring
- **Product org lead:** [name, title] [Last verified on LinkedIn: [date]]
- **Likely hiring manager:** [name, title, LinkedIn URL] [CONFIDENCE: HIGH if found on job board, MEDIUM if inferred from org]
- **Team size:** [N PMs, organized by X] [Data from [date]]
- **Recent [FUNCTION-ADAPTIVE] hires:** [backgrounds of last 2-3 hires, with HIRE DATES]
  - [Name] joined [date] from [background] [CONFIDENCE: HIGH if <6 months, MEDIUM if 6-12 months, LOW if >12 months]
- **Open roles:** [count and titles] [As of [date]]

### Career Changer Intel
- **Non-traditional precedent:** 
  - [FOUND] [Name] joined [Company] from [background] [Hire date: [date]] [CONFIDENCE: HIGH if <6 months, MEDIUM if 6-12 months, LOW if >12 months]
  - [OR] "None found in past 18 months" [CONFIDENCE: HIGH CONFIDENCE ABSENCE]
- **Culture fit assessment:** [assessment] [CONFIDENCE: MEDIUM - based on recent reviews and job posting language]

### Your Connection Map
- **Direct connections:** [names] [Last contact: [date]]
- **Alumni connections:** [names] [Last verified: [date]]
- **Recommended approach:** [strategy]

### Data Freshness Notes

| Data Type | Age | Confidence | Action Needed |
|-----------|-----|-----------|---------------|
| Funding/Stage | [age] | [HIGH/MEDIUM/LOW/STALE] | [Verify? / Safe to use / Refresh before deciding] |
| Product/Launches | [age] | [HIGH/MEDIUM/LOW/STALE] | [Verify? / Safe to use / Refresh before deciding] |
| Leadership/Strategy | [age] | [HIGH/MEDIUM/LOW/STALE] | [Verify? / Safe to use / Refresh before deciding] |
| Team/Hiring | [age] | [HIGH/MEDIUM/LOW/STALE] | [Verify? / Safe to use / Refresh before deciding] |
| H-1B Sponsorship | [age] | [HIGH/MEDIUM/LOW/STALE] | [Verify? / Safe to use / Refresh before deciding] |

### Research Hooks for Work Product
Ready to feed into `/work-product`:
1. [Source]: "[quote]" [DATE: [date]] [CONFIDENCE: HIGH/MEDIUM] — Implication: [what this means]
2. [Source]: "[quote]" [DATE: [date]] [CONFIDENCE: HIGH/MEDIUM] — Implication: [what this means]
3. [Source]: "[quote]" [DATE: [date]] [CONFIDENCE: HIGH/MEDIUM] — Implication: [what this means]

---

## Recommended Next Steps
- [ ] [Verify funding round] - data from [date], consider refresh if >30 days old
- [ ] [Verify org structure] - last checked [date], recheck LinkedIn if >7 days old
- [ ] [Check for recent hires] - as of [date]
- [ ] If visa sponsorship needed: [Verify USCIS data] - data from [year]
- [ ] Add/update this company in `target-companies.md`
- [ ] If connections exist: run `/referral-request`
- [ ] If no connections: run `/connection-request` targeting [suggested people]
- [ ] Run `/work-product` using the research hooks above
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
- [ ] **User sentiment includes verbatim quotes, not summaries.** "Users say onboarding is hard" is useless. "Setting up Notion for my team was painful. Half the team never moved past their first page" (G2, 2-star review, 2026-04-15) is useful. [Must include date and confidence level]
- [ ] **Hiring manager identification is specific.** Not "probably a Director of Product." Instead: "Jane Smith, Director of Product, Growth -- she has been at [Company] for 2 years and her team owns [area]. LinkedIn: [URL]. [Last verified on LinkedIn: 2026-05-10]"
- [ ] **Recent PM hires section reveals actual hiring patterns with dates.** If the last 3 PM hires all came from FAANG with 5+ years PM experience (hired 2025-2026), that is important context. [Each hire must have a hire date and confidence level based on recency]
- [ ] **Research hooks are concrete and dated.** Each hook must have a source, a specific quote or data point, a DATE, and an implication. Example: "[Lodgify 2026 Industry Report]: '66% of hosts struggle with direct bookings' [DATE: May 2026] [CONFIDENCE: HIGH] — Implication: Your work product should address this pain point."
- [ ] **Every major claim includes a confidence level.** Not just "[CONFIDENCE: MEDIUM - based on available sources]" but specific: "[CONFIDENCE: MEDIUM - funding round announced Nov 2022, now May 2026. Consider verifying current burn rate.]"
- [ ] **STALE data is flagged.** If any data point is >6 months old, there's a [VERIFY] or [CAUTION] warning in the output. Data older than 180 days should NOT be cited without a refresh.
- [ ] **Absence vs. outdated data is distinguished.** "[None found - searched LinkedIn, h1bdata.info, Glassdoor as of 2026-05-10] [CONFIDENCE: HIGH CONFIDENCE ABSENCE]" (actively searched, found nothing) vs. "[Data from November 2025] [CONFIDENCE: LOW] - recommend refresh before interviews"
- [ ] **Career changer section is honest about data age.** If precedent found but >12 months old, flag: "[PRECEDENT: [Name] joined 18 months ago from [background]. May no longer be representative of current hiring—verify with recent LinkedIn search.]" If no precedent found, say: "[NONE FOUND in past 18 months - HIGH CONFIDENCE ABSENCE]"
- [ ] **Connection map is actionable.** Not "you might know someone." Instead: "Sarah Kim (Wharton '18) is a PM at [Company]. She's in your connection-tracker -- last contact was 2 weeks ago (2026-04-28). Recommend running /referral-request."
- [ ] **Data Freshness Notes table is complete.** Every data type (Funding, Product, Leadership, Team, H-1B) has an age, confidence level, and action recommended. Users can scan this table to see at a glance what's current and what needs refreshing.

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
