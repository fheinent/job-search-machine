---
name: referral-request
description: Generate the full three-message referral request sequence for a specific person and role.
---

# /referral-request - Referral Request Sequence Generator

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In referral request contexts, this means: never include private details in any of the three messages, the copy-paste blurb, or coaching notes that the user might forward to their contact.

## When to Use

Run `/referral-request [person name + role link]` when:
- You have an existing connection at a company (they accepted your LinkedIn request, you had a coffee chat, you know them from a previous job) and you want to ask them for a referral to a specific role
- A job-fit-score came back 75+ and you have a warm contact at that company
- A connection at a target company told you about an open role
- The morning briefing flagged a new posting at a company where you already have connections

Do NOT use this skill if you have never interacted with the person. Use `/connection-request` first to establish the relationship, then come back here after at least one meaningful exchange.

**Network type detection:** If `connection-tracker.md` shows the user's connections are primarily from consulting, MBA, or non-PM networks (no current PMs in tracker), adapt the messaging:
- The referrer likely cannot speak to the user's PM skills -- so the qualification pitch must be self-contained and metric-driven, not dependent on the referrer vouching for PM ability.
- Alumni and consulting networks respond to different social proof: mention the shared institution ("fellow Wharton alum" / "former McKinsey") early in Message 1.
- The copy-paste blurb (Step 4) must work even when the referrer has never seen the user do PM work. Frame it as: "I worked with [Name] at [McKinsey/Wharton] -- sharp analytical thinker who led [specific deliverable]. They're transitioning to product and I think they'd bring a strong strategic lens to the team."

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
- `[person name]` -- the name of your connection, exactly as it appears in `connection-tracker.md`
- `[role link]` -- the URL or title of the specific role you want a referral for

**Required files (read automatically):**
- `@context-library/connection-tracker.md` -- relationship history with this person: when you connected, meeting notes, last contact, any prior asks
- `@context-library/experience-library.md` -- your qualifications, key metrics, relevant stories (used to write a concise "why I'm qualified" pitch)
- `@context-library/career-plan.md` -- your target level and function (used to frame the role as a natural fit)

**Optional (read if available):**
- The job description for the role (paste it in or provide a link)
- `@context-library/target-companies.md` -- for company context and any notes about the hiring team

## Process

### Step 1: Pull Relationship Context

1. Look up the person in `connection-tracker.md`.
2. Extract:
   - How you know them (mutual connection, coffee chat, former colleague, event, LinkedIn).
   - When you last interacted and what you discussed.
   - Whether you have asked them for anything before.
   - Their current role and seniority (to gauge how close they are to the hiring team).
3. If the person is not in `connection-tracker.md`, STOP. Tell the user: "I don't have relationship context for [person]. Add them to connection-tracker.md first, or tell me how you know them."

### Step 2: Parse the Role

1. Read the job description (if provided).
2. Identify the 2-3 strongest qualification matches from `experience-library.md`.
   - **For career changers:** If the user has no PM-titled experience, match on TRANSFERABLE skills. Consulting deliverables (client presentations, market sizing, operational transformations, due diligence) map to PM skills. A McKinsey engagement leading a bank's digital lending launch maps to "fintech product experience." Frame the match in PM language, not consulting language: "led the product strategy for" not "advised the client on."
   - **If fewer than 3 years experience targeting a role requiring more:** Preempt the referrer's concern about the experience gap. Add to the qualification pitch: "I know the posting says X+ years -- my output matches the level. [Specific metric proving impact-per-year at the target level]." This gives the referrer confidence that they are not sticking their neck out for someone who will be immediately filtered. The referrer needs to believe you can pass the screen -- arm them with the data.
   - **[FUNCTION-ADAPTIVE]** Function-specific qualification pitch examples: SWE: "I designed the payment retry system handling 12K TPS at Shopify -- sounds like similar scale to what your platform team is building." Design: "I led the design system rebuild at Spotify serving 50+ product teams -- the consistency challenges sound similar to what your design org faces." Data Science: "I built the recommendation engine at Spotify driving 30% of daily streams -- your team's personalization work is the exact problem space I want to go deeper on." Marketing: "I grew Lattice inbound pipeline from $2M to $8M ARR -- your growth team's B2B motion is the same playbook." CS: "I drove 118% NRR across $45M in enterprise ARR at Salesforce -- your enterprise CS team's expansion challenges are right in my wheelhouse."
3. Note the hiring team or org if visible in the JD.
4. Identify the likely hiring manager title (e.g., "Director of Product, Growth" or "VP Engineering, Platform"). **[FUNCTION-ADAPTIVE]** For non-PM roles, the HM is NOT "Director of Product." SWE: Engineering Manager or Director of Engineering. Design: Head of Design or VP Design. Data Science: Head of Data or VP Analytics. Marketing: VP Marketing or CMO. CS: VP CS or CRO.

**Domain-locked referral framing:** If the user's experience is concentrated in one domain and the referral is for an out-of-domain role, the qualification pitch and copy-paste blurb must use universal PM language, not domain jargon. The referrer may not understand domain-specific terms, and the HM reading the blurb is in a different domain entirely. "Led experimentation across 4M users, increasing conversion 18%" works everywhere. "Optimized Medicare Advantage enrollment funnels" only works in healthcare.

### Step 2.5: Classify Relationship Strength

Before generating messages, classify the relationship into one of three tiers based on `connection-tracker.md` data:

**Tier A -- Strong relationship** (former colleague, multiple meetings, worked together on something):
- Ask directly for a referral. You have earned the right.
- Message 2 can push hard for the strong referral (HM Slack ping).
- Casual tone. Use first name, informal language.

**SENIOR-TO-JUNIOR REFERRAL DYNAMICS:** If career-plan.md shows the user is at Director level or above AND the referrer (from connection-tracker.md) is at a lower seniority (e.g., Senior PM, PM, or IC-level), adjust the messaging to avoid the awkwardness of a senior person asking a junior person to vouch for them:
- **Tone shifts to peer/mentorship framing.** Do not ask the referrer to "vouch" for you -- they would feel uncomfortable endorsing someone more senior. Instead, frame the ask as seeking an informed perspective: "You know the team from the inside -- would you feel comfortable flagging my application to the recruiter?" This positions the referrer as providing information, not making a judgment call.
- **The qualification pitch is minimal.** When the candidate outranks the referrer, over-explaining qualifications feels patronizing. One sentence with a scope metric is sufficient. The referrer already knows (or can see from LinkedIn) that the candidate is senior.
- **The copy-paste blurb is written so the referrer does not feel like they are vouching UP.** Instead of "I worked closely with [Name] and can vouch for their product judgment," write the blurb as: "[Name] is a product leader I've worked with who is exploring VP-level roles. They led [scope metric] at [Company]. I thought the team should see their application." This frames the referrer as surfacing a strong candidate, not personally endorsing someone above their pay grade.
- **Message 1 includes an explicit out.** Add: "I know this is a bit unusual since the role is at [level] -- totally understand if you'd rather just point me to the right person to talk to instead." This acknowledges the dynamic and gives the referrer a graceful alternative.
- **If the referrer is significantly junior (2+ levels below),** consider skipping the referral ask entirely and instead asking for an introduction to someone at or above the candidate's level: "Do you know who leads the [team] org? I'd love to reach out to them directly." This is often more effective and less awkward for everyone.

**Tier B -- Moderate relationship** (one coffee chat, 1-2 meaningful LinkedIn exchanges, mutual friend introduced you):
- Ask for a referral, but lead heavier with why you are qualified (they need ammunition to feel good about vouching).
- Message 2 should frame the strong-referral ask as optional ("If you happen to know the HM, a quick ping goes a long way -- but the ATS referral alone is a huge help").
- Warm but slightly more formal tone.

**Tier C -- Weak relationship** (accepted LinkedIn request, one brief exchange, no real rapport yet):
- Do NOT ask for a referral directly. Instead, ask for an informational conversation first: "Would you have 15 minutes to chat about what the [team] is working on? I'm exploring roles in this space and your perspective would be valuable."
- If they agree to the conversation, THEN follow up with the referral sequence (re-run this skill after the chat, updating connection-tracker.md with meeting notes).
- Message 2 and Message 3 are NOT generated for Tier C. Only Message 1 (the informational ask) is produced.
- Tell the user: "This relationship is too thin for a direct referral ask. I've drafted an informational conversation request instead. After you meet with them, re-run `/referral-request` and I'll generate the full sequence."

### Step 2.7: Detect Post-Referral State

Before generating the standard three-message sequence, check `connection-tracker.md` for whether a referral has ALREADY been submitted for this person + role combination:

**If referral is already submitted (referral-received = yes):**
- Do NOT generate Message 1 (the initial ask) -- the ask is done.
- Check if a strong referral (HM ping) has happened:
  - **If HM was pinged AND no response from HM yet:** Generate a "strong push follow-up" message instead of the standard sequence. This message asks the referrer to nudge the HM again, provides updated context (e.g., "I submitted my application on [date]"), and optionally includes a new asset (updated resume, work product) the referrer can forward. Frame as: "Hey [Name], just wanted to follow up on the [Role] referral. I submitted my application on [date]. If David hasn't had a chance to look yet, would you mind giving him another gentle nudge? Happy to send you anything updated to forward along."
  - **If HM was pinged AND responded positively:** Generate a "keep warm" message that thanks the referrer, shares any process updates ("I heard from the recruiter"), and asks for any insider prep tips for the interview.
  - **If referral was ATS-only (no HM ping):** Generate Message 2 (the strong referral push) to upgrade from weak to strong referral. Skip Messages 1 and 3.
- **If referral was requested but NOT confirmed received:** Generate a gentle check-in: "Hey [Name], just following up on the [Role] referral -- any update on your end? Totally understand if you haven't had a chance yet."

This prevents the embarrassing scenario of re-asking someone who already helped you, and ensures the skill adapts to the full lifecycle of a referral relationship.

### Step 3: Generate Three Messages

Generate all three messages as a sequence. The user sends them at different times depending on how the conversation unfolds.

---

**Message 1: The Initial Ask**

Purpose: Remind them of your relationship, mention the role, establish why you are a fit, and make the ask.

Structure:
1. **Personal opener** -- reference your last interaction specifically. Not "Hope you're doing well." Instead: "That recommendation you made about [specific thing] was spot on" or "Been thinking about what you said about [topic] when we grabbed coffee." Pull the details from `connection-tracker.md` meeting notes.
2. **The bridge** -- transition naturally from the personal reference to the professional ask. One sentence max.
3. **The role + why you are qualified** -- name the specific role. Then 1-2 sentences on why you are a fit, pulling the strongest metrics from `experience-library.md`. Be specific. Not "I have relevant experience." Instead: "I spent 2 years building exactly this -- grew activation from 23% to 41% on an onboarding flow that sounds similar to what this team owns."
4. **The ask** -- direct but respectful. "Would you be open to putting in a referral? Happy to send my resume and a quick blurb you can forward."
5. **Pressure release** -- "Totally understand if the timing isn't right or if you don't feel comfortable. No pressure at all."

Tone: Warm, direct, not desperate. This person likes you -- remind them why.

Length: 100-200 words. Short enough to read on a phone.

---

**Message 2: The Strong Referral Push (send after they agree to refer)**

Purpose: Thank them and push for a STRONG referral (not just an ATS submission -- an actual Slack message or email to the hiring manager).

Structure:
1. **Thank them** -- genuine, brief. Not over-the-top.
2. **Provide everything they need** -- "Here's my resume and a 2-line blurb you can copy-paste if helpful: [blurb]." Remove all friction. They should be able to forward your info in 30 seconds.
3. **The strong referral ask** -- "One thing that makes a huge difference: if you could ping the hiring manager directly on Slack or email to flag my application, it's night and day compared to just the ATS submission. Would you be comfortable doing that?"
4. **Ask who the HM is** -- "Do you happen to know who the hiring manager is for this role? I'd love to reach out to them on LinkedIn as well -- not to go around the process, but to share a quick piece of analysis I did on [topic relevant to the role]."

Tone: Appreciative, practical, specific about what you need. You are coaching them on how to give you the best referral possible.

Length: 80-150 words.

---

**Message 3: HM Identification (send if they do not know who the HM is)**

Purpose: Suggest who you think the hiring manager might be, so they can confirm and connect you.

Structure:
1. **Your research** -- "I did some digging on LinkedIn. Based on the team structure, I think the HM might be [Name, Title]. They seem to lead the [team/area] that this role sits under."
2. **Ask for confirmation** -- "Does that sound right? Or is there someone else who owns hiring for this team?"
3. **Offer an alternative path** -- "If you're not sure, no worries -- even knowing which org this sits in would help me figure it out."

Tone: Helpful, not presumptuous. You did the work; you are asking them to validate, not to do research for you.

Length: 50-80 words.

### Step 4: Generate the Copy-Paste Referral Blurb

In addition to the three messages, generate a short blurb (2-3 sentences) that your connection can copy-paste into their referral submission or Slack message. This blurb should:
- Name you and the role
- State the single most relevant qualification
- Include a specific metric
- Be written in third person from the referrer's perspective
- **International employer brand rule:** If the user's employers are not well-known to the likely reader of the referral blurb (e.g., a US hiring manager reading about a non-US company, or vice versa), include a brief parenthetical that contextualizes the company's scale and market position. The HM or recruiter reading this blurb has never heard of the company -- the parenthetical converts the unknown name into an impressive signal. Example: "They spent 5 years building merchant tools at Rakuten Ichiba ($15B GMV, Japan's largest e-commerce marketplace)" rather than just "They worked at Rakuten." Check `career-plan.md` addressing-weaknesses for any "unknown employer brand" weakness to confirm this applies.
- **Visa sponsorship in the blurb:** Do NOT mention visa requirements in the copy-paste blurb. The blurb is about qualification and fit, not logistics. Visa is a separate conversation between the candidate and recruiter. Including it in the blurb gives the HM a reason to filter before evaluating merit.

Example: "I'd like to refer [Your Name] for the Senior PM, Growth role. They led activation at [Company], moving 7-day retention from 23% to 41%. Strong product thinker with deep growth experience -- I think they'd be a great fit for the team."

## Output

```
## Referral Request Sequence: [Person Name] -> [Role Title] at [Company]

**Relationship context:** [summary of how you know them, last interaction]
**Role:** [title + link]
**Strongest qualification match:** [the 1-2 experience bullets you're leading with]
**Likely HM:** [best guess from LinkedIn research, or "unknown"]

---

### Message 1: Initial Ask
*Send via: [LinkedIn DM / iMessage / email -- based on relationship closeness]*
*Timing: Send now*

> [message text]

---

### Message 2: Strong Referral Push
*Send via: [same channel as Message 1]*
*Timing: Send after they agree to refer you*

> [message text]

**Copy-paste referral blurb for them:**
> [blurb text]

---

### Message 3: HM Identification
*Send via: [same channel]*
*Timing: Send only if they don't know who the HM is*

> [message text]

---

## After Sending
- [ ] Update connection-tracker.md: set "Referral requested: yes, [date], [role]"
- [ ] If they share the HM name, run `/hiring-manager-msg` immediately
- [ ] If they agree to a strong referral, update "Strong referral (HM pinged): pending"
- [ ] Set a reminder to follow up in 3 days if no response to Message 1
- [ ] Send a thank-you note regardless of outcome (use `/thank-you-note` if needed)
```

## Example

Input: `/referral-request Sarah Kim + https://boards.greenhouse.io/notion/jobs/senior-pm-growth`

After reading `connection-tracker.md`:
- Sarah Kim, PM at Notion. LinkedIn connected 3 weeks ago. Had a 30-min coffee chat last Tuesday. She mentioned her team is focused on enterprise onboarding. She asked about your experience with PLG funnels.

Sample Message 1:

> Sarah -- really enjoyed our coffee chat last week. Your insight about enterprise onboarding being more about activation than seat count stuck with me.
>
> I saw the Senior PM, Growth posting on Notion's board and it feels like a strong fit. I spent 2 years owning activation at [Company], where we moved 7-day retention from 23% to 41% by redesigning the first-run experience -- sounds like similar territory to what your growth team is tackling.
>
> Would you be open to putting in a referral? Happy to send my resume and a short blurb you can forward. Totally understand if the timing doesn't work -- no pressure.

## Quality Checks

- [ ] **Message 1 references a specific past interaction.** Not "It was great connecting." Instead: a detail from `connection-tracker.md` meeting notes. If meeting notes are empty, ask the user to fill them in before generating.
- [ ] **Qualification pitch uses real metrics from experience-library.** No vague claims. At least one number.
- [ ] **The ask is direct.** No passive hints like "I was wondering if maybe..." Just: "Would you be open to referring me?"
- [ ] **Message 2 includes the copy-paste blurb.** The referrer should not have to write anything from scratch. Remove all friction.
- [ ] **Message 2 explicitly asks for the Slack/email ping.** This is the difference between a weak referral (ATS submission only) and a strong referral (HM knows your name before they see the application). Do not skip this.
- [ ] **Message 3 does the research for them.** You suggest who the HM is. You do not ask them to go figure it out.
- [ ] **Tone matches the relationship.** If `connection-tracker.md` shows they are a former colleague, be more casual. If they are a recent LinkedIn connection, be warmer and more formal. Never robotic.
- [ ] **No message exceeds its length target.** Message 1: 100-200 words. Message 2: 80-150 words. Message 3: 50-80 words.
- [ ] **Channel recommendation makes sense.** Former colleague = iMessage or Slack. Recent LinkedIn connection = LinkedIn DM. Someone you have their email = email for the referral, LinkedIn for the initial ask.
- [ ] **Visa is NOT mentioned in Messages 1-3 or the copy-paste blurb.** Visa sponsorship is a recruiter/HR conversation, not a referral conversation. The referrer is vouching for qualification and fit. Mentioning visa in the referral materials gives the HM a logistical reason to filter before evaluating merit. If the referrer asks about visa status, the user can share it directly -- but the skill must not include it in any generated message.
- [ ] **International employer context is embedded in the qualification pitch.** If the user's employers are not famous in the target market, Message 1's qualification pitch must include the parenthetical (e.g., "I spent 5 years building merchant tools at Rakuten Ichiba -- Japan's largest e-commerce marketplace, $15B GMV"). The copy-paste blurb must also include this context since the HM reading it has never heard of the company.
- [ ] **Cross-geography relationship dynamics handled.** If the referrer is in a different country than the target office (e.g., referrer in Sydney, role in SF), Message 1 must acknowledge the distance naturally: "I know you're based in Sydney and this role is in [location], but your perspective on the team would be invaluable." This prevents the referrer from self-filtering with "but I'm not in the US office."

### Career Gap / Returner: Referral Framing Adjustments

If `career-plan.md` shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), apply these adjustments:

- **Returner-specific referral framing:** The qualification pitch in Message 1 must emphasize the WORK RELATIONSHIP, not the time elapsed. Structure: "I worked with [referrer] at [company] on [specific project] -- they can speak to my [specific skill]." This anchors the referrer's memory to the quality of work, not the gap since.
- **Time-since-contact check:** If the referrer has not been in contact for 2+ years (check connection-tracker.md for last contact date), recommend a re-engagement message BEFORE asking for the referral. Do NOT generate the full referral sequence for a dormant contact. Instead: (1) Generate a re-engagement message first: "Hi [Name], it's been a while! I'm exploring PM roles again and would love to catch up. Any chance you'd be open to a quick chat?" (2) Tell the user: "This contact has been dormant for [N] years. Send the re-engagement message first. After you reconnect, re-run `/referral-request` to generate the full sequence."
- **Copy-paste blurb for returners:** The referral blurb must frame the candidate's experience as current and relevant, not as historical. Good: "[Name] is a PM with deep experience in [domain] -- they led [specific project] that delivered [metric]. They're exploring PM roles and I think they'd be strong for this team." Bad: "[Name] used to be a PM before taking a career break -- they're trying to get back into the industry." The blurb must read as a recommendation of a strong candidate, not an explanation of a career trajectory.
- **Do NOT mention the career gap in Messages 1-3 or the copy-paste blurb.** The referral conversation is about qualification and fit. The gap is a timeline detail that the candidate addresses in interviews, not in referral materials.

### Remote-Only Candidate: Referral Adaptations

If `career-plan.md` shows remote-only preference or caregiver constraints:
- **Pre-referral remote verification:** Before requesting a referral, verify the role's remote policy: "Before asking for a referral, check whether the role is confirmed remote or if the referrer can confirm. Do not invest social capital on a referral for a role that turns out to be hybrid-required."
- **Referral blurb adaptation:** Include a subtle remote signal: "I'm targeting distributed-first teams where I can contribute from [city]" -- do not explain WHY remote.
- **PRIVACY GUARDRAIL:** Never mention caregiving, family, or health reasons in any referral communication.
- **"Role turned hybrid" scenario:** When the referrer proactively discloses "this role is actually hybrid now," generate a pre-drafted response: "Thanks for the heads-up -- I'm focused on distributed-first teams right now. Would love to stay connected for future remote roles on the team." Do NOT explain WHY remote-only (privacy guardrail applies). Mark the opportunity as "paused - remote policy mismatch" in the app tracker.

### Veteran (15+ Years): Referral Adaptations

If `career-plan.md` shows 15+ years experience:
- **Legacy employer de-emphasis in referral blurb:** Lead with the work and impact, not the employer name. "I led the cloud infrastructure pivot that drove $180M in migration revenue" not "I was VP Product at Oracle."
- **Referrer comfort:** For referrers who are significantly junior, explicitly note: "I understand this might feel unusual. I'm genuinely excited about this role because [specific reason]. Your referral would mean a lot."
- **Skills-forward copy-paste blurb:** Frame around capabilities and recent outcomes, not career history length.
- **"Overqualified" objection handling:** When a referrer hesitates because the candidate seems overqualified for the role, generate a pre-drafted response: "I hear that concern -- I'm deliberately targeting this scope because [specific reason from career plan, e.g., 'I want to go deep on AI/ML platform products rather than managing the entire org']. My experience means I can contribute immediately while the team sees the fit firsthand." Never respond defensively. Frame the scope choice as strategic, not a step down.

### Military-to-PM: Referral Adaptations

If `career-plan.md` shows military background:
- **Civilian framing in copy-paste blurb:** Translate all military experience into civilian language. No acronyms, no rank references, no military jargon. The referrer may need to explain you to a hiring manager -- give them civilian words to use.
- **Defense-tech vs. general-tech adaptation:** For defense-tech referrals, clearance and military background are assets -- mention them. For general-tech referrals, lead with analytical and leadership skills, mention military as "leadership background in [operations/logistics/intelligence]."
- **Veteran network leveraging:** If the referrer is also a veteran, the blurb can be more direct about the transition. If the referrer is civilian, frame military experience as "X years of complex program management."
- **Zero-PM-experience military referral reassurance:** When the candidate has zero PM titles, the copy-paste blurb must proactively establish PM credibility with a "PM-equivalence" statement: "In my military role, I owned the requirements definition, stakeholder alignment, and delivery timeline for [specific project] -- the same muscles PMs use daily, just in a different context." Additionally, reassure the referrer that they will not be going out on a limb: "I know it's a non-traditional background -- happy to chat with you first so you can assess the fit before making any intro." This gives the referrer an off-ramp and reduces the perceived risk of vouching for a non-traditional candidate.

### Dual-Role Referral

If the user is applying to two roles at the same company:
- Send ONE referral message mentioning primary interest with a secondary note: "I'm most interested in [Primary Role] because [reason], and I also see strong fit with [Secondary Role]. Would you be open to referring me? Happy to discuss which is the better match."
- Do NOT send two separate referral requests to the same person for two roles — it appears unfocused.
- If referring through different contacts for each role, ensure the framing is consistent (same person, different emphasis — not contradictory narratives).

### Failed Founder / Shut-Down Company: Stigma-Aware Referral Coaching

If `career-plan.md` shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, apply these adjustments:

- **Prepare the referrer for the "why did their company fail?" question.** When a referrer submits someone with founder experience at a company that no longer exists, the HM or recruiter may ask the referrer directly: "What happened with their company?" The referrer needs a ready answer. Add a coaching note to Message 2: "Quick heads-up -- if anyone asks about [company name], the short version is: '[Name] built [product] that served [users/customers]. They learned [specific skill] and decided to bring that experience to a larger org.' That's the whole story."
- **Qualification pitch leads with SCALE, not company outcome.** Message 1's qualification pitch must emphasize what the founder BUILT, not what happened to the company. Good: "I built [product] from 0 to [X users/customers] and owned the full product lifecycle -- strategy, roadmap, execution, and GTM." Bad: "I was a founder/CEO at [company] (which shut down) and now I'm looking for PM roles."
- **Copy-paste blurb for founders:** The referral blurb must frame the founder as a BUILDER, not a failure. Template: "[Name] built [product] from scratch -- took it from zero to [metric]. They owned product strategy, shipped [N] major features, and managed a [N]-person team. They're looking for a PM role where they can go deep on [relevant area] and I think they'd be strong for this team." Do NOT include: "former founder," "startup didn't work out," "looking to get back into a stable role," or any language that frames the transition as a step down.
- **Do NOT mention the company failure in Messages 1-3 or the copy-paste blurb.** The referral conversation is about qualification and fit. The company outcome is a detail the candidate addresses in interviews if asked directly. The referrer should not have to explain or defend it.
