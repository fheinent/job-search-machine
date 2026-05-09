---
name: negotiate
description: Analyze a job offer, identify leverage, draft counter-offer language, and prep for the negotiation call.
---

# /negotiate - Offer Analysis & Counter-Offer Strategy

## When to Use

Run this skill when you receive a job offer and need to decide whether to accept, counter, or walk away. Provide the offer details and get a full analysis: market comparison, leverage identification, counter-offer strategy with specific dollar amounts, draft language for email and verbal delivery, and a call prep guide with BATNA.

**Trigger:** `/negotiate [offer details OR offer letter file path]`

Examples:
- `/negotiate base 180k equity 200k/4yr bonus 15% sign-on 25k at Stripe L5 PM`
- `/negotiate ~/Documents/offers/anthropic-offer-letter.pdf`
- `/negotiate` (then paste or describe the offer)

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

**Required:**
- Offer details: base salary, equity (grant value and vesting schedule), bonus (target %), sign-on bonus, level/title, and any other compensation components

**Optional:**
- Offer letter file (PDF or text -- will be parsed automatically)
- Competing offers (if not already in app-tracker)
- Specific concerns about the offer (e.g., "Equity seems low," "Title is a downlevel")
- Timeline/deadline for responding

**Auto-read (do not ask the user for these -- read them directly):**
- `context-library/career-plan.md` -- dream offer, comp target, walkaway number, what would make you say no
- `context-library/qa-master.md` -- compensation expectations, data sources, scripts for comp discussions
- `context-library/experience-library.md` -- unique value proposition for justifying above-band comp
- `context-library/target-companies.md` -- context on the company
- `insider-data/company-intel/[company].md` -- comp data, negotiation flexibility intel (if exists)
- App-tracker data (if exists) -- competing offers and active processes for leverage

## Process

### Step 1: Parse the Offer
Break the offer into components:
- **Base salary:** $X
- **Equity:** $X total grant / vesting schedule (e.g., 4-year with 1-year cliff) / equity type (RSU, ISO, NSO) / current stock price or last valuation
- **Bonus:** X% target / guaranteed first year or not
- **Sign-on bonus:** $X / clawback terms
- **Level/Title:** [level] / how this maps to industry standard levels
- **Other:** relocation, benefits, PTO, 401k match, learning budget, etc.

**[FUNCTION-ADAPTIVE]** Function-specific comp components. CS/Sales: base + variable comp (tied to NRR/retention metrics with quota mechanics) + equity + sign-on. SWE: base + RSU/equity + sign-on + bonus (plus negotiate for: on-call expectations, conference budget, open-source time). Design: standard comp + negotiate for design tool budget, conference attendance. The priority order varies by function. CS: base > variable comp terms > equity > sign-on > team headcount. SWE: base > equity > sign-on > bonus > scope/title.

Calculate:
- **Total Year 1 comp:** base + first-year equity + bonus + sign-on
- **Total annual comp (steady state):** base + annual equity vesting + bonus (no sign-on)
- **Total 4-year comp:** sum of all components over 4 years

### Step 1b: Comp Data Staleness Check
If the user references compensation data from company-intel files (e.g., `insider-data/company-intel/[company].md`) without having run `/salary-research` for this specific company recently, prompt: "The comp ranges in the intel file may be outdated. I recommend running `/salary-research` first for current market data before building your counter-offer. Comp bands shift quarterly at many companies, and negotiating with stale data can lead to anchoring too low or making an unrealistic ask. Proceed anyway, or run /salary-research first?"

If the user chooses to proceed without running /salary-research, note in the output under Market Comparison: "Warning: comp data sourced from company-intel file, which may not reflect current market rates. Verify ranges before the negotiation call."

### Step 2: Market Research
Search for current market data:
- `levels.fyi [company] [level] [role] total compensation`
- `levels.fyi [company] product manager [location]`
- `Glassdoor [company] [role] salary [location]`
- `Blind [company] [level] offer [current year]`
- Check `insider-data/company-intel/[company].md` for any comp data or negotiation intel

Extract:
- Market range (P25, P50, P75) for this company/level/role/location
- How this offer compares (percentile)
- Whether this company is known for negotiation flexibility or rigidity
- Typical counter-offer outcomes at this company (from Blind/Glassdoor reports)

For equity at pre-IPO companies:
- Note the risk: equity value is not guaranteed
- Check for recent funding round, valuation, and revenue trajectory if available
- Apply appropriate discount to paper equity value

### Step 3: Compare Against Your Targets
From `career-plan.md`:
- How does this offer compare to your dream offer target?
- How does it compare to your walkaway number?
- Does the role/scope/title match what you wanted?
- Are there non-comp factors that matter (from "what would make you say no")?
- **Accommodations:** If the user needs workplace accommodations (flexible schedule, equipment, remote days for health reasons), these are negotiable post-offer items. Frame as setup needs, not limitations: "To do my best work, I'd appreciate [specific accommodation]. Is that something we can include?" Get accommodations confirmed in writing (offer letter addendum or email confirmation). *This is strategic career coaching, not legal advice. Consult an employment attorney for your specific situation.*

From `qa-master.md`:
- What range did you communicate during the process?
- Is the offer within, above, or below what you signaled?

**Pay-Cut Scenario Detection:**
- Compare the user's CURRENT total comp (from career-plan.md or experience-library.md) against the offer AND the target range.
- If the user's current comp is HIGHER than the offer or the target range, this is a pay-cut scenario. This changes the negotiation strategy fundamentally:
  - The user is NOT negotiating from a position of "I need more money to move." Instead, they are signaling "I am willing to take less for the right opportunity."
  - Do NOT anchor to current comp -- it will scare the company or make the user seem overqualified/flight-risk.
  - Do NOT reveal current comp unless legally required. If asked, redirect: "I'm focused on what's fair for this role at [company]. My research shows [market range]."
  - The walkaway number may be BELOW current comp. This is valid. Acknowledge it: "You are currently at $[X] and willing to go to $[Y], which is a $[delta] cut. Make sure this is a deliberate choice, not a concession made under pressure."
  - Negotiate for non-comp factors more aggressively: title/level (for long-term comp trajectory), equity upside (especially at pre-IPO companies where growth potential compensates for current cash cut), scope/team size, learning opportunities, sign-on bonus to soften the transition.
  - Frame the negotiation as "I want to be at the top of the band for this level" rather than "I need to match my current comp." The latter signals you are not committed to the move.

**Career Changer Counter-Offer Framing:**
If `career-plan.md` indicates the user is a career changer (no PM title, transitioning from consulting/engineering/other field), the counter-offer language requires specific adjustments:
- **Do NOT lead with "I'm willing to take less."** Even if the user is taking a pay cut from their previous career, the counter should be framed around market value for the role, not as a concession. "I'm targeting top-of-band for this level based on levels.fyi data" -- not "I know I'm a career changer so I'm flexible."
- **Leverage the unique value proposition.** Career changers bring skills that pure-PM candidates often lack: consulting analytical rigor, engineering technical depth, domain expertise. The counter must articulate this: "My McKinsey fintech experience means I'll ramp on payments domain knowledge in weeks, not months. That's worth positioning me at P60-P75 in the band."
- **Sign-on bonus as transition bridge.** If the user is taking a base-salary cut from their previous career, push harder on sign-on bonus. Frame: "A sign-on of $[X] would help bridge the transition from my current comp structure to [Company]'s. It's a one-time cost that makes the move work for me."
- **Title/level negotiation matters MORE for career changers.** A career changer hired at PM level who should be at Senior PM is harder to promote (they lack the "PM years" even after performing well). Push for the right level at entry: "Given my total years of product-adjacent work, I believe [Senior PM / PM-II] is the right level. This aligns with where I'd contribute from day one."
- **If the offer is between walkaway and target:** This is the most common scenario for career changers. The offer is likely reasonable for the level but below what they earned in their previous career. The counter should focus on: (a) pushing base to top-of-band (5-10% increase), (b) sign-on to bridge the gap, (c) equity or equity refresh timeline, (d) written agreement on 6-month performance review with path to level adjustment.

### Step 4: Identify Leverage Points
Enumerate every piece of leverage you have:

1. **Below market:** If the offer is below P50 for the company/level, this is leverage. Quantify: "Your offer is at P30. The median for [level] at [company] is $X higher."
2. **Competing offers:** Check app-tracker for other active offers or late-stage processes. Even processes without offers yet create time pressure leverage.
3. **Unique value:** From `experience-library.md`, identify what you bring that most candidates at this level do not. Specific domain expertise, rare technical + product combination, relevant industry experience, etc.
4. **Their hiring urgency:** From company-intel or target-companies, assess their hiring velocity. High hiring velocity = more leverage (they need to fill the role).
5. **Internal equity mismatch:** If the level seems low for your experience, this is leverage for a level bump (which often unlocks a higher band).
6. **Timing:** If you have a deadline from another company, this creates urgency for them.

Also identify what you do NOT have leverage on:
- If the offer is at or above market, acknowledge it
- If you communicated a lower range earlier, note this constraint
- If you have no competing offers, do not fabricate leverage

**Visa sponsorship leverage constraints:** If the user needs visa sponsorship (check `career-plan.md` and `qa-master.md`):
- The candidate pool is smaller for visa-sponsoring roles, giving the user some leverage (the company chose to sponsor, meaning they value international talent). But the user also has fewer alternatives (many companies do not sponsor), which limits walkaway power.
- Do NOT push for aggressive counters if the user has no competing offers AND needs sponsorship. The risk of offer rescission is higher when the negotiation feels adversarial for a candidate who "needs" the company for visa reasons.
- Frame negotiation as collaborative: "I want to make this work. Here's what would help me commit with full confidence." NOT "I have other options" (unless genuinely true).
- Focus leverage on market data and unique value, not competing offers (unless they genuinely exist).
- Note: companies that sponsor H-1B have established comp bands that apply equally to visa and non-visa candidates. Visa status should not reduce comp. If it does, that is a red flag worth flagging to the user.

**International relocation cost factor:** If the user is relocating internationally (check `qa-master.md` and `career-plan.md`):
- Standard international relocation costs: $15K-$40K (shipping, temporary housing, flights, deposits, visa legal fees).
- If the offer includes a relocation package, evaluate whether it covers actual costs. Many packages are $5K-$15K, which is inadequate for international moves.
- If the package is insufficient, flag it as a negotiation point: "The relocation package covers about [X]% of estimated international move costs. Could we discuss increasing it to $[Y], or adding a sign-on bonus to bridge the gap?"
- Factor relocation costs into Year 1 comp: "Total Y1 comp after estimated relocation costs: $[offer Y1] - $[relocation gap] = $[adjusted Y1]."
- For moves from lower cost-of-living markets to SF/NYC, note the purchasing power difference so the user has a realistic view of the net financial impact.

**Single-offer / no-leverage scenario handling:**
When the user has only one offer AND no late-stage processes creating time pressure, the negotiation strategy changes fundamentally:

1. **Do NOT bluff about competing offers.** Recruiters talk to each other. Getting caught in a bluff destroys trust and can result in a rescinded offer. Never suggest or imply the user should fabricate leverage.
2. **Leverage sources when you have no other offers:**
   - **Market data:** "My research shows P50 for this role is $X. I'd love to be positioned at P50-P60 given [specific experience]." Market data is leverage that does not require competing offers.
   - **Current employment (if employed):** "I'm happy in my current role, so I want to make sure the move makes sense financially." This signals you have a walkaway option even without another offer.
   - **Unique value:** "My experience with [specific domain/skill] is directly relevant to [company's stated priority]. That specialization typically commands [data point]."
   - **Time:** "I'm early in my search and expect to have other conversations in the coming weeks." This is honest if true and creates soft urgency without fabricating offers.
3. **Adjust the anchoring ask:** With strong leverage (multiple offers), anchor 15-20% above target. With limited leverage (single offer, no alternatives), anchor 5-10% above target. The ask must be defensible with data alone.
4. **Emphasize non-comp negotiation:** With limited comp leverage, push harder on title/level, scope, start date, sign-on bonus (often easier to get), remote flexibility, learning budget, or equity refresh timeline. These items often have more flexibility than base salary.
5. **Tone shift:** With competing offers, the tone is "help me choose you." Without competing offers, the tone is "help me say yes enthusiastically." The second framing is collaborative, not adversarial, and works well even without leverage.
6. **Set realistic expectations:** Note in the output: "With limited external leverage, expect 5-10% movement on the initial offer. Focus negotiation energy on the components with the most flexibility at this company. The goal is to get to the top of the band, not to create a bidding war."

**Prior Comp Anchor Recovery:**
If `interview-history.md` or the user's notes indicate they communicated an anchoring number earlier in the process (recruiter screen, HR chat) that was too high, too low, or revealed current comp they should not have, generate a "Comp Anchor Recovery" section:
- **Anchored too high (e.g., said $400K when range is $300-380K):** The company may have already mentally filtered the user as "too expensive." Recovery script: "I've done more research since our initial conversation and I have a better understanding of the range for this level. I'm focused on the role and team -- I'm confident we can find a number that works. My target is [revised number backed by market data]." This resets the anchor without seeming inconsistent.
- **Anchored too low (e.g., said $250K when they could have gotten $320K):** The company will try to close at or near the stated number. Recovery is harder. Strategy: "Since we last discussed comp, I've received additional market data [cite levels.fyi, salary-research output]. Given the scope of this role, I'd like to discuss positioning closer to [higher number]." Be prepared for pushback -- the company may cite the earlier number. Have a response ready: "I appreciate that I mentioned a different range earlier. My research since then has given me a clearer picture of what's competitive for this level."
- **Revealed current comp when they should not have:** This limits upside if current comp is low, or creates flight-risk perception if high. If current comp was revealed and is LOW: emphasize market rate, not history. "My comp reflected [reason: different market, career change, early-stage equity gamble]. The market rate for this role is [data]." If current comp was revealed and is HIGH: defuse the flight-risk signal. "I'm targeting this level because [genuine reason]. I'm not chasing my previous comp number -- I'm optimizing for [role fit / growth / product area]."

**Manager-to-IC Transition Level Negotiation:**
If `career-plan.md` indicates the user is transitioning from a management track to an IC track at the same or similar level (e.g., Senior PM who managed a team now targeting Senior IC PM):
- **Title/level becomes the #1 negotiation priority, above base salary.** A manager-to-IC candidate hired one level below their management seniority (e.g., PM instead of Senior PM) faces a compounding disadvantage: they lack "IC years at level" to justify promotion, even though their total experience warrants the higher level. Push for the correct IC level at entry.
- **Frame management experience as IC leverage:** "My management experience means I bring stakeholder alignment, hiring judgment, and cross-functional influence on day one -- skills most IC PMs at this level are still developing. That experience warrants Senior-level positioning."
- **If the company offers a lower IC level:** Counter with a written agreement on an accelerated review timeline (3-6 months) with explicit criteria for level adjustment. "If leveling is the concern, I'm happy to prove it -- could we agree on a 6-month review with clear Senior PM criteria?"

**EARLY-CAREER LEVEL-UP NEGOTIATION:** If `career-plan.md` shows the user's target title is above their current title (e.g., APM targeting PM, PM targeting Senior PM) AND total experience is under 3 years, title/level becomes the #1 negotiation priority. Apply these adjustments:
- **Priority reorder:** title/level > base > equity > sign-on > bonus. Getting the right level at entry is more valuable than a 5% base bump, because level determines comp band ceiling, promotion timeline, and peer calibration for the next 2-3 years.
- **Frame scope as evidence for level:** "My output over the past 18 months -- [specific metric] -- maps to the scope expectations of a [target level]. I'd like to discuss entering at [target level], which aligns with where I'll contribute from day one."
- **If the company offers a lower title:** Counter with scope evidence. Pull 2-3 metrics from experience-library.md that demonstrate impact at the target level, not the offered level. "The scope of my work -- owning a product with [X] users, running [Y] experiments, driving [Z] revenue impact -- is consistent with [target level] scope at [Company] based on levels.fyi benchmarks."
- **If the company insists on the lower level:** Request an accelerated performance review with explicit promotion criteria. "I understand the leveling concern. Could we agree on a 6-month review with clear [target level] criteria? That gives both sides confidence -- I get a path to the right level, and you get proof before committing." Also push for top-of-band comp at the offered level plus a sign-on bonus to bridge the gap.
- **Never accept a lower title passively.** Even if the base salary is acceptable, entering at the wrong level creates a compounding disadvantage. Every year at the wrong level is a year where promotion requires proving you deserve the level you should have started at.

**EXECUTIVE NEGOTIATION POSTURE:** If `career-plan.md` shows VP/Director/CPO/SVP level AND 12+ years experience, apply these adjustments to the negotiation strategy:
- Executives negotiate a fundamentally different package than ICs. The priority order shifts to: equity structure > reporting line > team headcount/budget > base > sign-on > scope definition
- **Equity structure:** At VP+, negotiate for equity type (RSUs vs. options vs. profits interest), vesting schedule modifications (quarterly vs. cliff, acceleration on termination), and refresh grant commitments. Frame: "At this level, I'm investing my career in [Company]'s success. I want the equity structure to reflect that partnership."
- **Reporting line:** Who the role reports to is a compensation element. Reporting to CEO vs. CTO vs. CRO dramatically affects scope, influence, and future comp trajectory. If the reporting line is ambiguous, clarify before negotiating comp.
- **Team and budget:** Negotiate headcount commitments and budget authority. "I want to confirm: I'll have authority to build a team of [X] with a budget of [$Y] in the first 12 months."
- **Scope protection:** Negotiate explicit scope boundaries in the offer letter or at minimum in a written email: "My responsibility includes [X, Y, Z]. I want to confirm this before accepting."
- **Severance/protection:** At VP+, negotiate severance terms (6-12 months is standard at VP, 12-18 at C-level), acceleration of unvested equity on termination without cause, and garden leave provisions.
- **Tone:** peer-to-peer throughout. Do NOT use "I'd be grateful for" or "I understand this is a lot to ask." Frame as: "Here's what I need to commit fully to this opportunity."

**LEGACY BENEFITS REPLACEMENT NEGOTIATION:** If `career-plan.md` shows the user is leaving a company with 10+ years tenure AND mentions any of: pension, deferred compensation, RSU vesting schedule (golden handcuffs), retiree healthcare, defined benefit plan, or long-term incentive plan (LTIP), apply these adjustments:
- **Calculate true departure cost:** The user is not just comparing offer vs. current comp — they are forfeiting accumulated benefits. Itemize what they lose by leaving: unvested RSUs (remaining vest schedule × current price), pension accrual (years to vesting or to enhanced benefit), deferred comp payouts (timing and tax implications), retiree healthcare (estimated annual value × expected years of use), 401k match forfeiture (if vesting schedule is incomplete), sabbatical eligibility, or any tenure-based perks (extra PTO, stock purchase discount tiers). Present as: "**Departure Cost Analysis:** By leaving [Company] now, you forfeit approximately $[X] in unvested/accumulated benefits over the next [Y] years."
- **Bridge the gap explicitly in the counter:** The departure cost must be reflected in the counter-offer, not absorbed silently. Strategies:
  - **Sign-on bonus as forfeiture offset:** "I'm forfeiting $[X] in unvested RSUs by leaving [Company]. A sign-on of $[Y] would offset this forfeiture and make the transition financially viable." This is standard practice — companies expect to "buy out" unvested comp for senior hires.
  - **Equity front-loading:** Request a front-loaded vesting schedule (e.g., 40/30/20/10 instead of 25/25/25/25) or an accelerated first-year vest to replace the steady income from the legacy employer's vesting schedule.
  - **Guaranteed bonus Year 1:** If the legacy employer pays predictable annual bonuses based on tenure/seniority, request a guaranteed (not target) bonus for Year 1 at the new company to replace the certainty.
- **Pension/defined benefit replacement:** If the user has a pension or defined benefit plan:
  - Calculate the annual pension value they are forfeiting (estimated annual payout × years they would have received it, discounted to present value).
  - Frame the negotiation: "My pension at [Company] vests fully in [X] years and represents approximately $[Y] in lifetime value. I need the equity component of this offer to provide comparable long-term financial security."
  - Push for: larger equity grant, equity acceleration on termination without cause, or a supplemental retirement contribution (some companies offer this for VP+ hires).
- **RSU vesting cliff replacement:** If the user has RSUs about to vest (within 6-12 months), the standard approach is:
  - "I have $[X] in RSUs vesting at [Company] over the next [Y] months. I'd like to discuss a sign-on that accounts for this forfeiture, structured as [lump sum / matching vest schedule]."
  - Some companies will match the vesting schedule (e.g., pay $50K at 3 months, $50K at 6 months) to mirror what the candidate is leaving behind.
- **Healthcare/benefits gap:** For users leaving companies with premium benefits (retiree healthcare, Cadillac health plans, generous parental/family leave they may still use), flag any benefits downgrade: "The benefits package at [new company] has a higher out-of-pocket maximum and no retiree healthcare benefit. This represents approximately $[X]/year in additional cost. Factor this into your total comp comparison."
- **Tone for legacy departure:** The negotiation tone should acknowledge the gravity of leaving a long-tenure position: "I'm making a deliberate decision to leave a stable, well-compensated position for this opportunity. I want the package to reflect that commitment." This is NOT weakness — it signals the candidate is serious, thoughtful, and expects to be treated accordingly.
- **Never let departure cost be invisible.** Many 15+ year veterans accept offers without calculating what they forfeit. The negotiate skill MUST always surface the departure cost analysis when tenure exceeds 10 years, even if the user does not ask for it.

**REMOTE COMP FRAMING:** If `career-plan.md` shows the user has a remote-only preference or caregiver/family constraints, apply these adjustments to the negotiation strategy:
- **Geo-differential detection:** If the offer includes a location-based pay adjustment (geo-differential) or mentions "remote pay band" that is lower than the onsite band, flag it immediately and provide the negotiation strategy: "My output is location-independent. Here's what I delivered: [pull 2-3 top metrics from experience-library.md]. I'd like to discuss comp based on the value I bring rather than my zip code."
- **Remote vs. onsite pay band delta:** If the company has different pay bands for remote vs. onsite employees, identify the delta (search levels.fyi, Blind for "[company] remote pay band" or "location-based pay"). Build the counter-argument: "I notice the remote band is approximately [X]% below the onsite band. Given that my output -- [specific deliverables/metrics] -- is identical regardless of location, I'd like to discuss positioning within the onsite band."
- **Never accept a remote discount passively.** Always flag location-based pay adjustments for negotiation. Many candidates accept geo-differentials without questioning them. The negotiation skill must always surface this as a negotiation point, even if the user does not raise it.
- **Equity refresh considerations for remote roles:** Note that remote roles at some companies have different equity refresh schedules or smaller refresh grants than onsite roles. If the offer seems light on equity vs. market data for the level, flag it: "This equity grant is at P[X] for the level. Some companies apply smaller equity grants to remote roles. Verify whether this reflects a remote adjustment and push for parity if so."
- **PRIVACY GUARDRAIL:** The negotiation language must never reference WHY the user needs remote work. No mention of caregiving, family, health, or personal circumstances. Frame remote as a performance choice: "I do my best work in a distributed environment" -- not as a need or accommodation.

**CAREER RETURNER NEGOTIATION:** If `career-plan.md` shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), apply these adjustments:
- **CRITICAL: Do NOT let the user accept a level-down offer just because of the gap.** If they were a Senior PM before the break, they should negotiate for Senior PM, not PM. The gap does not erase the skills -- it pauses the timeline. Level determines comp band ceiling, promotion timeline, and peer calibration for the next 2-3 years. Accepting the wrong level compounds into a multi-year disadvantage.
- **Counter-argument for gap-based down-leveling:** "My [X] years of pre-break experience included [specific scope: team size, revenue owned, user base]. The skills that drove those results don't atrophy -- here's evidence I've stayed current: [certifications, freelance projects, coursework, advisory roles from experience-library.md]. I'd like to discuss entering at [pre-gap level], which aligns with where I'll contribute from day one."
- **Return-to-work / returnship program offers:** If the offer comes through a returnship program (Path Forward, iRelaunch, company-specific), note that these often convert at a lower level than the candidate's pre-gap seniority. Negotiate the conversion level upfront: "I'd like to discuss the expected conversion level now rather than leaving it ambiguous. Based on my pre-break scope, I'd expect to convert at [level]. Could we agree on the criteria and timeline for that conversion?"
- **Gap-based comp discounting:** Flag if the comp offer is significantly below the user's pre-gap comp (adjusted for market changes since the gap). Compare the offer against CURRENT market rates at the offered level, not the user's pre-gap comp. If the offer is below current market P50 for the level, it may indicate gap-based discounting: "This offer is at P[X] for [level]. Market data shows P50 at $[Y]. I'd like to discuss positioning at P50, which reflects the current market for this level regardless of my career timeline."
- **Sign-on as gap bridge:** If there is a comp gap between the pre-gap trajectory and the current offer, push for a sign-on bonus to bridge the transition: "A sign-on of $[X] would help bridge the transition back to a full-time role. It's a one-time cost that makes this move work for me."

**INDUSTRY-ANOMALY COMP CONCEALMENT:** If `career-plan.md` shows the user is transitioning from a company or industry where compensation is structurally below market (not due to underperformance) — examples: Epic Systems (private company, no equity, Midwest-anchored), government/military, academia, non-profits, pre-revenue startups with below-market cash — AND the user's current comp is 30%+ below the target range for comparable roles at market-rate companies, apply these adjustments:
- **CRITICAL: Never reveal current comp.** The gap is large enough that disclosure undermines credibility. If asked directly: "I'm focused on what's competitive for this level at [Company]. My research shows the range is $[X]-$[Y] based on levels.fyi and Glassdoor data."
- **If current comp was already disclosed:** Immediately reframe: "My comp at [Company] reflects their unique structure — [Company] is [private with no equity / Midwest-headquartered / non-profit] and compensates differently than the broader market. The market rate for this role is $[X]-$[Y], and that's the benchmark I'm using."
- **Pre-disclosure prep script:** Before any recruiter call, generate a rehearsed deflection: "If asked about current comp: 'I'd prefer to focus on the market rate for this role. My research shows $[range]. What does your band look like for this level?' If they push: 'My current employer has a non-standard comp model that doesn't translate well to market benchmarks. I'm targeting $[target] based on my scope and market data.'"
- **Counter-offer anchoring:** Anchor to market rate for the target company/level, never to current comp. Even if the counter represents a 40-70% increase over current comp, frame it as "targeting P50-P60 for this level" — which is a legitimate, data-backed ask. The size of the increase is irrelevant; what matters is where the ask falls in the company's band.
- **Avoid over-gratitude tone:** Candidates making large comp jumps often unconsciously signal "I can't believe you're offering this much" through deferential language. The skill must use the same confident, data-backed tone regardless of the delta between current and offered comp. Never write "I really appreciate this generous offer" — write "Thank you for the offer. I'd like to discuss a few components."
- **Salary history ban law integration:** Check the target role's location against salary history ban jurisdictions. States with bans include: California, New York, Colorado, Washington, Illinois, Connecticut, Delaware, Hawaii, Maine, Maryland, Massachusetts, Nevada, New Jersey, Oregon, Rhode Island, Vermont, plus many major cities (NYC, Philadelphia, Chicago, Cincinnati, Pittsburgh, etc.). If the role is in a ban jurisdiction AND the recruiter or application asks for current or prior salary, arm the user with the legal backstop: "That information is protected under [State]'s salary history law. I'd prefer to focus on the market rate for this role — my research shows $[range]." This is the user's strongest shield and should be layered on TOP of the deflection scripts above. If the role is in a non-ban jurisdiction, note: "This state does not have a salary history ban. Use the deflection scripts above, but be aware the company CAN legally ask. The scripts are designed to redirect without refusing."
- **Post-verification disclosure contingency:** Some companies run employment verification (via background check or reference check) that may surface prior compensation. If this occurs after an offer is made, prepare the user: "If the background check reveals your prior comp, here is the script: 'As I mentioned, my prior employer has a non-standard comp model — [private company/no equity/Midwest-anchored]. That comp reflected their structure, not my market value. The offer we discussed is aligned with market data for this level, which is the right benchmark.' Do not apologize for the gap or volunteer further explanation. The offer was made based on your qualifications and the market — your prior comp is irrelevant to the value you bring."
- **No-equity-to-equity transition support:** If the candidate is coming from a no-equity employer (like Epic, government, academia, or bootstrapped startups), add an equity education primer to the negotiation prep: briefly explain RSU vs. ISO vs. NSO, vesting schedules (standard 4-year with 1-year cliff), refresh grant cadences (annual at public companies), and how to value private company equity (apply 50-75% discount to paper value unless company is late-stage with clear IPO/acquisition timeline). This is not condescension — it is closing a structural knowledge gap created by the prior employer's comp model, and ensures the candidate negotiates equity effectively rather than defaulting to "I'll just focus on base."
- **Zero-equity employer negotiation angle:** Since there is no forfeited equity to buy out, reframe the sign-on request as "transition investment" rather than "forfeiture offset." Request more equity in the package since there is no equity-vesting pattern to replace. Candidates from zero-equity employers may have unusually strong liquid savings -- consider requesting equity-heavy packages with lower base if the company's equity is compelling.

**[FUNCTION-ADAPTIVE] Variable Comp Terms (CS/Sales):** If the role has OTE/variable comp, negotiate: guaranteed variable for first quarter during ramp, attainment curve details, accelerator thresholds above 100%, measurement period alignment, and what happens to variable comp when you inherit accounts mid-cycle.

**[FUNCTION-ADAPTIVE] Function-Specific Negotiation Guidance:**

**Marketing-Specific Negotiation:**
- **Comp structure:** Base + performance bonus (typically 15-30% at Director+) + equity + sign-on. Marketing bonus is often tied to pipeline/MQL targets, not company-wide performance.
- **Priority order:** base > bonus structure (tied to controllable metrics) > equity > sign-on > team headcount
- **Key negotiation levers:** marketing budget authority (larger budget = more impact = higher future comp), team headcount, conference/event budget, agency relationships
- **Watch for:** bonus tied to revenue targets the marketer doesn't control (e.g., sales closing rate). Push for bonus tied to marketing-controlled metrics (MQLs, pipeline, brand awareness).
- **Sub-function comp differential:** Growth/performance marketing Directors at PLG companies typically earn 10-20% above brand marketing Directors at the same level. When anchoring comp expectations, identify whether the role is growth/demand-gen/performance marketing vs. brand/comms/content marketing and anchor to the correct sub-function benchmark. If the offer blends both, anchor to the higher-paying sub-function: "This role owns both brand and demand generation. Demand-gen Directors at PLG companies at this level benchmark 10-20% higher than pure brand roles -- I'd like to anchor to that range given the full scope."
- **Marketing-specific scope negotiation:** Beyond comp, negotiate scope levers that determine future comp trajectory and career capital:
  - **Channel ownership breadth:** How many channels does the role own? Owning paid + organic + lifecycle vs. only paid acquisition is a materially different scope. More channels = more headcount = Director+ trajectory. Push for clarity: "I want to confirm the role owns [list channels]. If it's narrower, that changes the level and comp conversation."
  - **Agency spend authority:** Direct control of agency budgets ($500K+ annually) is a scope signal that justifies Director-level comp. If the role manages agencies, negotiate explicit budget authority: "What is the agency spend I'd manage directly? A $[X]M agency budget is Director-scope responsibility and should be reflected in the comp."
  - **Cross-functional dotted lines:** Marketing roles that have dotted-line influence over PM (product-led growth) or Sales (enablement, pipeline handoff) are higher-impact and should comp accordingly. Negotiate for explicit cross-functional authority in the role description if it exists informally: "This role partners closely with Product and Sales on pipeline. I'd like to see that cross-functional scope reflected in the job architecture."
- **Performance bonus nuance:** Push hard for bonus tied to marketing-controlled metrics, not downstream sales outcomes:
  - **Good bonus metrics (negotiate for these):** Pipeline generated, MQLs, CAC efficiency, brand lift scores, website traffic/conversion, email engagement, campaign ROAS. These are directly within marketing's control.
  - **Bad bonus metrics (negotiate away from these):** Sales close rate, revenue closed-won, net retention. These depend on Sales execution, product quality, and customer success -- not marketing performance.
  - **Draft language:** "I'd like to discuss the bonus structure. I want to ensure my variable comp is tied to metrics I can directly influence -- pipeline generated, MQL volume, and CAC targets -- rather than downstream conversion rates that depend on Sales execution. Can we align the bonus plan to marketing-controlled KPIs?"
  - **If bonus is partially tied to company revenue (common at Director+):** Accept the company-revenue component but negotiate the split: "I'm comfortable with a portion tied to company performance, but I'd like at least 60-70% of the bonus weighted toward marketing-specific KPIs. That way both sides have alignment."

**First-Time Director/VP Negotiation Template:**
If `career-plan.md` shows the user is targeting Director or VP level without having previously held that title (e.g., current Senior Manager targeting Director, or Senior IC targeting VP):
- **Negotiate explicit team-building commitments:** "I'll have authority to hire 2-3 people within the first 6 months" and a timeline for scope expansion. First-time Directors without headcount guarantees risk being Directors in title only.
- **Title with growth:** If they offer Senior Manager, counter with "Director with a 6-month performance review for scope expansion." Frame: "I want us both to have confidence -- a 6-month checkpoint lets me prove the Director-level impact."
- **Budget authority:** First-time Directors should negotiate explicit budget ownership, not just headcount. "What budget will I manage directly? I want to confirm operational authority, not just team management."
- **Scope protection:** Get the reporting line and cross-functional scope in writing before accepting. First-time Directors are especially vulnerable to scope erosion in the first 6 months.

**Design-Specific Negotiation:**
- **Comp structure:** Base + equity + sign-on + bonus (typically 10-15% at Lead+). Design comp historically lags engineering comp by 10-20% at the same level — this is a known inequity to push back on.
- **Priority order for IC roles:** base > equity (push for eng-parity) > scope/title > team size > sign-on > design tool budget
- **Priority order for Head of Design / Design Director:** reporting line (CPO vs. CTO vs. CEO) > team headcount > design system ownership > base > equity > design tool budget. Reporting line determines scope, influence, and whether design has a seat at the strategy table. A Head of Design reporting to a CTO often means design is treated as a service org to engineering. Reporting to a CPO or CEO signals design as a strategic function. This single factor affects career trajectory, team growth, and future comp more than any dollar amount in the initial offer. Negotiate reporting line FIRST -- if the reporting line is wrong, negotiate to change it or factor the diminished scope into a higher comp ask to offset the career cost.
- **Key negotiation levers:** design-to-engineering comp parity, team size, reporting line, design system ownership
- **Design-to-engineering comp parity (expanded):** The 10-20% design-to-eng gap is well-documented and should be challenged directly in every negotiation. Use this specific language: "Your Staff Engineer band for this level is $[X]. Design leadership at this level drives equivalent business impact -- I designed the [specific feature/system] that drove [metric]. I'd like to benchmark against your engineering IC comp bands for this level." If they push back ("design and engineering are different ladders"), counter with: "I understand the ladders are separate, but the business impact is equivalent. A design system that reduces engineering build time by 30% or a redesign that lifts conversion by 15% has the same P&L impact as a Staff Engineer's infrastructure work. I'm asking for parity in recognition of that impact." Always have 2-3 specific impact examples ready from experience-library.md.
- **Research team access negotiation:** If the role involves or should involve user research, negotiate for dedicated UX researchers reporting directly to design, not to PM or a shared research pool. Shared researchers get pulled to PM priorities, and design loses the ability to drive its own research agenda. Draft language: "I'd like to discuss the research team structure. In my experience, design teams produce significantly better outcomes when UX researchers report into design rather than a shared pool. Is there flexibility to structure a dedicated research function within the design org?" If the company has no researchers at all, negotiate a headcount commitment: "I'd like to include one UX researcher hire in my first-year headcount plan. Research-informed design reduces rework and accelerates shipping -- it pays for itself within two quarters."
- **Design exercise / case study compensation awareness:** If the company required a design exercise, portfolio presentation, or case study during the interview process, recognize that this represents significant unpaid labor (often 10-20+ hours of work). While you should not demand payment for past interview work, use it as a signal of your investment and commitment during negotiation: "I invested significant time in the design exercise for this process because I'm genuinely excited about this role. That level of investment reflects my commitment -- I'd like the offer to reflect the same." This is a soft leverage point, not a hard ask, but it reinforces that the candidate is serious and has already demonstrated value.
- **Watch for:** "We don't have a separate design leadership ladder" -- this often means design comp is capped at IC levels. Negotiate for the creation of the ladder or equivalent engineering-track comp. Also watch for: design tool budget being counted as "part of your comp" -- tools like Figma, Framer, or prototyping software are operational costs, not compensation. If a company frames tool access as a perk, push back: "Design tools are a cost of doing business, not a benefit. I'd expect those to be covered as operational expense, separate from the comp discussion."

**Data Science / ML Engineer-Specific Negotiation:**
- **Comp structure:** Base + equity (often heavy at research-oriented companies) + sign-on + bonus. Research roles skew equity-heavy; applied ML roles are more balanced.
- **Priority order:** base > equity (especially for MLE roles) > sign-on > scope/title > conference/publication support
- **Key negotiation levers:** publication and conference support (NeurIPS/ICML attendance, paper budget), compute budget (access to GPU clusters), open-source contribution time, title (Data Scientist vs. ML Engineer vs. Research Scientist — each has different comp bands)
- **DS-to-MLE pay differential as negotiation lever:** If transitioning from DS to MLE, or if the role blends DS and MLE responsibilities, anchor comp to the MLE band (typically 10-20% higher than DS at the same level). Use this specific framing: "This role involves production ML systems -- model deployment, inference optimization, and pipeline reliability. I'd like to benchmark against your MLE comp bands, not the DS ladder. The production ownership component is what differentiates MLE comp from DS comp." If the company pushes back ("we classify this as Data Science"), counter with: "I understand the title, but the responsibilities -- production model serving, CI/CD for ML pipelines, latency optimization -- are MLE work. I'd like comp to reflect the actual scope rather than the title." If they will not move on comp band classification, negotiate for an MLE title instead, which sets up future comp correctly: "If the comp band is fixed to DS, could we discuss an MLE title? That ensures my comp trajectory aligns with the production work I'll be doing."
- **Manager-level DS/MLE negotiation:** For DS/MLE Manager, Senior Manager, or Director roles, negotiate beyond cash comp for scope commitments that determine effectiveness and career trajectory:
  - **Team headcount commitments:** Get a written or documented commitment to team size. "I'd like to confirm the team headcount plan for Year 1. Managing a team of 3 vs. 8 is a fundamentally different scope -- and I want to ensure the headcount plan matches the level and comp of this role." Push for specific approved headcount, not vague "we'll grow the team."
  - **Compute budget authority:** Negotiate explicit authority over compute spend. "What compute budget will I have direct authority over? I'd like to understand whether I'll need to go through a centralized approval process for GPU allocation or whether I'll have a dedicated budget." A clear compute budget (even $200K-$500K/year) signals the company is serious about ML investment. Lack of one signals ML may be under-resourced.
  - **Conference and publication budget:** Negotiate a per-person annual conference budget ($5K-$10K per IC for top-tier conferences: NeurIPS, ICML, KDD, AAAI). This is a recruiting and retention tool, not a perk. Frame it as such: "A conference budget of $[X] per team member annually is standard for competitive ML teams. It's also a retention lever -- ML engineers expect publication and conference support."
  - **Patent bonus structure:** If the company has a patent program, negotiate the bonus structure upfront. Standard ranges are $2K-$10K per patent filing, $5K-$15K per grant. "Does the company have a patent incentive program? I'd like to understand the bonus structure for patent filings and grants, as my team will likely generate patentable IP."
- **Research time allocation:** For roles with a research component (Research Scientist, Applied Scientist, or any role where publishing or experimentation is part of the job description), negotiate protected research time explicitly: "I'd like to discuss research time allocation. For roles with a research component, I've found that 20% protected time for papers, experiments, and exploratory work -- not subject to sprint commitments -- is the minimum to produce meaningful research output. Can we formalize that expectation?" If the company is hesitant, frame research time as a retention and recruiting tool: "Protected research time is table stakes for hiring and retaining top ML talent. Without it, the role is applied ML, not research, and should be scoped and titled accordingly."
- **Compute budget as compensation:** For research-oriented roles, access to GPU clusters (internal or cloud) has real dollar value and should be factored into the total comp evaluation. A $50K/year dedicated compute budget is functionally equivalent to $50K in additional comp for a researcher, because it directly enables the work that drives career advancement (publications, model development, experimentation velocity). When evaluating an offer: "This role includes a dedicated compute allocation of $[X]/year -- factor that into your total comp comparison. A $250K base + $50K compute budget at Company A may be more valuable for your career than a $280K base with shared, constrained GPU access at Company B." When negotiating: "I'd like to discuss the compute resources allocated to this role. A dedicated annual compute budget of $[X] -- whether through internal cluster allocation or cloud credits -- would ensure I can deliver on the research and model development goals. Can we formalize a compute allocation?"
- **Watch for:** companies offering DS comp for MLE work. If the role involves production systems and deployment, it's MLE and should be compensated accordingly. Also watch for: "Research Scientist" titles with no actual research time or publication support -- this is a comp arbitrage where companies use a prestigious title to attract talent without providing the resources that make the title meaningful. If the role is called Research Scientist but has no protected research time, no compute budget, and no publication support, it is an Applied Scientist or MLE role and should be evaluated against those comp bands instead.

### Regional Negotiation Norms

**UK:** Similar to US but less aggressive. Equity is less common outside startups. Negotiate on base + bonus + pension contribution + remote days. Notice periods are typically 1-3 months.

**Germany:** Negotiate on annual gross salary. Notice periods are 3-6 months and affect start dates — a critical factor. During Probezeit (6-month trial), notice is only 2 weeks. Negotiate Urlaubstage (vacation days — 25-30 standard, push for 30+). Home office Pauschale (WFH allowance) is negotiable. Equity rare outside startups.

**India:** Negotiate on CTC. Variable pay (10-20% of CTC) may not be guaranteed — negotiate for higher fixed component. Joining bonus is a standard lever. Notice periods are 60-90 days (not 2 weeks) — negotiate buyout if needed for faster start. Relocation allowance for city moves is common.

**Middle East:** Package-oriented negotiation — housing allowance, education allowance, flights, car allowance are all standard negotiable items. End-of-service gratuity is statutory (not negotiable). Tax-free income means gross = net — compare to pre-tax offers elsewhere. Salary history disclosure is expected and refusing may disqualify.

### Step 5: Build Counter-Offer Strategy
Determine:
- **Target:** Your ideal counter (with justification from market data + unique value)
- **Walkaway:** Your floor (from career-plan.md). Below this, you decline.
- **Anchoring ask:** Typically 10-20% above target, depending on leverage strength
- **Priority order:** Which components to push on first (usually: base > equity > sign-on > bonus > title/level). **Exception:** For manager-to-IC transitions, reorder to: title/level > base > equity > sign-on > bonus.
- **Fallback pivots:** If they cannot move on base, pivot to equity. If equity is fixed, pivot to sign-on. If all cash comp is firm, push for level/title/scope.

### Step 6: Draft Counter Language
Write two versions:

**Option A -- Email counter:**
- Lead with genuine enthusiasm for the role (2-3 sentences that reference specific things from the interview process)
- Transition: "I'd love to make this work. After reviewing the offer against market data and my other options, I'd like to discuss a few components."
- Present the counter with data backing every ask
- Close with flexibility signal: "I'm confident we can find a package that works for both sides."

**Option B -- Verbal counter (for phone/video call):**
- Opening: genuine enthusiasm (rehearsable talking points)
- Transition to the ask (natural, not scripted-sounding)
- Key data points to cite verbally (2-3 max -- do not overwhelm)
- Responses to common pushbacks
- Silence technique: after stating the ask, stop talking

### Step 7: Call Prep with BATNA
Prepare for the negotiation conversation:
- What to say if they ask "Is this your top choice?"
- What to say if they push back on base
- What to say if they say "final offer"
- What to say if they offer a level bump instead of comp
- Your BATNA (Best Alternative to Negotiated Agreement): the best outcome you have if this negotiation fails. From app-tracker: other offers, late-stage processes, or the option to walk.

## Output

```markdown
# Offer Analysis - [Company] [Role] [Level]
Date: [date]
Decision deadline: [date if known]

## The Offer
| Component | Amount | Notes |
|-----------|--------|-------|
| Base | $[X] | |
| Equity | $[X] over [Y] years | [type: RSU/ISO/NSO], [vesting schedule] |
| Bonus | [X]% target ($[Y]) | [guaranteed Y1 or not] |
| Sign-on | $[X] | [clawback terms if any] |
| Other | [list] | [relocation, benefits, etc.] |

**Total Year 1:** $[X]
**Total Annual (steady state):** $[X]
**Total 4-Year:** $[X]

## Market Comparison
| Source | Range | Your Offer | Percentile |
|--------|-------|------------|------------|
| levels.fyi [level] | $[X]-$[Y] | $[Z] | P[N] |
| Glassdoor [role] | $[X]-$[Y] | $[Z] | P[N] |
| Blind data points | [list recent] | — | — |
| Company-intel | [if available] | — | — |

**Assessment:** [Above market / At market / Below market] — [1 sentence justification with data]

## Your Targets (from career-plan.md)
- Dream offer target: $[X]
- Walkaway number: $[X]
- This offer vs target: [+/- $X] ([above/below] by [X]%)
- This offer vs walkaway: [+/- $X] ([above/below] by [X]%)

## Pay-Cut Analysis
[Only if current comp exceeds offer or target range]
- **Current total comp:** $[X]
- **This offer:** $[Y]
- **Delta:** -$[Z] ([X]% reduction)
- **Your stated walkaway:** $[W]
- **Is this deliberate?** [Confirm user is making a conscious trade-off, not capitulating]
- **What you are gaining:** [role quality, company trajectory, equity upside, career positioning, mission alignment -- must be specific]
- **Comp trajectory:** [At this company/level, what does Year 2-3 comp look like with refreshers/promotions? A short-term cut that leads to faster growth may be rational.]
- **Negotiation posture:** Do NOT anchor to current comp. Negotiate within the band for this level. Target top-of-band positioning: $[X].

## Leverage Points
1. **[Leverage type]:** [specific data-backed point]
   Strength: [strong / moderate / weak]
2. **[Leverage type]:** [specific data-backed point]
   Strength: [strong / moderate / weak]
3. **[Leverage type]:** [specific data-backed point]
   Strength: [strong / moderate / weak]

**Overall leverage assessment:** [strong / moderate / limited]

## Counter-Offer Strategy
| Component | Current | Ask | Target | Walkaway |
|-----------|---------|-----|--------|----------|
| Base | $[X] | $[X] | $[X] | $[X] |
| Equity | $[X] | $[X] | $[X] | $[X] |
| Sign-on | $[X] | $[X] | $[X] | $[X] |
| Total Y1 | $[X] | $[X] | $[X] | $[X] |

**Priority order:** [which component to push on first, second, third]
**Fallback pivots:** [if base is firm → push equity; if equity is firm → push sign-on; etc.]

## Draft Counter Language

### Option A: Email
---
Subject: [Company] - Offer Discussion

Hi [Recruiter Name],

[2-3 sentences of genuine enthusiasm about the role, referencing specific
conversations or aspects of the opportunity. NOT generic.]

I've reviewed the offer carefully and I'd love to make this work. After
looking at market data for [level] PMs at [company] and factoring in
[specific leverage point], I'd like to discuss a few components:

- **Base:** I'm targeting $[X], which aligns with [data source] for
  [level] in [location]. [1 sentence justification.]
- **Equity:** [If relevant: "Given [reason], I'd like to discuss a grant
  of $[X]."]
- **Sign-on:** [If relevant: "A sign-on of $[X] would help bridge [gap]."]

I'm confident we can find a package that reflects the value I'll bring to
[specific project/team]. Happy to discuss on a call whenever works for you.

Best,
[Your Name]
---

### Option B: Verbal (Call Talking Points)
1. **Open with enthusiasm:** "[Specific thing you're excited about]. I've
   really enjoyed the process and I'm excited about [specific project/team]."
2. **Transition:** "I've done my research on the compensation side and I'd
   love to talk through a few things."
3. **The ask:** "For base, I was hoping to land at $[X]. Looking at
   levels.fyi data for [level] and my [specific experience], that feels
   like the right range."
4. **Then stop talking.** Let them respond. Do not fill the silence.
5. **If they push back on base:** "I understand base bands can be tight.
   Could we explore [equity / sign-on / level adjustment] to close the gap?"
6. **If they say final offer:** "I appreciate that. Can I ask -- is there
   any flexibility on [component], or is the entire package final?" (Tests
   whether it's truly final.)
7. **If truly final and below walkaway:** "I really appreciate the offer
   and the time everyone has invested. I need to think about whether the
   total package works for my situation. Can I have until [date]?"

## Prep for the Call
- **Your BATNA:** [Best alternative -- other offer at $X from Company Y,
  or late-stage process at Company Z, or current role if staying is viable]
- **Their likely BATNA:** [They have other candidates, but if hiring
  velocity is high, backfilling takes time]
- **Tone:** Enthusiastic and collaborative, never adversarial. You are
  solving a problem together, not fighting over money.
- **Key data points to have ready:** [2-3 specific numbers from market
  research to cite if challenged]
- **Red flags during the call:** [If recruiter becomes hostile, if they
  rescind the offer, if they pressure you to decide on the spot]

### Background Check Timing

If the user has background check concerns (check career-plan.md):
- Clarify when the background check occurs: pre-offer, post-conditional-offer, or post-start.
- Help the user ask naturally: "Can you walk me through the onboarding timeline, including any background check?" — this is standard and does not raise flags.
- If post-conditional-offer: the offer may be rescinded based on results. Prepare a proactive disclosure script: "I want to be transparent about something that will appear in the background check: [brief factual statement]. Here's the context: [1-2 sentences]. It has no bearing on my ability to perform this role."
- If the user is in a ban-the-box jurisdiction, the company legally cannot ask before a conditional offer.
- *This is strategic career coaching, not legal advice. Consult an attorney specializing in employment law in your jurisdiction.*

## Decision Framework
- [ ] Does total comp meet your walkaway number? [yes/no]
- [ ] Does the role match your career plan priorities? [yes/no]
- [ ] Are there dealbreaker non-comp factors? [list any from career-plan.md "what would make you say no"]
- [ ] Is this better than your BATNA? [yes/no]
- [ ] After negotiation, will you feel good about the outcome? [gut check]
```

## Example

**Input:** `/negotiate base 175k equity 300k/4yr RSU bonus 15% sign-on 30k at Google L5 PM Seattle`

**Output would include:**
- Parsed offer: $175K base, $75K/yr equity, ~$26K bonus, $30K sign-on = ~$306K Y1, ~$276K steady state
- Market comparison: levels.fyi L5 PM Seattle median is $320K total. This offer is at ~P35.
- Leverage: below market by ~$44K annually, user has a competing Stripe offer at $310K from app-tracker, 8 years experience maps to mid-L5 not entry-L5
- Counter strategy: ask for $195K base (P50 at L5) and additional $50K equity, sign-on to $50K. Target total Y1: $350K.
- Draft email leading with enthusiasm for the specific team, citing levels.fyi data
- Call prep including BATNA (Stripe offer) and pivot strategy if base is band-locked

## Quality Checks

1. **Every ask backed by data.** Never recommend a counter-offer number without a data source. "I think you should ask for more" is useless. "$195K aligns with P50 for L5 PMs at Google per levels.fyi (N=847 data points)" is useful.
2. **Always lead with enthusiasm.** Check both email and verbal drafts. The first thing out of the user's mouth or email must be genuine excitement about the role. Never lead with the ask. Never make it adversarial.
3. **Walkaway number included.** Always reference the walkaway from career-plan.md. The user must know their floor before entering negotiation. If career-plan.md does not have a walkaway number, prompt: "Your career plan doesn't specify a walkaway number. Before negotiating, decide: what's the minimum total comp you'd accept? Set this BEFORE the call, not during."
4. **Competing offers referenced.** Always check app-tracker for other offers or active processes. These are the strongest leverage and must be incorporated. If no competing offers exist, note: "You have limited leverage without competing offers. Consider accelerating other processes before countering."
5. **Equity risk acknowledged.** For pre-IPO companies, always note that equity value is uncertain. Do not treat paper equity as equivalent to cash RSUs at public companies. Apply a reasonable discount and explain why.
6. **Silence technique.** The verbal script must include an explicit instruction to stop talking after the ask. This is the most common negotiation mistake -- filling silence with concessions.
7. **Fallback chain.** Always include a priority-ordered fallback chain. If the user can get nothing on base, they need to know immediately where to pivot. Do not let the user enter a call without knowing their next move if the first ask is rejected.
8. **Non-comp factors.** Check career-plan.md for "what would make you say no" and flag any non-comp dealbreakers in the decision framework. Comp negotiation is irrelevant if the role itself is wrong.
9. **Timeline awareness.** If the user has a deadline, build urgency into the strategy. If they do not have a deadline but have competing processes, suggest creating one strategically.
10. **Pay-cut scenario handling.** If the user's current comp exceeds the offer or the target range, the skill MUST detect this and switch to pay-cut negotiation mode. Never blindly tell a user to "ask for more to match current comp" when they are deliberately taking a cut for the right opportunity. Instead, help them negotiate to the top of the band while protecting against unnecessary concessions. Flag the pay cut explicitly so the user makes a conscious, informed decision.
11. **Current comp concealment.** In pay-cut scenarios, the counter language (both email and verbal) must NEVER reveal the user's current comp unless the user explicitly wants to. Revealing a higher current comp in a pay-cut scenario can signal flight risk or create awkwardness. Coach the user to redirect comp questions to market data for the target role.
12. **Cross-market comp concealment (non-US to US).** If the user's current comp is in a non-US market that pays significantly less than US rates (EUR, JPY, etc.), the negotiation strategy must treat current comp as CONFIDENTIAL. The counter language must never state or imply the current figure. If the user already disclosed their non-US comp during the process (check interview-history.md), generate a "Comp Anchor Recovery" section specifically addressing the cross-market disclosure: "You disclosed a non-US comp figure that sounds low in US context. Reframe: 'That figure reflects the [European/Japanese] market, which has a fundamentally different comp structure. For this role in [US city], I'm targeting the market rate of $[X]-$[Y] based on levels.fyi data.'" The verbal script must include this redirect practiced to fluency.
13. **International relocation in counter-offer.** If the user is relocating internationally (check career-plan.md for relocation indicators), the counter-offer must include relocation as an explicit negotiation point. Add a row to the Counter-Offer Strategy table for "Relocation" with estimated international move costs ($20K-$40K), assessment of whether the offer's relocation package covers actual costs, and a draft ask: "International relocation from [country] typically runs $[X]. Could we discuss increasing the relocation package to cover actual costs, or adding a sign-on to bridge the gap?"
14. **Visa-aware negotiation posture.** If the user needs visa sponsorship, the negotiation section must include visa-specific guidance: (a) Do NOT use visa as a reason to accept below-market offers -- companies that sponsor have comp bands that apply equally to all candidates. (b) If the user has limited competing offers due to visa constraints, acknowledge this honestly but do not telegraph it: "Frame enthusiasm for the role as genuine interest, not lack of alternatives." (c) If an L-1 transfer path is available (from target-companies.md), note it as potential negotiation leverage: "You could potentially start at [company's European office] on L-1, which removes lottery risk and may increase the company's willingness to invest in the offer."
15. **Founder comp framing (failed founder / shut-down company).** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, apply these adjustments to the negotiation strategy:
    - **Do NOT use the founder's previous salary as an anchor.** Founders at failed startups often paid themselves well below market (bootstrapped/early-stage) or above market (funded startup with inflated CEO comp). Neither is relevant. The anchor is the market rate for the TARGET role. If the recruiter asks about previous comp, the response is: "My founder comp reflected the economics of an early-stage startup, not the market rate for a [level] PM. Based on levels.fyi, the range for this role is $[X]-$[Y]." Practice this redirect until it is automatic.
    - **Counter with market rate language, not founder history.** The counter-offer email and verbal scripts must frame the ask in terms of the role's market data, not the founder's comp history. Do NOT write: "As a former CEO, I was earning $X." DO write: "Based on market data for [level] at [company], I'm targeting $[X], which aligns with P[N] on levels.fyi."
    - **If the recruiter anchors to the low founder salary:** Recovery script: "That figure reflected the reality of an early-stage startup where I chose to invest in the team rather than my own comp. For this role, I'm focused on what's competitive in the market. My research shows $[X]-$[Y] for [level] at [company]."
    - **If the recruiter anchors to a high funded-startup CEO salary:** Recovery script: "My comp at [startup] included a CEO-level package at a funded company, which isn't directly comparable to a [level] PM role. I'm targeting the market rate for this role: $[X]-$[Y] based on levels.fyi data."
    - **Equity negotiation for founders:** Former founders understand equity deeply. Use this as leverage: ask informed questions about vesting schedule, refresh grants, acceleration on change of control, and exercise windows. This signals sophistication without arrogance. Include in the verbal script: "Having built a company, I think a lot about equity structure. Could you walk me through the refresh grant cadence and what happens to unvested shares in an acquisition?"
16. **Industry-anomaly comp concealment.** If career-plan.md shows a structurally below-market employer (Epic Systems, government, academia, non-profit, pre-revenue startup), verify that: (a) all counter-offer language and verbal scripts anchor exclusively to market data, never to current comp, (b) salary history ban laws are cited when the target role is in a ban jurisdiction (CA, NY, CO, WA, etc.), (c) deflection scripts are included in the call prep, (d) the equity education primer is included if transitioning from a no-equity employer, (e) the over-gratitude tone check passes (no "generous offer" language despite the comp jump).
17. **Military-to-Civilian Comp Translation.** If career-plan.md shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), apply these negotiation adjustments: (a) Do NOT anchor to military base pay. Military candidates often undersell themselves by anchoring to their base pay (e.g., O-3 ~$65K) when their true total comp including BAH, BAS, TRICARE, and TSP is $90-110K+. The counter should be framed around market value for the role, not military pay: "My total military compensation was approximately $[calculated total]. For this civilian role, I'm targeting $[market rate] based on [X] years of leadership and analytical experience." (b) Clearance as leverage: for defense tech roles, the clearance itself has market value ($50K-$150K to sponsor, 6-12 month timeline). Use this in negotiation: "My active TS/SCI eliminates the 6-12 month clearance timeline and associated costs for your organization." This is a concrete, quantifiable value proposition that justifies top-of-band positioning. (c) For general tech roles: do NOT lead with clearance value unless the company does government work. Instead, focus on years of leadership experience and transferable skills as the comp justification.
