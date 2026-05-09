---
name: hiring-manager-msg
description: Draft a concise hiring manager outreach message that leads with a work product, not the ask.
---

# /hiring-manager-msg - Hiring Manager Outreach Message

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In hiring manager outreach contexts, this means: never include private details in LinkedIn messages, emails, or subject lines sent to hiring managers.

## When to Use

Run `/hiring-manager-msg [role + work product link + optional prototype link]` when:
- You have completed a work product (via `/work-product`) and want to send it directly to the hiring manager on LinkedIn
- A referral contact shared the HM's name and you want to reach out with substance, not just "I applied"
- You identified the HM through LinkedIn research and want a cold outreach that stands out
- You are already in-process and want to send a follow-up to the HM with additional work

Do NOT use this skill if you have no work product to share. An empty-handed HM message is just another cold LinkedIn message. Run `/work-product` first.

**For career changers with no PM portfolio:** If the user has never shipped a product feature, they almost certainly have no PM work products yet. In this case:
1. STILL require a work product -- but coach the user on what counts. A consulting-style analysis reframed as a product analysis IS a valid work product. Examples: a competitive teardown, a market sizing exercise reframed as a TAM analysis for a product bet, a user journey audit with specific recommendations, or a mock PRD for an improvement to the company's product.
2. Suggest running `/work-product` with an explicit note that consulting deliverables can be adapted: "You ran McKinsey engagements that produced strategic recommendations. Reframe one as a product analysis: what would you build, how would you measure it, what's the 90-day roadmap?"
3. The qualification sentence (Part 4 of the message) should translate consulting experience into PM-legible language: "This comes from 6 years leading strategy engagements at McKinsey, including [specific engagement that maps to this product area]" -- not "I was a management consultant."

**UXR-to-PM HM outreach:** If `career-plan.md` shows a user research background transitioning to PM, use this framing approach for the qualification sentence: "My 6 years of user research at Spotify and DoorDash gave me something most PMs lack -- direct, methodological understanding of user behavior. I've been building on that foundation with product ownership experience, and your team's challenge of [specific problem from company research] is exactly where research-informed product thinking shines."

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

**Required arguments:**
- `[role]` -- the specific role title and company (e.g., "Senior PM, Growth at Notion")
- `[work product link]` -- a link to the work product you created (Google Doc, Notion page, etc.)

**Optional arguments:**
- `[prototype link]` -- a link to a working prototype, Figma file, or demo (if you built one)

**Required files (read automatically):**
- `@context-library/experience-library.md` -- for the one-sentence qualification (pulls strongest relevant metric)
- `@context-library/target-companies.md` -- for company context, product focus, recent news
- `@context-library/connection-tracker.md` -- to check if you have any mutual connections with the HM, or if someone referred you (reference the referral)

**Optional (read if available):**
- Company research notes from `/company-research` (if the user has run it for this company)
- The job description (for role-specific language)

## Process

### Step 1: Gather Context

1. Read `target-companies.md` for the company entry: product focus, recent news, hiring status.
2. Read `experience-library.md` and identify the single most relevant qualification for this role. One metric. One sentence.
3. Check `connection-tracker.md`:
   - If someone referred you, mention them by name ("Sarah Kim on your growth team suggested I reach out").
   - If you have a mutual connection, consider referencing them.
   - If neither, proceed with cold outreach -- the work product carries the weight.
4. If the user provided a JD, identify the specific team or problem area the role focuses on.
5. **Early-career framing:** If `experience-library.md` shows fewer than 3 years of experience, frame the qualification sentence as insight-driven, not authority-driven. Instead of "This comes from 5 years leading growth at [Company]" (authority), write "This comes from personally running 30+ experiments on onboarding funnels, including one that moved activation from 23% to 41%" (insight). Early-career candidates cannot lean on tenure or title -- they lead with what they learned and what they shipped.
6. **Domain-locked framing:** If the user's employer brand is unknown in the target market (whether because the employer is in a different country, a niche vertical, or simply not famous in tech), the qualification sentence must lead with the metric, not the company name. "This comes from growing activation 4x across 2M users" is strong regardless of where it happened. "This comes from my work at [Unknown Company]" gives the HM nothing to anchor on. Add employer context parenthetically only if it adds scale signal.
   - **DOMAIN-LOCKED DUAL-TARGET HM RULE:** If `career-plan.md` shows the user targets both in-domain and out-of-domain roles, generate TWO versions of the HM message: (a) In-domain version: lead with domain expertise as the primary qualification. (b) Out-of-domain version: lead with transferable PM skills, use domain expertise as a differentiating bonus rather than the primary selling point.
7. **Engineering career changer work product coaching:** If the user is an engineer transitioning to PM, coach them on work product format. Engineering work products (architecture docs, technical specs) need to be reframed as product work products. A valid PM work product from an engineer: a product strategy memo that identifies a user problem, proposes a solution with technical feasibility analysis, defines success metrics, and includes a phased roadmap. The technical depth is the differentiator -- but the framing must be product-first, not engineering-first.

### Step 2: Draft the Message

**Seniority-aware tone adjustment:** Check career-plan.md for the user's current level. If the user is Director level or above, adjust the tone of the entire message:
- **When the HM is at or below the candidate's level** (e.g., candidate is VP, HM is Director or Senior PM): The soft ask becomes peer-framed. Replace "Would love 15 minutes to walk through my thinking" with "Would be great to compare notes on [specific challenge]" or "Happy to trade perspectives on how to approach [problem]." The message should read as one senior leader offering to discuss a shared problem, not as a candidate requesting an audience.
- **The qualification sentence is shorter** at Director+ level, since background speaks for itself. One scope metric is sufficient: "I run the $150M commerce platform at [Company]" or "This comes from leading the 40-person product org at [Company]." Do not list multiple achievements or spell out years of experience. Executives summarize; they do not enumerate.
- **When the HM is above the candidate's level** (e.g., candidate is Director, HM is VP or CPO): Use the standard tone but with confident framing. The qualification sentence can be slightly longer to establish scope, but the soft ask remains conversational, not deferential.

The message has exactly five parts, in this order:

1. **The hook (1 sentence)** -- Name the specific problem or opportunity you wrote about in the work product. Not "I'm excited about the role." Instead: "I noticed [specific product issue or opportunity] and put together an analysis on how to approach it."

2. **The work product (1-2 sentences)** -- Describe what it is and link it. Be concrete about what is in it. Not "I wrote a doc." Instead: "It covers [topic], including [specific insight] and [specific recommendation]. Here's the link: [URL]."

3. **The prototype mention, if applicable (1 sentence)** -- If you built something, say what it does and link it. "I also built a quick prototype showing [what it demonstrates]: [URL]."

4. **The qualification (1 sentence)** -- One sentence establishing why your perspective is informed. Pull from `experience-library.md`. Include a metric. "This comes from [X years / specific experience] -- I [specific achievement with number] at [Company]."

**[FUNCTION-ADAPTIVE]** The work product should match the target function. SWE: technical architecture analysis, open-source contribution, engineering blog post. Design: UX audit, design exploration. Data Science: data analysis, model proposal. CS: CS program design, QBR framework, health score proposal. Marketing: GTM analysis, campaign proposal. Do NOT default to PM-style product analyses.

**[FUNCTION-ADAPTIVE]** Function-specific qualification sentence examples: SWE: "I designed the distributed payment system handling 12K TPS at Shopify, reducing failed transactions 34%." CS: "I drove 118% NRR across $45M in enterprise ARR, building the health score system from scratch." Design: "I rebuilt Spotify's design system, adopted by 50+ product teams and reducing design-to-dev handoff time 40%." Marketing: "I grew Lattice's inbound pipeline from $2M to $8M ARR in 18 months by rebuilding the demand-gen engine — SEO, paid search, and content-led nurture sequences. Your team's B2B growth challenge is exactly the problem I want to solve next." Data Science: "I built the recommendation engine at Spotify that drives 30% of daily streams, reducing cold-start time for new users by 60%. Your ML team's personalization challenges are right in my wheelhouse."

5. **The soft ask (1 sentence)** -- Not "Can I interview?" Not "Are you hiring?" Instead: "Would love 15 minutes to walk through my thinking and hear how your team is approaching this." or "Happy to discuss if any of this resonates with what your team is working on."

If someone referred you, insert a referral mention between the hook and the work product: "[Name] on your team suggested I reach out."

### Step 3: Validate Length

Hard limit: 150 words. Count them. If over, cut. The HM will read this on their phone between meetings. Every word must earn its place.

Priority for cutting:
- Remove adjectives first ("really excited" becomes "excited" becomes cut entirely)
- Remove qualifiers ("I think" "I believe" "perhaps")
- Remove anything that is about you instead of about the work product
- The work product link and the soft ask are non-negotiable -- never cut these

### Step 4: Adapt for Channel

Generate two versions:
- **LinkedIn InMail/message version** -- the full 150-word message
- **Email version** -- same content but with a subject line. Subject line format: "[Specific topic] -- analysis for [Team/Role]" (not "Application for Senior PM role")

## Output

```
## Hiring Manager Outreach: [HM Name, if known] -- [Role] at [Company]

**Referral path:** [Name referred you / Mutual connection: Name / Cold outreach]
**Work product:** [link]
**Prototype:** [link, or "none"]
**Key qualification:** [the one metric you're leading with]

---

### LinkedIn Version

> [message text]

**Word count:** [N]/150

---

### Email Version

**Subject:** [subject line]

> [message text]

**Word count:** [N]/150

---

## Next Steps
- [ ] Send the LinkedIn message (Tuesday-Thursday, 8-10am their time zone performs best)
- [ ] If no response in 5 days, send a one-line follow-up: "Wanted to make sure this didn't get buried -- the [topic] analysis is here: [link]. Happy to chat anytime."
- [ ] Update connection-tracker.md with the HM's info and outreach date
- [ ] If they respond, immediately suggest 2-3 specific times for a call
```

## Example

Input: `/hiring-manager-msg Senior PM Growth at Notion + https://docs.google.com/doc/notion-growth-analysis + https://figma.com/notion-prototype`

After reading context files and finding that Sarah Kim referred you:

### LinkedIn Version

> Sarah Kim on your growth team suggested I reach out. I dug into Notion's enterprise activation flow and noticed a drop-off pattern between workspace creation and first shared page -- put together an analysis with three approaches to closing that gap.
>
> Here's the doc: [link]. I also built a quick Figma prototype showing a guided first-share experience: [link].
>
> This comes from owning activation at [Company], where I moved 7-day retention from 23% to 41% with a similar first-run redesign.
>
> Would love 15 minutes to walk through my thinking and hear how your team is approaching this.

**Word count:** 104/150

## Quality Checks

- [ ] **The work product is mentioned before any self-promotion.** The first thing the HM reads should be about their problem, not about you. If the message starts with "I" or your name, restructure it.
- [ ] **Under 150 words.** Count them. No exceptions.
- [ ] **The hook names a specific problem.** Not "I'm interested in growth." Instead: "I noticed a drop-off between X and Y." The specificity signals you did actual research.
- [ ] **The qualification includes a number.** Not "I have growth experience." Instead: "I moved activation from 23% to 41%." One metric. From `experience-library.md`.
- [ ] **The ask is for a conversation, not a job.** "Would love to discuss" not "I'd like to be considered for" -- the work product makes the case. You are offering to share thinking, not asking for a favor.
- [ ] **Referral is mentioned if one exists.** If `connection-tracker.md` shows someone at this company referred you or connected you, name them. Social proof is the single strongest signal in a cold message.
- [ ] **No banned phrases.** Reject: "I'm passionate about," "I'd be a great fit," "I'm reaching out because," "I came across this role," "I believe my experience," "I'm a seasoned professional." These are noise. Cut them all.
- [ ] **The subject line (email version) is about the work, not the application.** "Enterprise activation analysis" not "Application for Senior PM role." The HM should open it out of curiosity, not obligation.
- [ ] **Both links are included and clickable.** If the user provided a work product link and a prototype link, both must appear in the message.

**FOUNDER-TO-EMPLOYEE FRAMING:** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, apply these adjustments:
- Lead with the insight about their product domain, not "I was a founder."
- Work product: suggest a 1-pager that shows the person can GO DEEP on a specific area (not a "here's how I'd run your whole product org" pitch -- that triggers "this person can't be managed" alarm).
- Proactively signal team-player orientation: "I'd love to contribute to [specific initiative] alongside your team."

**LEGACY EMPLOYER DE-EMPHASIS RULE (Veteran / 15+ years):** If career-plan.md shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, etc.), or explicit mention of age-related concerns, the outreach should lead with WHAT THEY DID, not WHERE THEY DID IT. Instead of: "As a VP Product at Oracle..." use "I led the modernization of a $200M enterprise platform, rebuilding the entire PM process around continuous discovery..." The company name comes second, after the impact.

**CAREER RETURNER HM OUTREACH RULE:** If career-plan.md shows a career gap > 1 year, apply these adjustments:
- Qualification sentence: MUST be achievement-anchored, NOT timeline-anchored. "I grew activation from 31% to 44% at [Company]" NOT "From 2019-2023, I grew..." Timelines draw attention to the gap; achievements draw attention to the impact.
- If the role is at a return-to-work program: can acknowledge the program context briefly. "I'm particularly excited about [Company]'s return-to-work program -- my 8 years in [domain] make me a strong candidate for [specific role]."
- NEVER lead with the gap or reference "returning to work" in the outreach. The message should read identically to any other strong candidate's outreach.
- Privacy guardrail: no personal reasons for career break. Do not include health, family, caregiving, or any other explanation for the gap. The HM message is about the work product and the value the candidate brings, not about explaining absence.

**REMOTE-ONLY HM OUTREACH RULE:** If `career-plan.md` shows remote-only preference:
- **Pre-outreach verification:** Before drafting, check the JD or role listing for remote policy. If the role says "hybrid," "on-site," or is ambiguous, flag: "WARNING: This role may not be remote-compatible. Verify remote policy before investing in work product and outreach." Do NOT send HM outreach for roles with confirmed non-remote policies.
- **Async-capability signal:** Subtly signal distributed work capability without making remote the focus. Example: "I've built async-first processes adopted across multiple teams -- standups replaced by written updates, decision logs that eliminated meeting bloat, and cross-timezone collaboration rituals that kept shipping velocity high." Lead with the PROCESS you built, not just that you worked remotely.
- "I've consistently delivered [metrics] while working in distributed teams -- including [specific async collaboration example]."
- Never mention WHY remote. PRIVACY GUARDRAIL applies.

**MILITARY-TO-PM HM OUTREACH RULE:** If career-plan.md shows military background, apply these adjustments:
- Lead with the TRANSFERABLE SKILL insight about the company's product, not "I was a military officer." The hook and work product must be product-focused. Military identity is supporting context, not the lead.
- Work product recommendation: suggest a 1-pager that demonstrates PM analytical skills using the company's domain -- especially powerful for military candidates who lack traditional PM portfolios. Frame it as: "I put together an analysis of [company's specific product challenge]" not "here is my military experience translated to PM."
- For defense tech HMs: can lean into shared military context. "My 6 years in military intelligence give me native understanding of the end-user problem space." Military experience is a primary asset in defense tech and should be featured prominently.
- For general tech HMs: pure civilian framing. Military experience mentioned only as supporting context (30% or less of the message). The qualification sentence should translate military scope into PM-legible language: "I led product decisions for analytical tools used by 200+ analysts daily" not "I was an S2 for a battalion."
- Clearance mention: for defense tech, include it as a relevant qualification. For general tech, omit unless the company does government work.
- Do NOT use military jargon in ANY HM message. No acronyms (S2, OPORDs, CONOPs, ISR, C2), no rank references, no unit designations. Every concept must be expressed in civilian business language.

**AGENCY-TO-IN-HOUSE DESIGN FRAMING:** If `career-plan.md` shows a design background at an agency or consultancy (IDEO, Frog, Pentagram, AKQA, McKinsey Design, BCG Digital Ventures, etc.) targeting in-house product roles:
- The qualification sentence should NOT default to in-house metrics (e.g., "design system adopted by 50+ teams"). Agency designers do not have those.
- Instead, lead with depth on ONE engagement that demonstrates product-level thinking: "At IDEO, I spent 8 months embedded with [Client]'s product team, shipping a [specific deliverable] that [measurable outcome]."
- Include a signal of long-term product interest: "I'm looking for the depth that comes from living with a product through launch and iteration."
- The work product should demonstrate sustained product thinking, not client-presentation polish.

**CS FIRST-TIME-MANAGER VP TARGETING:** If detected function is CS AND `career-plan.md` shows targeting VP/Director level AND no management experience:
- The qualification sentence must implicitly signal team-building readiness WITHOUT explicitly stating "I've never managed."
- Example: "I designed the QBR framework now used by 12 CSMs across 3 regions -- and I'm ready to build and lead the team that scales it further."
- The hook should lead with organizational impact (program design, process creation, framework adoption) rather than individual account metrics.
- Work product recommendation: a CS org design 1-pager or scaled playbook proposal -- this demonstrates management-level thinking before having the title.

**HEALTHCARE-TO-GENERAL-TECH DUAL-TARGET EXAMPLE:** When the domain-locked dual-target rule applies and the user's domain is healthcare/health-tech (Epic, Cerner, athenahealth, Veeva, etc.):
- In-domain version example: "7 years building Epic's API platform (200+ third-party integrations, 12M+ patient records processed daily) means I understand the regulatory and interoperability challenges your health-tech product faces at a molecular level."
- Out-of-domain version example: "I built an API platform connecting 200+ third-party applications on top of a monolithic legacy system -- that platform-thinking and integration complexity is exactly what your [product area] needs."
- Note: the out-of-domain version translates "Epic" into generic "API platform" language and drops healthcare jargon entirely. The metric (200+ integrations) transfers; the domain context does not.
