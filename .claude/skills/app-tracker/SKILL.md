---
name: app-tracker
description: Central application pipeline tracker with add, update, status, and pipeline view actions, plus auto-behaviors after other skills run.
---

# /app-tracker - Application Pipeline Tracker

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In app-tracker contexts, this means: pipeline entries and notes fields must never contain private reasons for preferences or constraints; only professional and logistical information belongs in the tracker.

## When to Use

- User applies to a new role and needs to log it (`/app-tracker add`)
- User receives an update on an application and needs to record it (`/app-tracker update`)
- User wants to check the status of a specific application (`/app-tracker status`)
- User wants a full pipeline overview with stats (`/app-tracker pipeline`)
- Auto-triggered after `/resume-tailor`, `/referral-request`, or `/interview-debrief` to keep the tracker current

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

- **Required for `add`:** Company name, role title, date applied (defaults to today if not provided)
- **Required for `update`:** Company name (or role title), new status
- **Required for `status`:** Company name (or role title)
- **Required for `pipeline`:** No additional input needed
- **Auto-loaded:** `context-library/target-companies.md` (to cross-reference company info)
- **Auto-loaded:** `context-library/connection-tracker.md` (to show referral status)
- **Storage file:** `context-library/app-tracker.md` (this file is the persistent tracker -- create it if it doesn't exist)

## Process

### Action: `add` -- Add New Application

**Trigger:** `/app-tracker add [Company] [Role] [Date]`

1. Parse the company name, role title, and application date (default to today's date if not provided)
2. Check if this company+role combination already exists in `app-tracker.md` -- if so, warn the user and ask if they want to update instead
3. Cross-reference `target-companies.md` for the company's tier, stage, and any notes
4. Cross-reference `connection-tracker.md` for any existing connections at this company
5. Create a new entry with the full application record
6. Append to `app-tracker.md` in the correct stage section
7. Output confirmation with the entry details and any relevant context (connections, company tier)

**Entry format in app-tracker.md:**
```markdown
### [Company] - [Role Title]
- **Status:** Applied
- **Date applied:** [YYYY-MM-DD]
- **Referral:** [Yes (name) / No / Requested (name)]
- **Resume version:** [link or note about which tailored version]
- **Cover letter:** [Yes / No]
- **Connection at company:** [name from connection-tracker, or None]
- **Work product sent:** [Yes (link/title) / No / In progress] -- career changers: track this; it is your strongest differentiator
- **Visa/sponsorship:** [Confirmed sponsor / Sponsorship TBD / Not required] -- auto-populate from target-companies.md if available; update after recruiter screen confirms or denies sponsorship for this specific role. If the user needs sponsorship (check career-plan.md), this field is required for every entry. Track any visa-specific notes: "Recruiter confirmed H-1B for this role," "L-1 transfer path available via Munich office," "Sponsorship policy unclear -- follow up." For TN visa holders: track TN category eligibility separately -- not all role titles qualify for TN status. Add a `tn-eligible` field (yes/no/verify) and flag roles where the title may not align with NAFTA professional categories.
- **TN eligible:** [Yes / No / Verify] -- only for TN visa holders. Indicates whether the role title aligns with a NAFTA professional category. If "Verify," flag for review before investing interview prep time.
- **Background check stage:** [pre-offer / post-offer / unknown] -- helps users with background check concerns plan their disclosure timing.
- **Company tier:** [from target-companies.md, or Unranked]
- **Last action:** Applied [date]
- **Next action:** Follow up if no response by [date + 7 days]
- **Notes:** [any context]
- **History:**
  - [YYYY-MM-DD] Applied
```

### Action: `update` -- Update Application Status

**Trigger:** `/app-tracker update [Company] [New Status]`

Valid statuses (in pipeline order):
1. `applied` -- Application submitted
2. `referral-requested` -- Asked someone for a referral
3. `referral-received` -- Referral confirmed submitted
4. `recruiter-screen` -- Recruiter call scheduled or completed
5. `phone-interview` -- Phone/video interview scheduled or completed
6. `onsite` -- Onsite/final round scheduled or completed
7. `offer` -- Received an offer
8. `rejected` -- Rejected at any stage
9. `withdrawn` -- User withdrew from the process
10. `ghosted` -- No response after 14+ days with no follow-up remaining

**[FUNCTION-ADAPTIVE]** Some functions have additional/different stages. SWE: may include "take-home-assessment" and "system-design-round" as distinct stages. Design: may include "portfolio-review" and "design-challenge" stages. Marketing: may include "case-study-presentation" and "campaign-exercise" stages. DS/MLE: may include "take-home-modeling-exercise," "research-presentation," and "technical-screen" stages. CS: may include "case-study" and "role-play" stages.

Steps:
1. Find the matching application in `app-tracker.md` (match on company name, fuzzy match if needed)
2. If multiple roles at the same company, list them and ask user to specify

### Dual Application Protocol

When the user adds a second application at the same company:
- Trigger advisory: "You're applying to two roles at [Company]. Consider: (a) Are these in the same org? Hiring managers may compare notes. (b) Pick a primary and secondary preference. (c) Frame as flexibility, not indecision: 'I'm most interested in [primary], but I also bring strong fit for [secondary].'"
- Track both applications with a linked status — updates to one should prompt consideration of the other.
- If one role rejects while the other is active, note this for interview prep (they may ask about it).
3. Update the Status field to the new status
4. Append the status change with date to the History log
5. Update the "Last action" field
6. Set a new "Next action" based on the status:
   - `applied` --> "Follow up if no response by [+7 days]"
   - `referral-requested` --> "Check in with [name] if no update by [+3 days]"
   - `referral-received` --> "Expect recruiter outreach within [+5 days]; follow up if silent"
   - `recruiter-screen` --> "Send thank-you within 24 hours; prep for next round"
   - `phone-interview` --> "Send thank-you; run /interview-debrief; prep for onsite"
   - `onsite` --> "Send thank-you notes to each interviewer; run /interview-debrief"
   - `offer` --> "Run /negotiate before responding; do not accept on the spot"
   - `rejected` --> "Send gracious reply; ask for feedback; add learnings to interview-history.md"

### Re-Application Workflow

When the user adds an application at a company where a prior "rejected" entry exists:
- Calculate months since rejection. Note: most companies have 6-12 month cooldown policies.
- Trigger: "You were rejected at [Company] on [date] ([N months] ago). Check their re-application policy. If eligible, I'll build a re-application strategy that addresses your prior rejection reasons."
- Track as a new entry linked to the prior one. Include field: `prior_attempt: [date, outcome, weakness areas]`.
- Auto-prompt: resume-tailor should differentiate from the prior resume, and interview-prep should include prior-cycle intelligence.
   - `ghosted` --> "Send one final follow-up, then archive"
7. **Stage skip validation:** Before applying the update, check if the user is skipping stages. Valid skip paths:
   - Any status --> `rejected` (can be rejected at any stage)
   - Any status --> `withdrawn` (can withdraw at any stage)
   - Any status --> `ghosted` (can be ghosted at any stage)
   - `applied` --> `recruiter-screen` (normal progression, skipping referral steps is fine)
   - Forward progression through the pipeline order is valid (e.g., `recruiter-screen` --> `onsite` if the company skips phone rounds)
   - **Invalid skips to warn about:** `applied` --> `offer` (did you skip interview stages? These should be logged for accurate conversion tracking), `applied` --> `onsite` (confirm: did this really skip straight to onsite?)
   - If an invalid skip is detected, warn: "You're moving [Company] from [old status] to [new status], which skips [skipped stages]. Is this correct? If intermediate stages happened, log them for accurate pipeline analytics."
8. Output the updated entry with what changed highlighted

### Action: `status` -- Check Single Application

**Trigger:** `/app-tracker status [Company]`

1. Find the matching application(s) in `app-tracker.md`
2. Display the full entry with all fields
3. Calculate days since last action
4. Highlight if any next action is overdue
5. Show the full history timeline
6. If the user has connections at this company (from connection-tracker.md), remind them

### Action: `pipeline` -- Full Pipeline View

**Trigger:** `/app-tracker pipeline`

1. Read all entries from `app-tracker.md`
2. Group by current status
3. Calculate pipeline statistics
4. Flag applications needing attention (overdue next actions)
5. Output the pipeline view using the appropriate format based on pipeline size

**Scalability rules for large pipelines (30+ active applications):**
- **Compact mode (30-49 active):** In the Applied -- Waiting section, show only the 10 most recent applications and a count of older ones: "[N] older applications not shown -- run `/app-tracker status [company]` for details." Show all entries in Interview, Onsite, and Offer stages (these are high-priority and must be visible).
- **Summary mode (50+ active):** Switch the Applied -- Waiting and Referral In Progress sections to summary tables instead of individual entries:

  | Status | Count | With Referral | Avg Days Waiting | Oldest |
  |--------|-------|---------------|------------------|--------|
  | Applied | [N] | [N] ([%]) | [N] | [Company] ([N] days) |

  Show individual entries ONLY for: Offers, Onsite, Phone Interview, Recruiter Screen, and Needs Attention. These are the stages where individual visibility matters for decision-making.
- **Always show full detail for:** Needs Attention (overdue items), Offers, and any application with an interview in the next 7 days. These are never summarized regardless of pipeline size.
- **Closed section:** In all modes, show only counts for Rejected/Withdrawn/Ghosted with the most recent 3 entries each. Full closed history stays in `app-tracker.md` but is not displayed in pipeline view.

## Output

### For `add`:
```markdown
## Application Added
**[Company]** - [Role Title]
- Applied: [date]
- Referral: [status]
- Company tier: [tier from target-companies]
- Connections: [names or "None -- consider /connection-request"]
- Next action: Follow up by [date + 7 days]

*Application logged to app-tracker.md*
```

### For `update`:
```markdown
## Application Updated
**[Company]** - [Role Title]
- Previous status: [old status]
- New status: [new status]
- Updated: [date]
- Next action: [auto-generated next step]

*History updated in app-tracker.md*
```

### For `status`:
```markdown
## Application Status - [Company] [Role]
- **Current status:** [status]
- **Days in current stage:** [N]
- **Applied:** [date] ([N] days ago)
- **Referral:** [details]
- **Next action:** [action] -- [OVERDUE if past due date]

### Timeline
- [date] Applied
- [date] Referral requested (via [name])
- [date] Referral confirmed
- [date] Recruiter screen completed
[... full history ...]
```

### For `pipeline`:
```markdown
## Application Pipeline - [date]
**Active applications:** [N]
**Interviews scheduled:** [N]
**Offers:** [N]
**Rejection rate:** [N]% ([rejected] / [total])
**Average days to first response:** [N]
**Referral rate:** [N]% of applications have referrals

---

### Offers ([N])
- [Company] [Role] - Offer received [date] - Comp: [if known] - Deadline: [if known]

### Onsite / Final Round ([N])
- [Company] [Role] - Onsite [date] - Prep: [done/needed] - Run `/interview-prep` if needed

### Phone Interview ([N])
- [Company] [Role] - Interview [date] - Prep: [done/needed]

### Recruiter Screen ([N])
- [Company] [Role] - Screen [date or "awaiting scheduling"]

### Referral In Progress ([N])
- [Company] [Role] - Referral via [name] - Status: [requested/received] - Days waiting: [N]

### Applied -- Waiting ([N])
- [Company] [Role] - Applied [date] - Referral: [yes/no] - Days waiting: [N]

### Needs Attention (OVERDUE)
- [Company] [Role] - [what's overdue and what to do about it]

---

### Closed
#### Rejected ([N])
- [Company] [Role] - Stage: [where rejected] - [date]

#### Withdrawn ([N])
- [Company] [Role] - Reason: [if noted] - [date]

#### Ghosted ([N])
- [Company] [Role] - Last contact: [date] - Days silent: [N]

---

### Pipeline Health
- **Top of funnel:** [N] applications in last 7 days (target: 3-5/week with referrals)

**[FUNCTION-ADAPTIVE]** Staff+ SWE and Director+ CS roles are scarcer than PM roles. Adjust "low volume" threshold: SWE Staff+: 2-3/week is healthy. CS Director+: 2-4/week is healthy. Marketing Director: 2-4 quality apps/week (Marketing Director roles are scarcer at Series B-C companies). DS/MLE Manager: 2-4 quality apps/week (MLE Manager roles are competitive; target companies with established ML orgs).
- **Conversion: Applied --> Screen:** [N]% ([N]/[N])
- **Conversion: Screen --> Interview:** [N]% ([N]/[N])
- **Conversion: Interview --> Offer:** [N]% ([N]/[N])
- **Referral vs cold conversion:** Referral [N]% vs Cold [N]%
- **Weakest stage:** [stage with highest drop-off] -- consider [suggestion]. **[FUNCTION-ADAPTIVE]** Function-specific coaching for weak stages: Design: "Consider running /mock-interview design-challenge or /mock-interview portfolio-review." Marketing: "Consider running /mock-interview campaign-strategy." DS: "Consider running /mock-interview case-study or /mock-interview technical." CS: "Consider running /mock-interview cs-strategy or /mock-interview cs-roleplay."
- **Work products sent:** [N] (career changers: track work products sent with HM outreach -- this is your substitute for a PM portfolio and the #1 differentiator for career switchers)

**[FUNCTION-ADAPTIVE]** Function-specific work products: SWE: technical blog posts, open-source contributions, architecture analyses. Design: UX audits, design explorations. Marketing: GTM analyses, campaign proposals, growth audits. DS: model proposals, analytical frameworks, data analysis writeups. CS: CS program designs, QBR proposals. Track these, not PM-style product analyses.
```

## Auto-Behaviors

These run automatically after other skills complete. The user does not invoke them manually.

### After `/resume-tailor` completes:
Prompt the user: "Resume tailored for [Company] [Role]. Add to pipeline? `/app-tracker add [Company] [Role] [today's date]`"
Do not auto-add -- the user may be preparing but not yet applying.

### After `/referral-request` completes:
Auto-update the matching application: set status to `referral-requested`, add the contact name, update history. If no matching application exists, prompt the user to add one first.

Output: "Updated [Company] pipeline entry: referral requested via [name] on [date]."

### After `/interview-debrief` completes:
Auto-update the matching application: advance status to reflect the completed interview stage, update history with interview details. If the debrief indicates rejection signals, note them but do not change status to rejected until confirmed.

Output: "Updated [Company] pipeline entry: [interview type] completed on [date]. Next action: [auto-generated]."

## Example

**Input:**
```
/app-tracker pipeline
```

**Output:**
```markdown
## Application Pipeline - 2026-03-24
**Active applications:** 12
**Interviews scheduled:** 3
**Offers:** 1
**Rejection rate:** 25% (4/16 total)
**Average days to first response:** 8
**Referral rate:** 67% (8/12 active have referrals)

---

### Offers (1)
- Stripe Senior PM, Growth - Offer received 2026-03-20 - $340K TC - Deadline: 2026-03-27 - RUN /negotiate

### Onsite / Final Round (1)
- Notion Senior PM, AI Platform - Onsite 2026-03-26 - Prep: NEEDED - Run /interview-prep

### Phone Interview (2)
- Anthropic PM, Claude Code - Interview 2026-03-25 - Prep: done
- Figma Senior PM, AI - Interview 2026-03-28 - Prep: needed

### Recruiter Screen (1)
- Ramp Senior PM - Screen scheduled 2026-03-25

### Referral In Progress (2)
- Databricks Senior PM, Vector DB - Referral via Sarah Chen - Status: received - Days waiting: 3
- Vercel Infrastructure PM - Referral via Sam Reyes - Status: requested - Days waiting: 5

### Applied -- Waiting (5)
- Airbnb Senior PM, Payments - Applied 2026-03-18 - Referral: yes (via Tom W) - Days waiting: 6
- Plaid PM, Platform - Applied 2026-03-20 - Referral: no - Days waiting: 4
- Scale AI PM - Applied 2026-03-21 - Referral: no - Days waiting: 3
- Vercel Senior PM - Applied 2026-03-22 - Referral: requested - Days waiting: 2
- Linear PM - Applied 2026-03-23 - Referral: no - Days waiting: 1

### Needs Attention (OVERDUE)
- Vercel Infrastructure PM - Referral requested 5 days ago via Sam Reyes. Check in today: "Hey Sam, just following up on the Vercel referral -- any update?"

---

### Closed
#### Rejected (3)
- Google PM, Gemini - Stage: Phone interview - 2026-03-15
- Meta PM, Instagram - Stage: Recruiter screen - 2026-03-10
- Coinbase Senior PM - Stage: Applied (no response) - 2026-03-01

#### Withdrawn (1)
- Uber PM, Eats - Reason: Comp below range - 2026-03-12

---

### Pipeline Health
- **Top of funnel:** 3 applications in last 7 days (on target)
- **Conversion: Applied --> Screen:** 62% (8/13)
- **Conversion: Screen --> Interview:** 75% (6/8)
- **Conversion: Interview --> Offer:** 25% (1/4)
- **Referral vs cold conversion:** Referral 71% to screen vs Cold 33% to screen
- **Weakest stage:** Interview --> Offer at 25%. Consider running /mock-interview more frequently and reviewing /interview-debrief patterns.
```

## Quality Checks

**Good output looks like:**
- Pipeline view groups applications cleanly by stage with zero ambiguity about where each stands
- Every entry has a "Next action" with a specific date -- nothing falls through the cracks
- Auto-behaviors fire reliably after resume-tailor, referral-request, and interview-debrief
- Statistics are calculated correctly from actual data (conversion rates, averages, counts)
- Overdue items are flagged prominently with specific suggested actions
- Pipeline health section provides actionable coaching, not just numbers
- The app-tracker.md file stays clean and parseable as entries accumulate
- Status transitions make sense (can't go from "applied" to "onsite" without intermediate steps -- warn if skipping stages)

**Bad output looks like:**
- Applications with no "Next action" (things get forgotten)
- Pipeline view that's just a flat list without grouping or stats
- Auto-behaviors that silently fail or create duplicate entries
- Statistics that don't add up (rejected + active != total)
- No "Needs Attention" section (the most actionable part of the pipeline view)
- Entries that pile up without ever being marked rejected, withdrawn, or ghosted (stale pipeline)
- Missing conversion rate analysis (the user can't see which stage is their bottleneck)

**Persona-specific checks (verify these when applicable):**
- **Visa-requiring candidates:** The "Visa/sponsorship" field must be populated for every entry when career-plan.md indicates the user needs sponsorship. When running `pipeline` view, include a "Visa Status Summary" line in Pipeline Health: "Visa confirmed: [N] applications. Visa TBD: [N] applications. Action: Confirm sponsorship status for TBD entries at recruiter screen stage." This prevents the user from investing interview prep time in roles that may not sponsor.
- **International/unknown employers in pipeline notes:** When auto-behaviors fire after resume-tailor, check whether the tailored resume included employer brand parentheticals. If the resume-tailor output flagged employer brand issues, carry that note into the app-tracker entry under Notes: "Resume included employer context parentheticals for [Company names]."
- **Company Type tag (failed founder / shut-down company).** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, add a "Company Type" field to every application entry with one of these values: `startup` (sub-50 employees), `scaleup` (50-500), `enterprise` (500+), `agency/consulting`. This field enables the weekly-retro to segment conversion rates by company type and identify where the founder background converts best vs. where it triggers filtering. When running `pipeline` view, include a "Company Type Mix" summary in Pipeline Health: "Startup: [N] apps ([X]% callback). Scaleup: [N] apps ([X]% callback). Enterprise: [N] apps ([X]% callback)." If the mix is 100% one type, flag: "All applications are to [type]. Consider diversifying to test where your founder experience converts best." During the weekly review, note funnel differences by type and surface any statistically significant conversion gaps.
- **Career returner application tracking.** If career-plan.md shows a career gap > 1 year, apply these adjustments:
  - Add a `return-to-work-program: [Yes (program name) / No]` field to each application entry.
  - For return-to-work program applications: add a `program-period` stage between `offer` and a `converted` stage in the valid statuses pipeline.
  - Pipeline health for returners: track returnship vs. standard application conversion rates separately. Display both funnels in the Pipeline Health section: "Returnship funnel: [N] apps, [X]% conversion. Standard funnel: [N] apps, [X]% conversion."
  - Flag if the user is only applying to return-to-work programs (should mix with standard applications): "WARNING: All [N] applications are to return-to-work programs. Consider mixing in standard applications to broaden your pipeline and avoid over-reliance on structured programs."
  - Track "gap handling" performance per interview as a field (`gap-handling-rating: [strong / neutral / weak / not asked]`) on each application entry for downstream analysis in interview-debrief and weekly-retro.
- **Remote-only application tracking.** If career-plan.md shows a remote-only preference, apply these adjustments:
  - Add a `remote-policy: [remote-first / remote-friendly / hybrid / onsite / unverified]` field to each application entry.
  - Pipeline health for remote candidates: segment conversion rates by remote policy type. Display in Pipeline Health: "Remote-first: [N] apps ([X]% callback). Remote-friendly: [N] apps ([X]% callback). Hybrid: [N] apps ([X]% callback). Unverified: [N] apps."
  - WARNING if adding an application where remote policy is "unverified" or "hybrid" or "onsite": prompt the user to verify or reconsider. "WARNING: [Company] remote policy is '[policy]'. You indicated remote-only preference. Please verify this role supports fully remote work before investing application time."
  - Track "Remote Status Summary" in pipeline view: how many apps at remote-first vs. remote-friendly vs. hybrid vs. unverified.
  - Flag when > 20% of applications are at non-remote-first companies (for strictly remote-only candidates): "WARNING: [X]% of your applications are at companies that are not remote-first. For a remote-only search, this increases the risk of wasted effort on roles that may require relocation or hybrid attendance."
- **Veteran (15+ years) application tracking.** If career-plan.md shows 15+ years of experience, apply these adjustments:
  - Add optional `ageism-signals-detected: [count]` field populated from job-fit-scorer output (e.g., "digital native" language, "recent graduate" preference, or capped YOE ranges in the JD).
  - Track rejection patterns by company age profile (startup vs. scaleup vs. enterprise). In Pipeline Health, display: "Startup rejection rate: [X]%. Scaleup rejection rate: [X]%. Enterprise rejection rate: [X]%."
  - Pipeline health: if resume-stage rejection rate > 50%, surface a recommendation: "WARNING: Resume-stage rejection rate is [X]% (above 50% threshold). Review resume compression -- ensure it does not list all 15+ years in detail. Check LinkedIn for age signals (graduation year, early career roles). Consider running /resume-tailor with veteran-specific compression."
  - Segment callback rates by company type to identify where veteran experience is valued vs. discounted. Display in Pipeline Health: "Callback rate by company type -- Startup: [X]%. Scaleup: [X]%. Enterprise: [X]%. Highest-converting segment: [type]."
- **Military-to-PM application tracking.** If career-plan.md shows military background, apply these adjustments:
  - Add a `track: [defense-tech / general-tech]` field to each application entry.
  - Add a `clearance-required: [Yes / No / Unknown]` field to each application entry.
  - Pipeline health: separate defense-tech and general-tech funnels with independent conversion rates. Display in Pipeline Health: "Defense-tech funnel: [N] apps, Applied->Screen [X]%, Screen->Interview [X]%, Interview->Offer [X]%. General-tech funnel: [N] apps, Applied->Screen [X]%, Screen->Interview [X]%, Interview->Offer [X]%."
  - Track "jargon incidents" per interview (`jargon-incidents: [count]`) as a field on each application entry for downstream weekly-retro analysis. If jargon incidents trend upward, surface: "Jargon incident trend is rising. Review /interview-debrief feedback and practice civilian framing for military concepts."
  - WARNING if > 80% of applications are on one track: "WARNING: [X]% of your applications are [dominant track]. Consider diversifying across defense-tech and general-tech to maximize your pipeline breadth and discover where your background converts best."
- **Executive-Level Pipeline Rule.** If `career-plan.md` shows VP/Director/CPO/SVP level AND 12+ years experience:
  - Volume adjustment: 1-3 quality applications/week is healthy for VP/CPO-level searches. These roles are scarcer, and each application requires more research and customization. Do NOT flag "low volume" warnings when an executive has 1-2 apps/week.
  - Additional stages: "retained-search-intro," "compensation-committee," "board-interview," "executive-references" -- executive hiring cycles are longer with more stakeholders.
  - Timeline expectation: VP/CPO searches typically take 16-24 weeks (vs. 10-16 for IC/Senior). Set expectations accordingly and do NOT trigger stall warnings before week 20.
  - Channel tracking: track "retained search firm," "board network," "direct outreach," "PE/VC network" as sources alongside standard LinkedIn/referral/cold-apply channels.
  - Pipeline health: flag when 100% of pipeline comes from one channel (e.g., all from search firms). Executive candidates should diversify: 40-50% search firms, 30-40% network/board connections, 10-20% direct outreach.
  - Add a `comp-range-confirmed` field (Yes / No / TBD) to every executive-level pipeline entry. After recruiter screen or intake call, if comp-range-confirmed is still "No" or "TBD," flag "ADVANCE WITH CAUTION: Comp band not yet confirmed." Warning in pipeline view: "Executive searches can invest 8-12 weeks before comp surfaces. Confirm band before advancing past recruiter-screen stage to avoid sunk-cost on misaligned roles."
- **Dual-Track Pipeline Segmentation.** If `career-plan.md` indicates the user is targeting two distinct role types simultaneously (e.g., ML EM + Senior MLE, or PM + TPM):
  - Generate separate pipeline sections for each track with independent conversion metrics.
  - Add a `track` field to each application entry indicating which track it belongs to.
  - Per-track coaching in Pipeline Health: "Your [Track A] has [X]% callback rate vs. [Y]% for [Track B] -- the [weaker track] narrative may need strengthening."
  - Cross-track insight: "Consider whether your interview experience on [Track A] can inform your positioning for [Track B]."
  - Trigger: career-plan.md shows two or more target role types (distinct titles or functions).
- **CS-Specific Executive Pipeline Guidance.** If detected function is CS AND career-plan.md shows VP/Director level:
  - Add CS-specific executive interview stages: "meet-the-CEO" and "customer-reference-calls" (common in VP CS hiring where the candidate meets actual customers before offer).
  - Add tracking field: `cs-reporting-structure` (Reports to CRO / CEO / CPO / COO) to each CS executive entry -- this significantly impacts role scope and comp.
  - Coaching note in Pipeline Health: "VP CS roles where CS reports to the CRO tend to be more quota-carrying; VP CS reporting to CEO tends to be more strategic. Track this to calibrate expectations."
- **Early-Career Volume Benchmark.** If `career-plan.md` shows < 3 years of experience, adjust the "Top of funnel" benchmark in Pipeline Health from "3-5/week with referrals" to "5-8 quality apps/week." Early-career candidates need higher volume to compensate for lower callback rates and thinner networks. This aligns with the weekly-retro early-career benchmarks.
