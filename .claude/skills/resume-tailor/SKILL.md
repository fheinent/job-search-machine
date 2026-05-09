---
name: resume-tailor
description: Generate an ATS-optimized resume tailored to a specific JD from the user's real experience, with keyword coverage scoring and gap analysis.
---

# /resume-tailor - ATS-Optimized Resume Tailoring

## When to Use

- User pastes a job description and wants a tailored resume for that specific role
- User says "tailor my resume" or "help me apply" with a JD attached
- User references a company and role they want to apply to and needs resume output

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
- **Auto-loaded:** `context-library/experience-library.md` (source of truth for all experience bullets)
- **Auto-loaded:** `context-library/career-plan.md` (addressing-weaknesses strategy, level preferences)

If `experience-library.md` is empty or contains only template placeholders, STOP and tell the user: "Your experience library is empty. Run `Help me build my experience library` first. A tailored resume without real experience data produces generic output."

If `experience-library.md` has Resume Text pasted but the "Organized Experience" sections still contain template placeholders (e.g., brackets like "[bullet with specific metric...]"), STOP and tell the user: "Your resume text is pasted but hasn't been organized yet. Run `Help me build my experience library` so I can structure your experience into searchable categories. Matching against raw resume text produces weaker results."

**Thin experience library warning:** After loading `experience-library.md`, count the total number of concrete experience bullets (lines with specific metrics, outcomes, or project descriptions — not headers or template text). If there are fewer than 15 substantive bullets, display this warning before proceeding: "**Heads up:** Your experience library has [N] bullets. Resumes tailored from thin libraries tend to be generic. For the best results, aim for 20+ bullets with specific metrics. You can continue now, or run `Help me build my experience library` to add more detail first." Then proceed — do not block the user, just warn them.

## Process

### Step 1: Parse the JD
Extract and categorize every requirement from the job description:
- **Required skills** (explicitly stated as required)
- **Preferred skills** (nice-to-haves, preferred qualifications)
- **Years of experience** (total and domain-specific)
- **Key responsibilities** (what the role actually does day-to-day)
- **Level signals** (IC vs manager, scope indicators, team size mentions)
- **Tech stack or tools** (specific platforms, languages, frameworks)
- **Soft skills and culture signals** (collaboration style, autonomy, pace)

Label each requirement as REQUIRED or PREFERRED. Count total requirements for the coverage score denominator.

**Handling narrative or non-standard JDs:** Some JDs lack structured "Requirements" and "Preferred Qualifications" sections. They may be a single paragraph, a recruiter's LinkedIn message, or a conversational description. When this happens:
- Infer requirements from responsibilities and repeated themes. A JD that says "you will build ML pipelines and partner with data science" implies ML experience and cross-functional collaboration are required even if never listed as "requirements."
- If the JD is too vague to extract at least 5 distinct requirements, STOP and ask the user: "This JD is light on specifics. Can you paste the full posting, or share what you know about the role's actual requirements? I need enough detail to tailor effectively -- otherwise the resume will be generic."
- When you cannot clearly distinguish REQUIRED from PREFERRED, label everything mentioned in the first half of the JD or mentioned more than once as REQUIRED, and everything else as PREFERRED. Note in the output that the classification was inferred.
- **Coverage score calibration:** For JDs with 12+ extracted requirements, a coverage score above 70% is strong. Do not treat anything below 85% as alarming -- real-world JDs often include aspirational wish lists. Note in the output when the requirement count is high: "This JD lists [N] requirements, which is above average. A coverage score of [X]% on a JD this broad indicates [strong/solid/moderate] fit."

### Customization Philosophy
"The goal is not to represent all of yourself. The goal is represent the best parts of yourself for that job." One deeply customized application per day beats spray-and-pray.

**The 4 Categories of Changes:**
When tailoring, mentally color-code every edit:
- **RED changes:** Tough removals -- delete favorite flourishes, proud bullets, and impressive-sounding details that are irrelevant to THIS specific role. This is the hardest part.
- **GREEN changes:** Coverage -- ensure every major JD requirement has at least one corresponding bullet. Identify gaps and add bullets that address weak points.
- **BLUE changes:** Through-line -- add thematic coherence. Every bullet should reinforce the same brand identity. Re-tell the career story as a straight line pointing at this role, not a zigzag of interesting detours.
- **ORANGE changes:** Subtle similarities -- mirror the JD's language patterns, tone, and emphasis. Recast experience to match the ideal archetype the JD describes.

**6 Key Customization Principles:**
1. Recast experience to match the ideal candidate archetype
2. Re-tell your career story as a straight line pointing at this role
3. Customize every bullet to address a specific JD requirement
4. Use exact ATS keywords from the JD
5. Drop specific examples that intrigue and invite follow-up questions
6. Flip your weaknesses by reorganizing bullets so weakness-addressing content appears first

**Customization Process:** Open JD and resume side by side. Delete irrelevant bullets. Identify weaknesses vs. the JD. Add bullets addressing those weak points. Reorganize to put weakness-addressing bullets near the top of each role.

**OVERQUALIFICATION / DOWNLEVELING RULE:** If the user's most senior title (from experience-library.md) is meaningfully above the JD's level (e.g., VP applying for Senior PM, Director applying for IC), apply these adjustments throughout the entire process:
- **Summary:** Scope DOWN. Emphasize hands-on IC craft, direct execution, and builder identity -- not team size, org scope, or strategic vision. A VP downleveling to Senior PM should sound like "Product leader who still writes specs, runs experiments, and ships features directly" not "Visionary executive who scaled a 40-person product org."
- **Bullet selection:** Prefer bullets that show individual contribution and craft over management and org-building. "Personally designed and ran 12 A/B tests" beats "Built and led 15-person experimentation team." If only leadership-level bullets exist, rewrite to foreground the hands-on component while preserving factual accuracy.
- **Title presentation:** Keep titles factual (do not downgrade "VP Product" to "Product Manager"). But under each role, the bullet selection does the scoping work.
- **Gap analysis:** Add a row to the gap table flagging overqualification risk: "Recruiter may perceive flight risk or poor IC fit. Mitigate by: (1) cover letter explaining motivation for the move (growth opportunity, domain passion, company mission), (2) referral who can vouch for your hands-on orientation."
- **RED changes are critical here.** The hardest cuts for an overqualified candidate are the impressive VP-level accomplishments that signal "I will be bored at this level." Be aggressive with RED changes.

**EQUIVALENT SCOPE REFRAMING RULE:** If career-plan.md shows the user holds a title perceived as more senior (e.g., CPO, SVP, Head of Product) but is targeting roles at equivalent effective scope (e.g., VP Product at a larger company, Director at a FAANG), apply these adjustments throughout the entire process:
- **Summary:** Emphasize scope comparability, not a step down. Frame the move as lateral in real scope. Good: "Product executive who built and scaled a $200M product line with 50-person cross-functional org -- the same scope as a VP Product at a Series D+ company." Bad: "Former CPO seeking VP-level roles." The summary must make clear that the title difference reflects company-stage differences, not a demotion.
- **Bullet selection:** Do NOT hide leadership accomplishments. Unlike a true downleveling scenario, this user is applying at the same scope -- so P&L ownership, org building, board communication, and executive stakeholder management are all relevant. Select bullets that demonstrate the SCALE of impact (revenue, users, team size, budget) to prove the scope matches the target role.
- **Title presentation:** Keep titles factual. If helpful, add a scope parenthetical: "CPO (equivalent to VP Product at a 500+ person company)" -- but only if career-plan.md's addressing-weaknesses section flags title-level mismatch as a concern.
- **Gap analysis:** Add a row to the gap table: "Title mismatch perception: Recruiter may assume candidate is overqualified or will be unsatisfied. Mitigate by: (1) cover letter framing the move as pursuing equivalent scope at a larger/different-stage company, (2) referral who can confirm the candidate is genuinely targeting this level, (3) summary that anchors on scope metrics (revenue, users, team) rather than title hierarchy."
- **Key distinction from OVERQUALIFICATION RULE:** The overqualification rule scopes DOWN (VP to Senior PM). This rule scopes ACROSS (CPO at 200-person company to VP at 2,000-person company). Do not apply RED changes aggressively here -- the leadership accomplishments ARE the selling point, not the liability.

**MANAGER-TO-IC TRANSITION RULE:** If career-plan.md indicates the user is transitioning from a management role to an IC role at the SAME level (e.g., Senior PM who managed a team now targeting Senior IC PM), apply these adjustments. This is distinct from downleveling -- the user is not dropping a level, but shifting track:
- **Summary:** Lead with IC craft and hands-on product work. Frame management experience as ADDITIVE to IC effectiveness, not as the primary identity. Good: "Product manager who ships directly -- and brings the stakeholder judgment, hiring instincts, and org-design perspective of someone who has led teams." Bad: "Experienced people manager seeking an IC role." The summary should make the reader think "strong IC who also managed" not "manager who wants to stop managing."
- **Bullet selection:** For every management-flavored bullet (team size, hiring, org process), pair it with or replace it with a bullet showing direct product contribution from the SAME project. "Managed team of 8 engineers" is less useful than "Designed multi-device orchestration integrating 14 partner APIs." If the user's experience library has both management and hands-on bullets for the same project, always select the hands-on version. Include ONE management bullet per role (max) to show leadership range, but it should never be the lead bullet.
- **Addressing the "why IC" question:** In the gap table, add a row: "Interviewer may ask why the user is moving from manager to IC. Mitigate by: (1) summary that frames IC as a deliberate choice toward product depth, (2) cover letter that explains the motivation positively: 'I managed because the team needed it, and I'm proud of the team I built. But I do my best work close to the product.'"
- **Avoid management-heavy language:** Scan all bullets for phrases like "managed a team of," "oversaw," "built and scaled the org," "drove OKR process," "hired N people." These are valid accomplishments but signal "manager" to a recruiter scanning for IC fit. Rewrite or deprioritize them. Keep management references to the supporting detail level, not the lead.

**SINGLE-EMPLOYER CONCENTRATION RULE:** If 60%+ of the user's experience-library.md entries come from ONE company (common for candidates with 5+ years at a single employer), apply these adjustments:
- **Experience ordering:** Break up the visual monotony of a single company name. If the user held different roles at the same company, ensure each role has a distinct identity -- different bullet themes, different keywords, different impact areas. The resume should read as "3 distinct product roles that happened to be at Amazon" not "6 years at Amazon doing Amazon things."
- **Summary:** Do NOT mention the company name in the first sentence of the summary. Lead with the skill identity and domain expertise, then reveal the company context. Good: "Product manager specializing in AI-powered consumer experiences and marketplace platforms, with 8 years shipping products to 150M+ users across smart home, e-commerce, and seller tools." Bad: "Amazon Senior PM with 6 years of experience."
- **Breadth signaling:** Ensure the resume surfaces diversity within the single employer: different product areas, different customer types (B2B vs B2C), different product stages (0-to-1 vs optimization), different functions influenced (ML, design, legal, partnerships). If the user also worked at other companies, even briefly, give those roles proportionally MORE space than their tenure alone would warrant -- they break the single-employer pattern.
- **Gap table:** If single-employer concentration is detected, add a row: "Single-employer pattern: [N] of [M] years at [Company]. Mitigate by: (1) emphasizing diversity of roles and product areas within [Company], (2) giving proportional weight to other employers, (3) cover letter noting intentional internal mobility."

**DECLINING PRODUCT RULE:** If career-plan.md's addressing-weaknesses section mentions a declining, deprioritized, or struggling product (or if the user's most recent role is on a product widely known to be in decline), apply these adjustments:
- **Bullet framing:** Every bullet from the declining product must lead with the USER's impact and transferable skill, not the product's identity. "Grew routine adoption 4.5x across 22M households" is strong because the metric stands on its own regardless of Alexa's trajectory. "Led Alexa Smart Home strategy" is weak because it ties the accomplishment to a product whose trajectory the interviewer may question.
- **Summary:** Do NOT name the declining product in the first sentence. Name the domain and skill first: "AI product leader who grew engagement 4.5x and shipped features saving users $40M" puts the focus on results. Then context can follow.
- **Proactive reframing:** In the gap table, add a row: "Product trajectory risk: [Product] is publicly perceived as declining. Mitigate by: (1) leading with feature-level impact metrics that are product-agnostic, (2) cover letter framing the departure as evidence of good product judgment -- the user recognized strategic headwinds and chose to move proactively, (3) referral who can speak to the user's impact despite org-level challenges."

**EARLY-CAREER / THIN EXPERIENCE RULE:** If `experience-library.md` shows fewer than 3 years of total PM or target-role experience, apply these adjustments throughout the entire process:
- **Summary:** Lead with the user's strongest output metric, not years of experience. Good: "Product manager who grew activation 4x across 2M users." Bad: "Product manager with 1.5 years of experience." Never open with tenure.
- **Bullet density:** Maximize bullet count per role. Primary role gets 5-6 bullets (not the standard 3-5). Internships and part-time roles get 3-4 bullets. Every bullet must carry a metric or concrete deliverable -- thin resumes cannot afford vague bullets.
- **Academic projects and thesis:** If the user's experience library includes academic projects, capstone work, or thesis research with measurable outcomes, include these in a dedicated "Projects" section between Experience and Skills. Only include if they have metrics (e.g., "Designed and tested a mobile checkout prototype with 50 users, improving task completion 34%").
- **Gap table framing:** For every years-of-experience gap, use this format in the gap table: "JD requires X years. Candidate has Y actual. Framing: lead with output metrics that demonstrate impact-per-year above the typical candidate at X years."
- **RED changes matter less here.** Early-career candidates have less to cut. Focus energy on GREEN changes (coverage) and BLUE changes (through-line coherence).

**DOMAIN-LOCKED RULE:** If 80% or more of the user's experience in `experience-library.md` is concentrated in one specialized domain (e.g., fintech, healthcare, defense, e-commerce), and the current application is for a role OUTSIDE that domain, apply these adjustments:
- **Bullet framing:** Every bullet from the domain-concentrated experience must lead with the transferable PM skill, not the domain context. "Designed and executed a multi-variant pricing experiment across 4M users, increasing conversion 18%" is strong because the skill (experimentation, pricing optimization) transfers anywhere. "Optimized healthcare claims processing workflow" leads with domain and loses out-of-domain readers.
- **Employer description:** Describe each employer by scale metrics (revenue, users, team size, growth rate), not by domain position. "Built merchant tools at a $15B GMV marketplace" transfers better than "Built merchant tools at Japan's largest e-commerce platform" when the target role is not in e-commerce. Use domain-neutral framing for out-of-domain applications.
- **Summary:** Lead with the transferable skill identity, not the domain identity. Good: "Product manager who builds growth loops and experimentation infrastructure, with experience scaling products to 50M+ users." Bad: "Healthcare product manager with 6 years in digital health."
- **Translation dictionary:** If `career-plan.md` contains a domain-to-target translation dictionary (mapping domain-specific terms to universal PM terms), apply it to every bullet. If no dictionary exists, create implicit translations: "claims adjudication workflow" becomes "multi-step approval workflow," "merchant onboarding" becomes "B2B user onboarding," etc.
- **Gap table:** Add a row: "Domain mismatch: [N]% of experience is in [domain]. Target role is in [target domain]. Mitigate by: (1) leading every bullet with transferable skill label, (2) cover letter framing domain expertise as a cross-pollination advantage, (3) referral who can speak to the candidate's adaptability and PM fundamentals."

**REMOTE-ONLY CANDIDATE RULE:** If `career-plan.md` shows the user has a remote-only preference or caregiver/family constraints, apply these adjustments throughout the entire process:
- **Bullet framing:** Lead every bullet with outcome/metric, NOT "worked remotely" or "managed distributed team." Remote is the HOW, not the WHAT. The reader should see impact first and only infer distributed work from context.
- **Async experience as a skill:** If the user has async-first experience, highlight it as a demonstrable skill: e.g., "Designed async decision framework adopted by 4 time zones" or "Built documentation-first culture enabling 3 distributed teams to ship independently." Async fluency is a competitive advantage -- surface it.
- **Location-neutral language:** Remove or reframe any location-specific language. "Bay Area startup" becomes "Series B startup." "NYC-based fintech" becomes "$40M ARR fintech." The resume should be location-agnostic so it passes through any recruiter's filter without anchoring to a geography.
- **Gap or part-time handling:** If the resume has gaps or part-time periods that correlate with caregiving, do NOT highlight or explain them -- just present the work done. No "part-time" labels unless the user explicitly requests them.
- **PRIVACY GUARDRAIL:** Never reference caregiving, children, family obligations, health conditions, or any personal reason for remote preference. This information, even if shared in career-plan.md, is NEVER included in any external-facing document. This is a hard rule with no exceptions.

**INVOLUNTARY DEPARTURE RULE:** If the user was fired (not laid off) from their most recent role: still list it with accurate dates. Do not remove it -- gaps are more suspicious than short tenure. Do not add departure annotations. The resume is for selling strengths; departure framing belongs in interview prep.

**CAREER GAP / RETURNER RULE:** If `career-plan.md` shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), apply these adjustments throughout the entire process:
- **No "Career Break" line item:** NEVER include a "Career Break" entry on the resume. The gap speaks for itself via dates. Adding a line item draws attention to the gap and invites questions the resume cannot answer.
- **During-gap professional activity:** Frame the return narrative entirely through what the person DID during the gap that is professionally relevant: freelance projects, volunteer board roles, certifications, coursework, advisory roles. Present these as natural resume entries with metrics where possible.
- **If nothing professional during the gap:** Simply let the dates tell the story. No explanation line, no "Career Sabbatical" entry, no footnote. Silence is better than a placeholder.
- **Pre-gap experience emphasis:** Emphasize the MOST RECENT pre-gap experience heavily -- it is the proof the skills exist. Give the last pre-gap role 5-6 bullets (more than standard). Select bullets that demonstrate skills most likely to be questioned after a gap (current tools, modern methodologies, relevant domain knowledge).
- **Return-to-work programs:** If the user completed a return-to-work program (e.g., Path Forward, reaccelerate, iRelaunch), include it prominently in Education or Certifications. These programs carry credibility with hiring managers who know them.
- **PRIVACY GUARDRAIL:** Never reference the REASON for the gap (health, caregiving, personal, travel, etc.). Even if shared in career-plan.md, external documents just present the work history without explanation. This is a hard rule with no exceptions.

### Step 2: Match Against Experience Library
For each parsed JD requirement:
1. Search `experience-library.md` organized sections (Growth/Metrics, Technical/Building, Leadership, Strategy, Domain Expertise, Other Notable). **[FUNCTION-ADAPTIVE]** Search for experience organized by the user's actual category headers in experience-library.md, not the PM defaults. SWE libraries organize by: Systems Built, Scale Achieved, Technical Leadership, Architecture Decisions. Design libraries: User Research, Design Systems, Shipped Products, Team Leadership. Data Science: Models Built, Business Impact, Technical Infrastructure, Stakeholder Influence. Marketing: Campaign Results, Growth Metrics, Brand Impact, Channel Expertise. CS/Sales: Revenue Metrics (NRR, GRR), Account Management, Team Leadership, Operations.
2. Search the Story Bank for relevant STAR stories
3. Score each potential match: STRONG (direct experience with metrics), PARTIAL (related but not exact), or NONE
4. Select the single strongest matching bullet for each requirement

**CAREER CHANGER RULE:** If the user has zero PM-titled roles in experience-library.md (e.g., management consultant, engineer, designer pivoting to PM), do NOT treat every PM-specific requirement as NONE. Instead:
- **Map adjacent experience to PM skills by underlying competency.** Consulting deliverables (market sizing, due diligence, ops transformation, client recommendations) map to PM skills (analytical rigor, cross-functional leadership, customer discovery, roadmap prioritization). Engineering experience maps to: technical feasibility judgment, experiment design, metric definition, cross-functional coordination, and build-vs-buy decisions. UXR/Design experience maps to: customer discovery, experimentation design, data-driven prioritization, insight-to-roadmap translation, and user journey optimization. Score these as PARTIAL with a note explaining the transferable framing.
- **For "X+ years PM experience" requirements when the user has 0 PM years:** Score as NONE. Do NOT count non-PM years as PM years. In the gap table, provide specific framing language that reframes the adjacent experience as product-adjacent (e.g., "My 3 years leading cross-functional teams at McKinsey involved the same core PM activities -- customer discovery, prioritization, stakeholder alignment -- applied in a consulting context"). Do not claim or imply the user has PM experience they do not have.
- **Title handling:** Keep original titles honest. Write "Engagement Manager, McKinsey" not "Product Manager, McKinsey." The bullets underneath do the reframing work through the SAD formula; the title must remain factual.
- **Summary for career changers:** The summary must frame the non-traditional path as intentional and additive, not as a gap. Lead with the transferable strength: "Growth strategist with 3 years driving $200M+ client outcomes at McKinsey, now bringing analytical rigor and customer-obsession to product management." Do NOT open with "Aspiring PM" or "Transitioning professional."

### Step 3: Rewrite Bullets with JD Keywords
For each matched bullet:
- Incorporate the exact keywords from the JD (ATS systems match on exact strings)
- Preserve the original metric and factual accuracy completely -- do not inflate numbers or add scope
- Front-load the action verb and result
- Keep each bullet to 1-2 lines max
- If the JD says "cross-functional collaboration" and your bullet says "worked with eng and design," rewrite to use "cross-functional collaboration" while keeping the same facts

**SAD Formula for Bullet Points:**
Every bullet must follow the SAD structure:
- **S - Surface:** What was the surface area / scope of the work? (product, feature, team, user base)
- **A - Action:** What did YOU specifically do? Use strong action verbs.
- **D - Data:** What was the quantified result? (metric moved, revenue impact, user growth)
Example: "Led the checkout redesign (Surface) by running 12 A/B tests on conversion funnel (Action), increasing purchase completion rate from 34% to 47% (Data)."

**Bullet Length:** Medium-length bullets outperform both short and long ones. Aim for 1.5-2 lines. One-liners feel thin. Three-liners get skimmed.

**Strong vs Weak Verbs:**
- AVOID: helped, worked, did, made, managed (excessive), was responsible for, participated, assisted, implemented (without specifics)
- USE: spearheaded, executed, pioneered, engineered, cultivated, optimized, amplified, orchestrated, accelerated, transformed

**Focus on Input Metrics:** Prioritize product input metrics (activation rate, conversion rate, time-to-value) over output metrics (revenue, headcount). Input metrics show PM craft; output metrics can be circumstantial. **[FUNCTION-ADAPTIVE]** Function-specific input metrics: SWE: latency, throughput, uptime, deployment frequency, code review velocity. Design: usability scores, task completion rates, NPS, design system adoption. Data Science: model accuracy, prediction lift, experiment velocity, data pipeline reliability. Marketing: CAC, conversion rate, MQL/SQL ratio, brand lift. CS/Sales: NRR, gross retention, churn rate, health score accuracy, expansion ARR, time-to-value.

**Handling PARTIAL matches for career pivoters:** When a JD requirement has no STRONG match but the user has transferable experience from a different domain (e.g., automotive PM pivoting to AI PM), rewrite the bullet to emphasize the transferable skill while preserving the original context. Frame it as: "[Transferable skill] applied in [original context] with [metric]." Do NOT remove the original context to make the bullet seem like direct experience. Example: A Tesla PM with "Led sensor data pipeline optimization" can frame it as data/ML-adjacent work, but must not rewrite it as "Led ML model development." The gap table should still flag the requirement as PARTIAL with a note about the transferable framing.

**CRITICAL RULE: NEVER add skills, projects, metrics, or experience not found in experience-library.md. If no match exists, it goes in the Gaps section. Do not invent.**

### Regional Format Detection

Before structuring the resume, check career-plan.md for target market. Adapt format to regional norms:

**US (default):** 1 page maximum. No photo. No personal details (DOB, marital status). Reverse-chronological. MM/YYYY dates.

**UK:** 2 pages maximum (1.5-2 pages ideal). Add "Personal Profile" section (3-4 sentences, UK equivalent of Summary). UK spelling (organisation, optimisation). DD/MM/YYYY dates. "References available upon request" footer optional.

**Germany:** 2 pages. Chronological order (oldest to newest). Professional headshot top-right corner. Include nationality, DOB. German section headers if role is German-language (Berufserfahrung, Ausbildung, Kenntnisse). Reverse-chronological acceptable for international companies.

**India:** 2-3 pages acceptable for senior roles. Include DOB, nationality, languages spoken for domestic roles. Add "Declaration" footer for traditional companies. For MNC India offices, use hybrid format (US structure, 2 pages OK).

**Middle East (UAE/Saudi/Qatar):** Include professional photo, nationality, visa status, DOB. 2 pages. More formal tone.

If target market is not specified, default to US format. If JD is clearly from a non-US company (UK spelling, EU location, etc.), ask the user to confirm target market before proceeding.

### Step 4: Structure the Resume
Build the full resume in this order:
1. **Header:** Name, contact info, links (pulled from experience-library.md)
2. **Summary (2-3 sentences):** Incorporate the addressing-weaknesses strategy from career-plan.md. Position strengths that directly counter the user's identified gaps. Weave in top JD keywords. Build a "pointy profile" identity -- a through-line that brands the candidate (e.g., "the growth PM who builds experimentation infrastructure") not a jack-of-all-trades ("enterprise SaaS solutions expert").
3. **Experience:** Most relevant role first (not necessarily most recent). Under each role, lead with bullets that match JD requirements. Limit to 3-5 bullets per role, most matched first. For lesser-known companies, add a parenthetical with size/revenue context (e.g., "Series B fintech, $40M ARR, 200 employees"). **International employer brand rule:** If the user's employers are well-known in their home market but unknown to US recruiters (or vice versa), the parenthetical must include both scale metrics AND a market-positioning anchor that gives the reader instant calibration (e.g., "Rakuten Ichiba ($15B GMV, Japan's largest e-commerce marketplace)" or "Personio (Series E, $8.5B valuation, Europe's leading HR platform)"). The goal is to convert an unfamiliar company name into an immediately impressive signal. Check `career-plan.md` addressing-weaknesses for any "unknown employer brand" weakness -- if present, ensure EVERY employer in the experience section has a contextualizing parenthetical. When the user's experience library already contains these parentheticals, preserve them exactly.
4. **Skills section:** Mirror the JD's skill categories exactly. Only list skills with evidence in the experience library. Do NOT include cross-functional team sizes (table stakes for PMs -- everyone works cross-functionally). **[FUNCTION-ADAPTIVE]** For SWE: cross-functional influence scope IS a key Staff+ signal, include it. For CS: cross-functional work with Sales and Product is important, include it.
5. **Education / Certifications:** Include if JD mentions specific requirements. Do NOT lead with certifications/skills -- they belong at the bottom.

**F-Pattern Reading Rule:** Recruiters scan resumes in an F-pattern (top-left, across, then down the left edge). The top-left quadrant of the resume must contain the strongest, most JD-relevant content. Place the most compelling role, bullet, or summary statement there.

**Hard Constraint: 1 page maximum, always (US format).** For non-US formats where the Regional Format Detection section specifies a higher page limit, use that limit instead. Use every square centimeter -- no wasted white space. If content overflows, cut the weakest bullets first.

### Step 5: Calculate Keyword Coverage Score
Count: (number of JD requirements with STRONG or PARTIAL match) / (total JD requirements). Display as percentage. Also show the raw numbers.

### Step 6: Flag Gaps
For each JD requirement scored NONE:
- State the gap clearly
- Suggest specific language for the cover letter to address it (reference `/cover-letter` skill)
- Suggest whether a referral message should mention it (reference `/referral-request` skill)
- If the gap is a years-of-experience shortfall, suggest how the addressing-weaknesses framework handles it

### Step 7: Inline Reviews
Run these two reviews inline (these are not separate skills -- execute them as part of this skill's output):
1. **Recruiter scan review** -- Simulate a 6-second recruiter scan. Check: Does the resume pass the glance test? Is the most relevant experience visible in the top third? Is the summary compelling? For career changers: does the summary successfully reframe the non-traditional path? For downleveled candidates: does the resume read as IC-oriented, not executive?
2. **ATS compatibility review** -- Check ATS compatibility: standard section headers, no tables/columns/graphics in markdown, keyword density, parseable date formats.

If either review flags issues, auto-correct the resume and note what changed in a "Revisions" section.

### Dual Application Coherence Check

If the user is tailoring a resume for a company where they have already tailored a resume in this session or recently:
- Compare the two target roles. The resumes should tell different but non-contradictory stories -- same person, different emphasis.
- Flag any bullets that appear in one resume but would undermine the narrative of the other.
- Advise: "You're applying to two roles at [Company]. The hiring managers may compare notes. Both resumes should be truthful and consistent -- just different in emphasis."

### Re-Application Differentiation

Before generating, check interview-history.md for prior applications at this company. If a prior rejected application exists:
- Identify weakness areas from the prior cycle.
- The new resume MUST include at least 2 pieces of new evidence (new projects, skills, certifications gained since the rejection) that address prior weaknesses.
- Do NOT re-use the same resume. Differentiate meaningfully.

### Step 8: Traceability Audit

Before assembling the final output, create a traceability table mapping every resume bullet to its source in experience-library.md. This ensures nothing was fabricated and every claim is verifiable.

For each bullet in the resume:
1. Find the original text in experience-library.md that the bullet was derived from.
2. Classify the match type:
   - **EXACT** -- the bullet uses the same wording as the source, with only minor keyword swaps for ATS optimization.
   - **REWORDED** -- the bullet conveys the same fact/metric but restructured for the JD. The original meaning is preserved.
   - **INFERRED** -- the bullet was synthesized from multiple sources or extrapolated from the experience library. Flag these with: "[VERIFY: This bullet was inferred from your experience library. Confirm accuracy before submitting.]"
3. If a bullet has NO source in experience-library.md, REMOVE it from the resume. Do not include fabricated bullets.

Format the table as:

| Resume Bullet (first 60 chars) | Source Section | Original Text | Match Type |
|-------------------------------|----------------|---------------|------------|
| Led cross-functional team of 8 to ship AI recomm... | Growth/Metrics | Led cross-functional team of 8 (eng, design, data) to ship AI recommendation engine... | EXACT |
| Drove data-driven experimentation framework acros... | Technical/Building | Built A/B testing framework, running 40+ experiments... | REWORDED |
| Orchestrated enterprise onboarding redesign that... | [multiple sources] | [combined from Story 3 + Growth bullet 4] | INFERRED [VERIFY] |

After building the table:
- If any bullets are INFERRED, add the verification flag to the resume output and alert the user.
- If any bullets had no source, report them as removed: "Removed [N] bullet(s) with no traceable source in experience-library.md."
- Include this table in the final output after the ATS Review section.

### Classified Experience Handling

If experience-library.md contains entries marked as classified or with redacted details:
- Allow generalized bullets describing TYPE of work and SCALE without specifics: "Led analytical team of 12 producing decision-support products for senior government leaders."
- Flag these as [CLASSIFIED -- generalized per security obligations], NOT as [UNVERIFIED].
- Advise the user to have their security officer review the resume before submitting.

### Step 9: Final Output
Assemble the complete output in the format specified below.

## Output

```markdown
## Resume Output - [Company Name] [Role Title]
**Keyword Coverage: [XX]% ([N]/[Total] requirements matched)**

### Gaps ([N] unmatched requirements)

| # | JD Requirement | Gap Type | Suggested Response |
|---|---------------|----------|-------------------|
| 1 | [requirement text] | No match | Cover letter: "[specific suggested sentence]" |
| 2 | [requirement text] | Partial only | Referral message: "[specific suggested framing]" |

### Resume

[Full formatted resume in clean markdown]

---

### Recruiter Review
- **First impression (6-second scan):** [Pass/Fail + notes]
- **Relevance signal:** [Does top third match the JD?]
- **Readability:** [Clean, scannable, right length?]

### ATS Review
- **Section headers:** [Standard / Non-standard]
- **Keyword matches:** [List of matched keywords]
- **Formatting issues:** [Any parsing risks]

### Traceability Audit
| Resume Bullet (first 60 chars) | Source Section | Original Text | Match Type |
|-------------------------------|----------------|---------------|------------|
| [first 60 chars of bullet]... | [section name] | [original text from experience-library.md] | EXACT/REWORDED/INFERRED |
| ... | ... | ... | ... |

**Bullets removed (no source):** [N] — [list if any]
**Bullets flagged for verification:** [N] — [list any INFERRED bullets with "[VERIFY: This bullet was inferred. Confirm accuracy before submitting.]"]

### Revisions Made
- [List of auto-corrections from sub-agent reviews, if any]
```

## Example

**Input:**
```
/resume-tailor

Senior Product Manager, AI Platform - Notion
Requirements: 6+ years PM experience, AI/ML product experience,
platform/API experience, cross-functional leadership, data-driven
decision making, B2B SaaS experience, user research skills
```

**Output:**
```markdown
## Resume Output - Notion Senior PM, AI Platform
**Keyword Coverage: 71% (5/7 requirements matched)**

### Gaps (2 unmatched requirements)

| # | JD Requirement | Gap Type | Suggested Response |
|---|---------------|----------|-------------------|
| 1 | "6+ years PM experience" | Partial (4 years PM + 2 years adjacent) | Cover letter: "My 4 years as PM are preceded by 2 years in product-adjacent consulting at Deloitte, where I led client discovery and roadmap development -- giving me 6 years of end-to-end product thinking." |
| 2 | "Platform/API experience" | No match | Referral message: "I don't have direct platform PM experience, but I've built on top of APIs extensively and shipped integrations that increased ecosystem engagement 34%." |

### Resume

**[Name]**
[email] | [phone] | [linkedin] | [portfolio]

**Summary**
Product manager with 4 years shipping AI-powered B2B SaaS products, backed by 2 years product-adjacent consulting. Track record of data-driven decision making that moved activation rates 23% to 41%. Experienced leading cross-functional teams of 8+ across eng, design, and data science.

**Experience**

**Product Manager, [Company A]** | 2022 - Present
- Led cross-functional team of 8 (eng, design, data) to ship AI recommendation engine serving 2M daily users, increasing engagement 28%
- Drove data-driven decision making through A/B testing framework, running 40+ experiments that improved activation rate from 23% to 41%
- Conducted 60+ user research interviews informing B2B SaaS product roadmap, reducing churn 15%

[... continued ...]

### Recruiter Review
- **First impression:** PASS. AI and B2B SaaS experience visible in top third.
- **Relevance signal:** Strong. Summary directly addresses the role.
- **Readability:** Clean. 1-page length appropriate for senior PM.

### ATS Review
- **Section headers:** Standard (Summary, Experience, Skills, Education)
- **Keyword matches:** AI/ML, cross-functional, data-driven, B2B SaaS, user research
- **Formatting issues:** None detected

### Revisions Made
- Moved AI experience bullet to first position under most recent role (recruiter review flagged it was buried)
- Added "B2B SaaS" to summary (ATS review flagged missing keyword)
```

## Quality Checks

**Good output looks like:**
- Coverage score is honest, not inflated. Partial matches are labeled partial.
- Every bullet in the resume traces back to a specific entry in experience-library.md
- Gaps section provides actionable language, not vague advice like "consider mentioning this"
- Resume reads naturally despite keyword insertion -- not keyword-stuffed
- Summary incorporates the addressing-weaknesses strategy without sounding defensive
- Sub-agent reviews caught at least one thing and the revision is noted

**Bad output looks like:**
- Coverage score of 95%+ with vague matches (inflated to look good)
- Bullets that contain skills, metrics, or projects not in the experience library (fabricated)
- Generic gap suggestions like "mention this in your cover letter" without specific language
- Keywords crammed in unnaturally ("I leveraged cross-functional synergies to streamline...")
- No sub-agent review output, or reviews that say "everything looks great" with no specifics
- Resume longer than 1 page for roles requesting under 10 years experience

**Persona-specific checks (verify these when applicable):**
- **Single employer (5+ years):** Company name does NOT dominate visual scan. Summary leads with transferable identity, not employer brand.
- **Declining product:** Bullets lead with user outcomes and transferable skills, not the product name. At least one bullet explicitly frames "constrained environment" as a strength.
- **Manager-to-IC transition:** No "managed a team of X" bullet appears in the first 3 bullets of any role. IC craft bullets (shipped, designed, analyzed, defined, tested) lead.
- **Career changer:** Competency mapping is explicit. Title integrity preserved (no fake PM titles). The gap table includes a cover-letter-ready sentence for the title gap.
- **International/unknown employers:** Every non-US-famous employer has a parenthetical with scale metrics AND a market-positioning anchor (e.g., "Japan's largest" or "$8.5B valuation"). If career-plan.md lists a "zero US network" or "unknown employer brand" weakness, confirm the summary leads with universal metrics (revenue, users, GMV) not employer names. The summary should be impressive to someone who has never heard of any company on the resume.
- **Visa-requiring candidates:** If career-plan.md mentions visa sponsorship needs, the resume header includes "H-1B Sponsorship Required" (or equivalent) only if the user's experience-library.md header already contains it. Do NOT add visa language to bullet points or summary -- visa is a logistics conversation, not a qualification signal. Verify the summary does not contain defensive language about relocation or authorization status.
- **Early-career (fewer than 3yr):** Summary opens with the strongest output metric, never tenure. Education section is promoted above Skills if the user has a relevant degree or thesis with metrics. No apologetic language anywhere ("despite my limited experience," "although I'm early in my career" -- ban these). Gap table uses "output metrics" framing for every years-of-experience shortfall.
- **Domain-locked (80%+ in one vertical):** For out-of-domain applications, every bullet leads with the transferable skill label. Employer descriptions use scale metrics, not domain positioning. Summary leads with skill identity, not domain identity. Translation dictionary from career-plan.md (if present) is applied to all bullets.
- **Remote-only candidate:** If career-plan.md indicates remote-only preference, verify: (a) No bullet leads with "worked remotely" or "managed distributed team" -- remote is the HOW, not the WHAT. Every bullet leads with outcome/metric. (b) Async experience is highlighted as a skill, not a circumstance. (c) No location-specific language remains (e.g., "Bay Area startup" should be "Series B startup"). (d) PRIVACY GUARDRAIL: No reference to caregiving, children, family obligations, health conditions, or any personal reason for remote preference appears anywhere in the resume. This information is NEVER included in external-facing documents even if present in career-plan.md.
- **Career gap / returner:** If career-plan.md shows a career gap (gap_years > 0 or explicit career break mention), verify: (a) No "Career Break" line item appears on the resume -- dates tell the story. (b) During-gap professional activities (freelance, board roles, certifications, coursework) are naturally woven into the resume. (c) Most recent pre-gap experience is emphasized heavily. (d) Return-to-work programs (Path Forward, reaccelerate, etc.) appear in Education or Certifications if applicable. (e) PRIVACY GUARDRAIL: No reference to the REASON for the gap (health, caregiving, personal) appears anywhere.
- **Traceability table present:** The table mapping every bullet to its source in experience-library.md is included. Any INFERRED bullet is flagged for user confirmation.

**[FUNCTION-ADAPTIVE] Function-Specific Resume Structure:**

When the detected function is NOT PM, add these function-specific structural elements:

- **SWE:** Include a "Technical Skills" or "Technologies" section near the top listing: languages, frameworks, infrastructure tools, and system design domains. If the candidate has open-source contributions or a GitHub profile, include a link. For Staff+ roles, include a "Technical Leadership" subsection highlighting architecture decisions, design doc authorship, and mentoring scope.
- **Design:** Include a portfolio link prominently (below name/contact, above summary). Structure experience bullets around case study format: Problem → Approach → Outcome. Include a "Design Tools" section (Figma, Sketch, Principle, Framer, etc.). For Lead+ roles, include design system contributions and team mentoring.
- **Data Science:** Include a "Technical Skills" section: languages (Python, R, SQL), ML frameworks (PyTorch, TensorFlow, scikit-learn), data tools (Spark, Airflow, dbt), and statistical methods. If the candidate has publications (NeurIPS, ICML, etc.), include a "Selected Publications" section. For ML Engineer roles, also include infrastructure skills (Kubernetes, Docker, MLflow).
- **Marketing:** Include a "Channel Expertise" section listing channels managed (paid search, SEO, email, social, content, events) with spend levels where impressive. For Director+, include team size and budget authority. Include relevant certifications (Google Analytics, HubSpot, etc.).
- **CS/Sales:** Include "Book of Business" summary: total ARR managed, number of accounts, average deal size. Include CS platform expertise (Gainsight, Totango, ChurnZero, Salesforce). For Director+, include team size and NRR/GRR ownership scope.
- **Failed founder / shut-down company:** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, verify: (a) Company name is used (not hidden), with a one-line descriptor if the company is obscure: "Acme Health (health-tech startup, $2M seed, 15-person team)." (b) Title "Founder & CEO" is fine but responsibilities are framed in EMPLOYEE terms: "Led product strategy" not "Started a company." (c) Bullet format is OUTCOME-first: "Grew MAU from 0 to 12K in 8 months" not "Founded a company that achieved 12K MAU." (d) No bullet includes "Company shut down," "Failed to raise Series A," or any shutdown framing -- just present the work. The dates tell the story. (e) Transferable scope is extracted: "Managed $800K annual burn" becomes "Owned P&L decisions across a $800K budget." (f) If the startup had notable investors, advisors, or customers, they are included -- they validate the person's judgment even if the outcome was unfavorable.
- **Veteran / 15+ years experience:** If career-plan.md shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, etc.), or explicit mention of age-related concerns, verify: (a) Only the last 10-12 years of experience have DETAILED bullets. Earlier roles are consolidated into a 1-line "Earlier: [Title] at [Company] (Year-Year)" format. (b) Graduation year is REMOVED from Education section -- this is the #1 age signal. (c) Skills section leads with CURRENT tech/methodologies; outdated technologies (Waterfall, legacy tools) are removed or listed after current ones. (d) If the resume template has a photo placeholder, the user is explicitly recommended against including one (age signal). (e) RECENT impact (last 3-5 years) is quantified most heavily -- hiring managers give most weight to recent work.
- **Military-to-PM career changer:** If career-plan.md shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), verify: (a) JARGON TRANSLATION: Every military term is translated to civilian business language. "Commanded a 30-person platoon" becomes "Led a 30-person cross-functional team across 3 time zones." "Conducted intelligence preparation of the battlefield" becomes "Led strategic competitive analysis informing executive-level decisions." "Managed battalion S2 intelligence operations" becomes "Directed analytical operations for a 500-person organization, synthesizing data from 12+ sources into actionable recommendations." "Theater-level SIGINT collection" becomes "Designed and managed large-scale data collection programs across a distributed organization." "Battle damage assessment" becomes "Developed impact measurement framework for high-stakes operational decisions." Flag any untranslated military jargon. (b) CLASSIFIED EXPERIENCE HANDLING: If the user mentions classified work, frame it as: "Led [scope descriptor] analytical projects for [organization size] organization. Details available upon appropriate clearance verification." Never ask the user to describe classified work -- just frame the SCOPE and SKILLS. (c) SECURITY CLEARANCE: If the user holds an active clearance (TS/SCI, TS, Secret), include it prominently -- it is a MAJOR differentiator for defense tech roles and some enterprise roles. (d) DUAL-FORMAT RESUME: Recommend creating TWO versions -- one for defense tech (clearance prominent, military terminology partially preserved, mission-focus) and one for general tech (fully translated, clearance mentioned but not prominent). (e) Summary for military-to-PM: lead with transferable leadership and analytical skills, not military rank. Good: "Operations and intelligence leader with 6 years directing analytical teams of 30+ across distributed organizations, now bringing structured decision-making and data-driven leadership to product management." Bad: "Former Army Captain seeking PM roles."
