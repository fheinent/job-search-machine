---
name: briefing-part2-networking
description: Part 2 of daily briefing. Network intelligence, follow-ups, referral opportunities.
---

# Morning Briefing — Part 2: Networking
# Connection requests, follow-ups, referral nudges

**Time:** 7:10 AM (runs 10 min after Part 1) | **Duration:** 3-5 min | **Output:** `briefings/briefing-{DATE}-part2-networking.md`
> This part runs independently. It reads Part 1 output if available for role context.

---

Read all files in the job-search-os/context-library/ folder. Also read job-search-os/CLAUDE.md for system rules. If today's Part 1 output exists at `briefings/[YYYY-MM-DD]-part1-roles.md`, read it for top role context.

## Quality Gate

Verify these files contain real data (not template placeholders):
1. **connection-tracker.md** -- Needed for follow-ups and referral nudges. If empty, networking will be limited to new outreach only.
2. **target-companies.md** -- Needed to identify coverage gaps. If empty, STOP and say: "Fill in target-companies.md first."
3. **career-plan.md** -- Needed for function detection and persona modes. If empty, STOP and say: "Fill in career-plan.md first."

## Role Type Detection

Read `career-plan.md` to detect the user's target function. Target function-appropriate networking contacts (not PMs for non-PM users).

---

## New Connection Requests

Identify companies in target-companies.md where the user has fewer than 4 connections in connection-tracker.md. These are coverage gaps.

**Default: 25 connection requests**, round-robin distributed across gap companies (do not send all 25 to one company).

**SENIOR-LEVEL / EMPLOYED MODE:** If career-plan.md shows Director+ AND currently employed, reduce to 5-10 requests. Target only VP/Director peers, CPO/SVP hiring executives, and executive recruiters. Provide strategic rationale for each. Add confidentiality note: "Employed executive mode: All outreach framed as professional networking, not job searching. No 'Open to Work' signals."

**REMOTE-ONLY MODE:** If career-plan.md shows remote-only preference, prioritize remote-friendly companies (GitLab, Automattic, Zapier, Buffer, and any flagged in target-companies.md). Allocate at least 50% of batch to confirmed remote-friendly companies. Also suggest 1-2 virtual communities: PM: Product School Slack, Lenny's community. SWE: Discord servers, open-source communities. Design: ADPList. Format: "This week's virtual networking: Join [community] and comment on 2-3 relevant threads."

**VETERAN / 15+ YEARS MODE:** If career-plan.md shows 15+ years or legacy/enterprise employers, prioritize connections who also have 10+ years of experience. Avoid over-indexing on early-career contacts.

**FOUNDER-TO-EMPLOYEE MODE:** If career-plan.md shows founder/CEO at shut-down company, frame connection requests based on target company type. Enterprise targets: lead with strongest employer brand identity. Startup targets: leading with "former founder" is an asset. Format: "CONNECTION REQUEST FRAMING: [N] enterprise targets, [N] startup targets."

**CAREER RETURNER MODE:** If career-plan.md shows a career gap, check if user has re-engaged any dormant connections this week. If not: "NETWORK RE-ENGAGEMENT: Send 3-5 messages to former colleagues at or near target companies. Template: 'Hi [Name], it's been a while! I'm exploring [function] roles again -- would love to hear what you've been up to. Any chance you'd be open to a quick catch-up?'"

For each connection request:
- One personalized message (300 characters max, LinkedIn limit)
- Must include: specific reference to the person's work/background, a connection point (mutual connection, shared school, shared company, location, or role-specific detail), and user's one-line qualifier
- Tone: warm, human, slightly casual. Not corporate. Not desperate.

Output as table:
| # | Name | Company | Role | Message |
|---|------|---------|------|---------|

---

## Follow-Ups (Connections Accepted in Last 48 Hours)

Check connection-tracker.md for connections that went from "requested" to "connected" in the last 48 hours.

For each newly accepted connection, draft a follow-up:
- Thank them for connecting
- Reference something specific about their background
- Soft ask for a 15-minute conversation (not a referral -- too early)
- Under 500 characters

---

## Referral Nudges (Stale Requests)

Check connection-tracker.md and referral-tracker-template.md for:
- **Referral requests sent 5+ days ago with no response:** Draft a gentle one-time nudge. Short. Low pressure. Example: "Hey [Name], just checking in on the referral for the [Role] position. Totally understand if the timing doesn't work -- appreciate you either way."
- **Roles applied to in the last 48 hours with no referral:** Identify closest connection at that company and draft a referral request.

---

## Military Networking

If `career-plan.md` shows military background, add:
- 1-2 veteran-to-tech events, communities, or networking opportunities this week (Shift.org, VetsinTech, Service2Software, BreakLine, Hiring Our Heroes, Military MBA networks)
- Defense tech hiring events or veteran-specific career fairs
- Fellow military transitioners at target companies who recently posted on LinkedIn

Format: "VETERAN NETWORKING: [Event/Community] -- [date if applicable] -- [why relevant]. Action: [specific thing to do today]."

If pursuing BOTH defense tech and general tech, split networking into dual tracks:
- **Defense Tech Track:** Target defense tech veteran communities, clearance value emphasized
- **General Tech Track:** Target general communities and military-to-tech transitioners at general tech companies

---

## Output

Save everything to `job-search-os/briefings/[YYYY-MM-DD]-part2-networking.md` using this format:

```markdown
# Part 2: Networking - [Full Date]

## Connection Requests ([N] total)

| # | Name | Company | Role | Message |
|---|------|---------|------|---------|
| 1 | [Name] | [Company] | [Role] | [300 char message] |
| ... | | | | |

## Follow-Ups (Newly Accepted)

### [Name] at [Company]
Connected: [date]
Message: [draft follow-up]

## Referral Requests & Nudges

### New Referral Requests
- [Name] for [Role] at [Company]: [draft message]

### Nudges (5+ days, no response)
- [Name] for [Role] at [Company]: [draft nudge]
```

---

## Sample Output

**Example output from May 8, 2026 for Monica Vega (Staff PM, infrastructure focus):**

```markdown
# Part 2: Networking - Wednesday, May 8, 2026

## Connection Requests (12 total this week)

| # | Name | Company | Role | Message |
|---|------|---------|------|---------|
| 1 | Alex Torres | Databricks | Senior PM, Distributed Systems | Alex, saw your recent talk on cost optimization at QCon. That's the exact problem I've been solving at AcmeAI. Would love to grab coffee + chat about infrastructure challenges. |
| 2 | Sam Reyes | Databricks | PM, Platform | Your product blog on Lakehouse architecture is sharp. Infrastructure isn't my typical angle, but your approach to data pipeline design maps to my API platform work. Quick 15-min? |
| 3 | Priya Sharma | Vercel | Head of Product, Infrastructure | Following your build in public — Edge Functions DX reminded me of the SDK strategy work I led at Amadeus. Would be great to learn from what you're building. |
| 4 | Mike Chen | Anthropic | Product Manager | Your team's approach to API developer experience caught my attention. I've built similar platforms at scale. Would love to understand your current bottlenecks. |
| 5 | Elena Brooks | Retool | Senior PM | I know Jamie Gin who's at Retool; he mentioned your platform direction. I've optimized infrastructure APIs for developer adoption and think there's overlap. Would be good to sync? |
| 6 | Carlos Rodriguez | Stripe | Head of Payments Product | Noticed your recent hiring for infrastructure roles. I've navigated infrastructure scaling in fintech (Amadeus + AcmeAI) and sense there might be interesting problems you're solving. Open to a chat? |

(6 more requests queued for other companies in Tier 2: Elastic, GitLab, MongoDB, Supabase, Fly.io, Linear)

---

## Follow-Ups (Newly Accepted)

### Sarah Chen at Databricks
**Connected:** May 7, 2026 (from ProductCon introduction message sent May 5)

**Draft follow-up message:**
"Sarah, thanks for connecting! I've been thinking about your API design talk from ProductCon — specifically the part on latency optimization across distributed teams. I've spent the last 3 years solving similar problems at AcmeAI (platform API serving 100K+ concurrent users). Would be great to grab 15 minutes and learn what's top of mind on your team right now."

---

### Jordan Liu at Elastic
**Connected:** May 6, 2026 (from cold outreach message sent May 1)

**Draft follow-up message:**
"Jordan, thanks for the quick connect! I was impressed by your recent post on observability at scale — that's exactly what we're tackling at AcmeAI. Would love to hear your perspective on how you're thinking about cost/performance trade-offs in search infrastructure. Open for a quick 15-min call this week?"

---

## Referral Requests & Nudges

### New Referral Requests (from Part 1 top roles)

**Databricks (Vector DB PM role):**
- **Referrer:** Sarah Chen (PM, Distributed Systems at Databricks)
- **Draft message:** "Sarah, I came across the Principal PM role for Vector DB — that's exactly the intersection of infrastructure + AI that I find most interesting. Would you be open to introducing me to the hiring manager? Happy to send you my thinking on the role first, or jump on a quick call to discuss fit."

**Vercel (Senior PM, Infrastructure):**
- **Referrer:** (No direct connection; flagged for networking) Priority: Connect with someone on Vercel engineering or PM team via mutual connection (check Stripe PM who went to Vercel)

---

### Nudges (5+ days, no response)

**Retool referral (May 1 request):**
- **Referrer:** Marco Vidal (Product Lead at Retool; known from startup cohort)
- **Nudge message:** "Hey Marco, just checking in on the Retool referral for the Senior PM role we discussed. Totally understand if now isn't the right time — either way, appreciate you thinking about it. Would love to connect regardless of the role status."

---

## Networking Wins This Week

- Sarah Chen connected immediately (warm intro context helped)
- Jordan Liu responded within 48h (cold outreach to people who post about your specialty works)
- Marco Vidal acknowledged but hasn't submitted referral yet (nudge sent)

## Quick Wins for Today

1. **Send follow-up messages to Sarah and Jordan** (2 min)
2. **Reach out to 3 people from your Databricks list** (8 min)
3. **Send nudge to Marco** (1 min)

Total time investment: ~15 min
```

---

## Handoff

When Part 2 is done, Part 3 runs in ~10 min: `/briefing-part3-coaching`
