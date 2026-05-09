---
name: connection-request
description: Generate personalized LinkedIn connection requests for daily outreach, targeting coverage gaps across target companies.
---

# /connection-request - LinkedIn Connection Request Generator

## When to Use

Run `/connection-request [batch]` when:
- The morning briefing identifies networking gaps (companies with fewer than 4 connections)
- You want to start a daily outreach cadence of 25 connection requests
- You are entering a new target company into your pipeline and need to build a network there fast
- A company moved up in your priority list and you have zero connections

The `[batch]` argument is optional. If omitted, defaults to generating one full batch of 25 requests. If a number is provided (e.g., `/connection-request 10`), generates that many instead.

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

**Required files (read automatically):**
- `@context-library/connection-tracker.md` -- current connection state per company, relationship history, last contact dates
- `@context-library/target-companies.md` -- prioritized company list with product focus, recent news, and existing connections
- `@context-library/experience-library.md` -- your background, schools, past companies, skills, and story bank (used for finding authentic connection points)
- `@context-library/career-plan.md` -- level and function preferences (used to target people at the right seniority)

**User-provided (prompted if missing):**
- LinkedIn search results or people list for gap companies. Since Claude cannot search LinkedIn directly, prompt the user with this exact template for each gap company:

```
I need LinkedIn profiles to build connection requests for [Company Name]. Please run this LinkedIn search and paste the results (name, title, any recent post headline):

LinkedIn search: "[Company Name]" AND ("Product Manager" OR "PM" OR "Engineering Manager" OR "Design Lead") AND "[City if relevant]"

**[FUNCTION-ADAPTIVE]** Replace the search terms above with function-appropriate targets: SWE: "Staff Engineer OR Principal Engineer OR Engineering Manager OR Tech Lead". Design: "Design Lead OR Head of Design OR Senior Product Designer". Data Science: "Senior Data Scientist OR ML Engineer OR Analytics Lead OR Head of Data". Marketing: "Marketing Director OR VP Marketing OR Growth Lead". CS: "Director of CS OR VP Customer Success OR CS Manager OR CRO".

I need [N] people from [Company Name]. Mix of:
- [N] PMs at your level (Senior PM, PM)
- [N] PM one level up (Director, Group PM)
- [N] adjacent function (Eng Manager, Design Lead, Data Lead)
- [N] wildcard (Recruiter, different team PM, active poster)

For each person, note if they have any recent LinkedIn posts or shared background with you (same school, past company, city).
```

## Process

### Step 1: Identify Coverage Gaps

1. Parse `connection-tracker.md` and count connections per company. Also check for pending requests (entries where "LinkedIn connected: no" but a sent date exists) -- these people are already in-flight and must be excluded from this batch.
2. Cross-reference against `target-companies.md` priority rankings.
3. Flag every company with fewer than 4 connections as a "gap company."
4. Sort gap companies by priority rank (Rank 1 companies first).

**Cold-start handling:** If `connection-tracker.md` is empty or contains only template placeholders (no real people listed), do NOT try to spread across all target companies. Instead: select the top 5 companies from `target-companies.md` by priority rank, allocate 5 people per company, and tell the user: "Your connection tracker is empty. Starting with your top 5 priority companies. After this first batch gets responses, we'll expand to more companies in future batches."

### Step 2: Allocate Targets Across Gap Companies

1. Select the top gap companies (aim for 5-8 companies per batch).
2. Allocate 25 people total using round-robin distribution:
   - If 5 gap companies: 5 people each.
   - If 8 gap companies: 3 each, plus 1 extra for the top-ranked company.
   - Never more than 7 from one company in a single batch.
3. For each company, target a mix of seniority levels:
   - 1-2 PMs at your target level (peers you would work with)
   - 1 PM one level above (potential hiring managers)
   - 1 person from an adjacent function (engineering lead, design lead, data lead)
   - 1 wildcard (recruiter, PM from a different team, someone who posts actively on LinkedIn)

### Step 3: Find Connection Points

For each person, search for an authentic connection point. Check in this priority order:

1. **Mutual connections** -- check `connection-tracker.md` for shared contacts at the same company. If you know someone they know, reference it.
2. **Shared school** -- check `experience-library.md` for university or program overlap.
3. **Shared past company** -- check if they previously worked somewhere you worked.
4. **Location overlap** -- same city, especially if you are both transplants.
5. **Something specific about their work** -- a LinkedIn post they wrote, a product they shipped, a talk they gave, an article they published. This is the fallback, but it is the strongest hook when it is specific.

If no connection point can be identified, flag the person as "needs manual research" and skip. Do not generate a generic message.

**Batch recovery rule:** If more than 30% of the batch (8+ out of 25 people) fail the connection-point check, the batch is under-researched. Do NOT output a partial batch of 17 generic-ish messages. Instead:
- Output the messages that passed (with full quality).
- For the failed people, provide the user with specific research prompts: "For [Name] at [Company], check their LinkedIn activity from the last 30 days, or search for '[Name] [Company] talk OR blog OR podcast' -- I need one specific thing they said or did."
- Tell the user: "This batch has [N] people who need manual research before I can write strong messages. Complete the research and re-run, or swap in different people from the same companies."

### Step 4: Draft Each Message

For each of the 25 people, write a single connection request message that includes all four required elements:

1. **Proof of research** -- reference something specific about them (not their company, not their title -- something they personally did or said).
2. **Connection point** -- why you are reaching out to them specifically (mutual connection, shared school, their LinkedIn post, etc.).
3. **Qualifying yourself** -- one phrase that establishes credibility without bragging. Pull from `experience-library.md`. Match it to what they care about. **If fewer than 3 years experience, lead the qualifier with the most impressive METRIC, not title or company name.** "I grew activation 4x across 2M users" beats "I'm a PM at [Company]" when the company and title are not yet impressive. The metric does the credibility work that tenure cannot. **Career changer language rule:** If the user has no PM title in `experience-library.md`, frame the qualifying phrase in PM-relevant language, not in the title/function language of their current role. By background:
   - **Consulting:** Write "I've spent 4 years defining fintech product roadmaps and running user research at McKinsey" -- not "I'm an Engagement Manager at McKinsey."
   - **Engineering:** Write "I've spent 3 years shipping ML features and designing experiments that grew engagement 28%" -- not "I'm a software engineer at [Company]."
   - **UXR/Design:** Write "I've spent 4 years turning user research into shipped product changes that moved activation 3x" -- not "I'm a UX researcher at [Company]."
   The recipient is a PM; speak their language. Translate deliverables into PM equivalents in the qualifier. **Domain-locked qualifier:** If the user's experience is concentrated in one domain but the outreach target is at an out-of-domain company, use universal PM language in the qualifier, not domain jargon. "I grew a B2B onboarding funnel from 23% to 41% activation" works at any company. "I optimized healthcare claims processing workflows" only works at healthcare companies.
   **[FUNCTION-ADAPTIVE]** Function-specific qualifying phrase examples: SWE: "I designed the payment retry system handling 12K TPS at Shopify." Design: "I led the design system rebuild at Spotify serving 50+ product teams." Data Science: "I built the recommendation engine at Spotify driving 30% of daily streams." Marketing: "I grew Lattice inbound pipeline from $2M to $8M ARR." CS: "I drove 118% NRR across $45M in enterprise ARR at Salesforce." Use the function-appropriate language for the user's target role -- the recipient should recognize the qualifier as coming from someone in their function.
4. **Call to action** -- a soft, specific ask. Not "let's connect." Instead: "would love to hear how your team thinks about X" or "happy to share what we learned about Y."

**EXECUTIVE PEER OUTREACH RULE:** If career-plan.md shows the user is at Director level or above, replace the standard "qualifying yourself" element with "establishing shared strategic context." At this seniority, the recipient does not need to be convinced of your competence -- they need to understand why a conversation would be mutually valuable. Apply these adjustments:
- **Tone is peer-to-peer.** The message should read as one executive reaching out to another, not as a job seeker reaching out to a contact. No deference, no "I'd love to pick your brain," no implicit ask for help. Instead: "Would be great to compare notes on [shared strategic challenge]" or "Curious how your team is thinking about [industry trend relevant to both of you]."
- **Target selection shifts.** Do NOT target mid-level PMs or recruiters. At Director+ level, the outreach targets are: (1) VP/Director-level product peers at target companies who would be lateral colleagues, (2) CPO/SVP/Head of Product who would be the hiring executive, (3) senior leaders in adjacent functions (VP Engineering, VP Design) who would be cross-functional partners. Targeting a Senior PM when you are a VP creates an awkward dynamic and signals desperation.
- **Qualifying phrase is shorter.** At this level, one scope metric suffices: "I run the $150M commerce platform at [Company]" or "I lead the 40-person product org at [Company]." Do not list accomplishments -- executives summarize, they do not enumerate.
- **Connection points shift to strategic interests.** Instead of referencing their LinkedIn post about a product feature, reference industry-level observations: market shifts, competitive dynamics, organizational challenges at scale. "I noticed [Company] is expanding into [area] -- I built a similar motion at [my company] and would love to compare approaches."
- **Recruiter targeting exception.** The one exception to "do not target recruiters" is executive recruiters (VP+ search firms, retained search partners). These are valid targets for Director+ candidates and should receive a different message format: lead with your current scope and what you are exploring, not with research about them.

### Step 5: Validate and Output

1. **Character-count enforcement (CRITICAL):** LinkedIn's connection request limit is 300 characters. LLMs estimate character counts imprecisely, so apply these rules:
   - **Target 280 characters maximum** to leave a 20-character safety buffer. This accounts for estimation error.
   - Count characters by examining each word's length explicitly. Do not round or estimate.
   - If a message is between 280-300 characters, attempt to shorten it. Cut filler words ("really," "just," "actually"), shorten phrases ("would love to" -> "happy to"), or remove one qualifying detail.
   - If a message is over 300 characters, it MUST be rewritten shorter. Do not present it to the user.
   - Display the character count for every message so the user can verify before sending.
   - **Best practice:** Shorter messages (200-250 chars) have higher accept rates than messages pushing the limit. Aim short.
2. Verify no two messages for the same company use the same connection point template.
3. Verify no message could be sent to a different person and still make sense. If it could, it is too generic. Rewrite.

## Output

Return a numbered list formatted as:

```
## Connection Request Batch - [Date]

Gap companies targeted: [list]
Total requests: 25

---

### 1. [Full Name]
**Company:** [Company] | **Role:** [Their Title]
**Connection point:** [mutual connection / shared school / their post about X / etc.]
**Message:**
> [connection request text, under 300 characters]

**Character count:** [N]/300

---

### 2. [Full Name]
...
```

After the list, include:

```
## Post-Send Checklist
- [ ] Send all 25 requests on LinkedIn
- [ ] Update connection-tracker.md with sent date for each person
- [ ] Note which connection point you used (for follow-up context)
- [ ] Flag any that were "needs manual research" for tomorrow's batch
```

### LinkedIn Rate-Limit Warning

LinkedIn may restrict accounts that send 20+ similar connection request messages in a single day. This can result in temporary send limits or account warnings. Mitigations:

1. **Cap daily volume:** Limit to 15-20 personalized requests per day for non-Premium accounts. LinkedIn Premium and Sales Navigator accounts have higher thresholds, but still exercise caution above 25/day.
2. **Vary message structure:** Rotate across 4-5 distinct templates. Some messages should be 1-sentence. Some should lead with a question. Some should lead with a compliment. Some should reference a specific post. Structural variety reduces pattern-detection risk.
3. **Space throughout the day:** Do not send all requests in a single 10-minute burst. Spread them across morning, midday, and afternoon. If using a scheduling tool, stagger by 15-30 minutes.
4. **Mix in no-message requests:** For strong mutual connections (2+ shared connections), send the request with no custom message at all. LinkedIn's default "I'd like to connect" is fine when the mutual connection speaks for itself. This breaks up the pattern of always-customized messages.
5. **If the user reports a restriction:** Reduce to 5-10 requests per day for 2 weeks. After the restriction lifts, ramp back up gradually (10/day for a week, then 15/day, then back to 20/day). Do not immediately return to full volume.

## Example

Input: `/connection-request`

After reading files, Claude identifies that Notion (Rank 3) has 1 connection, Figma (Rank 5) has 0, and Anthropic (Rank 1) has 2.

Sample output for one person:

```
### 7. Marcus Chen
**Company:** Notion | **Role:** Senior PM, Core Product
**Connection point:** His recent LinkedIn post about block-based editing trade-offs
**Message:**
> Marcus -- your post on the block model migration trade-offs was sharp, especially the backwards compatibility piece. I led a similar data model migration at [Company] (serving 2M users). Would love to compare notes on how your team handled it.

**Character count:** 271/300
```

## Quality Checks

Before finalizing the batch, validate every message against these rules:

- [ ] **Under 300 characters.** No exceptions. LinkedIn silently truncates.
- [ ] **No generic openers.** Ban: "I came across your profile," "I see we're both in product," "I'd love to connect," "I admire your work."
- [ ] **Proof of research is specific.** If you removed the person's name, could this message apply to anyone else at their company? If yes, rewrite.
- [ ] **Connection point is real.** It references a verifiable thing -- a post, a mutual contact, a shared school, a specific product they shipped.
- [ ] **Qualifying phrase draws from experience-library.** Do not invent credentials. Use real experience.
- [ ] **Call to action is low-pressure.** Not "Can we get coffee?" on a first touch. Instead: "happy to share" or "curious how your team thinks about X."
- [ ] **Tone is warm and human.** Read it out loud. If it sounds like a LinkedIn automation bot, rewrite. Slight casualness is good. Corporate speak is death.
- [ ] **No two messages in the batch use identical structure.** Vary the order of elements. Some lead with the connection point, some lead with research, some lead with a question.
- [ ] **Round-robin distribution is maintained.** No company has more than 7 people. Gap companies with higher priority get +1 allocation if numbers do not divide evenly.

### Cultural Adaptation
If the user's career-plan.md indicates a target market outside the US or the user mentions an international search:
- **UK/Western Europe:** Slightly more formal first contact. Use full name. Less casual humor. Professional but warm.
- **Germany/Nordics:** More formal. Lead with professional credentials. Direct but not overly friendly on first contact.
- **Japan/Korea:** Formal. Include your current title and company. Reference institutional connections (alumni, mutual employers) prominently. Avoid first-name-basis.
- **India:** Warm and direct. Alumni connections are extremely high-value. Reference shared educational institutions prominently.
- **LATAM:** Warm tone works well. Slightly more personal than US standard.

For any international search: if the target company is a US company with international offices, use US-style messaging regardless of the user's location.

### Remote-Only Candidate Networking Strategy

If `career-plan.md` shows the user has a remote-only preference or caregiver/family constraints, apply these adjustments to the connection request strategy:

- **Prioritize connections at companies with known remote culture.** When allocating the batch across gap companies, give priority weighting to companies with distributed-first cultures (GitLab model companies: GitLab, Automattic, Zapier, Buffer, Doist, Basecamp, InVision, Help Scout, and others identified in target-companies.md as remote-friendly). These companies are more likely to have roles matching the user's remote-only constraint.
- **Non-hub city networking focus:** If the user is in a non-hub city (not SF, NYC, Seattle, Austin, or other major tech hubs), networking should focus on online communities rather than local meetups. Adjust the connection point search to prioritize: (1) shared online communities (Slack groups, Twitter/X spaces, LinkedIn groups for remote PMs), (2) shared interests in distributed work practices, (3) people who have posted about remote work culture or async practices. Do NOT suggest local meetups or in-person coffee chats as the default -- suggest virtual alternatives.
- **Connection point adaptation:** When writing messages to people at remote-first companies, the connection point can reference the company's distributed culture as a shared interest: "I've been following how [Company] approaches async decision-making -- your post about [specific topic] resonated." This signals culture fit without making "remote" the entire identity.

### Career Gap / Returner: Dormant Network Reactivation Mode

If `career-plan.md` shows a career gap > 1 year, apply these adjustments:

- **Networking priority #1: Re-engage EXISTING connections before making new ones.** The user's pre-gap network already knows their work quality. These warm connections have 3-5x the conversion rate of cold outreach for returners. Before generating a standard batch of 25 new connection requests, check `connection-tracker.md` for existing connections that have gone dormant (last contact > 12 months ago).
- **Re-engagement template:** Warm, brief, no guilt: "Hi [Name], it's been a while! I'm exploring PM roles again -- would love to hear what you've been up to. Any chance you'd be open to a quick catch-up?" This template is intentionally casual and asks about THEM first. Do not lead with the job search.
- **Prioritize former colleagues, managers, and clients.** They already know the person's work quality. A re-engagement message from a former colleague who did great work carries far more weight than a cold connection request to a stranger, regardless of how well-crafted the message is.
- **Batch allocation for returners:** If the user has dormant connections, allocate at least 40% of the batch (10+ requests) to re-engagement messages to existing contacts. The remaining 60% goes to new connection requests following the standard process.
- **Tone for re-engagement:** Acknowledge the time gap naturally but briefly. Do not over-explain. "It's been a while" is sufficient. Do not mention the reason for the gap.

### International-to-US Networking (Zero US Network)
If `connection-tracker.md` shows the user has zero or near-zero US-based connections AND is targeting US companies from abroad:
- **The cross-cultural experience IS the connection point.** Use the user's international background as a differentiator, not a liability. Messages should lean into the unique perspective: "I've spent 5 years building merchant tools at Japan's largest marketplace -- curious how your team thinks about international seller needs" is more compelling than a generic message from a US-based PM.
- **Unknown employer brands in messages:** When the user's employer is not recognized in the US, include a brief contextualizing phrase in the qualifying sentence. Instead of "I lead analytics at Personio," write "I lead analytics at Personio ($8.5B, Europe's leading HR platform)." This burns characters but is essential -- the recipient needs to instantly understand the scale.
- **Prioritize alumni and diaspora networks.** Search for alumni of the user's universities at target companies (these are the highest-conversion cold outreach paths for international candidates). Also search for people at target companies who previously worked in the user's home market or at their former employers.
- **Leverage cross-market product knowledge.** If the user has deep knowledge of how a product category works in another market (e.g., e-commerce in Japan, HR tech in Germany), use this as the hook: "I've watched how [comparable product] works in [market] -- would love to compare notes on how [target company] approaches the same problem."
- **Tone calibration for international users writing to US recipients:** Use US-style casual-professional tone (first name, warm but direct, light humor acceptable). Do NOT use the formal style the user might default to from their home culture. The messages should read as written by someone comfortable in US professional norms, even if the user is still adapting.
- **Do NOT mention visa needs in connection requests.** Visa sponsorship is a logistics detail for recruiter conversations, not a networking conversation. Including "I need H-1B sponsorship" in a connection request signals dependency and gives the recipient a reason to filter. The connection request is about building a professional relationship, not applying for a job.
- **Alumni and diaspora networks as priority multiplier.** For international candidates with zero US network, allocate at least 30% of the batch (8+ requests) to alumni connections (same university, same former employer) and diaspora connections (people from the user's home country/market at target companies). These have 2-3x the acceptance rate of pure cold outreach for international candidates. Search experience-library.md for universities and former employers, then prioritize people at target companies who share those affiliations.

### Military Networking Ecosystem
If `career-plan.md` shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), apply these adjustments to the connection request batch:
- **Priority network: veteran-to-tech communities first.** These contacts understand the military-to-civilian translation and can vouch for the candidate. Prioritize connections from: Shift.org, VetsinTech, Service2Software, BreakLine, Hiring Our Heroes, Military MBA networks. Also target defense tech companies with veteran hiring programs: Palantir, Anduril, Shield AI, Rebellion Defense, and similar.
- **For defense tech targets:** Leverage military network directly -- fellow officers who transitioned, military advisors at defense startups. These are the warmest possible leads. Allocate at least 40% of the batch to veteran-network connections when targeting defense tech.
- **For general tech targets:** Prioritize connections who are ALSO military-to-tech transitioners at the target company -- they are the warmest leads and most likely to refer. Search for veterans at target companies using LinkedIn veteran filters or military alumni networks.
- **Qualifying phrase adaptation for military candidates:** Frame the qualifier in PM-relevant language that translates military experience. Good: "I led intelligence operations for a 500-person organization, making product-level decisions about analytical tools used by 200+ analysts daily." Bad: "I was an S2 for a battalion." The qualifier must sound like a PM describing their work, not a veteran describing their service.
- **Connection point for veteran-to-veteran outreach:** When reaching out to another veteran at a target company, the shared military background IS the connection point. Lead with it: "Fellow [branch] officer here -- I saw you made the transition from [military role] to [their current PM role] at [Company]. I'm making a similar move and would love to hear how you positioned your military experience."

### Veteran / 15+ Years Experience: Legacy Employer De-Emphasis

If `career-plan.md` shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, Cisco, Dell, Accenture, Deloitte, etc.), or explicit mention of age-related concerns, apply these adjustments to connection requests:

- **Lead with WHAT THEY DID, not WHERE THEY DID IT.** For veteran candidates, the qualifying phrase must emphasize the work and impact, not the employer name. Instead of: "I spent 12 years at Oracle building enterprise products" use "I modernized a $200M enterprise platform, taking it from monolithic to microservices architecture." The first version anchors the reader to "Oracle" (legacy signal); the second anchors to the work (modern signal).
- **Prioritize connecting with people who have similar enterprise-to-startup/growth-stage transition backgrounds.** These contacts understand the transition and are more likely to accept and engage. Search target companies for people whose LinkedIn shows a trajectory from enterprise (IBM, Oracle, SAP, etc.) to growth-stage or modern tech companies. These people are warm leads because they have walked the same path.
- **Skills-forward qualifying phrase.** When the user's experience is at legacy companies, the qualifying phrase must lead with CURRENT skills and methodologies: "I led the migration to a modern data stack (Snowflake, dbt, Looker) serving 200+ analysts" beats "I managed the BI team at HP." The first signals currency; the second signals tenure.
- **Connection point adaptation for veteran candidates.** When reaching out to people at modern/growth-stage companies, avoid referencing shared legacy-company backgrounds unless the recipient also came from a legacy company. Instead, reference shared INTERESTS: a mutual passion for a product category, a shared problem space, or a recent industry trend. This positions the candidate as forward-looking, not anchored to the past.
- **Do NOT reference years of experience in connection messages.** "15 years of product experience" sounds like a credential but can trigger age bias in the reader. Instead, reference SCOPE: "I've owned products serving 4M+ users across 3 platforms" communicates seniority through impact, not tenure.

### Failed Founder / Shut-Down Company Networking Rule

If `career-plan.md` shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, apply these adjustments to connection requests:

- **IDENTITY RULE:** If the user has a stronger prior employer brand (e.g., Nubank, Google, Meta) in addition to their founder experience, DEFAULT to leading with that employer brand in all connection requests, not the founder identity. "I led growth product at [Strong Brand]" is a better opener than "I co-founded [Shut-Down Startup]." The strong employer brand provides instant credibility that a shut-down startup cannot. Only deviate from this default if the user explicitly requests founder-first framing.
- **The qualifying phrase should reference the SCALE of impact, not the company name, for the startup:** "I built a consumer fintech product from 0 to 50K users" not "I was CEO of PagaRapido." Scale communicates competence; the company name communicates nothing (or worse, triggers a "what happened?" question in the reader's mind).
- **For connections at founder-friendly companies** (startups, VCs, founder-led companies, etc.): can lean slightly more into the founder identity, as these audiences value entrepreneurial experience. "I built and scaled a consumer fintech startup to 50K users" is appropriate here because the audience respects the founder journey regardless of outcome.
- **For connections at enterprises:** Pure PM framing, founder experience as supporting context only. Lead with the PM-legible impact metrics. "I led product for a consumer fintech platform serving 50K users" positions the work as PM work, not founder work.
- **Never mention the shutdown, failure, or negative outcome in any connection request.** No "after we shut down," no "the company didn't make it," no "post-exit." The connection request is about building a forward-looking professional relationship. The startup's outcome is irrelevant to the networking conversation and only introduces a negative anchor.
