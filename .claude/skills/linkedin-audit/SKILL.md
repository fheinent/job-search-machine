---
name: linkedin-audit
description: Compare LinkedIn profile against target JDs and suggest specific before/after edits to improve alignment.
---

# /linkedin-audit - LinkedIn Profile Optimization Audit

## When to Use

- User asks to review or improve their LinkedIn profile
- User has been applying to roles and getting low response rates -- profile may be misaligned
- User is pivoting to a new role type (e.g., from Growth PM to AI PM) and needs to update positioning
- After filling `target-companies.md` or updating `career-plan.md` -- profile should reflect the new direction
- Periodically (monthly) to ensure LinkedIn matches the current job search strategy

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

- **Auto-loaded:** `context-library/experience-library.md` (contains the user's LinkedIn profile text in the "LinkedIn Profile" section, plus all organized experience)
- **Auto-loaded:** `context-library/target-companies.md` (companies being targeted -- reveals which industries and roles to optimize for)
- **Auto-loaded:** `context-library/career-plan.md` (level preference, industry preference, addressing-weaknesses strategy, dream offer)
- **Optional:** Recent JDs from `/app-tracker` pipeline or pasted by the user (the more JDs available, the more specific the audit)

If the LinkedIn Profile section in `experience-library.md` is empty or contains only template placeholders, switch to **build-from-scratch mode:**

**Build-from-scratch mode (no existing LinkedIn content):**
Instead of auditing existing text, generate a complete LinkedIn profile draft using the user's `experience-library.md`, `career-plan.md`, and `target-companies.md`. Output format changes to:

1. **Skip the comparison/audit steps.** There is nothing to compare against.
2. **Generate a complete profile:**
   - **Headline:** Write 2-3 options following the formula: `[Target Title] | [Specialty/Domain] | [Notable Signal (Ex-Company, Metric, Expertise)]`
   - **About section:** Write a full summary (under 2,000 characters) using the Hook + Story structure. Pull metrics and narrative from experience-library.md. Address weaknesses from career-plan.md proactively.
   - **Experience entries:** For each role in experience-library.md, write 3-5 LinkedIn-optimized bullets with metrics, using SAR structure. Ensure target JD keywords are woven in naturally.
   - **Skills list:** Generate a prioritized list of 30-50 skills based on target JDs and experience-library.md.
   - **Recommendations strategy:** Identify 3-5 people the user should request recommendations from (based on roles and projects in experience-library.md) with specific prompts to send each person.
3. **Include the keyword gap analysis** (comparing the generated profile against target JDs to ensure coverage).
4. **Include the priority action list** formatted as a setup checklist: "1. Create LinkedIn account / update profile. 2. Paste this headline. 3. Paste this About section. 4. Update each role with these bullets. 5. Add these skills. 6. Send these recommendation requests."

Note: If the user has a LinkedIn URL but has not pasted their content, prompt: "I can generate a profile from scratch using your experience library, or you can paste your current LinkedIn text for an audit. Which do you prefer?"

## Process

### Step 1: Extract Current LinkedIn Positioning
Parse the user's LinkedIn profile text from `experience-library.md`:
- **Headline:** Current headline text
- **About/Summary:** Full summary section
- **Experience titles and descriptions:** Each role's title and bullet points
- **Skills section:** Listed skills (if provided)
- **Featured section:** Any featured content mentioned

### Step 2: Build Target Profile from JD Analysis
Analyze the user's target roles to build a "target LinkedIn profile":
1. Read `target-companies.md` -- identify the top 10-15 companies and their common role types
2. Read `career-plan.md` -- identify target level, industry, function
3. If recent JDs are available (from app-tracker or pasted), extract the most common:
   - Job titles used (exact wording matters for LinkedIn search)
   - Top 10 most-repeated required skills across JDs
   - Top 5 most-repeated preferred skills
   - Common responsibility themes
   - Industry keywords
4. Build a "target keyword set" -- the words that should appear on the user's LinkedIn for recruiters to find them. **[FUNCTION-ADAPTIVE]** Build target keyword set from JDs matching the user's target function, NOT PM JDs. SWE keywords: distributed systems, Kubernetes, system design, Go/Python/Java, microservices, CI/CD. Design keywords: Figma, design systems, user research, prototyping, accessibility. Data Science: Python, SQL, ML, A/B testing, statistical modeling, Spark. Marketing: SEO, demand gen, content strategy, marketing automation, HubSpot. CS: NRR, Gainsight/Totango, QBR, health score, renewal management, churn.

### Step 3: Compare and Flag Misalignments
For each LinkedIn section, compare current state against target:

**Headline audit:**
- LinkedIn headlines have a 220-character limit. Use the full space.
- Recommended formula: `[Title - Company] Specializing in [Sub-Sector] | [Brands/Notable Companies]`
- **[FUNCTION-ADAPTIVE]** Function-specific headline patterns: SWE: "Staff Backend Engineer | Distributed Systems & Payments | Ex-Stripe, Shopify". Design: "Product Design Lead | Design Systems | Ex-Spotify, Airbnb". Data Science: "Senior Data Scientist | ML & Experimentation | Ex-Spotify". Marketing: "Growth Marketing Manager | B2B SaaS | Ex-Lattice". CS: "Director of Customer Success | Enterprise SaaS | Ex-Salesforce".
- Does the headline contain the job title recruiters search for? (e.g., if targeting "AI Product Manager" roles but headline says "Growth PM," that's a mismatch)
- Is it specific enough? ("Product Manager" is too vague; "AI Product Manager | B2B SaaS | Ex-[notable company]" is searchable)
- Does it include 1-2 keywords from the target keyword set?
- Flag: "Your headline says '[current]' but [X] of [Y] target applications are for [target title] roles"
- **Manager-to-IC transition check:** If `career-plan.md` indicates the user is transitioning from manager to IC track, check whether the headline signals "manager" or "IC." A headline that reads "Senior PM | Managing AI products at [Company]" signals manager identity. For IC targeting, the headline should emphasize craft and domain depth: "AI Product Manager | Smart Home, ML, Consumer Platforms | Stanford, IIT Delhi." If the user's current LinkedIn headline includes "team lead," "managing," "leading a team of," or similar management signals, flag it: "Your headline signals management orientation, but your career plan targets IC roles. Reframe toward domain expertise and product craft."
- **Early-career level-up check:** If `career-plan.md` shows the user's current title is below their target title (e.g., APM targeting PM, PM targeting Senior PM), the headline must NOT include the lower-level prefix. An APM targeting PM roles who headlines as "Associate Product Manager at [Company]" is anchoring recruiters to the junior title before they read a single bullet. Instead, headline with target function + domain: "Product Manager | Growth & Experimentation | [Domain/School/Notable Metric]." Do not lie about current title -- just omit the explicit level prefix from the headline. The Experience section shows the real title; the headline sells the direction.

**About/Summary audit:**
- Does the first line hook a recruiter? (LinkedIn truncates after ~2 lines in search results)
- Is it written in first person? (Third person reads as corporate and impersonal)
- Does it follow the Hook + Story structure? Open with a compelling hook, then tell your story across 4+ paragraphs.
- Does it address the user's biggest weakness proactively (from career-plan.md addressing-weaknesses)?
- Does it contain the top 5 keywords from the target keyword set?
- Is it under 2,000 characters? (Longer summaries aren't read)
- Does it include a metric in the first 2 sentences?
- Flag any keywords that are in 5+ target JDs but missing from the summary
- **[FUNCTION-ADAPTIVE]** For SWE: check for technical depth signals (open-source contributions, tech talks, engineering blog posts). For Design: check for portfolio link, case studies, design process description. For Data Science: check for publications, Kaggle, technical blog. For CS: check for CS methodology expertise, thought leadership.

**Experience section audit:**
- Do role titles match what recruiters search for? (Some companies use unusual titles -- the user can add a parenthetical like "Product Lead (Senior PM equivalent)")
- Do bullet points contain metrics? (LinkedIn bullets without numbers get skimmed over)
- Do bullets tell stories using SAR (Situation-Action-Result) structure? Explain what part of the product you owned, not just what the company does.
- Are the most relevant experiences (to target roles) detailed enough?
- Are less relevant experiences taking up too much space?
- Are JD keywords present in experience descriptions?
- Flag: "Your [Company X] role doesn't mention [skill] but it's in your experience library -- add it"

**Skills section audit:**
- LinkedIn allows up to 50 skills. Fill all 50 slots -- more skills = more search surface area.
- Are the top 10 target keywords in the skills list?
- Are skills added to each individual job entry? (LinkedIn lets you associate skills with specific roles, which strengthens the signal.)
- Are outdated or irrelevant skills diluting the profile? (LinkedIn's algorithm weights skills in search)
- Flag skills to add and skills to remove/reorder
- Suggest asking 3-5 colleagues for endorsements on the top skills that match target roles

**Overall positioning audit:**
- Is there a coherent narrative? (Do headline, summary, and experience tell the same story?)
- Does the profile match where the user is going, not just where they've been?
- Would a recruiter searching for [target role title] at [target company type] find this profile?

**Unknown/Niche Employer Brand audit (if user's employers are prestigious in their vertical but unknown in general tech):**
- This applies to BOTH international candidates with non-US employers AND domestic candidates from companies that are well-known within a specialized industry (e.g., defense, healthcare, fintech, supply chain, energy) but unknown in general tech PM circles. A PM from Epic Systems, Palantir's government division, Lockheed Martin, or a top regional health system faces the same brand recognition problem as a PM from Rakuten or Personio.
- Check `career-plan.md` for any "unknown employer brand" weakness. If present, verify that EVERY employer in the Experience section includes a parenthetical that contextualizes the company for target-market recruiters. "Senior PM at Epic Systems" means nothing to an AI startup recruiter; "Senior PM at Epic Systems (largest US healthcare EMR, 300M+ patient records)" instantly communicates scale.
- Assess whether the headline anchors on a recognizable signal. If no employer name will register, the headline MUST lead with a metric, domain expertise, or educational brand: "Product Manager | Grew activation 4x to 22M users | Stanford GSB" is stronger than "Product Manager at [Unknown Company]."
- Check if the About/Summary section leads with universal metrics (revenue, users, GMV, experiments run) rather than employer names. The summary should be impressive to someone who has never heard of any company on the profile.
- Flag if the profile relies on employer brand for credibility without providing scale context. Every mention of an unknown employer needs a parenthetical on first reference.

**International-to-US profile audit (if user is targeting US roles from a non-US background):**
- Check `career-plan.md` for any "unknown employer brand" weakness. If present, verify that EVERY employer in the Experience section includes a parenthetical that contextualizes the company for US recruiters. "Senior PM at Personio" means nothing to a US recruiter; "Senior PM at Personio ($8.5B valuation, Europe's leading HR platform)" instantly communicates scale. Flag any employer missing context.
- Assess whether the headline reads well for US recruiters. International candidates often use headline formats common in their home market but invisible to US recruiters. The headline should include the target US role title, not the local-market equivalent.
- Check if the About/Summary section tells the international-to-US narrative as an intentional career move, not a question mark. The summary should frame cross-market experience as a unique asset: "8 years building products across Japan and Europe, now bringing [specific expertise] to [US market/company type]." Flag if the summary reads as "I'm looking for a job in the US" (reactive) instead of "I bring a cross-market perspective that US-only PMs don't have" (proactive).
- Flag if the profile lacks any US-market signals: US-relevant skills, US-based connections, US community memberships, or engagement with US PM thought leaders. Suggest specific actions: join visible US PM communities, engage with content from target company leaders, add US-relevant certifications or publications.
- Check for cultural communication patterns that may not translate well to US LinkedIn: excessive humility ("had the privilege of contributing to"), overly formal language ("I was entrusted with the responsibility of"), or consensus-oriented framing ("the team achieved") when individual contribution framing would be stronger for a US audience.

**Employer & Product Concentration audit:**
- Does the profile over-index on a single employer? If the user spent 3+ years at one company and it dominates their profile (70%+ of content), assess whether this creates a perception problem. Long tenure at one company can signal loyalty but can also signal lack of breadth -- especially if the target roles are at companies with different cultures.
- Does the profile over-emphasize a declining or deprioritized product? If the user's most prominent bullets describe work on a product that has publicly lost market share, been shut down, deprioritized, or received negative press, the profile needs rebalancing. Highlight transferable skills and outcomes, not the product name.
- Check for "single-company identity" -- if the headline, summary, and most experience bullets all reference the same employer brand, suggest diversifying. Even within one employer, highlight cross-functional projects, different product areas, or initiatives that demonstrate range.
- If the user's current employer carries a specific brand stigma at their target companies (e.g., "process-heavy," "slow-moving," "growth-at-all-costs"), check whether the profile inadvertently reinforces that stigma. E.g., bullets heavy on "process improvements," "operational excellence," or company-specific frameworks for a PM leaving Amazon reinforce the "Amazon PMs are operators, not product thinkers" perception at Google or Anthropic. Suggest reframing toward innovation, user insight, product craft, and speed.
- Check for excessive internal jargon from the current employer (e.g., Amazon Leadership Principle names, company-specific acronyms like "PRFAQ," "WBR," "OP1"). Target company recruiters may not recognize these or may associate them negatively with the source company's culture. Translate to universal PM language.

**Recommendations audit:**
- Does the user have 1-3 recommendations per job? (Recommendations are high-signal for recruiters.)
- If missing, suggest the user request recommendations by providing specific prompts to recommenders (e.g., "Could you speak to my work on [specific project] and its impact on [metric]?")

**Profile picture audit:**
- Is the photo professional? Consider an AI-generated professional headshot if the current photo is casual, outdated, or missing.

**"Open to Work" status:**
- If unemployed: turn on "Open to Work" (visible to all). The signal helps recruiters find you.
- If employed: use the "visible only to recruiters" setting to hide from current employer.

**Engagement strategy audit:**
- Commenting strategy is higher-ROI than content creation for most job seekers. Suggest commenting thoughtfully on posts from target companies and hiring managers.
- 15-20 personalized connection requests per day to people at target companies.
- **[FUNCTION-ADAPTIVE]** Recommend engaging with function-specific thought leaders and communities, not PM content creators. SWE: engage with engineering blogs, open-source maintainers, and tech conference speakers at target companies. Design: engage with design community leaders, Dribbble/Behance content, and design system authors. Data Science: engage with ML researchers, data community leaders, and Kaggle contributors. Marketing: engage with marketing thought leaders, growth community content, and brand strategy discussions. CS: engage with CS community leaders (Gainsight Pulse, SuccessHacker), and CS methodology authors.

**EXECUTIVE PASSIVE SEARCH RULE:** If career-plan.md shows the user is at Director level or above AND is currently employed, apply these adjustments to the audit. Executives searching while employed have fundamentally different LinkedIn dynamics -- visibility is dangerous, and the profile must attract inbound interest without broadcasting a job search:
- **(a) Open to Work -- extreme caution.** Use the recruiter-only "Open to Work" setting, but flag the risk: "In small industries, recruiter-only is not truly private. Recruiters at your current company's competitors, board members, and exec recruiters all see this signal. If your industry has fewer than 50 companies in the target segment, consider leaving Open to Work OFF entirely and relying on inbound from your profile strength and targeted outreach instead." Never recommend the visible-to-all green banner for Director+ employed candidates.
- **(b) Headline as executive identity statement.** At Director+ level, the headline is NOT a keyword-optimized search string. It is an executive identity statement that signals authority and domain ownership. Do NOT suggest headlines like "VP Product | AI/ML | B2B SaaS | Growth | Ex-Google." Instead, suggest a headline that reads as a leadership brand: "Building AI products that [outcome] | VP Product at [Company]" or "[Domain] product leader | Scaling [specific thing] at [Company]." The headline should make a recruiter think "this person leads something important" not "this person is optimizing for job search."
- **(c) About section as leadership philosophy.** For Director+ profiles, the About section should NOT be a career summary or keyword repository. It should read as a leadership philosophy statement: what you believe about building products, how you lead teams, what problems you are drawn to. This attracts the RIGHT executive recruiters and repels keyword-matching junior recruiters. Structure: (1) Opening statement of product leadership philosophy, (2) Evidence paragraph with 2-3 scope metrics that demonstrate scale, (3) What you are focused on now / what excites you about the current moment in your domain. Keep it under 1,500 characters.
- **(d) Engagement shifts to publishing.** At Director+ level, commenting for visibility is insufficient and may appear junior. Instead, recommend publishing 1-2 substantive LinkedIn posts per month on topics relevant to the target role: leadership lessons, product strategy observations, industry analysis. These posts serve as "work samples" for executive recruiters and establish thought leadership. Suggest specific post topics based on the user's experience library and target roles. Flag: "At your level, your LinkedIn activity IS your interview. Executive recruiters review your posts, comments, and engagement patterns before reaching out. One thoughtful post per month is worth more than 50 comments."

**REMOTE-READY PROFILE AUDIT:** If `career-plan.md` shows the user has a remote-only preference or caregiver/family constraints, apply these additional audit checks:
- **Headline:** Should NOT say "Remote PM," "Remote Product Manager," or "Remote [Any Title]." This brands the person as location-constrained and limits search visibility. Instead, lead with expertise: "AI Product Manager | B2B SaaS | Growth + Experimentation" -- the remote preference is a logistics detail for the application, not a profile identity.
- **Location field:** Recommend "United States" (or broadest applicable region such as "European Union" or "Canada") rather than a specific city. A specific city signals the recruiter can filter by geography. Broad location keeps options open and avoids triggering location-based search filters.
- **About section:** If the About mentions "remote work," "working remotely," "distributed teams," or similar phrases more than once, flag it: "Your About section references remote work [N] times. The About should be about WHAT you do and the impact you create, not WHERE you work. Keep at most one natural reference to distributed team experience and remove the rest."
- **Experience bullets:** Check for bullets that lead with "Remote" or "distributed" as the primary descriptor. Reframe: "Managed remote team of 8" becomes "Led cross-functional team of 8 across 4 time zones, shipping [product] with [metric]." The distributed nature is supporting context, not the headline.
- **PRIVACY GUARDRAIL:** Audit the entire profile for any inadvertent personal disclosure -- caregiving responsibilities, health conditions, family obligations, children, or any personal reason for remote preference. If found, flag for immediate removal: "PRIVACY FLAG: Your [section] contains a reference to [personal detail]. Remove this. Personal circumstances should never appear on a professional profile."

**CAREER RETURNER PROFILE AUDIT:** If `career-plan.md` shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), apply these additional audit checks:
- **Experience section -- Career Break entry:** Do NOT recommend adding a "Career Break" entry in the Experience section. LinkedIn offers this feature, but it signals more than it helps -- it draws attention to the gap and invites assumptions about the reason. The gap is visible from dates; adding an entry amplifies it.
- **During-gap activities:** Recommend adding any during-gap professional activities (advisory roles, freelance projects, certifications, board service, consulting) as separate Experience or Education entries. These fill the timeline with professional signals without explaining the gap.
- **Dates:** Keep dates accurate. Do not recommend hiding or obscuring dates. Integrity matters more than gap minimization.
- **About section:** Should read as FORWARD-LOOKING. Good: "PM with 8 years in B2B SaaS, focused on AI-powered growth and experimentation." Bad: "Returning to the workforce after a career break." The About section establishes where the user is going, not where they have been. If the current About mentions "returning," "career break," "time away," or "back to work," flag it for rewrite.
- **Headline:** Absolutely no mention of "returning," "career break," "comeback," or similar language. The headline leads with expertise and target function. Good: "Product Manager | Growth & Experimentation | B2B SaaS." Bad: "PM Returning to Industry" or "Career Returner | Product Management."
- **Engagement strategy for returners:** Recommend increased posting and commenting activity for 4-6 weeks before actively applying. This rebuilds visible professional presence and pushes the profile higher in LinkedIn's algorithm. Specific recommendations: comment thoughtfully on 3-5 posts per day from target company leaders, share 1-2 articles per week with brief professional commentary, and engage with industry content to signal "I'm current and active." This creates a trail of recent activity that counterbalances the employment gap.

**Section Priority Tiers:**
- **Tier 1 (non-negotiable, do first):** Headline, About, Current Experience
- **Tier 2 (high-impact, do second):** Recommendations, Skills, Complete Experience history, Open to Work status, Commenting activity, Privacy settings, Connection requests

### Step 4: Generate Specific Before/After Edits
For every flagged misalignment, produce a concrete before/after edit. Not "consider updating your headline" -- instead, provide the exact new text.

### Step 5: Prioritize Edits
Rank all suggested edits by impact:
1. **High impact:** Headline changes, first line of summary, missing critical keywords (these affect search visibility)
2. **Medium impact:** Experience bullet rewrites, skills reordering (these affect conversion once a recruiter finds you)
3. **Low impact:** Minor wording tweaks, formatting improvements (nice to have)

## Output

```markdown
## LinkedIn Audit Report
**Audit date:** [date]
**Target role:** [derived from career-plan.md and recent applications]
**Target industries:** [from career-plan.md]

### Alignment Score: [X]% of target keywords present on profile

---

### Critical Misalignments

#### 1. Headline
**Issue:** [specific problem]
**Before:** "[current headline text]"
**After:** "[suggested headline text]"
**Why:** [1 sentence explaining the impact]

#### 2. About Section - Opening
**Issue:** [specific problem]
**Before:** "[current first 2 sentences]"
**After:** "[suggested first 2 sentences]"
**Why:** [1 sentence]

#### 3. [Next misalignment]
[... continue for all critical items ...]

---

### Employer & Product Concentration Issues
[Only if flagged in the audit]

#### Single-Employer Dominance
**Issue:** [e.g., "80% of your profile content references Amazon. Your profile reads as 'Amazon PM' rather than 'PM with Amazon experience.'"]
**Risk:** [e.g., "At Google and Anthropic, this signals you may be too process-dependent or narrow in your product thinking."]
**Fix:** [specific reframing suggestions -- e.g., "Lead summary with transferable skills, not employer name. Rewrite Alexa bullets to emphasize the user problem and your product craft, not Amazon's internal process."]

#### Declining Product Over-Emphasis
[Only if applicable]
**Issue:** [e.g., "Your headline and 4 of 6 top bullets reference Alexa, which is publicly perceived as a declining product line."]
**Risk:** [e.g., "Recruiters at AI-first companies may question whether your product instincts are current."]
**Fix:** [specific before/after edits that reframe toward transferable outcomes]

#### Internal Jargon Detected
[Only if applicable]
**Jargon found:** [e.g., "PRFAQ, Bar Raiser, LP, WBR, OP1"]
**Fix:** [translation to universal PM language -- e.g., "'Wrote PRFAQs' -> 'Authored product strategy documents starting from customer outcomes'"]

---

### Keyword Gap Analysis

| Keyword | In Target JDs | On Your Profile | Action |
|---------|--------------|-----------------|--------|
| [keyword 1] | 8/10 JDs | Missing | Add to summary + skills |
| [keyword 2] | 7/10 JDs | In skills only | Add to experience bullets |
| [keyword 3] | 6/10 JDs | Present | No action |
| [keyword 4] | 5/10 JDs | Missing | Add to skills section |
[... top 15 keywords ...]

---

### Section-by-Section Edits

#### Headline (HIGH IMPACT)
**Before:** "[full current headline]"
**After:** "[full suggested headline]"

#### About Section (HIGH IMPACT)
**Before:**
> [current full summary text]

**After:**
> [suggested full summary text]

#### [Company A] - [Role Title] (MEDIUM IMPACT)
**Title edit:**
- Before: "[current title]"
- After: "[suggested title, if needed]"

**Bullet edits:**
- Before: "[current bullet 1]"
- After: "[rewritten bullet 1 with JD keywords]"
- Before: "[current bullet 2]"
- After: "[rewritten bullet 2]"
**Add these bullets (from your experience library, currently missing from LinkedIn):**
- "[new bullet from experience-library.md not on LinkedIn]"

#### Skills Section (MEDIUM IMPACT)
**Add:** [skill 1], [skill 2], [skill 3]
**Remove/deprioritize:** [skill that's irrelevant to target roles]
**Reorder top 3 to:** [skill A], [skill B], [skill C]

---

### Priority Action List
1. [ ] [Highest impact edit - do this first]
2. [ ] [Second highest]
3. [ ] [Third]
[... max 10 items ...]

### Next Audit
Run `/linkedin-audit` again after making these changes, or after your target role focus shifts.
```

## Example

**Input:**
```
/linkedin-audit
```

**Output (abbreviated):**
```markdown
## LinkedIn Audit Report
**Audit date:** 2026-03-24
**Target role:** Senior AI Product Manager
**Target industries:** AI/ML, B2B SaaS

### Alignment Score: 47% of target keywords present on profile

---

### Critical Misalignments

#### 1. Headline
**Issue:** Headline says "Growth PM" but 6 of 8 recent applications are for AI PM roles. Recruiters searching "AI Product Manager" will not find you.
**Before:** "Growth PM | B2B SaaS | Driving activation & retention"
**After:** "AI Product Manager | B2B SaaS | Growth + ML Experience | Ex-[Company]"
**Why:** LinkedIn search heavily weights headline text. This single change makes you visible to AI PM recruiters.

#### 2. About Section - Opening
**Issue:** First line talks about "passion for growth" -- no mention of AI, and no metric. Recruiters see 2 lines before they click "see more."
**Before:** "I'm a product manager passionate about growth and user experience."
**After:** "Product manager who ships AI-powered features to millions of users. Built an ML recommendation engine that increased engagement 28% and an experimentation platform that ran 40+ A/B tests."
**Why:** Leads with AI + metric. Hooks the recruiter in the truncated preview.

#### 3. Experience - [Company A] Missing AI Bullet
**Issue:** Your experience library has "Led AI recommendation engine serving 2M daily users" but it's not on your LinkedIn profile.
**Before:** [bullet not present on LinkedIn]
**After:** Add: "Led cross-functional team shipping AI recommendation engine serving 2M daily users, increasing engagement 28%"
**Why:** This is your strongest AI experience and it's invisible to recruiters.

---

### Priority Action List
1. [ ] Update headline to include "AI Product Manager" (5 min, highest search impact)
2. [ ] Rewrite About section opening 2 sentences (10 min)
3. [ ] Add AI recommendation engine bullet to [Company A] (2 min)
4. [ ] Add "Machine Learning," "AI Products," "LLMs" to Skills section (2 min)
5. [ ] Reorder Skills so AI-related skills appear in top 3 (1 min)
```

## Quality Checks

**Good output looks like:**
- Every edit has a specific BEFORE and AFTER -- not vague suggestions like "consider updating"
- Misalignments reference actual data: "6 of 8 recent applications are for AI PM roles" not "you might want to consider"
- Keyword gap table shows real counts from analyzed JDs
- Edits preserve accuracy -- never suggests adding skills or experience not in experience-library.md
- Priority list is ordered by impact and includes estimated time to implement
- The audit feels actionable: user can sit down for 30 minutes and execute every edit

**Bad output looks like:**
- Vague suggestions: "Your headline could be more specific" (how? be specific)
- No before/after text (just descriptions of what to change)
- Ignoring the career-plan.md addressing-weaknesses strategy (the profile should preempt doubts)
- Suggesting skills or experience not in the experience library (fabrication)
- Missing the keyword gap analysis (the most data-driven part of the audit)
- Not considering LinkedIn search algorithm behavior (headline weight, skills weight, keyword density)
- A priority list with 25 items (should be max 10, ruthlessly prioritized)
- Ignoring employer brand concentration: if 3+ years at one company dominates the profile and that company carries stigma at target companies, this MUST be flagged. A profile that reads as "[Company] PM" instead of "PM who happened to work at [Company]" limits options.
- Not catching declining product over-emphasis: if the user's headline or top bullets reference a product known to be struggling, this is a critical misalignment that affects first impressions. Reframe toward transferable skills and outcomes.

**Persona-specific checks (verify these when applicable):**
- **International-to-US profile:** If career-plan.md shows the user is targeting US roles from a non-US background, verify: (a) Every employer in Experience has a parenthetical contextualizing it for US recruiters (scale metrics + market position). (b) The About section frames cross-market experience as a differentiator, not a question mark. (c) The headline uses the US-standard target role title, not a local-market equivalent. (d) No excessive humility or consensus-oriented framing that reads as passive to US recruiters. (e) The profile includes at least one US-market signal (US PM community membership, engagement with US thought leaders, US-relevant certifications).
- **Function change (eng to PM, UXR to PM, design to PM):** If career-plan.md indicates the user is changing functions (not just companies or levels), apply this audit: (a) Headline must signal the TARGET function, not the current/past function. "Software Engineer at [Company]" is invisible to PM recruiters. Reframe to "Product Manager | [Domain] | Ex-[Company] Engineering." (b) About section must tell the transition story in 2-3 sentences -- why the switch, what transfers, and what the user brings that pure-PM candidates lack. (c) Experience bullets must emphasize DECISIONS over IMPLEMENTATIONS. An engineer's "Built recommendation engine using collaborative filtering" becomes "Defined product requirements and technical approach for recommendation engine, driving 28% engagement lift." A UXR's "Conducted 40 user interviews" becomes "Translated 40 user interviews into 3 product recommendations adopted by the roadmap." The audit must flag any bullet that reads as pure implementation or pure research with no decision-making signal.
- **Communication weakness visible in profile:** If career-plan.md flags conciseness or assertiveness weaknesses, audit the About section for those same patterns. A user whose interview weakness is "too verbose" likely wrote a verbose About section. Flag if the About section exceeds 1,500 characters or buries the strongest metrics below the fold. Flag if bullet points use hedging language ("contributed to," "was involved in," "helped with") instead of direct ownership language ("led," "shipped," "drove").
- **Zero US network visible:** If connection-tracker.md shows near-zero US connections, the audit must recommend specific engagement actions: "Your profile shows limited US engagement. Action items: (1) Follow and comment on posts from 5 target company leaders, (2) Join 2 visible US PM communities and list them in your profile, (3) Post 1-2x/week about international PM perspectives -- this is a unique angle that builds visibility."
- **Failed founder / shut-down company (founder profile audit):** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value: (a) Title risk: if current headline says "Founder" or "CEO," recommend changing to "Product Leader" or similar. "Founder" as a current title signals "not looking for a regular job" to recruiters. (b) Company description: ensure the LinkedIn company page (if it exists) or the experience description frames the company neutrally -- what it did, who it served, what was built. Not "unfortunately we had to close." (c) Recommendations: encourage requesting recommendations from startup advisors, investors, or early customers that speak to the PERSON's skills, not the company's outcome.
- **Veteran / 15+ years experience (age signal audit):** If career-plan.md shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, etc.), or explicit mention of age-related concerns: (a) Profile photo: if it looks significantly different from the person's current appearance, recommend updating (outdated photos are an ageism trigger in both directions). (b) Headline: lead with current expertise, not career longevity. "VP Product, Enterprise SaaS" not "18-Year Product Leader." (c) Experience section: same compression as resume -- detailed for last 10 years, consolidated for earlier. (d) Education: remove graduation years if visible. (e) Skills endorsements: ensure top-listed skills are current (if "Waterfall" is above "Agile," reorder). (f) Activity: recommend engaging with current-generation content (AI, modern frameworks, new methodologies) to signal currency.
- **Remote-only candidate:** If career-plan.md indicates remote-only preference: (a) Headline does NOT say "Remote PM" or "Remote [Title]" -- it brands the person as location-constrained. Lead with expertise instead. (b) Location field recommends "United States" or broadest applicable region, not a specific city. (c) About section does not mention "remote work" more than once -- the About is about WHAT they do, not WHERE. (d) PRIVACY GUARDRAIL: Profile is audited for any inadvertent personal disclosure (caregiving, health, family) and flagged for removal.
- **Career gap / returner:** If career-plan.md shows a career gap: (a) Do NOT recommend adding a "Career Break" entry in the Experience section (LinkedIn has this feature but it signals more than it helps). (b) Dates are kept accurate; during-gap professional activities are listed as separate entries. (c) About section reads as FORWARD-LOOKING: "PM with 8 years in [domain], focused on [target area]" -- not "Returning after a career break." (d) Headline has absolutely no mention of "returning" or "career break." (e) Engagement strategy: increased posting/commenting recommended for 4-6 weeks before applying to rebuild visible presence.
- **Military-to-PM career changer:** If career-plan.md shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), apply this audit: (a) Headline: For defense tech track, use format like "Product Manager | Military Intelligence to Tech | TS/SCI Cleared." For general tech track, use "Product Manager | Operations & Strategy Leader." The headline should NOT lead with "Veteran" or "Former Captain" -- lead with the target function. (b) Experience section: ALL military experience bullets must be translated to civilian language. Flag any untranslated jargon (AOR, OPORD, S2/S3/S4, battle rhythm, MDMP, IPB, CONOP, SIGINT, etc.). Each military role should read as a business leadership role to a civilian recruiter. (c) About section: should tell the TRANSITION story -- what military taught them that makes them a great PM. NOT a military bio. Good: "6 years leading intelligence operations taught me to make decisions with incomplete data, prioritize under pressure, and lead diverse teams toward a common objective -- the same skills that drive great product management." Bad: "Decorated Army Captain with combat deployments and intelligence certifications." (d) Recommendations: encourage requesting LinkedIn recommendations from military colleagues that speak to LEADERSHIP and ANALYTICAL skills in civilian language. Coach recommenders to avoid military jargon in their recommendations. (e) Skills section: ensure civilian PM skills are listed (Agile, Scrum, Product Analytics, User Research, Cross-Functional Leadership, Data Analysis, Strategic Planning, etc.) NOT just military skills. Military-specific skills (Intelligence Analysis, Security Clearance, etc.) can be listed but should not dominate the top positions.
