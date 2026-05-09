---
name: weekly-retro
description: End-of-week analysis of job search performance with data-driven coaching and bottleneck identification.
---

# /weekly-retro - Weekly Performance Retrospective

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In weekly retro contexts, this means: the retro may use private information for internal analysis (e.g., adjusting benchmarks for visa-constrained searches) but must never surface private details in the output text that the user might share with a coach or accountability partner.

## When to Use

- End of each week (Friday afternoon or Sunday evening)
- When you feel stuck and want a data-driven diagnosis
- After a particularly good or bad week to capture what changed
- Monthly for a longer-term trend view (run with `/weekly-retro monthly`)

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

- **Auto-loaded:** `context-library/app-tracker.md` - The persistent application tracker file. Read this file directly to extract all pipeline data, status history, dates, referral information, and stage transitions. This is the primary data source for all pipeline metrics. If this file does not exist, note: "No app-tracker.md found. Pipeline metrics cannot be calculated. Run `/app-tracker add` for your first few applications to start tracking."
- **Auto-loaded:** `context-library/connection-tracker.md` - Networking activity and referral data
- **Auto-loaded:** `context-library/interview-history.md` - Interview scores, patterns, and weakness heatmap
- **Auto-loaded:** `briefings/` folder - Daily briefings for activity history
- **Auto-loaded:** `templates/referral-tracker-template.md` - Referral status per role
- **Auto-loaded:** `context-library/career-plan.md` - For context on targeting strategy
- **Auto-loaded:** `context-library/target-companies.md` - For pipeline status data that may be tracked there instead of app-tracker.md

If any input file is empty or missing, note it in the output and work with available data. Never fabricate metrics.

**Graceful degradation when app-tracker.md is missing or empty:** If `context-library/app-tracker.md` does not exist or is empty, the retro MUST still produce useful output by assembling pipeline data from other sources:
1. **From target-companies.md:** Scan the Status fields (e.g., "IN PROCESS -- Round 1 complete," "REFERRAL SUBMITTED," "NOT STARTED") and the Summary by Status table to reconstruct the current pipeline state. Count companies by status to derive application volume, interview activity, and pipeline movement.
2. **From connection-tracker.md:** Extract referral request/received dates, last contact dates, and next actions to derive networking activity metrics.
3. **From interview-history.md:** Extract interview dates, companies, rounds, and scores to derive interview performance metrics and weekly interview count.
4. **From briefings/ folder:** Check recent briefing files for any logged activity.
5. **Output a degraded-but-useful retro** that says: "Note: No app-tracker.md found. This retro is assembled from target-companies.md, interview-history.md, and connection-tracker.md. Metrics are approximate. For precise pipeline tracking, run `/app-tracker add` for each active application."
6. At the bottom of the retro, include a setup prompt: "To enable full pipeline analytics next week, run these commands to initialize your tracker:" followed by `/app-tracker add` commands for each in-process company found in target-companies.md.

## Process

### Step 1: Collect This Week's Raw Data

Read all data sources and extract activity from the current week (Monday through today).

**Applications:**
- Count new applications submitted this week
- List each: company, role, fit score, referral status
- Note the fit score distribution (are they targeting 70+ roles or spraying?)

**Networking:**
- Connection requests sent this week
- Connections accepted this week
- Follow-up messages sent
- Coffee chats / calls completed
- Referral requests sent
- Referrals received (ATS submissions)
- Strong referrals received (HM pings)

**Interviews:**
- Interviews completed this week
- For each: company, role, round, overall score
- Interview prep packages generated
- Mock interviews run

**Pipeline movement:**
- New rejections this week
- New interviews scheduled
- Roles that advanced to next round
- Offers received

### Step 2: Calculate Metrics

Compute each metric and compare against benchmarks:

| Metric | This Week | Benchmark | Status |
|---|---|---|---|
| Applications sent | [N] | 10-15/week | [Above/Below/On track] |
| Avg fit score of applications | [N]/100 | 70+ | [Above/Below] |
| Applications with referrals | [N] ([%]) | 60%+ | [Above/Below] |
| Applications with strong referrals (HM ping) | [N] ([%]) | 25%+ of referrals | [Above/Below] |
| Connection requests sent | [N] | 25/day, 125/week | [Above/Below] |
| Connection acceptance rate | [%] | 20-30% | [Above/Below] |
| Referral request conversion | [%] | 40-60% | [Above/Below] |
| Interviews scheduled | [N] | 2-4/week (at steady state) | [Above/Below] |
| Interview scores (avg) | [X]/10 | 7+/10 | [Above/Below] |
| Callback rate (overall) | [%] | 10-15% (with referrals) | [Above/Below] |
| Callback rate (with referral) | [%] | 15-25% | [Above/Below] |
| Callback rate (cold) | [%] | 3-5% | [Above/Below] |

**SENIOR-LEVEL BENCHMARK ADJUSTMENT:** If career-plan.md shows the user is TARGETING Director level or above (regardless of current level), apply senior-level benchmarks. This includes candidates currently at Senior Manager or IC level who are pursuing Director+ roles. **Stretch-level targeting:** If the candidate's current level is 2+ levels below the target (e.g., IC targeting VP, Senior Manager targeting VP), apply senior-level benchmarks AND add a "stretch-level flag" noting that conversion rates will be lower than standard and timeline should be extended 20-30% beyond the senior benchmark. Replace the standard benchmarks with executive-search benchmarks. Senior roles have fundamentally different dynamics -- fewer open positions, longer hiring cycles, and higher referral dependency. Apply these adjusted benchmarks:
- **Applications sent:** 2-5/week (NOT 10-15). Senior roles are scarce and each application requires significant customization. Applying to 10+ VP roles per week signals either spray-and-pray targeting or applying below level.
- **Connection requests sent:** 5-15/week (NOT 125/week). Executive networking is about depth, not volume. Five meaningful connections with VP/Director peers are worth more than 100 cold requests to Senior PMs.
- **Referral rate:** 80%+ (NOT 60%). At Director+ level, cold applications are near-zero value. Every application should go through a warm channel -- either a direct referral, an executive recruiter, or a hiring-manager outreach with a work product.
- **Application volume below 5/week is NOT flagged as a bottleneck** if the following conditions are met: (1) average fit scores are 75+, AND (2) referral coverage is above 80%. Low volume with high quality and warm channels is the correct executive search strategy. Flag it as a bottleneck ONLY if fit scores are below 70 or referral coverage is below 50%.
- **Interviews scheduled:** 1-2/week at steady state (NOT 2-4). Senior interviews are multi-round and time-intensive. One VP-level loop per week is a healthy pipeline.
- **Connection acceptance rate:** 30-50% (higher than standard, because targets are peers, not strangers).
- **Search timeline expectation:** 10-20 weeks (NOT 6-10). VP/Director searches take longer. Do not alarm the user at week 8 if the pipeline is healthy.

**[FUNCTION-ADAPTIVE]** Adjust benchmarks by function:

**SWE Staff+ Benchmarks:**
- Apps/week: 2-5 quality applications (these roles are scarcer)
- Interviews/week at steady state: 1-2
- Expected search timeline: 10-16 weeks

**Design Leadership Benchmarks:**
- Apps/week: 2-4 quality applications (portfolio prep adds 1-2 hours per application; design challenges are common take-home assignments consuming 4-8 hours each)
- Interviews/week at steady state: 1-2 (design interviews include portfolio review + design challenge rounds that take longer than standard interviews)
- Expected search timeline: 12-18 weeks (design hiring includes portfolio review + design challenge rounds that extend timelines)
- Design-specific tracking: portfolio prep time (hours/week), design challenges submitted, portfolio case studies refreshed
- Pacing alert: "If design challenges are consuming >10 hours/week, you're over-investing in individual applications. Target 4-6 hours per design challenge maximum."

**Marketing Manager/Director Benchmarks:**
- Apps/week: 3-5 quality applications (similar to PM but marketing role variation means more time evaluating fit)
- Interviews/week at steady state: 2-3
- Expected search timeline: 10-14 weeks
- Marketing-specific tracking: sub-function alignment (are you consistently targeting growth vs brand vs product marketing?), marketing case study prep time
- Sub-function drift alert: "If >30% of applications cross marketing sub-functions (e.g., growth marketing person applying to brand roles), flag for strategy review. Sub-function switching mid-search dilutes your positioning."

**Data Science / MLE Benchmarks:**
- Apps/week: 2-4 quality applications (technical prep including coding screens + modeling exercises requires dedicated time)
- Interviews/week at steady state: 1-2 (DS/MLE interviews include coding screen + case study + modeling round, often 4-6 rounds total)
- Expected search timeline: 10-16 weeks (longer at Staff/Manager level due to fewer roles and more competitive rounds)
- DS-specific tracking: coding practice hours/week, case study performance scores, take-home completion rate
- DS-to-MLE transition tracking: "If targeting MLE roles from a DS background, track system design performance separately from statistical modeling performance. MLE interviews weight system design more heavily."

**CS/Sales Director+ Benchmarks:**
- Apps/week: 3-5 quality applications (VP CS searches have a smaller role universe than PM or SWE)
- Interviews/week at steady state: 1-2 (CS hiring includes case study + multiple stakeholder interviews + role-play rounds)
- Expected search timeline: 12-20 weeks (VP-level CS roles have longer hiring cycles due to multiple stakeholder sign-offs and role-play evaluation)
- CS-specific tracking: NRR story refinement, role-play prep hours, executive communication practice
- CS-specific pacing: "VP CS roles often require meeting 4-6 stakeholders (CEO, CRO, CFO, VP Sales, VP Engineering, Board). Expect 3-4 week gaps between rounds — this is normal, not a red flag."

**Callback rate calculation:**
- Callback rate = (applications that received any positive response: screen, interview, or request for more info) / (total applications submitted at least 7 days ago)
- Only include applications old enough to have received a response (7+ days)
- Separate into: with referral vs. cold

**Fit score distribution:**
- Count applications in each band: 80-100, 70-79, 60-69, below 60
- If more than 30% of applications are below 70, flag targeting issues

### Step 2b: Visa-Constrained Candidate Context Check

Before analyzing bottlenecks, check `career-plan.md` and `qa-master.md` for visa sponsorship requirements. If the user needs H-1B or other work visa sponsorship, adjust the analysis framework:

- **Smaller target pool is expected, not a problem.** Visa-requiring candidates may have 30-50% fewer eligible companies than unrestricted candidates. A smaller application volume (5-8/week instead of 10-15) is normal and expected if every company has been pre-filtered for sponsorship. Do NOT flag low volume as a bottleneck if the user is correctly filtering for sponsorship. Instead, check whether the user is exhausting their filtered list efficiently.
- **Benchmarks shift for timeline.** International candidates with visa requirements typically take 8-14 weeks to receive an offer vs 6-10 weeks for unrestricted candidates. Factor in: visa confirmation delays at recruiter screen stage, additional legal review before offers, and H-1B lottery timing constraints (April registration, October start). Adjust weekly coaching accordingly: "Week 5 of a visa-sponsored search. You're on a slightly longer timeline than unrestricted candidates. The pipeline is building correctly."
- **Track visa-specific pipeline data:**
  - How many target companies have confirmed H-1B sponsorship?
  - Have any applications been rejected specifically due to visa issues?
  - Are there alternative visa paths being explored (L-1 transfer, O-1)?
- **Networking is even more critical.** Cold applications from international candidates with unknown employer brands face double filtering (unknown company + visa cost). Referral rate target should be 70%+ (vs 60% benchmark) for visa candidates.
- **Motivation section must acknowledge the constraint without being discouraging.** Reference the specific pool size and progress within it.
- **Unknown employer brand + visa = double-filter metric.** For international candidates with unknown employer brands AND visa requirements, cold application callback rates may be as low as 1-2%. Do NOT treat this as a personal failure -- it reflects structural filtering. The coaching recommendation must emphasize referrals even more aggressively: "Your cold callback rate of [X]% reflects the double filter of unfamiliar employer brands and visa sponsorship requirements. This is structural, not personal. Target 80%+ referral coverage. Every cold application without a referral is near-zero expected value for your profile."
- **Comp framing progress tracking.** If interview-history.md shows comp framing as a weakness (score below 7/10), add a dedicated "Comp Readiness" row to the coaching recommendations: "Your comp framing scored [X/10] in prior interviews. Before any call this week that might touch comp, rehearse the redirect from qa-master.md: never state current non-US comp, always cite levels.fyi market rate. Run `/mock-interview behavioral` and request a compensation question."

### Step 2c: Career Changer Context Check

Before analyzing bottlenecks, check `career-plan.md` for the addressing-weaknesses section. If the user has NO prior PM title (career changer), adjust the analysis framework:

- **Benchmarks shift.** A career changer's callback rate will be lower than an experienced PM's, especially cold. Do not alarm the user with "your 5% callback rate is below the 10-15% benchmark" if they have zero PM experience on paper. Instead, benchmark against career-changer norms: 3-8% overall callback rate is typical for career changers in weeks 1-4; it improves as the portfolio and network build.
- **Different bottlenecks matter.** For career changers, the most common bottleneck is not application volume -- it is POSITIONING. If callbacks are low despite referrals, the issue is likely that the resume/cover letter still reads as "consultant trying to break in" rather than "product thinker with consulting superpowers." Flag this and suggest re-running `/resume-tailor` and `/cover-letter` with explicit career-changer framing.
- **Track career-changer-specific metrics:**
  - Work products created this week (via `/work-product`) -- career changers need these to compensate for no PM portfolio
  - "Transition narrative" consistency -- is the user telling the same story across resume, cover letter, and interviews?
  - Informational interviews with PMs at target companies (these build PM vocabulary and signal commitment to the transition)
- **Motivation section must acknowledge the transition.** "Week 3 of your first PM search. Most career changers from consulting see their first interview in weeks 3-5. Your work product for [Company] is exactly the kind of signal that gets HMs to take a call. Keep building the portfolio -- each one compounds."
- **Critical interview weakness flag for career changers:** Check `interview-history.md` for any question type scored at or below 5/10. For career changers, scores at this level on "PM narrative" (TMAY), "product you built," or "consulting-to-PM translation" are EMERGENCY items that must appear as the #1 coaching recommendation. These are not just low scores -- they are the exact questions that gatekeep career changers out of PM roles. If "product you built" is scored 4/10, the retro must say: "CRITICAL: Your 'walk me through a product you built' answer is scoring 4/10. This question appears in nearly every PM interview and a 4/10 will end your candidacy regardless of how strong your other answers are. This week: run `/mock-interview behavioral` and practice this specific question 5 times until you score 7+. Nothing else matters more than fixing this."
- **Consulting-specific career changer diagnostics (McKinsey, BCG, Bain, Deloitte, Accenture):** If the career changer comes from consulting: (1) If callback rate is low despite referrals, check if resume still reads as "consultant" rather than "product thinker" -- flag: "Your resume may still signal 'consultant looking for exit' rather than 'product person with consulting superpowers.' Re-run `/resume-tailor` with career-changer framing." (2) Comp anchoring risk: consulting EM/AP comp ($220-280K) may exceed target PM bands. If screened out at recruiter stage, comp expectations may be the filter -- consider adjusting stated range. (3) Track "consulting-to-PM narrative consistency" across interviews: are they using the same framing every time? Inconsistent narrative is a common consulting-to-PM failure mode.

### Step 2d: Early-Career Context Check

Before analyzing bottlenecks, check `experience-library.md` and `career-plan.md` for total PM/target-role experience. If the user has fewer than 3 years of experience, adjust the analysis framework:

- **Benchmarks shift.** Early-career candidates should target 5-8 quality applications per week (not 10-15). Each application requires more effort because the resume has fewer bullets to work with and needs heavier tailoring. Do NOT flag 5-6 apps/week as low volume for early-career candidates -- flag only if below 4/week.
- **Referral rate target is HIGHER.** Early-career candidates benefit disproportionately from referrals because their resume alone may not survive ATS filtering. Target 70%+ referral rate (not 60%). Flag any week where referral rate drops below 50%: "With fewer than 3 years of experience, cold applications have an even lower callback rate than the general benchmark. Every application without a referral is near-zero expected value."
- **Track work-product creation.** Early-career candidates should be creating 1-2 work products per week (via `/work-product`). Work products compensate for thin resumes. If no work products were created this week, flag: "You have fewer than 3 years of experience. Work products are your primary differentiator. Create at least one this week for your top-priority application."
- **Timeline expectation: 8-14 weeks.** Early-career PM searches typically take longer because fewer roles are entry-friendly. Do not alarm the user at week 6 if the pipeline is healthy. Adjust motivation accordingly: "Week [N] of your search. Early-career PM searches average 8-14 weeks. Your pipeline is [healthy/building/needs attention]."
- **Motivation must acknowledge the experience gap without being discouraging.** Reference progress in skill-building terms: "You created 2 work products this week and your interview scores improved from 5.5 to 6.8. You're building the PM portfolio that makes up for the years you don't have yet."

### Step 2e: Career Changer Engineering-Specific Context

If `career-plan.md` indicates the user is an engineer transitioning to PM, add this motivation framing: "Your engineering background is a genuine asset, not a liability. The companies that understand this will value your technical judgment, experiment design instincts, and system-level thinking. Track which companies respond well to your background -- those are the ones where you'll thrive, not the ones where you have to over-explain why an engineer belongs in product."

### Step 2f: Career Returner Context Check

Before analyzing bottlenecks, check `career-plan.md` for a career gap (gap_years > 0, or explicit mention of career break/return). If the user is a career returner, adjust the analysis framework:

- **Returner benchmarks:** Career returners should target lower application volume with higher quality per application. Benchmarks shift to: 3-5 applications per week (not 10-15), each with a referral path. Application cycle is longer because each application requires more positioning work. Do NOT flag 3-4 apps/week as low volume for returners -- flag only if below 2/week.
- **Longer expected timeline: 12-20 weeks.** Career returner searches take longer than standard searches due to gap bias, network dormancy, and the need to rebuild professional visibility. Do not alarm the user at week 8. Adjust motivation accordingly: "Week [N] of your search. Career returner searches average 12-20 weeks. Your pipeline is [healthy/building/needs attention]."
- **Track returner-specific wins:** In addition to standard metrics, track and celebrate: informational interviews completed (these rebuild confidence and market knowledge), network re-engagement rate (what % of dormant connections responded to re-engagement messages), during-gap skills validated (certifications completed, advisory projects referenced in applications), and return-to-work programs applied to.
- **Gap bias detection:** If the user is getting interviews but not advancing past the phone screen, flag potential "gap bias" and recommend adjusting how they present the gap story: "You've had [N] phone screens this week but none advanced. If the gap is coming up in phone screens, your gap answer may need tightening. Run `/mock-interview behavioral` and practice the gap question. Target: under 45 seconds, forward-looking, no over-justification."
- **Confidence tracking -- "self-selecting down" detection:** Add a "confidence signal" check. Are they applying to roles at their pre-gap level, or self-selecting into lower roles? If career-plan.md shows they were a Senior PM pre-gap but they are only applying to PM roles, flag it: "CONFIDENCE CHECK: Your pre-gap title was Senior PM, but [N] of [M] applications this week are for PM-level roles. If you're deliberately targeting PM for re-entry, that's a valid strategy. But if you're self-selecting down because of the gap, reconsider -- your pre-gap scope qualifies you for Senior PM. The gap doesn't erase the skills."
- **Motivation for returners must acknowledge the unique challenge.** "Week [N]. Returner searches take patience -- you're rebuilding visibility while also applying. Your [specific metric: e.g., 'network re-engagement rate of 60%'] shows your former colleagues remember your work. That's the strongest signal in a returner search."

### Step 2g: Multi-Track Analysis

If `career-plan.md` shows the user is running a split strategy across multiple domains or role types (e.g., applying to both fintech PM and general growth PM roles, or targeting both in-domain and out-of-domain companies), segment ALL metrics by track and provide differentiated coaching:

- **Separate funnel tables by track.** If the user applies to 8 fintech roles and 5 general PM roles, show two separate funnel tables. The conversion rates may be dramatically different, and blending them masks the signal.
- **Compare callback rates by track.** "Your in-domain applications have a 22% callback rate. Your out-of-domain applications have a 5% callback rate. This tells you: [interpretation and recommendation]."
- **Differentiated coaching per track.** The bottleneck may be different for each track. In-domain applications may need more volume; out-of-domain applications may need stronger positioning and referrals.
- **Track allocation recommendation.** Based on conversion rates, recommend whether the user should shift effort between tracks: "Your out-of-domain callback rate is 5% vs 22% in-domain. Consider shifting 70% of effort to in-domain applications and reserving out-of-domain for roles where you have a referral AND a work product."

### Step 3: Identify the Bottleneck

Analyze the full pipeline to find the single weakest conversion point. The pipeline stages are:

```
Target companies (100)
  -> Applications submitted
    -> Applications with referrals
      -> Callbacks / screens
        -> First interviews
          -> Second+ interviews
            -> Final rounds
              -> Offers
```

For each transition, calculate the conversion rate. The lowest conversion rate is the bottleneck.

**Stage drop-off analysis (calculate from app-tracker.md History entries):**
For each stage transition, compute:
- Conversion rate: (applications that advanced to next stage) / (applications that entered this stage)
- Average days in stage before advancing
- Average days in stage before rejection/ghosting
- Compare referred vs. cold applications at each stage transition

Present as a funnel table:

| Stage Transition | Total | Advanced | Rejected/Ghosted | Conversion | Avg Days | Referred Conv | Cold Conv |
|-----------------|-------|----------|-------------------|------------|----------|---------------|-----------|
| Applied -> Screen | [N] | [N] | [N] | [%] | [N] | [%] | [%] |
| Screen -> Interview | [N] | [N] | [N] | [%] | [N] | [%] | [%] |
| Interview -> Onsite | [N] | [N] | [N] | [%] | [N] | [%] | [%] |
| Onsite -> Offer | [N] | [N] | [N] | [%] | [N] | [%] | [%] |

The stage with the lowest conversion rate is the primary bottleneck. If two stages have similar conversion rates, prioritize the earlier stage (fixing top-of-funnel has higher total impact).

**Common bottleneck diagnoses:**

1. **Low application volume (under 5/week):**
   - Root cause: Not enough target roles found, or perfectionism slowing applications
   - Prescription: Lower the fit score threshold to 65. Apply to more "stretch" roles with referrals. Set a daily application target of 2.

2. **Low referral rate (under 40% of applications have referrals):**
   - Root cause: Applying before building network, or not asking for referrals aggressively enough
   - Prescription: Do NOT submit any application without first checking connection-tracker for a referral path. If no connection exists, spend 2-3 days building one before applying. The 48-hour delay is worth the 5x callback improvement.

3. **Low callback rate despite referrals (under 10% with referrals):**
   - Root cause: Resume mismatch, weak referral (ATS only, no HM ping), or targeting roles that are a poor fit
   - Prescription: Review keyword coverage scores. Are they consistently below 80%? Run /linkedin-audit. Push for strong referrals (HM pings), not just ATS submissions. Check fit score distribution -- are you applying to sub-70 roles?

4. **Callbacks but no interviews converting to next rounds:**
   - Root cause: Interview performance issues
   - Prescription: Check interview-history.md scores. Run /mock-interview targeting weak question types. Review the weakness heatmap. Consider running more mock sessions before real interviews.

5. **Strong pipeline but no offers:**
   - Root cause: Final round performance or compensation misalignment
   - Prescription: Review final round debrief scores. Check if compensation expectations from qa-master.md are aligned with the roles you're reaching. Run /negotiate prep before final rounds.

6. **Everything looks healthy:**
   - Diagnosis: The system is working. Job searches take time. Keep running the process.
   - Prescription: Optimize the highest-leverage activity based on current pipeline state.

### Step 4: Week-over-Week Trends

Compare this week to last week (and to the week before, if available):

- Applications: [N] vs [N] last week (up/down X%)
- Referral rate: [X]% vs [X]% last week
- Interview scores: [X]/10 avg vs [X]/10 last week
- Callback rate: [X]% vs [X]% last week

Flag any metric that changed by more than 20% in either direction with an explanation hypothesis.

### Step 5: Generate Coaching Recommendations

Based on the bottleneck analysis, provide 3 specific, actionable recommendations for next week. Each must include:
- What to do differently (specific behavior change)
- Why it matters (connected to a specific metric)
- How to measure if it worked (what number to check next Friday)

These should NOT be generic advice. They must reference the user's actual data.

**Bad example:** "Network more."
**Good example:** "You applied to 8 roles this week but only 2 had referrals (25%). Your callback rate on referred applications is 18% vs 2% on cold. Next week, before submitting ANY application, check connection-tracker for a referral path. If none exists, send connection requests first and delay the application by 2-3 days. Target: 60% referral rate next week."

### Step 6: Motivation (Data-Driven, Not Generic)

Write 2-3 sentences of encouragement grounded in the user's actual numbers. Reference specific improvements, milestones, or positive signals.

**Never use:**
- "Keep going, you've got this!"
- "The right opportunity is out there!"
- "Stay positive!"
- Any motivational platitude not backed by data

**Instead, use patterns like:**
- "Your interview scores improved from 5.8 to 7.1 avg over the last 3 weeks. The mock interview practice is clearly working. You're approaching the 7.5+ range where interviewers start writing 'strong hire.'"
- "You built 12 new connections at target companies this week. That's 12 potential referral paths that didn't exist last Monday. Three of those are at companies with active roles -- follow up this week."
- "Week 6. The first 4-6 weeks are the hardest because you're building the machine while also running it. Your referral network is now 34 people across 18 companies. That network compounds. Every week it gets easier."
- "You got rejected from [Company] but your interview score was 7.8/10 -- above the typical hire bar. Sometimes it's a headcount or internal candidate issue, not you. The prep you did transfers to the next interview."

## Output Format

```markdown
# Weekly Retro - Week of [Start Date]

## Your Numbers

| Metric | This Week | Last Week | Benchmark | Status |
|---|---|---|---|---|
| Applications sent | [N] | [N] | 10-15 | [emoji-free status] |
| Avg fit score | [N] | [N] | 70+ | |
| With referrals | [N] ([%]) | [N] ([%]) | 60%+ | |
| Strong referrals (HM ping) | [N] | [N] | 25%+ of referrals | |
| Interviews completed | [N] | [N] | 2-4/week | |
| Avg interview score | [X]/10 | [X]/10 | 7+ | |
| Connection requests sent | [N] | [N] | 125/week | |
| Offers | [N] | [N] | -- | |

## Callback Rate: [X]%

Benchmark: 10-15% for targeted applications with referrals.
[Above/At/Below] benchmark.

Breakdown:
- With referral: [X]% callback rate ([N] callbacks / [N] applications)
- Cold (no referral): [X]% callback rate ([N] callbacks / [N] applications)

[1-2 sentence interpretation. E.g., "Your referred applications are converting at 20%, well above benchmark. But 65% of your applications are still cold. Shifting even 20% more applications to referred would likely add 1-2 more callbacks per week."]

## Fit Score Distribution

| Band | Count | % of Total | Notes |
|---|---|---|---|
| 80-100 (strong match) | [N] | [%] | [are these converting?] |
| 70-79 (good match) | [N] | [%] | [most of your apps should be here] |
| 60-69 (stretch) | [N] | [%] | [only worth it with referral] |
| Below 60 (poor fit) | [N] | [%] | [these should be zero] |

[1 sentence on targeting quality]

## Your Bottleneck This Week

**[Bottleneck name in bold]**

[3-5 sentence analysis. Reference specific numbers. Explain why this is the bottleneck and what the downstream impact is. E.g., "You applied to 12 roles this week but only 2 had referrals (17%). Your callback rate on referred applications is 22% vs 3% on cold -- a 7x difference. Those 10 cold applications have an expected callback of 0.3 interviews. The same effort spent building referral paths first would yield an expected 2.2 interviews. Your bottleneck is not application volume; it's referral coverage."]

## Coaching Recommendations

### 1. [Specific action]
**Why:** [Connected to a metric]
**How to measure:** [What to check next Friday]

### 2. [Specific action]
**Why:** [Connected to a metric]
**How to measure:** [What to check next Friday]

### 3. [Specific action]
**Why:** [Connected to a metric]
**How to measure:** [What to check next Friday]

## Interview Performance (if interviews this week)

| Interview | Company | Round | Score | Strongest Law | Weakest Law |
|---|---|---|---|---|---|
| [date] | [company] | [round] | [X/10] | [Law N: X/10] | [Law N: X/10] |

**[FUNCTION-ADAPTIVE]** Track function-specific question types. SWE: system design scores, coding scores, architecture scores (not product sense). Design: portfolio review scores, design challenge scores. Data Science: case study scores, technical scores. CS: CS strategy scores, role-play scores, operations scores.

[1-2 sentence pattern observation if applicable]

## Adjustments for Next Week

- **Targeting:** [Specific adjustment, e.g., "Add 5 more AI-focused companies to target list" or "No change -- targeting looks right"]
- **Networking:** [Specific adjustment, e.g., "Increase connection requests to 30/day for companies with active roles" or "Focus follow-ups on the 8 people who accepted this week"]
- **Interview prep:** [Specific adjustment, e.g., "Run 2 mock interviews focused on 'say no' questions before Thursday's interview" or "No interviews next week -- focus on applications"]
- **Positioning:** [Specific adjustment if resume/profile changes needed, e.g., "Keyword coverage averaging 72% -- review base resume bullets for [skill area]"]

**[FUNCTION-ADAPTIVE]** Recommend function-appropriate drills. SWE: "/mock-interview system-design". Design: "/mock-interview portfolio-review". CS: "/mock-interview cs-strategy". Do NOT recommend PM mock types for non-PM searches.

## Motivation

Week [N] of your search.

[2-3 sentences grounded in actual data. See Step 6 guidelines. Reference specific numbers, improvements, or milestones. No platitudes.]

---

*Next retro: [date]. Run `/weekly-retro` then or schedule it in Cowork.*
```

## Quality Checks

A good weekly retro:
- Every number is calculated from actual data, not estimated
- The bottleneck diagnosis is specific and actionable, not "do more of everything"
- Coaching recommendations reference specific metrics and set measurable targets for next week
- Motivation section references real data points, never generic encouragement
- Week-over-week trends are tracked to show progress (or lack thereof)
- Missing data is acknowledged, not fabricated

A bad weekly retro:
- Vague bottleneck diagnosis ("networking needs work")
- Generic coaching ("apply to more roles")
- Motivational fluff not connected to data
- Missing the callback rate calculation (the most important leading indicator)
- Not comparing referred vs. cold application performance
- Skipping the fit score distribution (which reveals targeting problems)

**Persona-specific checks (verify these when applicable):**

- **Company-type segmentation (failed founder / shut-down company).** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, add a "Company Type Analysis" section to the retro. Track applications by company type: startup (sub-50 employees), scaleup (50-500), enterprise (500+), and agency/consulting. Compare conversion rates across types. If startup conversion is significantly higher than enterprise (or vice versa), flag: "Your callback rate at startups is [X]% vs [Y]% at enterprise companies. This suggests [interpretation: e.g., 'startups value your founder experience while enterprise companies may be filtering on it']. Recommendation: [shift allocation / adjust positioning for enterprise applications / lean into startup-friendly companies]." If the user is only applying to one company type, flag: "All [N] applications this week are to [type]. Consider diversifying -- founder experience plays differently at startups vs enterprise. A mixed pipeline gives you data on where your background converts best."
- **Profile-based bias detection (veteran / 15+ years experience).** If career-plan.md shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, Cisco, Dell, Accenture, Deloitte, etc.), or explicit mention of age-related concerns, add an "Age Bias Signal Check" section. Flag if more than 70% of resume-stage rejections come from companies known for younger workforces (check against company-research data or target-companies.md notes). Track rejection patterns by company type and stage: are rejections clustering at the resume screen (before any human interaction) or at the interview stage? Resume-stage clustering suggests profile-based filtering; interview-stage clustering suggests performance issues. If resume-stage rejections exceed 80%, recommend: "Your rejection rate at the resume stage is [X]%. This may indicate profile-based filtering. Actions: (1) Run `/resume-tailor` with veteran compression rules -- ensure graduation years are removed, early career is compressed, and skills section leads with current tech. (2) Run `/linkedin-audit` for age-signal review. (3) Consider mixing application targets -- include 2-3 companies per week known to value experienced hires (companies with 'seasoned leadership' or 'diverse experience' signals in their JDs)."

## Example: Bottleneck Diagnosis in Action

```
## Your Bottleneck This Week

**Referral Coverage**

You submitted 11 applications this week. Only 3 had referrals (27%).
Your callback rate tells the story:
- With referral: 2 callbacks out of 3 applications (67%)
- Cold: 0 callbacks out of 8 applications (0%)

You're effectively wasting 73% of your application effort. Each cold
application takes ~30 minutes (tailoring + submitting). That's 4 hours
this week with a near-zero expected return.

If you had spent those 4 hours building referral paths for 4-5 of
those roles instead, your expected callback count would roughly double
based on your referral callback rate.

Next week: do not submit a single application without a referral path.
If no connection exists, spend the time building one first. The 2-3 day
delay is worth the 7x improvement in callback rate.
```

## Remote Strategy Analysis

If `career-plan.md` shows a remote-only preference, add a "Remote Strategy Analysis" section to the retro:

- **Segment conversion rates by remote policy type:** remote-first vs. remote-friendly vs. hybrid. Pull the remote-policy field from each application in app-tracker.md. Display: "Remote-first: [N] apps ([X]% callback). Remote-friendly: [N] apps ([X]% callback). Hybrid: [N] apps ([X]% callback)."
- **If conversion rate at remote-first companies is significantly higher** (2x or more vs. remote-friendly/hybrid): flag as evidence to focus targeting there. "Your remote-first callback rate is [X]% vs [Y]% at remote-friendly companies. Remote-first companies are converting [Z]x better -- consider concentrating your applications there."
- **Track "remote conversation performance"** from interview-debrief data -- are remote discussions going better or worse over time? If interview-history.md logs remote-related questions and scores, compare this week's remote question scores to the prior 2-week average. "Remote question performance: [X/10] this week vs [Y/10] prior 2-week average. [Improving/Declining/Stable]."
- **Flag misaligned applications:** If the user applied to any non-remote-first companies this week when career-plan says remote-only, flag: "WARNING: You applied to [N] non-remote-first companies this week ([company names]) despite a remote-only preference. Your conversion data shows remote-first companies convert [X]x better. Recommend stopping hybrid/onsite applications unless you have a strong referral AND the company has a track record of exceptions."
- **Virtual networking effectiveness:** Track which online communities are generating the most connections. "This week's networking sources: [Community A]: [N] new connections. [Community B]: [N] new connections. [LinkedIn cold outreach]: [N] new connections." Flag the highest-performing source.
- **Recommend adjustments:** If remote-first conversion is 3x hybrid, recommend stopping hybrid applications entirely: "Your data is clear: remote-first companies convert at [X]% vs [Y]% for hybrid. Recommendation: stop applying to hybrid/onsite roles and reallocate that effort to remote-first pipeline building and networking in remote-friendly communities."

## Military-to-PM Dual-Track Analysis

If `career-plan.md` shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), add these sections to the weekly retro:

### Defense Tech vs. General Tech Dual-Track Analysis
If the user is pursuing BOTH defense tech and general tech tracks, analyze conversion rates separately in the retro:
- **Separate funnel tables by track.** Show defense tech applications and general tech applications as two distinct funnels. The conversion rates will likely be dramatically different -- defense tech roles should convert significantly better for military candidates due to clearance value and mission understanding.
- **Track allocation recommendation.** If defense tech is converting at 2x+ the rate of general tech, recommend focusing there: "Your defense tech callback rate is [X]% vs [Y]% for general tech. Consider shifting [percentage] of effort to defense tech applications where your military background is a direct asset, not a translation challenge."
- **If general tech is NOT converting:** Diagnose whether the issue is jargon translation (resume/cover letter still reads too military), positioning (summary leads with military identity instead of PM skills), or targeting (applying to roles where military experience is irrelevant).

### Jargon Improvement Tracking
If `interview-history.md` has logged military jargon flags from mock interviews or real interview debriefs:
- Track the jargon flag count week over week. Are military jargon flags decreasing over time?
- If the count is stable or increasing: "JARGON ALERT: Military jargon flags have not decreased over the last [N] weeks ([count] flags this week vs [count] last week). This suggests the translation is not becoming automatic yet. Recommendation: run `/mock-interview behavioral` with 5 questions this week, focusing specifically on telling military stories in civilian language. Practice until zero jargon flags in a full mock session."
- If the count is decreasing: "Jargon improvement: [N] military jargon flags this week vs [M] last week. The translation practice is working. Keep drilling -- the goal is zero flags in general tech interviews."
