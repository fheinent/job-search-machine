---
name: daily-morning-briefing
description: Master daily briefing that runs all three intelligence parts. Scheduled for 7:00 AM.
---

# Daily Morning Briefing — Master Task

Run this every morning to get a complete job search intelligence report.

**Scheduled:** 7:00 AM (via Claude Desktop Cowork)

---

## What This Does

This is a **parent task** that orchestrates three sub-briefings:

1. **Part 1 (7:00 AM)** → New roles + scoring → `/briefing-part1-roles`
2. **Part 2 (7:10 AM)** → Networking + follow-ups → `/briefing-part2-networking`
3. **Part 3 (7:20 AM)** → Pipeline health + priorities → `/briefing-part3-coaching`

All three outputs combine into a single briefing file: `briefings/briefing-{DATE}.md`

---

## How It Works

### Input Data
- Your `career-plan.md` (target companies, levels, geographies, deal-breakers)
- Your `target-companies.md` (prioritized list with notes)
- Your `app-tracker.md` (current pipeline status)
- Your `interview-history.md` (patterns, weaknesses, recent wins)
- Your `connection-tracker.md` (network status, follow-up dates)

### Processing
1. **Scan** all job boards for NEW roles matching your criteria (posted last 24h)
2. **Score** each role against your career plan (fit, urgency, tailoring effort)
3. **Identify** network gaps (who should you know at hot companies? Who did you not follow up?)
4. **Detect** pipeline bottlenecks (where are you stuck? What's your win rate by round?)
5. **Recommend** what to do today (which role to tailor, which person to reach out to, which weakness to address)

---

---

# Full Briefing (Single-Session Reference)

> For users with Claude Max who want to run the entire briefing in one shot, paste everything below the line as a single prompt. This is the original unabridged briefing.

> **Token usage:** On Claude Pro, use the 3-part split above instead. If the briefing cuts off, re-run with "Continue from Part [N]." Claude Max provides higher limits for full briefing runs.

---

# Morning Briefing - Job Search OS

Read all files in the job-search-os/context-library/ folder. Also read job-search-os/CLAUDE.md for system rules.

## QUALITY GATE -- Required Context Check

Before running any part of the briefing, verify these three files are filled with real data (not just template placeholders):

1. **experience-library.md** -- If this file is empty or still contains template placeholders (e.g., brackets like "[bullet with specific metric...]"), STOP. Tell the user: "Your experience library is not filled in. The morning briefing depends on it for resume tailoring and fit scoring. Run `Help me build my experience library` first, then re-run the briefing."
2. **career-plan.md** -- If this file is empty or still contains only template placeholders, STOP. Tell the user: "Your career plan is not filled in. The briefing uses it for fit scoring and positioning. Fill in career-plan.md first, then re-run the briefing."
3. **target-companies.md** -- If this file is empty or still contains only template placeholders, STOP. Tell the user: "Your target companies list is not filled in. The briefing scans these companies for new roles. Fill in target-companies.md first, then re-run the briefing."

If any of the three checks fail, do NOT proceed. The briefing will produce low-quality or useless output without these files.

## Role Type Detection

Read `career-plan.md` to detect the user's target function (PM, SWE, Design, Data Science, Marketing, CS/Sales). All sections below adapt based on the detected function:
- Part 1: Search for function-appropriate roles (not "PM/product postings" for non-PM users)
- Part 2: Target function-appropriate networking contacts (not PMs for non-PM users)
- Part 3: Generate function-appropriate work product prompts
- Pipeline Health: Use function-appropriate benchmarks and drill recommendations
- Interview Coaching: Reference function-appropriate mock types and question categories

---

Before anything else, calculate and display:

## Motivation & Status

Determine what week of the job search this is by counting from the earliest application date in app-tracker (or the creation date of the OS if no applications yet).

**If app-tracker.md does not exist or is empty:** Assemble pipeline data from alternative sources:
- From `target-companies.md`: Scan Status fields (e.g., "IN PROCESS," "REFERRAL SUBMITTED," "NOT STARTED") and the Summary by Status table.
- From `connection-tracker.md`: Extract referral dates and recent activity.
- From `interview-history.md`: Extract interview dates and companies.
- From `briefings/` folder: Check recent briefing files for logged activity.
- Use these to estimate application count, interview count, and pipeline status. Note in the output: "Pipeline stats assembled from target-companies.md and interview-history.md (no app-tracker.md found). For precise tracking, run `/app-tracker add` for each active application."

```
Week [N] of your search.

Stats since start:
- Applications submitted: [N]
- Interviews completed: [N]
- Offers received: [N]

[One sentence of contextual coaching. NOT generic motivation. Base it on actual data patterns. Examples:
- If callback rate is rising: "Your callback rate improved from X% to Y% over the last 2 weeks. The targeting changes are working."
- If interview volume is up: "3 interviews this week vs 1 last week. The networking investment is paying off."
- If it's early and volume is low: "Week 2. Volume is low but that's expected. The priority right now is building your referral network, not mass applying."
- If there's been a rejection: "[Company] passed, but your interview scores averaged 7.2/10. The performance is there -- keep going."
- If it's been a long search: "Week 8. Long searches test patience. Your conversion rate is actually above benchmark. Keep the system running."
]
```

---

## Part 1: New Roles

Search each company in target-companies.md for new PM/product postings from the last 24 hours. Check their careers pages and LinkedIn.

**[FUNCTION-ADAPTIVE]** Search for the user's target function postings, not PM postings. SWE: search for engineering roles. Design: search for design roles. CS: search for customer success roles. Etc.

### DATA QUALITY GATE
If web search is unavailable or returns errors for any company, skip that company and note it in the output as "[Company]: could not verify -- check manually." NEVER fabricate job listings. If you cannot find a real URL for a role, do not include it. Companies that fail search will be collected in the Search Failures section of the briefing output.

Prioritize checking:
- Companies where the user has connections (from connection-tracker.md) -- these have the highest conversion rate
- Companies in the top 20 of target-companies.md
- Companies that recently had funding rounds or product launches (from company research)

For each new role found:
1. Run the job-fit-scorer process (score 1-100 across 5 dimensions: skill match, seniority fit, culture signals, comp range, growth trajectory)
2. For roles scoring 70+:
   - Run the resume-tailor process using experience-library.md as the source
   - Calculate keyword coverage score (% of JD requirements matched)
   - Run the recruiter-reviewer sub-agent on the tailored resume
   - Run the ats-checker sub-agent on the tailored resume
   - Auto-correct any issues flagged by the sub-agents
   - Note all changes made during auto-correction
3. For roles scoring 60-69: flag as "Apply with referral only" and note which connections could refer
4. For roles scoring below 60: skip but log that they were reviewed

Surface the top 3 roles in the briefing, ranked by fit score.

---

## Part 2: Networking

Read connection-tracker.md and target-companies.md.

### New Connection Requests (25 total)

Identify companies in target-companies.md where the user has fewer than 4 connections logged in connection-tracker.md. These are coverage gaps.

Generate 25 connection requests, round-robin distributed across gap companies (don't send all 25 to one company).

**[FUNCTION-ADAPTIVE]** Target function-appropriate contacts for connection requests, not PMs.

For each person:
- One personalized message (300 characters max, LinkedIn limit)
- Must include: a specific reference to the person's work/background, a connection point (mutual connection, shared school, shared company, location, or something specific about their role), and the user's one-line qualifier
- Tone: warm, human, slightly casual. Not corporate. Not desperate.

### Follow-Ups (connections accepted in last 48 hours)

Check connection-tracker.md for connections that went from "requested" to "connected" in the last 48 hours.

For each newly accepted connection, draft a follow-up message:
- Thank them for connecting
- Reference something specific about their background
- Soft ask for a 15-minute conversation (not a referral -- too early)
- Under 500 characters

### Referral Nudges (stale requests)

Check connection-tracker.md and referral-tracker-template.md for:
- Referral requests sent 5+ days ago with no response: draft a gentle one-time nudge
- Roles applied to in the last 48 hours with no referral: identify the closest connection at that company and draft a referral request

For nudges:
- One message only. Short. Low pressure.
- Example: "Hey [Name], just checking in on the referral for the [Role] position. Totally understand if the timing doesn't work -- appreciate you either way."

---

## Part 3: For Top Roles

For each of the top 3 roles from Part 1 (scoring 70+), include:

### [Role Title] at [Company] (Fit Score: [X]/100)

**Why this is a strong match:**
[2-sentence summary of why this role scored high, highlighting the strongest dimensions]

**Tailored Resume:**
- Status: [Generated / Auto-corrected / Needs manual review]
- Keyword coverage: [X]% ([N]/[M] JD requirements matched)
- Recruiter review score: First impression [X]/10, Relevance [X]/10, Readability [X]/10
- ATS check: [PASS / PASS WITH WARNINGS / FAIL]
- Gaps identified: [list any JD requirements not matched by experience library]
- Changes made during auto-correction: [list specific changes]

**Referral Path:**
- Closest connection: [Name] at [Company] ([relationship strength])
- Draft referral message: [personalized message ready to send]
- If no connection: "No existing connection. Add to networking priority for this week."

**Work Product Prompt:**

**[FUNCTION-ADAPTIVE]** Generate function-appropriate work product prompts.

Ready-to-use prompt for `/work-product` to generate a 1-pager for this role:
```
/work-product [Company] [Role Title] get-interview
```
Research hooks to investigate before writing:
- [Specific thing to research about this company's product]
- [Specific recent event or launch to reference]
- [Specific user complaint or market dynamic to analyze]

---

## Output

Save everything to job-search-os/briefings/[YYYY-MM-DD]-briefing.md

Use this exact format for the saved file:

```markdown
# Morning Briefing - [Full Date, e.g., Monday, March 24, 2026]

## Week [N] | [Motivational line from above]

---

## Top Roles Today

### 1. [Role Title] at [Company] (Fit: [score]/100)
[2-sentence match summary]
**Resume:** [status + coverage score]
**Referral:** [connection name + draft message OR "No connection -- network first"]
**Work product prompt:** `/work-product [Company] [Role] get-interview`
**Research hooks:** [bulleted list]

### 2. [Role Title] at [Company] (Fit: [score]/100)
[Same structure]

### 3. [Role Title] at [Company] (Fit: [score]/100)
[Same structure]

### Other Roles Reviewed
- [Company] [Role] - Fit: [score] - [SKIP / APPLY WITH REFERRAL ONLY]
- [Company] [Role] - Fit: [score] - [SKIP / APPLY WITH REFERRAL ONLY]

### Search Failures
Companies that could not be checked (web search unavailable or returned errors):
- [Company]: could not verify -- check manually
- [Company]: could not verify -- check manually

---

## Networking To-Do (25 Connection Requests)

| # | Name | Company | Role | Message |
|---|------|---------|------|---------|
| 1 | [Name] | [Company] | [Role] | [300 char message] |
| 2 | [Name] | [Company] | [Role] | [300 char message] |
| ... | | | | |
| 25 | [Name] | [Company] | [Role] | [300 char message] |

---

## Follow-Ups (Newly Accepted Connections)

### [Name] at [Company]
Connected: [date]
Message: [draft follow-up]

---

## Referral Requests & Nudges

### New Referral Requests
- [Name] for [Role] at [Company]: [draft message]

### Nudges (5+ days, no response)
- [Name] for [Role] at [Company]: [draft nudge]

---

## Pipeline Summary

| Stage | Count | Details |
|---|---|---|
| Applied (waiting) | [N] | Oldest: [Company] ([N] days) |
| Referral requested | [N] | |
| Interview scheduled | [N] | Next: [Company] on [date] |
| Interviewed (awaiting result) | [N] | |
| Offer stage | [N] | |
| Rejected this week | [N] | |

**Active applications total:** [N]
**Interviews this week:** [N]

---

## Pipeline Health Check

Analyze the pipeline data above and flag the single biggest bottleneck:

- If applications > 10 this week but referrals = 0:
  "YOUR BOTTLENECK: Referrals. You're applying cold. Cold applications have a 3-5% callback rate vs 15-25% with referrals. Focus today's time on Part 2 networking and referral requests. Do not submit another application without a referral path."

- If referrals requested > 5 but interviews = 0:
  "YOUR BOTTLENECK: Resume/Positioning. Referrals are going in but not converting to interviews. Review whether your tailored resumes are matching JD requirements (check coverage scores). Consider running /linkedin-audit to check if your profile is reinforcing or contradicting your resume."

- If interviews > 2 this week but no /interview-prep has been run for them:
  "YOUR BOTTLENECK: Preparation. You have [N] interviews this week without prep packages. Run /interview-prep for each before doing anything else today. Unprepared interviews waste referral capital."

- If 0 applications this week:
  "YOUR BOTTLENECK: Volume. No applications yet this week. Review the roles above and submit at least 2 today. If no roles scored 70+, expand your target list or adjust career-plan.md criteria."

- If fewer than 3yr experience AND weeks 1-4:
  "EARLY-CAREER PACING: You have fewer than 3 years of experience and you're in the early weeks of your search. Prioritize referral coverage over application volume. Target 3-5 quality applications per week, each with a referral path. Create at least 1 work product this week for your top-priority role. Cold applications with a thin resume have near-zero callback rates -- every minute spent building a referral path or work product is higher ROI than another cold submission."

- If pipeline is healthy (applications steady, referral rate >40%, interviews converting):
  "Pipeline is healthy. [N] applications, [X]% referral rate, [N] interviews this week. Keep the system running. Focus today on: [most impactful single action based on pipeline state]."

- If career-plan.md indicates visa sponsorship needs AND connection-tracker.md shows near-zero US connections:
  "YOUR BOTTLENECK: US Network. You need referrals more than any other candidate type -- cold applications with an unfamiliar employer brand + visa requirement face double-filtering. Your connection tracker shows [N] US-based contacts across [M] target companies. Today: prioritize Part 2 networking. Send all 25 connection requests targeting alumni networks and diaspora connections at priority companies. Every US connection is an asset that compounds."

- If interview-history.md shows comp framing weakness (score below 7/10) AND there are interviews scheduled this week:
  "PREP ALERT: Comp question readiness. Your interview history shows comp framing scored [X/10]. Before [Company] interview on [date], rehearse: never state current non-US comp, always cite levels.fyi market rate. Run `/mock-interview behavioral` and ask for a compensation question drill."

- If career-plan.md indicates a career changer AND interview-history.md shows below 6/10 on "PM narrative," "product you built," or any career-change translation question:
  "CAREER CHANGER TRANSLATION BOTTLENECK: Your interview history shows [question type] scored [X/10]. This is the question that gatekeeps career changers. Before your next interview, run `/mock-interview behavioral` and practice this specific question 5 times. Your technical/research/consulting experience is strong -- the problem is translation, not substance. Also review: is your 'product you built' story specific enough? Does your TMAY lead with output, not background?"

- If career-plan.md shows a split strategy across multiple domains/tracks AND interviews are scheduled this week in DIFFERENT domains:
  "DUAL-TRACK INTERVIEW PREP: You have interviews at [in-domain company] and [out-of-domain company] this week. These require different prep. For [in-domain company]: lean into domain expertise, use technical vocabulary freely. For [out-of-domain company]: lead with transferable PM skills, translate every domain reference into universal language. Run `/interview-prep` for EACH company separately. Do not use the same TMAY for both."

- If career-plan.md shows the user is relocating AND connection-tracker.md shows limited connections in the target location:
  "RELOCATION-AWARE NETWORKING: You're targeting [location] but your connections are concentrated in [current location]. Allocate at least 40% of this week's connection requests to people based in [target location]. Prioritize alumni and diaspora connections there. If you have upcoming interviews with [target location] companies, mention in follow-ups that you're relocating -- this removes a filter."

- If career-plan.md shows the user's employers are not well-known in the target market:
  "BRAND AWARENESS: Your employers are not household names in the US. Every application and interview must include employer context. Verify: does your LinkedIn About section include parentheticals (e.g., 'Rakuten Ichiba -- $15B GMV, Japan's largest e-commerce marketplace')? Have you practiced your TMAY with these embedded naturally? If not, update your LinkedIn today and practice TMAY with a stopwatch."

**REMOTE-ONLY CANDIDATE MODE:** If career-plan.md shows the user has a remote-only preference or caregiver/family constraints, adjust the briefing:
- **Networking targets: filter for remote-friendly companies first.** When generating connection requests, prioritize companies in target-companies.md that are known remote-friendly or distributed-first (GitLab, Automattic, Zapier, Buffer, and any company flagged as remote-friendly in target-companies.md). Allocate at least 50% of the batch to contacts at confirmed remote-friendly companies.
- **Virtual networking section:** Suggest 1-2 relevant online communities, Slack groups, or Twitter/X spaces per week for the user to engage with. Examples by function: PM: Product School Slack, Lenny's Newsletter community, Mind the Product Slack. SWE: relevant Discord servers, open-source communities. Design: ADPList, Design Twitter. Match to the user's target function and domain. Format: "This week's virtual networking: Join [community name] ([link if known]) and comment on 2-3 threads relevant to [user's domain]."
- **Role scanning filter:** When scanning target companies for new roles in Part 1, filter for roles that explicitly mention "remote," "distributed," or "work from anywhere." Flag any role that says "hybrid" or "onsite" with a WARNING before scoring.

**CAREER RETURNER BRIEFING MODE:** If career-plan.md shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), adjust the briefing:
- **Return-to-work programs scan:** Search for active returnship programs at target companies. Check for: Path Forward partnerships, iRelaunch partnerships, company-specific return-to-work programs, and any "returner" or "returnship" postings. Include in the briefing: "Return-to-work programs: [list any found at target companies, or 'No active programs found at your target companies this week. Consider adding companies with known returnship programs to your target list: [suggest 2-3 companies with known programs].']"
- **Dormant network nudge:** If the user has not re-engaged any dormant connections this week (check connection-tracker.md for re-engagement messages sent in the last 7 days), prompt them: "NETWORK RE-ENGAGEMENT: You haven't re-engaged any former colleagues this week. Your pre-gap network is your strongest asset. Send 3-5 re-engagement messages today to former colleagues at or near your target companies. Template: 'Hi [Name], it's been a while! I'm exploring PM roles again -- would love to hear what you've been up to. Any chance you'd be open to a quick catch-up?'"
- **Gap-narrative improvement tracking:** After each interview, note how the gap was addressed and whether the approach is improving. If interview-history.md shows gap-related questions were asked, include in the briefing: "GAP NARRATIVE TRACKING: Your last interview at [Company] addressed the gap. Score: [X/10 if available]. [If improving: 'Your gap answer is tightening -- keep practicing.' If not improving or no data: 'Run `/mock-interview behavioral` and practice the gap question. Target: under 45 seconds, forward-looking, no over-justification.']"

**SENIOR-LEVEL / EMPLOYED CANDIDATE MODE:** If career-plan.md shows the user is at Director level or above AND is currently employed, adjust the briefing to reflect the reality of an executive conducting a confidential, time-constrained search:
- **Connection requests reduced to 5-10.** Executive networking is about quality, not volume. Target only VP/Director peers, CPO/SVP hiring executives, and executive recruiters. Do not generate 25 requests to mid-level PMs.
- **Company scanning limited to top 10.** Do not scan all companies in target-companies.md. Focus on the top 10 by priority rank. Senior roles open infrequently -- daily scanning of 50 companies is wasted effort. Instead, allocate that time to deeper research on the top 10.
- **Priority stack assumes 60-90 minutes daily.** Employed executives cannot spend 3 hours per day on their job search. Structure the priority stack for a focused 60-90 minute morning block: (1) respond to any active conversations or interview scheduling, (2) send 3-5 high-quality connection requests, (3) review any new roles at top 10 companies, (4) advance one work product or application. Everything else goes to the weekend.
- **Briefing condensed.** Skip the full 25-person connection request table. Instead, provide 5-10 targeted requests with strategic rationale for each. Skip the "Other Roles Reviewed" section for sub-70 roles -- only surface roles scoring 75+. The briefing should fit on one screen and be actionable in under 5 minutes of reading.
- **Confidentiality flag.** Add a note at the top of the briefing: "Employed executive mode: All outreach is framed as professional networking, not job searching. No 'Open to Work' signals. No references to being on the market in any generated messages."

**FOUNDER-TO-EMPLOYEE DAILY PREP:** If `career-plan.md` shows founder/CEO at a shut-down company, add these sections to the daily briefing:
- **Founder narrative drill:** When interviews are scheduled this week, include a daily prompt: "FOUNDER NARRATIVE DRILL: Practice your 30-second founder story. Lead with [Strong Brand] if applicable, then: what you built, what you learned, why THIS role. Time yourself -- if it exceeds 30 seconds, cut the middle. The interviewer needs to hear the arc, not the details."
- **Company-type awareness:** When generating connection requests, instruct to lead with strongest employer brand identity (not founder identity) for enterprise targets. Founder identity is OK for startup/VC targets. "CONNECTION REQUEST FRAMING: Today's requests target [N] enterprise companies and [N] startups. For enterprise targets, your message should lead with '[Strong Brand] PM' identity. For startup targets, leading with 'former founder' is an asset."
- **Comp anchor warning:** Before interviews, remind: "COMP ANCHOR WARNING: Your founder salary was $[X from career-plan.md]. Market rate for this role is $[Y from salary-research or target-companies]. Do NOT disclose founder comp. Use the market-rate framing from qa-master.md: 'Based on levels.fyi, [level] PMs at [company type] earn $[range]. I'm targeting within that range.'"
- **Stability signal:** Include a prompt to prepare one "team collaboration" story that demonstrates ability to work within a team structure (counters the "lone wolf founder" perception): "STABILITY SIGNAL PREP: Before today's interview, rehearse one story where you deferred to someone else's judgment, collaborated within an existing team structure, or supported another leader's vision. This counters the 'can this founder take direction?' concern."

**VETERAN / 15+ YEARS EXPERIENCE -- PROFILE-BASED REJECTION BOTTLENECK:** If career-plan.md shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, Cisco, Dell, Accenture, Deloitte, etc.), or explicit mention of age-related concerns, add these checks to the daily briefing:
- **Resume-stage rejection monitoring:** If app-tracker.md shows the user's resume-stage rejection rate exceeds 70% (rejections at the applied/screening stage before any human interview), surface a warning: "PROFILE BOTTLENECK: [X]% of your applications are being rejected at the resume stage. For candidates with 15+ years of experience, this often indicates profile-based filtering rather than qualification mismatch. Actions: (1) Run `/resume-tailor` with veteran compression rules for today's applications -- ensure graduation years are removed, only the last 10-12 years have detailed bullets, and the skills section leads with current tech. (2) Run `/linkedin-audit` for age-signal review -- check for outdated profile photo, graduation year visible, or early-career details that are too prominent. (3) Increase referral coverage to 80%+ -- referrals bypass the resume screen where profile-based filtering happens."
- **Experienced-hire-friendly companies:** Include 1-2 companies per day in the role scanning section that are known to value experienced hires. Look for signals in JDs: "seasoned leader," "deep expertise," "enterprise experience valued," "10+ years preferred," or companies with visibly senior leadership teams. Format: "EXPERIENCE-FRIENDLY: [Company] [Role] -- this JD explicitly values [signal]. Consider adding to your priority list."
- **Networking focus for veteran candidates:** When generating connection requests, prioritize people at target companies who also have 10+ years of experience (peers who understand the value of experience). Avoid over-indexing on connections with people early in their careers, as they may unconsciously filter based on seniority mismatch.
- **Interview energy prep reminder:** Before any interview this week, include: "ENERGY CHECK: Before today's interview at [Company], remember: lead with curiosity, not authority. Reference recent work (last 2-3 years) in your first answer. Avoid 'back in my day' framing. Match the interviewer's energy level."

---

## Interview Weakness Coaching

Read `context-library/interview-history.md` for documented weakness patterns. If any question type has an average score at or below 6/10, surface it here as a targeted coaching prompt -- regardless of whether the pipeline health check flagged preparation as the bottleneck.

- For each weakness pattern found (e.g., product sense 5/10, comp negotiation 6/10, "why leaving" narrative 6.5/10):
  "SKILL GAP: [Question type] is averaging [X]/10 across your interviews. This will cost you offers if not addressed. Today's drill: Run `/mock-interview [type]` and practice [specific question] until you score 7+. Estimated time: 30 minutes."

- If the user has interviews scheduled this week AND the scheduled company's likely interview format matches a documented weakness (e.g., a product sense round at a company when product sense is 5/10):
  "URGENT PREP: You have [interview type] at [Company] this week, and your [weakness] score is [X]/10. Run `/interview-prep [Company]` and `/mock-interview [type]` before the interview. This is your highest-priority action today."

- If no weakness patterns exist (fewer than 3 interviews logged), skip this section.

---

## Today's Priority Stack

Based on the pipeline health check and interview weakness coaching, here's your priority order for today:

1. [Highest priority action with specific instruction]
2. [Second priority]
3. [Third priority]
4. [If time permits]

Estimated time: [X] minutes total
```

---

## Notes for Cowork Configuration

- This prompt references files in the job-search-os/ directory. Make sure Cowork has access to the full project folder.
- The briefing saves output to the `briefings/` folder. Make sure this folder exists.
- If the briefing seems off (wrong companies, missing data), check that context-library files are populated.
- To run manually: paste this entire prompt into Claude Code and run it.
- Adjust the "25 connection requests" number based on your daily capacity. Some users prefer 10-15.

---

## Troubleshooting

**Briefing didn't run?**
- Check Cowork is enabled in Claude Desktop settings
- Check your internet connection (needs to fetch job board data)
- Check your context files exist and are readable

**Briefing shows no new roles?**
- Your target parameters might be too narrow (check `career-plan.md`)
- No roles matched this week (happens)
- Job boards have a lag (check manually on LinkedIn/Levels/etc)

**Briefing is taking too long?**
- This can happen if job board scraping is slow
- You can run parts manually instead of waiting for Cowork
- Or reduce the number of job sources in Part 1

---

This briefing system is your daily competitive advantage. Most people job search randomly. You're building a system.
