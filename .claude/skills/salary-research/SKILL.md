---
name: salary-research
description: Research market compensation for a specific company, role, level, and location before negotiation.
---

# /salary-research - Market Compensation Research

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In salary research contexts, this means: comp research output may reference the user's financial targets from career-plan.md but must never include the personal reasons behind those targets (e.g., "needs $X because of family obligations" must never appear).

## When to Use

Run this skill before entering salary discussions, before negotiating an offer, or when evaluating whether a role's compensation is competitive. Provides a comprehensive market data picture so you negotiate from facts, not feelings. Best run before `/negotiate` so the negotiation skill has fresh data to work with.

**Trigger:** `/salary-research [company] [role] [level] [location]`

Examples:
- `/salary-research Google PM L5 Seattle`
- `/salary-research Anthropic Senior PM San Francisco`
- `/salary-research Stripe Growth PM L3 Remote`
- `/salary-research Meta Product Manager E5 New York`

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
- Company name
- Role title
- Level (company-specific level if known, e.g., L5, E5, IC4; or generic like "Senior")
- Location (city or "remote")

**Optional:**
- Specific comp components to focus on (e.g., "mainly interested in equity structure")
- Whether this is pre-IPO (changes equity analysis significantly)
- Your current comp (for comparison context)

**Auto-read (do not ask the user for these -- read them directly):**
- `context-library/career-plan.md` -- dream offer target, walkaway number, level preference
- `context-library/experience-library.md` -- to map user's experience to the appropriate level
- `context-library/qa-master.md` -- previously communicated comp expectations
- `insider-data/company-intel/[company].md` -- any comp data, band info, or negotiation intel (if exists)

## Process

### Step 1: Web Research - levels.fyi
Search for compensation data on levels.fyi:
- `levels.fyi [company] [level] [role] total compensation`
- `levels.fyi [company] product manager [location]`
- `levels.fyi [company] [level] salary`

Extract:
- Total compensation range (P25, P50, P75 if available)
- Base salary range
- Equity range (annual value)
- Bonus range
- Number of data points (more data points = higher confidence)
- Recency of data (data from 2+ years ago is less reliable)
- Location-specific adjustments if available

### Step 2: Web Research - Glassdoor
Search for compensation data on Glassdoor:
- `Glassdoor [company] [role] salary [location]`
- `Glassdoor [company] product manager compensation`

Extract:
- Base salary range
- Additional cash compensation (bonus)
- Number of salary reports
- Note: Glassdoor often underreports equity, so treat as base salary reference primarily

**[FUNCTION-ADAPTIVE]** Use function-appropriate compensation data sources. SWE: levels.fyi (excellent SWE data), Glassdoor, Blind, teamblind.com. Design: levels.fyi, Glassdoor, AIGA salary survey, Coroflot salary guide. Data Science: levels.fyi, Glassdoor, Burtch Works DS salary study. Marketing: Glassdoor, Built In salary data, ANA salary survey. CS/Sales: Pavilion CS Compensation Survey, RepVue benchmarks, Bridge Group CS Comp Report, Glassdoor. Do NOT default to PM-specific search queries for non-PM roles.

NOTE: levels.fyi and Glassdoor have significantly less Design compensation data than SWE or PM. For Head of Design / Design Director targets, data sparsity is a real problem. Lower the confidence rating by one level (e.g., High → Medium) and supplement with: Dribbble salary survey, AIGA salary guide, and comparable-company estimation (anchor to the engineering leadership band at the same company, then apply the typical 10-15% Design discount). For CS roles, use Pavilion CS Compensation Survey and Bridge Group CS Comp Report as primary sources, as levels.fyi CS data is thin.

IMPORTANT: Marketing comp varies significantly by sub-function. Growth/performance marketing roles at PLG companies typically pay 10-20% above brand marketing roles at the same level and company. Product marketing comp is typically between growth and brand. When researching, segment queries by sub-function: search 'growth marketing director salary [company]' not just 'marketing director salary.' The ANA salary survey and Built In both allow sub-function filtering — use it. If the user is transitioning between marketing sub-functions (e.g., brand to growth), note the potential comp uplift as a positive factor.

### Step 3: Web Research - Blind
Search for recent compensation data points on Blind:
- `Blind [company] [level] offer [current year]`
- `Blind [company] product manager compensation [current year]`
- `teamblind.com [company] [level] TC`

Extract:
- Recent individual data points (people sharing their offers/current comp)
- Negotiation outcomes (what people were able to negotiate up to)
- Any notes about band limits, refresher grants, or promotion comp changes
- Note: Blind data is self-reported and may skew high (selection bias)

### Non-US Markets

If the target location is outside the US:
1. levels.fyi has limited international data -- use if available but note low confidence
2. Add Glassdoor [location] as primary source
3. Search for local compensation surveys: '[country] product manager salary survey [year]', regional salary platforms
4. Regional sources:
   - UK: Glassdoor UK, Reed.co.uk, Otta
   - Germany: Glassdoor DE, StepStone, Kununu
   - Singapore: Glassdoor SG, NodeFlair, MyCareersFuture
   - India: Glassdoor India, AmbitionBox, Naukri
   - Australia: Glassdoor AU, Seek, Hays Salary Guide
   - **MENA:** GulfTalent, Bayt.com, Hays Gulf Salary Guide, Robert Half Middle East Salary Guide.
5. Note comp structure differences: UK pension contributions (8-15%), European equity taxation, sign-on bonuses less common outside US
6. If company-intel comp data is US-only, flag: 'Comp ranges in the intel file are US-based. Apply location adjustment for [target location].'

### Regional Comp Structures

When target market is non-US, show comp in the local framework:

**UK:** Annual gross salary + bonus + equity (if startup). Pension contribution (employer typically 3-8%). Private health insurance as benefit. Show in GBP. No 401k equivalent discussion.

**Germany:** Annual gross salary. Note: 13th-month salary common (effectively ~8% bonus). Weihnachtsgeld (Christmas bonus) at many companies. Company car value (5-10K EUR/year, common at senior levels). Betriebsrente (company pension). Public health insurance (employer pays ~7.3% of gross). Show effective total comp including all components.

**India:** CTC (Cost to Company) is the primary number. Break down: CTC = Basic + HRA + Special Allowance + PF (employer contribution) + Gratuity + Variable Pay. Show actual in-hand (take-home) number vs CTC. Variable pay is often 10-20% of CTC and may not be guaranteed. ESOP vesting schedules vary widely at Indian startups.

**Middle East (UAE/Qatar):** Tax-free income — gross = net. Include housing allowance (30-40% of base), education allowance, annual flight home allowance, end-of-service gratuity (UAE: 21 days/year for first 5 years, 30 days/year after). These benefits are substantial and standard.

### Cross-Market Relocation (Non-US Current Comp to US Target)

If the user is currently compensated in a non-US market and targeting US roles (or any cross-market move where comp structures differ significantly):

1. **Do NOT treat the current non-US comp as a pay-cut baseline.** European, Japanese, and most non-US tech markets pay 40-60% less in total comp than US equivalents at the same level. A Senior PM earning EUR 130K in Munich is not "underpaid" -- they are at market for Munich. The comparison baseline must be the US market rate for the target role, not the user's current comp.
2. **Add a "Market Transition" section to the output** that shows:
   - Current comp in local currency and USD equivalent
   - US market rate for the equivalent role/level (from levels.fyi, Glassdoor)
   - The gap as both a dollar amount and a percentage
   - A framing note: "This gap reflects the US-vs-[market] comp differential, not a personal raise. Your target of $[X] is within the normal US range for this level."
3. **Cost-of-living adjustment context:** If the user is relocating from a lower-cost market to SF/NYC, note that the comp increase is partially offset by higher living costs. Provide a rough comparison: "SF cost of living is approximately [X]% higher than [current city]. Adjusted for living costs, $[US target] provides roughly [X]% more purchasing power than [current comp in local currency]."
4. **Comp question coaching:** Flag that the cross-market jump makes the comp question especially dangerous. Add: "CRITICAL: Never state your current non-US comp in interviews. The number will sound low to a US recruiter and anchor the negotiation against you. Always frame in terms of US market rate for the role: 'Based on levels.fyi, Senior PMs at [Company] earn $[X]-$[Y]. I'm targeting within that range.'" Cross-reference `qa-master.md` for any existing comp scripts.
5. **Currency and tax notes:** Note relevant differences in tax treatment, equity taxation, social contributions, and benefits that affect take-home pay comparisons. European comp often includes employer-paid social contributions (health, pension) that are separate from the stated salary, while US comp typically does not.

### Step 4: Insider Data Check
Check `insider-data/company-intel/[company].md` for:
- Compensation bands or ranges mentioned in the profile
- Negotiation flexibility notes (is this company known for moving on comp?)
- Equity structure (RSU schedule, refresh policy, cliff details)
- Any insider tips about comp discussions

**Insider Data vs User Research Cross-Check:** After reading the company-intel comp ranges, compare them against any comp data the user has already documented in `target-companies.md`, `qa-master.md`, or `career-plan.md`. If the user's self-researched ranges (from levels.fyi, Glassdoor, Blind, or conversations with contacts) diverge significantly (20%+ gap) from the company-intel ranges, flag this explicitly: "The company-intel file lists [range] for this level, but your own research in [file] shows [range]. This divergence may be due to: (1) different level interpretations (company-intel may reference a higher level), (2) stale data in one source, (3) different comp components included (some ranges include equity at paper value, others at cash-equivalent). I recommend treating the LOWER range as more conservative and the HIGHER range as the ceiling in a strong-leverage scenario. Clarify which level the company-intel range refers to before anchoring your negotiation."

This cross-check prevents candidates from anchoring their expectations to inflated or deflated numbers from a single source. It is especially important when company-intel comp ranges include pre-IPO equity at paper value while the user's research reflects cash-equivalent estimates.

### Step 5: Level Mapping

**[FUNCTION-ADAPTIVE]** Function-specific career ladder mapping. SWE: Junior -> Mid -> Senior -> Staff -> Principal -> Distinguished (L3-L8). Design: Junior -> Mid -> Senior -> Lead -> Principal -> VP. Data Science: Analyst -> Data Scientist -> Senior DS -> Staff DS -> Principal DS. CS: CSM -> Senior CSM -> CS Manager -> Director CS -> VP CS -> CCO. Marketing: Coordinator -> Manager -> Senior Manager -> Director -> VP -> CMO.

**[FUNCTION-ADAPTIVE]** CS/Sales roles often have OTE (On-Target Earnings) structures with variable comp tied to retention/revenue metrics. When detected: model total comp at 80%, 100%, and 120% attainment. Research accelerator curves above target. Factor in: ramp quota for new hires, measurement periods, and guaranteed variable in first quarter.

Using `experience-library.md`, map the user's experience to the appropriate level at this company:
- Years of PM experience
- Scope of work (IC vs team lead, 0-to-1 vs optimization, team size influenced)
- Impact level (metrics moved, revenue influenced, users affected)
- Compare against typical level expectations at this company (from levels.fyi career data or company-intel)

**Career Changer Level Translation:**
If the user is coming from a NON-PM role (consulting, engineering, design, etc.), the level mapping requires special handling:
- Do NOT map consulting seniority directly to PM seniority. A McKinsey Engagement Manager (EM) manages teams and drives $200M+ engagements, which is Director-level scope in consulting terms. But transitioning to PM, the user will typically be hired at PM or Senior PM level (1-2 levels below their consulting seniority) because they lack PM-specific execution experience (sprint planning, A/B testing, shipping iteratively).
- Provide an explicit cross-function level translation: "[User's title] at [current company] = [equivalent PM level] for hiring purposes. Your consulting scope is [level], but PM roles will level you based on PM-specific experience, which is [0/limited/partial]. Expect to be hired at [level], not [higher level]."
- The comp implication is critical: if the user's current comp at their non-PM role exceeds the PM-level band at the target company, this is a GUARANTEED pay-cut scenario. Flag explicitly: "McKinsey EM comp ($245K) is at or above the P50 for PM at [company] ($XXK). You are trading seniority (and possibly comp) for a career change. Make sure the non-comp factors justify this."
- Research whether the target company has precedent for hiring career changers at higher levels. Some companies (especially those that value analytical rigor) may level a McKinsey EM at Senior PM rather than PM. Check recent PM hires from consulting backgrounds if this data is available.

Flag if there is a mismatch:
- "Your experience suggests [level], but you're applying for [different level]. This may affect comp range expectations."
- "At [company], [level] typically requires [X years / Y scope]. Your experience could support [level] or [level+1]."

**Cross-Company Level Translation:**
- When the user is coming from a company with a different leveling system, provide an explicit level translation table. E.g., Amazon L6 = Google L5 = Meta E5. This is critical because level titles mislead -- "Senior PM" means different things at different companies.
- If the user is at a level at their current company where comp is HIGHER than the equivalent level at the target company (common when moving between companies with different comp philosophies, e.g., Amazon L7 $350K-$550K vs a target where equivalent level pays $300K-$450K), flag this explicitly: "Your current level's comp at [current company] exceeds the typical range at [target company] for the equivalent role. You may be in a pay-cut scenario. See below."

**Pay-Cut Detection:**
- Compare the user's current total comp (from career-plan.md) against the target level's P50 at the target company.
- If current comp > target P50, flag: "Your current comp of $[X] is above the P50 ($[Y]) for this role. Expect a comp discussion where you are explaining why you are willing to move for less, not asking for more. See `/negotiate` pay-cut scenario handling."
- If current comp > target P75, flag more strongly: "Your current comp of $[X] exceeds even P75 ($[Y]) for this role. You are almost certainly taking a pay cut. Make sure the non-comp factors justify this move."
- Research whether the target company offers equity upside, refresher grants, or faster promotion velocity that could close the gap over 2-3 years.

### Step 6: Synthesize and Position
Combine all data sources into a unified picture. For each data source:
- Note the confidence level (high/medium/low based on data point count and recency)
- Note any biases (Glassdoor skews low on equity, Blind skews high overall, levels.fyi is most balanced)
- Derive a recommended range that weighs the sources appropriately

Compare against the user's targets from `career-plan.md`:
- Dream offer target vs market reality
- Walkaway number vs market floor
- Is the user's target realistic for this company/level? If not, flag it with data.

### Step 7: Generate Negotiation Context
Provide strategic context for the upcoming negotiation:
- Is this company known for negotiating? (from company-intel or Blind reports)
- What components are most flexible? (base is often banded; equity and sign-on often have more room)
- Recent hiring velocity (from target-companies or web search -- high velocity = more leverage for candidates)
- Any company-specific quirks (e.g., "Google's L5 band tops out at $X base" or "Anthropic includes equity refreshers annually")

## Output

```markdown
# Salary Research - [Company] [Role] [Level] [Location]
Generated: [date]
Data confidence: [high / medium / low] (based on data point count and recency)

## Market Data

### levels.fyi
- **Total comp range:** $[X] - $[Y] ([N] data points, last updated [date])
  - P25: $[X]
  - P50 (median): $[X]
  - P75: $[X]
- **Base range:** $[X] - $[Y]
- **Equity range:** $[X] - $[Y] per year
- **Bonus range:** $[X] - $[Y]
- **Confidence:** [high/medium/low] — [N] data points, [recency assessment]

### Glassdoor
- **Base salary range:** $[X] - $[Y] ([N] salary reports)
- **Additional cash comp:** $[X] - $[Y]
- **Confidence:** [high/medium/low] — [note: typically underreports equity]

### Blind
- **Recent data points:**
  - [Date]: [Level] offered $[X] TC ([base/equity/bonus breakdown if shared])
  - [Date]: [Level] negotiated from $[X] to $[Y]
  - [Date]: [Level] current comp $[X]
- **Confidence:** [high/medium/low] — [note: self-reported, may skew high]

### Company Intel (insider-data)
[If company-intel file exists:]
- Comp bands: [any data]
- Negotiation flexibility: [flexible / moderate / rigid]
- Equity structure: [RSU/ISO/NSO, vesting schedule, refresh policy]
- Notes: [any relevant tips]

[If no company-intel file:]
- No insider data available for [company]. Relying on public sources.

## Compensation Breakdown

| Component | Low (P25) | Mid (P50) | High (P75) | Notes |
|-----------|-----------|-----------|------------|-------|
| Base | $[X] | $[X] | $[X] | [banded at most companies] |
| Equity | $[X]/yr | $[X]/yr | $[X]/yr | [vesting schedule, type] |
| Bonus | $[X] | $[X] | $[X] | [target % if known] |
| Sign-on | $[X] | $[X] | $[X] | [typical for new hires] |
| **Total Y1** | **$[X]** | **$[X]** | **$[X]** | [includes sign-on] |
| **Total Annual** | **$[X]** | **$[X]** | **$[X]** | [steady state] |

[If pre-IPO company:]
**Equity risk note:** [Company] is pre-IPO. Equity values above are based on
last known valuation ($[X], [date]). Actual value depends on future outcomes.
Apply a [30-50%] discount when comparing to public company RSU offers.

**Illiquid equity analysis (for pre-IPO companies):**
- **Liquidity status:** [Can shares be sold on secondary markets? Is there a tender offer program?]
- **Exercise cost:** [For ISOs/NSOs: strike price * shares = $X out-of-pocket to exercise. This is real money at risk.]
- **Tax implications:** [ISOs: AMT risk on exercise. NSOs: taxed as income on exercise. RSUs: taxed on vesting but no exercise cost.]
- **409A valuation date:** [When was the last 409A? How stale is it?]
- **Dilution risk:** [What funding round? Earlier rounds = more future dilution. Note: a Series A grant will be diluted significantly by the time of IPO.]
- **Realistic value scenarios:**
  - Bull case (IPO at 2-3x current valuation): equity worth $[X]/yr
  - Base case (IPO at current valuation, minus dilution): equity worth $[X]/yr
  - Bear case (down round, acquisition at discount, or no liquidity event in 5+ years): equity worth $[X]/yr or $0
- **Cash-equivalent comparison:** "To compare this offer against a public company RSU offer, use the base-case equity value with a 30-50% liquidity discount. Your $[X] equity grant has a risk-adjusted annual value of ~$[Y], compared to $[Z] in immediately-liquid RSUs at a public company."
- **If NO valuation data is available (very early stage, pre-Series A, or no public funding data):** State: "Equity valuation data unavailable. Treat equity as lottery upside, not compensation. Evaluate this offer on cash comp alone (base + bonus + sign-on). If cash comp alone does not meet your walkaway number, this offer relies on equity that may never be liquid."

## Your Position

### Level Mapping
Based on your experience library:
- **Your experience:** [X years PM, scope summary, impact summary]
- **Maps to:** [Level] at [Company]
- **Confidence:** [high/medium/low]
- [If mismatch: "You're targeting [Level] but your experience suggests [Level]. Consider [action]."]

### Cross-Company Level Translation
| Your Current | Target Company Equivalent | Comp Implication |
|-------------|--------------------------|------------------|
| [Current company] [Level] | [Target company] [Level] | [Higher / Similar / Lower comp band] |

[If pay-cut detected:]
**Pay-Cut Alert:** Your current comp of $[X] at [current company] is above the [P50/P75] for [target level] at [target company]. This is a -$[delta] ([X]%) reduction. Ensure the non-comp factors (equity upside, career trajectory, mission, scope) justify this trade-off. See `/negotiate` for pay-cut negotiation strategy.

### Targets vs Market
| | Your Target | Market P50 | Delta |
|---|------------|------------|-------|
| Dream offer | $[X] | $[X] | [+/- $X] |
| Walkaway | $[X] | $[X] | [+/- $X] |

- **Dream offer assessment:** [Realistic / Stretch / Unrealistic] — [1 sentence with data]
- **Recommended ask:** $[X] total comp
  - Justification: [specific data source + your unique value that warrants this position in the range]
- **Walkaway number:** $[X] (from career-plan.md)
  - Assessment: [Above market floor / At market floor / Below market floor]

### Comp Expectations Alignment
[From qa-master.md:]
- You previously communicated: $[X]-$[Y] range
- Market data shows: $[X]-$[Y] range
- Alignment: [your stated range is within / above / below market]
- [If misaligned: "You stated $X-$Y but market data supports $A-$B. Adjust your stated range or be prepared to justify the gap."]

## Negotiation Context

### Company Negotiation Profile
- **Flexibility:** [flexible / moderate / rigid]
- **Most movable components:** [typically: sign-on > equity > base at this company, or whatever the data shows]
- **Band limits:** [any known hard caps, e.g., "Google L5 base caps at ~$210K"]
- **Equity specifics:** [vesting schedule, cliff, refresh policy if known]

### Hiring Velocity
- **Current hiring pace:** [high / moderate / low] (from target-companies or web search)
- **Leverage implication:** [high velocity = more leverage; low velocity = less urgency on their side]

### Recent Context
- [Any relevant recent events: layoffs, hiring freezes, expansion, IPO plans, funding rounds]
- [How this context affects negotiation: e.g., "Post-layoff hiring means they're being selective but roles that are open have real budget"]

## Next Steps
1. Use this data to anchor your expectations before any comp conversation
2. If you receive an offer, run `/negotiate [offer details]` for full counter-offer strategy
3. If you need to state expectations in a screen, use: $[recommended range] with source: "[data source]"
4. If your career-plan targets are misaligned with market data, consider updating career-plan.md
```

## Example

**Input:** `/salary-research Anthropic Senior PM San Francisco`

**Output would include:**
- levels.fyi data: limited data points (Anthropic is newer/smaller), $280K-$400K total comp range from available reports
- Glassdoor data: $180K-$220K base range from 15 salary reports
- Blind data: 3 recent data points showing offers in $320K-$380K TC range for senior PMs
- Company-intel: Anthropic offers competitive equity with 4-year vesting, known to be moderately flexible on comp, strong emphasis on mission alignment
- Level mapping: user's 6 years PM experience + AI project work maps to Senior PM (IC3/IC4 equivalent)
- User's dream offer ($350K) is at ~P50 for this role -- realistic target
- Recommended ask: $370K total to anchor high, with $320K walkaway
- Negotiation context: Anthropic is hiring aggressively (high velocity = good leverage), equity is pre-IPO (apply 30% discount vs public company RSU comparisons)

## Quality Checks

1. **Multiple sources required.** Never rely on a single data source. Always search levels.fyi, Glassdoor, and Blind at minimum. If data is sparse on one source, note it and weigh the others more heavily.
2. **Data confidence ratings.** Every data source must include a confidence assessment based on: number of data points, recency, and known biases. Do not present low-confidence data as if it were definitive.
3. **Pre-IPO equity disclaimer.** For any pre-IPO company, always include the equity risk note. Never present pre-IPO equity at face value without a discount discussion. This is a common candidate mistake and the skill must prevent it.
4. **Level mapping honesty.** If the user's experience does not clearly map to the target level, say so. Do not inflate the level mapping to make the user feel good. A honest "your experience maps to L4, not L5" prevents embarrassment in negotiation.
5. **Career-plan alignment.** Always compare market data against the user's targets from career-plan.md. If the user's dream offer is unrealistic for this company/level, flag it respectfully: "Your target of $X is above P90 for this role. It's achievable only with exceptional leverage (competing offers at $X+, rare expertise)."
6. **Actionable ranges.** The recommended ask must be a specific number with a specific justification, not a vague range. "Ask for $350K, justified by P60 positioning on levels.fyi and your 8 years of relevant experience" is actionable. "Ask for somewhere between $300K and $400K" is not.
7. **Freshness.** Compensation data ages quickly. Flag if the most recent data is more than 6 months old. Note any market shifts (layoffs, hiring booms) that may have moved the market since the data was collected.
8. **No fabricated data.** If web research yields no results for a company/level combination, say so. "No levels.fyi data available for [Company] [Level]. Relying on Glassdoor and comparable companies." Never invent data points to fill gaps.
9. **Seamless handoff to /negotiate.** The output should contain everything `/negotiate` needs. After running `/salary-research`, the user should be able to run `/negotiate` and the system uses the research automatically.
10. **Pay-cut scenario detection.** If the user's current comp exceeds the P50 for the target role, this MUST be flagged. Many experienced PMs moving between companies (especially from high-comp companies like Google/Meta to pre-IPO companies, or from inflated levels at one company to correctly-leveled roles at another) face pay cuts. The skill must surface this honestly so the user enters negotiations with eyes open, not surprised when the offer comes in "low."
11. **Cross-company level translation.** Always provide an explicit level mapping table when the user's current company uses a different leveling system than the target. "Amazon L6 = Google L5" is the kind of insight that prevents candidates from anchoring to the wrong band.
12. **Cross-market relocation section required.** If the user's current comp is in a non-US currency and the target role is in the US, the output MUST include the "Market Transition" section showing: current comp in local currency, USD equivalent, US market rate for the role, the gap as a percentage, and the framing note that this gap reflects a market differential not a personal raise. Without this section, the user is left without the context they need to frame comp discussions correctly.
13. **Comp question danger flag for cross-market candidates.** If the user's current comp is significantly below the US target range (e.g., EUR 130K vs $280-340K target), the output must include a bolded warning in the Negotiation Context section: "CRITICAL: Your current comp in [currency] will sound dramatically low to a US recruiter. NEVER state it. Always frame as: 'Based on levels.fyi, Senior PMs at [Company] earn $[X]-$[Y]. I'm targeting within that range.' Rehearse this redirect until it is automatic."

**Career gap / returner comp adjustments:** If `career-plan.md` shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), add these adjustments to the salary research output:
- **Gap-adjusted benchmarks:** Note that market rates may have shifted during the gap. Pull CURRENT rates from levels.fyi, Glassdoor, and Blind -- not rates from when the user was last employed. If the user's last comp data is from 3+ years ago, flag: "Your last active comp was in [year]. Market rates for [level] at [company type] have [increased/decreased/shifted] since then. Current data shows $[X]-$[Y]. Do not anchor to your pre-gap salary -- the market may have moved significantly."

**Military Comp Structure Translation:** If `career-plan.md` shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), add these adjustments to the salary research output:
- **Military comp includes more than base pay.** Military compensation includes: base pay + BAH (Basic Allowance for Housing) + BAS (Basic Allowance for Subsistence) + TRICARE (healthcare, equivalent to $500-$800/mo employer-paid premium) + TSP matching (retirement, equivalent to 5% employer 401k match). When converting to civilian total comp, calculate the TRUE total military comp including all benefits. An O-3 (Captain) with ~$65K base pay has a true total comp of approximately $90-110K+ when all allowances and benefits are included.
- **Common mistake: military candidates anchor to their BASE pay and undersell themselves.** A Captain earning $65K base pay who targets $90K civilian salary is leaving $30-50K+ on the table. Flag this: "Your military base pay of $[X] does NOT reflect your total compensation. Your TRUE total military comp including BAH, BAS, TRICARE, and TSP is approximately $[calculated total]. For civilian roles, target market rate based on your TOTAL years of leadership and analytical experience, not your military base pay."
- **Defense tech clearance premium:** Defense tech roles often pay a premium for clearance holders because the clearance itself has market value ($50K-$150K to sponsor, 6-12 month timeline). Research this differential when the target role is at a defense tech company or any company doing classified work. Note: "Your active [clearance level] clearance has significant market value. Defense tech companies factor this into their comp -- expect a 10-20% premium over non-cleared equivalent roles."
- **Pre-gap salary anchoring risk:** Flag if the user's comp expectations (from career-plan.md) are anchored to their pre-gap salary rather than current market rates. If the pre-gap salary is significantly below current market (market moved up during the gap), note: "Good news: market rates have increased since your last role. Your pre-gap comp of $[X] would map to approximately $[Y] in today's market. Target current market rates, not your historical number." If the pre-gap salary is above current market (rare, but possible in a down market), note: "Market rates for [level] have [compressed/shifted] since [year]. Current P50 is $[X] vs your pre-gap $[Y]. Adjust expectations to current market data."
- **Return-to-work program comp data:** If available, note that returnship programs (Path Forward, iRelaunch, company-specific) often pay 80-90% of market rate during the program period, with full-market conversion rates upon conversion. Include this context: "Returnship programs typically pay $[X]-$[Y] for [level] during the program (80-90% of market). Conversion offers are usually at full market rate. Negotiate the conversion comp at program entry, not at conversion time."

**ZERO-EQUITY EMPLOYER DETECTION:** If `career-plan.md` indicates the candidate's current or most recent employer has NO equity compensation (private company with no equity plan like Epic Systems, government, academia, non-profit, or bootstrapped startup with no equity grants), apply these adjustments:
- Flag in the output: "ZERO-EQUITY EMPLOYER: Current comp is 100% cash. Do NOT let this anchor the negotiation low -- total comp at equity-granting companies will be significantly higher."
- Generate a comp comparison table showing: Current cash-only comp (base + bonus) vs. Target total comp at equity-granting companies (base + equity + bonus). This makes the gap visible: e.g., "Current: $180K all-cash at Epic | Target: $280-340K total comp (base $190K + equity $70K/yr + bonus $30K) at comparable-level roles."
- Note: Candidates from zero-equity employers often have strong cash savings habits -- this can be used as a negotiation asset. Request MORE equity and LESS sign-on (there is no "forfeited equity" to buy out, so sign-on has less justification). Frame: "I have no unvested equity to replace, so I'd prefer to weight the package toward equity to align my incentives with the company's long-term success."
- Specific example: Epic Systems (private, no equity, Midwest-anchored comp) -- an Epic PM earning $170K all-cash is at market for Epic but well below P25 total comp for equivalent PM roles at equity-granting tech companies. The transition to a company with equity means a significant total comp increase even if base salary stays flat.
- Trigger: career-plan.md mentions employer with no equity, explicitly states no equity in comp, or lists a known zero-equity employer (Epic, government agencies, non-profits, academia).

**HEALTH-TECH VS GENERAL-TECH COMP DIFFERENTIAL:** Health-tech PM roles typically pay 10-20% below general tech PM roles at the same level due to smaller equity grants, narrower comp bands, and regulated-industry constraints. Apply these adjustments:
- Segment research by industry when the candidate has health-tech domain experience: "Health-tech target: $250-280K | General tech target: $280-320K at the same level."
- Flag when a health-tech domain expert is also applying to general tech: "Your health-tech comp range may anchor you below the general-tech market. Research both ranges separately. Do not let a health-tech offer set your expectations for general tech negotiations."
- This differential applies to companies like Epic, Cerner/Oracle Health, Veeva, athenahealth, and health-tech startups vs. general tech companies at equivalent levels.

**Founder-to-employee comp reset (failed founder / shut-down company):** If `career-plan.md` shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, add a "Founder Comp Context" section to the salary research output:
- **Do NOT anchor to the founder's previous salary.** Founders at failed startups often paid themselves well below market (sometimes $0-$80K) or well above market (inflated CEO title with inflated comp at a funded startup). Neither number is relevant to the market rate for the target PM role. The anchor must be the ROLE's market rate from levels.fyi, Glassdoor, and Blind -- not the founder's historical comp.
- **Flag the anchoring risk explicitly:** "Your founder comp of $[X] at [startup] does not reflect the market rate for [target level] PM roles. Founders' self-set salaries are not comparable to market comp. Anchor your expectations to the role's market data: $[Y]-$[Z] based on [data sources]."
- **If the founder's previous comp was BELOW market (common for bootstrapped/early-stage founders):** Note: "Your previous comp was below the market rate for this role. This is an INCREASE scenario. Do not feel guilty about targeting market rate -- you were underpaying yourself as a founder. The market rate for [level] at [company] is $[X]-$[Y]. Target P50-P75."
- **If the founder's previous comp was ABOVE market (common for well-funded startups with inflated titles):** Note: "Your founder comp of $[X] included equity and/or a CEO-level salary at a funded startup. The market rate for [target level] PM is $[Y]-$[Z], which may be lower. This is a comp reset, not a pay cut -- you are moving from a founder role to an employee role at a different level. Adjust expectations to the employee market rate."
- **Equity sensitivity:** Founders are often equity-focused. Add context: "As a former founder, you may be tempted to over-weight equity in the offer evaluation. For PUBLIC companies, equity is comp -- value it fully. For PRE-IPO companies, apply a founder's skepticism: you know from experience that equity can go to zero. Apply a 40-60% discount to pre-IPO equity when comparing to your cash needs."
