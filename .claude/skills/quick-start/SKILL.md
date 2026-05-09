---
name: quick-start
description: Vet any job description in 60 seconds. Red flags, salary estimate, interview intel, verdict (pursue / pursue with referral only / skip).
---

# /quick-start — Job Description Rapid Vet

## When to Use

You found a job posting and want to know in 60 seconds whether it's worth 2 hours of your time.

Input: Paste any job description (LinkedIn, Angel List, company careers page, recruiter message, doesn't matter).

Output: Red flags, salary estimate for your market, interview intel, verdict.

---

## Role

Analyze the JD like a skeptical hiring advisor. Your job is to save the user time by flagging obvious mismatches early.

---

## Process

### Step 1: Parse the JD (10 seconds)

Extract:
- **Company name**
- **Role title**
- **Seniority level** (IC, Senior, Manager, Director, VP — infer from title and scope)
- **Team scope** (how many people? what functions? distributed?)
- **Key responsibilities** (top 3)
- **Hard requirements** (explicit MUSTs)
- **Nice-to-haves** (PREFERRED qualifications)
- **Location & remote policy**
- **Salary mention?** (sometimes listed; more often in "competitive compensation")

### Step 2: Red Flags (20 seconds)

Scan for mismatch signals:

**Role-level mismatch:**
- JD says "Senior PM" but describes IC tasks only? → Red flag: unclear on level
- JD describes managing 0 people but requires "proven team leadership"? → Red flag: inconsistent
- Your target is Director but JD is Senior IC? → Ask: are you applying for growth or stepping back?

**Scope mismatch:**
- JD says "fast-growing startup" but was founded 2019? → Probably past hypergrowth, slower now
- "Built from the ground up" but revenue mentioned is $100M+? → Probably false or misleading
- "Product leadership opportunity" but no direct reports? → Watch: might be title inflation without scope

**Culture/pace red flags:**
- "Always on-call, fast-paced startup environment" → Red flag: potential burnout culture
- "We move fast and break things" → Red flag: lack of process, might be chaotic
- Entire JD is vague platitudes? → Red flag: role undefined, hiring manager unclear on what they want
- No mention of team, users, metrics, or actual work? → Red flag: they don't know what you'll do

**Hidden signals:**
- High salary advertised + "competitive benefits"? → Might be below market (salary covers weak equity)
- "Flexible work" instead of "remote" → Might mean: in-office most days
- "Unlimited PTO" → Red flag: often means take less than explicit policy
- Newly created role → Could be great (new, needed), could be experimental (might get cut)

### Step 3: Salary Estimate (10 seconds)

If salary is listed, note it. If not:
- **Series A–B startup, your target level:** €90–130K + 0.25–0.5% equity
- **Series C–E, your target level:** €120–180K + 0.1–0.3% equity
- **Series F+, your target level:** €150–220K + 0.05–0.1% equity
- **FAANG, your target level:** €200–300K + significant RSUs
- **Public tech, your target level:** €200–350K + significant RSUs
- **Early-stage (pre-Series A):** €60–100K + 1–3% equity

*Adjust for your market (Europe vs. US), your years of experience (±20%), and your function (growth/infra roles often pay more than core product).*

### Step 4: Interview Intel (10 seconds)

What type of interview process does this company likely run?

**Common patterns:**

| Company Type | Typical Process |
|--------------|-----------------|
| Y Combinator startup | Phone screen → take-home → founder chat → culture fit |
| Series B–D scaling startup | Phone screen → product spec → lunch with team → HM final |
| FAANG (Google, Meta, Apple) | 2-3 interviews: behavioral, product sense, technical/design |
| Stripe, Anthropic, top late-stage | Phone screen → take-home (real-world) → architecture → values |
| Enterprise (Salesforce, SAP) | Recruiting screener → hiring manager → panel → exec |

**Red flag:** If the JD doesn't mention interview process, ask in the first communication.

### Step 5: Verdict (10 seconds)

**PURSUE** if:
- Role title matches your target
- Scope / team size makes sense for your level
- Location / remote policy works for you
- No major red flags
- Company stage matches your preference
- Salary range is within your acceptable band
- You don't have 50+ other stronger applications in pipeline

**PURSUE WITH REFERRAL ONLY** if:
- Role is a maybe (slightly under/over your level, but could work)
- You have a warm contact at the company
- Cold application would get lost (large company, many applications)
- Location is slightly off but role is strong
- Salary is slightly low but everything else is great

**SKIP** if:
- Role is clearly above or below your level
- Major red flags (culture, stability, scope)
- Location makes no sense
- Salary is 20%+ below your minimum
- They're asking for things you explicitly said no to in career-plan.md
- You already have 30+ applications in early stages (focus on pipeline depth, not new applications)

---

## Output Format

```markdown
## Quick Vet: [Company Name] — [Role Title]

**Verdict:** PURSUE / PURSUE WITH REFERRAL ONLY / SKIP

---

### The Role
- **Title:** [JD title]
- **Level:** [IC / Senior IC / Manager / Director / VP]
- **Team size:** [X people reporting / peer to X functions]
- **Key work:** [Top 2-3 responsibilities in plain language]

### Red Flags
- [Flag 1 — why it matters]
- [Flag 2 — why it matters]
- [Flag 3 — why it matters]
- *(Or: No major red flags detected)*

### Salary & Logistics
- **Advertised salary:** [€X–Y or "Competitive"]
- **Estimated band for this level/company:** [€X–Y]
- **Location:** [City/Remote/Hybrid]
- **Your fit:** [Match / Slight mismatch / Major mismatch]

### Interview Process
**Likely process:** [Phone screen → take-home → design discussion → team lunch → offer]
**Preparation:** [What you should prep for this company type]

---

### Next Steps
**If PURSUE:**
1. Run `/job-fit-scorer` for detailed fit analysis
2. Research the company with `/company-research [Company Name]`
3. Check your network for referrals in `connection-tracker.md`
4. If you have a referral: use `/referral-request`
5. If cold application: use `/resume-tailor` to customize

**If PURSUE WITH REFERRAL ONLY:**
1. Find the referral first (check `connection-tracker.md` or ask your network)
2. Use `/referral-request [person + role]` to activate
3. Don't cold apply — referral or nothing

**If SKIP:**
[Brief explanation of why / what would need to change for you to reconsider]
```

---

## Example Output

```markdown
## Quick Vet: Anthropic — Senior Product Manager, Claude

**Verdict:** PURSUE

---

### The Role
- **Title:** Senior Product Manager, Claude
- **Level:** Senior IC PM
- **Team size:** You'd be the PM for Claude product; report to VP Product; coordinate with 20+ engineers, research team, safety team
- **Key work:** Define Claude's capabilities roadmap, lead experimentation on inference speed, coordinate safety & alignment research with product launches

### Red Flags
- None detected. This is a strong match.

### Salary & Logistics
- **Advertised salary:** Not listed
- **Estimated band for Series F+ AI company, Senior PM:** €200–280K + meaningful equity
- **Location:** San Francisco (remote negotiable)
- **Your fit:** Strong match (assuming SF or remote)

### Interview Process
**Likely process:** Phone screen (recruiter) → product case study (30 min, live) → architecture discussion (60 min, whiteboard or discussion) → culture fit (30 min) → executive round (if advancing)
**Preparation:** Prep on Claude's capabilities, competitive positioning vs. ChatGPT/Claude competitors, inference speed optimization strategies

---

### Next Steps
1. Check `connection-tracker.md` — do you know anyone at Anthropic?
2. If yes: use `/referral-request [person + "Senior PM Claude role"]`
3. If no: use `/resume-tailor [JD]` to customize your resume for this specific role
4. Run `/interview-prep [Anthropic]` if an interview is scheduled
```

---

## Quality Checks

**Good output:**
- Verdict is clear and justified
- Red flags are specific (not vague)
- Salary estimate is reasonable for company stage
- Next steps are actionable

**Bad output:**
- "Looks good, go for it" with no specifics
- Vague red flags ("probably a tough interview")
- Next steps are generic ("apply and see what happens")
