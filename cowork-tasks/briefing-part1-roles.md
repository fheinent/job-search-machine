---
name: briefing-part1-roles
description: Part 1 of daily briefing. Scan for new roles, score them, recommend tailor order.
---

# Morning Briefing — Part 1: Roles

**Time:** 7:00 AM | **Duration:** 5-7 min | **Output:** `briefings/briefing-{DATE}-part1-roles.md`
> This part runs independently. Parts 2 and 3 reference its output.

---

## What This Does

Scans job boards for roles matching your criteria, scores them, and tells you which ones to tailor first.

**Input:** Your `career-plan.md` (targets) + last 24h of job postings  
**Output:** Ranked list of new roles with match scores + tailor recommendations

---

## Quality Gate

Before running, verify that **experience-library.md**, **career-plan.md**, and **target-companies.md** contain real data (not template placeholders like `[FILL IN]`). If any of them are empty, STOP and tell the user to fill them in.

---

## Role Type Detection

Read `career-plan.md` to detect the user's target function (PM, SWE, Design, Data Science, Marketing, CS/Sales). All sections below adapt to the detected function. Search for function-appropriate roles, not PM roles by default.

---

## Motivation & Status

Determine what week of the job search this is by counting from the earliest application date in app-tracker (or OS creation date if no applications yet).

**If app-tracker.md does not exist or is empty:** Assemble pipeline data from `target-companies.md` (Status fields, Summary by Status table), `connection-tracker.md` (referral dates), `interview-history.md` (interview dates), and `briefings/` folder (recent activity). Note: "Pipeline stats assembled from alternative sources. For precise tracking, run `/app-tracker add` for each active application."

Display:
```
Week [N] of your search.
Stats since start: Applications: [N] | Interviews: [N] | Offers: [N]
[One sentence of data-driven coaching -- NOT generic motivation. Base it on actual patterns.]
```

---

## New Roles Scan

Search each company in target-companies.md for new postings in the user's target function from the last 24 hours. Check careers pages and LinkedIn.

**DATA QUALITY GATE:** If web search is unavailable or returns errors for a company, skip it and note: "[Company]: could not verify -- check manually." NEVER fabricate job listings. If you cannot find a real URL, do not include it.

**Prioritize checking:**
- Companies where the user has connections (from connection-tracker.md)
- Top 20 companies in target-companies.md
- Companies with recent funding rounds or product launches

**SENIOR-LEVEL / EMPLOYED MODE:** If career-plan.md shows Director+ level AND currently employed, scan only the top 10 companies and only surface roles scoring 75+.

**REMOTE-ONLY MODE:** If career-plan.md shows remote-only preference, filter for roles mentioning "remote," "distributed," or "work from anywhere." Flag "hybrid" or "onsite" roles with a WARNING before scoring.

## Scoring & Tailoring

For each new role found:
1. Run job-fit-scorer (score 1-100 across 5 dimensions: skill match, seniority fit, culture signals, comp range, growth trajectory)
2. **Roles scoring 70+:**
   - Run resume-tailor using experience-library.md as source
   - Calculate keyword coverage score (% of JD requirements matched)
   - Run recruiter-reviewer sub-agent on the tailored resume
   - Run ats-checker sub-agent on the tailored resume
   - Auto-correct flagged issues and note all changes
3. **Roles scoring 60-69:** Flag as "Apply with referral only" and note which connections could refer
4. **Roles below 60:** Skip but log that they were reviewed

Surface the top 3 roles ranked by fit score.

## Top Role Cards

For each of the top 3 roles (scoring 70+), include:

### [Role Title] at [Company] (Fit Score: [X]/100)

**Why this is a strong match:** [2-sentence summary highlighting strongest dimensions]

**Tailored Resume:**
- Status: [Generated / Auto-corrected / Needs manual review]
- Keyword coverage: [X]% ([N]/[M] JD requirements matched)
- Recruiter review: First impression [X]/10, Relevance [X]/10, Readability [X]/10
- ATS check: [PASS / PASS WITH WARNINGS / FAIL]
- Gaps: [JD requirements not matched by experience library]
- Auto-correction changes: [list specific changes]

**Referral Path:**
- Closest connection: [Name] at [Company] ([relationship strength])
- Draft referral message: [personalized message ready to send]
- If no connection: "No existing connection. Add to networking priority for this week."

**Work Product Prompt:**
Function-appropriate prompt for `/work-product`:
```
/work-product [Company] [Role Title] get-interview
```
Research hooks:
- [Specific thing to research about this company's product]
- [Specific recent event or launch to reference]
- [Specific user complaint or market dynamic to analyze]

**EXPERIENCE-FRIENDLY (Veteran Mode):** If career-plan.md shows 15+ years or legacy/enterprise employers, flag roles with signals like "seasoned leader," "deep expertise," "10+ years preferred." Format: "EXPERIENCE-FRIENDLY: [Company] [Role] -- JD values [signal]."

---

## Output

Save everything to `job-search-os/briefings/[YYYY-MM-DD]-part1-roles.md` using this format:

```markdown
# Part 1: Roles - [Full Date, e.g., Monday, March 24, 2026]

## Week [N] | [Motivational line]

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

### Search Failures
- [Company]: could not verify -- check manually
```

---

## Running This Task

### Via Cowork (Automated)
Part of `/daily-morning-briefing`. Runs at 7:00 AM.

### Manual Trigger
```
/briefing-part1-roles
```

---

## Sample Output

**Example output from May 8, 2026 for Monica Vega (Staff PM, infrastructure background):**

```markdown
# Part 1: Roles - Wednesday, May 8, 2026

## Week 2 | You've applied to 3 roles so far. Conversion is low — time to focus on referrals or bigger-name companies.

## Top Roles Today

### 1. Principal Product Manager — Vector DB Platform at Databricks (Fit: 88/100)

Databricks is actively hiring for the vector DB team (just launched Mosaic AI). Your infrastructure background + API design experience maps perfectly. Only gap: no explicit vector DB experience, but it's a learning curve, not a skill gap.

**Resume:** Generated (vector DB keywords added). Keyword coverage: 94% (33/35 JD requirements matched). Recruiter review: 8/10 relevance. ATS: PASS. Auto-corrected: Added "vector search," "embedding optimization," "distributed indexing" from your Amadeus claims-processing architecture context.

**Referral:** You know a Databricks PM (Sarah Chen, met at ProductCon 2023). Strong connection. 
Draft: "Hi Sarah, saw the vector DB role opened up. Your team is solving exactly the problem I've been thinking about at AcmeAI — latency optimization for high-dimensional data. I'd love to chat about whether I'm the right fit. Would you be open to a quick intro with the hiring manager?"

**Work product prompt:** `/work-product Databricks "Principal PM Vector DB" get-interview`

**Research hooks:**
- Databricks' recent Vector Search GA launch (April 2026) and competitive positioning vs. Pinecone/Weaviate
- Customer complaints about vector DB latency in fintech use cases (your Amadeus angle)
- Your inference optimization work as case study for how you'd approach vector indexing

---

### 2. Senior Product Manager, Infrastructure at Vercel (Fit: 82/100)

Vercel is expanding the infrastructure team (Edge Functions, Deployments, Database). Your scaling background is a strong fit. Role is less senior than Databricks, but company is strong.

**Resume:** Generated. Keyword coverage: 87% (27/31). Recruiter review: 7/10. ATS: PASS WITH WARNINGS (dates need standardization). One auto-correction: standardized date format from "2023 - Present" to "June 2023 - Present."

**Referral:** No direct connection. Add to networking — you know a PM at Stripe who worked at Vercel (check connection-tracker.md).

**Work product prompt:** `/work-product Vercel "Senior PM Infrastructure" get-interview`

**Research hooks:**
- Vercel's competitive positioning on Edge Functions (vs. AWS Lambda@Edge, Cloudflare Workers)
- Developer DX friction points in their deploy pipeline (check GitHub discussions)
- Cost/latency tradeoffs in serverless architecture (your GPU scheduler work applies here)

---

### 3. Group PM, Developer Experience at Anthropic (Fit: 79/100)

Anthropic is building out product org around Claude API. Your developer platform + API design expertise applies. Only gap: no AI/ML infrastructure background, but DX principles transfer.

**Resume:** Generated. Keyword coverage: 81% (20/25). Recruiter review: 7/10. ATS: PASS. Auto-corrected: Added "API documentation," "developer workflows," "adoption metrics" as synonyms for your GraphQL platform work.

**Referral:** You met an Anthropic researcher at NeurIPS 2023 (acquaintance). Light connection. 
Draft: "Hi [Name], hope you're enjoying Anthropic's work on Claude. I've been following your research on model evaluation and got curious about how you're thinking about DX for the API. I've built developer platforms at scale (GraphQL SDKs, infrastructure APIs) and would love to understand the bottlenecks you're seeing. Would you be open to an intro with someone on the product team?"

**Work product prompt:** `/work-product Anthropic "Group PM Developer Experience" get-interview`

**Research hooks:**
- Claude API adoption bottlenecks (check their community forum, GitHub issues)
- Competitive DX positioning vs. OpenAI API (what's easier to integrate?)
- Your API design patterns from Amadeus as model for Claude platform

---

### Other Roles Reviewed

- **Stripe** | Senior PM, API Infrastructure | Fit: 73 | APPLY WITH REFERRAL ONLY — Role is strong fit but you have a warm contact (Stripe Partners manager from previous company).
- **Retool** | Senior PM, Internals | Fit: 68 | SKIP (below your level, but founder is warm connection — save for networking).
- **MongoDB** | Senior PM, Developer Experience | Fit: 65 | SKIP (interesting but apply only if you get referral).

### Search Failures

None today. All top 20 companies verified for new roles.

---

## Part 2 Coming Next

Networking scan (10 min): Which of today's 3 roles can you reach via referral? Who do you need to call first?
```

---

## Red Flags to Watch

🚩 **Same role listed from 3 sources** → Likely spam or repost → Skip  
🚩 **Role description is generic copy-paste** → Company doesn't care about fit → Lower priority  
🚩 **Role has been open >30 days** → Candidates rejected or they're being picky → Know what you're walking into  
🚩 **Salary is suspiciously low for level** → Might be EU pricing or bait-and-switch → Clarify before tailoring  

---

## Tips

1. **Speed over perfection:** This should take <10 min to scan and score. Don't overthink.
2. **Tailor URGENT same day:** Waiting means someone else tailors faster.
3. **Save links:** Use your `app-tracker.md` to log every role, even if you don't tailor it yet.
4. **Weekly pattern:** By Friday, you'll see which companies are hiring most in your space.

---

## Handoff

When Part 1 is done, Part 2 runs in ~10 min: `/briefing-part2-networking`
