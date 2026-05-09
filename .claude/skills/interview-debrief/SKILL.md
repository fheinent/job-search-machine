---
name: interview-debrief
description: Debrief a real interview from transcript with Three Laws grading, signal analysis, and next-round prediction.
---

# /interview-debrief - Post-Interview Debrief & Analysis

## When to Use

Run this skill immediately after a real interview while the conversation is fresh. Provide a transcript (from Granola, Otter, or manual notes) and get a full breakdown: every question graded, interviewer signals decoded, next-round predictions, and automatic updates to your interview history.

Also supports **recovery mode** -- if you fumbled a question, this skill helps you identify what went wrong and generates follow-up material for your thank-you note.

**Trigger:** `/interview-debrief [transcript file path]`

Examples:
- `/interview-debrief ~/Documents/granola/anthropic-round2-2024-03-15.md`
- `/interview-debrief` (then paste the transcript directly)

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
- Interview transcript (file path or pasted text) OR take-home exercise submission + feedback

**Optional:**
- Company name (if not apparent from transcript)
- Role title (if not apparent from transcript)
- Round number (if not apparent from transcript)
- Interviewer name (if not apparent from transcript)
- User self-assessment: "I think I bombed the prioritization question" (helps calibrate grading)
- Feedback received from the hiring team (for take-home exercises)

**Take-Home Exercise Mode:**
If the input is a take-home exercise submission (not a live interview transcript), adapt the debrief:
- Instead of extracting interviewer questions, extract each SECTION of the submission as a separate grading unit (e.g., problem definition, user research approach, proposed solution, wireframes, success metrics, roadmap).
- Grade each section using a modified Three Laws approach: Law 1 = Structure/Clarity, Law 2 = Specificity/Depth, Law 3 = Product Craft Demonstration (does this section show PM thinking, not just consulting/engineering thinking?).
- If the user provides feedback from the hiring team (e.g., "Strong strategic thinking, need more product intuition"), map each piece of feedback to the specific section(s) it applies to and generate targeted improvement actions.
- The "Signal Analysis" section becomes "Feedback Analysis" -- decode what the hiring team's feedback really means and what they will probe in the next round based on it.
- Recovery mode applies to the weakest-scoring sections: generate improved versions the user can reference for the live round.

**Auto-read (do not ask the user for these -- read them directly):**
- `context-library/experience-library.md` -- for writing better rewrites
- `context-library/interview-history.md` -- for pattern analysis across interviews
- `context-library/career-plan.md` -- for context on what this role means to the user
- `insider-data/behavioral-interview-frameworks.md` -- for Three Laws grading criteria
- `insider-data/company-intel/[company].md` -- for company-specific context (if exists)

## Process

### Step 1: Transcript Analysis
Read the full transcript. Extract:
- Every question the interviewer asked (including follow-up probes)
- The user's answer to each question
- Any meta-signals: where the interviewer spent extra time, where they moved on quickly, where they pushed back or probed deeper, tone shifts

**Transcript quality check:** Before grading, scan for signs of poor audio or auto-transcription artifacts:
- Garbled, incoherent, or nonsensical passages (common in AI transcriptions of crosstalk or low-quality audio)
- `[inaudible]`, `[crosstalk]`, `[unclear]`, or similar markers
- Sudden topic jumps that suggest missing segments
- Repeated phrases or sentence fragments typical of transcription errors

If quality issues are found: (1) Flag each affected section with `[TRANSCRIPT UNCLEAR — grading may be inaccurate for this segment]`. (2) Do NOT grade answers where the user's response is substantially garbled -- instead mark as `[UNGRADED — transcript too unclear to evaluate. Ask the user to fill in from memory.]`. (3) Still grade answers where the question is clear and the user's response is mostly intact, but note any gaps. (4) In the overall assessment, note: "Transcript quality was [poor/mixed]. [N] answers could not be fully evaluated. Consider re-recording or filling in gaps from memory before the next prep session."

### Step 2: Question Categorization
Categorize each question into one of these types:
- **Behavioral:** Tell me about yourself, weakness, failure, accomplishment, conflict, say-no, ambiguity, leading without authority, prioritization, why here, why leaving
- **Product sense:** Design a product, improve a product, identify opportunities, user problems, product strategy
- **Execution:** Metrics definition, goal setting, debugging drops, A/B testing, prioritization frameworks, launch planning
- **Technical:** System design, API design, technical tradeoffs, data modeling, architecture
- **Culture fit:** Values alignment, working style, team dynamics, what you look for in a company
- **Curveball:** Anything unconventional that doesn't fit the above

**[FUNCTION-ADAPTIVE]** Add function-specific question categories alongside PM categories. SWE: 'System Design', 'Coding', 'Architecture Review'. Design: 'Portfolio Review', 'Design Challenge', 'Design Critique'. Data Science: 'Case Study', 'Technical/ML', 'Experimentation'. Marketing: 'Campaign Strategy', 'Analytics Case'. CS: 'CS Strategy', 'CS Role-Play', 'CS Operations'. Categorize questions using the appropriate function's categories, not PM categories.

### Step 3: Three Laws Grading (per question)
For each question-answer pair, grade using the identical framework from `/mock-interview`:

**Law 1 -- Structure [X/10]:**
- Was the answer organized with clear signposting?
- Did it use rule of three or another framework?
- Was it under 2 minutes (~300 words spoken)?
- If the answer was rambling or stream-of-consciousness, score accordingly

**Law 2 -- Specificity [X/10]:**
- Did the answer include a real example with real metrics?
- Were there concrete details or only abstractions?
- "We improved revenue" = low specificity. "We increased revenue 11%, $14M annually" = high specificity.

**Law 3 -- Skill Demonstration [X/10]:**
- What PM skill was this question testing?
- **SWE:** "What engineering skill was this testing? System design depth, coding fluency, architecture trade-off reasoning, debugging methodology, technical communication."
- **Design:** "What design skill was this testing? User empathy, visual problem-solving, design process rigor, critique receptiveness, design system thinking."
- **Marketing:** "What marketing skill was this testing? Channel strategy thinking, attribution rigor, growth loop understanding, audience segmentation, campaign measurement."
- **DS:** "What analytical skill was this testing? Statistical methodology, experiment design, model selection reasoning, business translation, data storytelling."
- **CS:** "What CS skill was this testing? Retention strategy thinking, customer empathy, escalation management, revenue expansion, stakeholder communication."
- Did the answer prove that skill?
- Did the answer accidentally demonstrate a different skill while missing the target one?

For each question, also identify:
- **What worked:** Specific moments in the answer that landed well
- **Value left on the table:** What the user could have said but didn't (referencing experience-library.md)
- **Rewrite:** A better version of the answer using the user's real experience

### Step 4: Signal Analysis
Analyze the interviewer's behavior across the full transcript:
- **Probe depth:** Which topics did the interviewer follow up on multiple times? (3+ follow-ups = strong signal of importance or concern)
- **Quick moves:** Which topics did the interviewer accept quickly and move on? (May indicate satisfaction or may indicate they gave up)
- **Energy shifts:** Where did the interviewer seem most engaged? (Leaning in, asking for more detail, sharing their own perspective)
- **Concern indicators:** Where did the interviewer express skepticism, push back, or re-ask from a different angle?
- **Positive indicators:** Where did the interviewer nod along, say "great," share related context, or seem to sell the role?

### Step 5: Next-Round Prediction
Based on signals and company-intel (if available):
- What will the next round likely focus on?
- Which weaknesses from this round will they probe again?
- What should the user prepare differently?

### Step 6: Recovery Analysis (if applicable)
If the user flags a fumbled question, or if any answer scores below 4/10:
- Identify exactly where the answer went wrong
- Generate a recovery document suitable for attaching to a thank-you note (see `/thank-you-note` recovery mode)
- Frame it constructively: "I realized I jumped to solutions on [question]. Here's my typical process:"

**[FUNCTION-ADAPTIVE]** Recovery documents should match the function. SWE fumble: produce a technical design document (architecture diagram, API design, failure modes), not a PM 'My Approach' doc. Design fumble: produce a design exploration with wireframes and rationale. Data Science: produce a data analysis with methodology and findings. Marketing: produce a campaign strategy or analytics brief. CS: produce a CS strategy document with frameworks and playbooks.

### Step 6b: TMAY and Recurring Pattern Check
After grading all questions, cross-reference with `interview-history.md` patterns:
- If "Tell me about yourself" was asked and scored below 7/10, generate a rewritten TMAY that fits within 2 minutes (~280 words). Time the rewrite explicitly and note: "Rewrite timed at approximately [X] seconds when read at normal speaking pace."
- If the same weakness pattern appears in THIS interview that was flagged in `interview-history.md` (e.g., conciseness, assertiveness, hedging language), escalate the coaching: "This is the [Nth] interview where [pattern] has been flagged. This pattern is now a confirmed habit, not a one-time issue. Specific drill: [concrete exercise targeting the pattern]."
- If the user's answers consistently run over 2 minutes (check word counts), add a dedicated "Pacing Intervention" section with: the exact word count of each answer, the target word count (200 words), and a specific cut list for the longest answer showing what to remove.

### Step 6c: Early-Career Pattern Detection
If `experience-library.md` shows fewer than 3 years of PM/target-role experience, actively scan the transcript for these early-career-specific failure patterns:
- **Over-long TMAY background section:** Early-career candidates often over-explain their background to compensate for thin experience, spending 60+ seconds on context before reaching any accomplishment. If the TMAY answer dedicates more than 30% of its word count to background/context before the first metric or achievement, flag: "Your TMAY spends [X]% of its length on background before your first proof point. Early-career candidates have less background to share -- use that as an advantage. Lead with your strongest metric in the first 15 seconds, then provide context."
- **Story reuse across questions:** If the user tells the same story (same project, same metric) for 2+ different questions, flag: "You used the [project name] story for both [question A] and [question B]. With a thin experience base, story reuse is more visible and suggests limited depth. Build 2-3 additional stories from experience-library.md -- even smaller wins count if they demonstrate different PM skills."
- **Flustered by unexpected questions:** If the transcript shows a sharp quality drop (score dropping 3+ points) on an unexpected or unconventional question, flag the pattern: "Your answer quality dropped significantly on [unexpected question]. Early-career candidates are more vulnerable to curveballs because they have fewer experiences to draw from. Drill: practice 3 wildcard questions per mock session until you can buy thinking time without losing composure."

### Step 6d: Domain Translation Failure Detection
If `experience-library.md` shows 80%+ of experience in one domain and the interview is at an out-of-domain company, segment failure analysis by domain context:
- **Failure Mode Segmentation:** When interview-history.md contains interviews at companies in DIFFERENT domains, segment the performance data: "Your in-domain interviews average [X]/10. Your out-of-domain interviews average [Y]/10. The gap suggests [interpretation]."
- Flag any answer where domain jargon was used without translation: "You referenced '[domain term]' without context. The interviewer at [out-of-domain company] may not know what this means. Practice translating every domain term into universal PM language."

### Step 7: Auto-Update Interview History
Append to `context-library/interview-history.md`:
- Date, company, role, round number
- Interviewer name (if known)
- Interview format type
- Every question with its type and score
- Overall assessment (strong / adequate / weak)
- Signals identified
- Key improvement area
- Next-round prediction

After 3+ interviews logged, also update the Patterns section:
- Strengths: question types with consistently high scores
- Weaknesses: question types with consistently low scores
- Recommended practice: specific mock prompts targeting weakness areas

## Output

```markdown
# Interview Debrief - [Company] [Role] - Round [N]
Date: [date]
Interviewer: [name if known]
Overall Score: [X/10]

## Questions & Grades

### Question 1: "[exact question text]"
**Type:** [behavioral / product sense / execution / technical / culture fit]
**Your answer (summary):** [2-3 sentence summary of what the user said]

**Law 1 — Structure: [X/10]**
[Specific feedback]

**Law 2 — Specificity: [X/10]**
[Specific feedback]

**Law 3 — Skill Demonstration: [X/10]**
Skill tested: [skill name]
[Specific feedback]

**Overall: [X/10]**
**What worked:** [specific moment that landed well]
**Value left on the table:** [what could have been added from experience-library]
**Rewrite:**
[Full rewritten answer using experience-library.md entries]
[Note which entries were used]

---

### Question 2: "[exact question text]"
[Same format]

---
[Continue for all questions]

## Interviewer Signals

### What They Probed Hardest
- [Topic]: [N] follow-up questions. Interpretation: [what this likely means]

### Where They Moved Quickly
- [Topic]: Asked once, accepted answer, moved on. Interpretation: [what this likely means]

### Concern Areas
- [Specific concern the interviewer seemed to have, with evidence from transcript]

### Positive Indicators
- [Specific positive signal, with evidence from transcript]

## Next-Round Prediction
Based on this interview's signals and [company]'s typical process:
- **Likely format:** [what the next round will be]
- **They will probe:** [topics based on signal analysis]
- **Prepare for:** [specific question types or topics]
- **Address:** [any concerns that surfaced in this round]

## Recovery Items
[Only if applicable — questions scored below 4/10 or user-flagged fumbles]
- **Question: "[fumbled question]"**
  What went wrong: [specific diagnosis]
  Recovery strategy: [attach to thank-you note / prepare better answer for next round / both]
  Recovery draft: [short document or reframed answer for follow-up]

## Action Items
1. [ ] Send thank-you note within 24 hours (run `/thank-you-note`)
2. [ ] Practice [weakness area] before next round (run `/mock-interview [type]`)
3. [ ] Add [missing story type] to experience-library.md
4. [ ] [Any other specific action]

## Pattern Update (if 3+ interviews in history)
Your interview-history now shows:
- Strongest area: [question type] — avg [X/10]
- Weakest area: [question type] — avg [X/10]
- Trend: [improving / declining / stable] over last [N] interviews
```

## Example

**Input:** `/interview-debrief ~/Documents/granola/stripe-round1-behavioral.md`

**Output would include:**
- 6 questions extracted and categorized (3 behavioral, 2 culture fit, 1 execution)
- Grading: strongest on accomplishment story (8/10 -- strong metrics, U-shaped arc), weakest on "why Stripe" (4/10 -- generic answer, no specific product knowledge)
- Signals: interviewer probed 3x on cross-functional collaboration (concern area), moved quickly past technical questions (satisfied or not relevant for this round)
- Next-round prediction: Round 2 will be product sense with a focus on payments/fintech domain. Prepare for "improve Stripe Checkout" or "design a new Stripe product for [segment]"
- Recovery: "Why Stripe" answer flagged for thank-you note recovery with specific Stripe product insights

## Quality Checks

1. **Every question graded.** Do not skip questions. Do not summarize multiple questions into one grade. Each question-answer pair gets its own Three Laws breakdown.
2. **Honest scoring.** Use the same calibration as mock-interview. A 5/10 is average. Do not inflate because this was a real interview. The user needs honest feedback to improve.
3. **Signal analysis must cite evidence.** Do not speculate on interviewer intent without pointing to specific transcript moments. "They asked 3 follow-ups on your leadership example" is evidence-based. "They seemed concerned about your experience" without evidence is speculation.
4. **Rewrites use experience-library.** Every rewrite must pull from the user's actual experience. If no relevant experience exists, flag the gap.
5. **Interview history auto-update.** Always update `interview-history.md`. This is not optional. The compound value of the system depends on tracking patterns across interviews.
6. **Pattern detection after 3+ interviews.** Once 3 or more interviews are logged, the Patterns section in interview-history.md must be updated with cross-interview analysis. This is what makes the system get smarter over time.
7. **Actionable next steps.** Every debrief must end with specific actions, not generic "practice more." Tell the user exactly what to practice, which skill to run, and what to add to their library.
8. **Recovery mode trigger.** If any question scores below 4/10, automatically generate recovery material without the user asking. Proactively flag: "This answer scored below 4. I've drafted recovery material you can attach to your thank-you note."
9. **Transcript quality graceful degradation.** If the transcript has significant quality issues (garbled audio, missing segments, unclear attribution), do not silently guess what was said. Mark affected sections as ungraded, ask the user to fill in gaps, and adjust the overall confidence of the debrief: "This debrief is based on a [partial/complete] transcript. [N] of [M] answers were fully graded. Confidence in overall assessment: [high/medium/low]."
10. **Visa and comp question grading.** If the transcript includes a visa question or compensation question, grade these with special attention: (a) For visa questions: score on confidence, brevity (target 30 seconds), and whether the user conveyed logistics vs. asking for permission. Flag apologetic tone or over-explanation. The rewrite must use the exact script from qa-master.md. (b) For comp questions: score on whether the user avoided disclosing current non-US comp, cited market data, and maintained confidence. If the user disclosed current comp (especially a non-US figure that sounds low), flag as CRITICAL and generate a Comp Anchor Recovery strategy in the Recovery Items section.
11. **Cross-cultural communication pattern detection.** If career-plan.md flags communication-style adaptation (e.g., Japanese consensus-driven to US direct), actively scan the transcript for: (a) hedging language ("perhaps we could consider," "I think maybe," "there are several things"), (b) excessive "we" when "I" would be more appropriate, (c) answers that bury the conclusion after extensive context-setting, (d) understated results that downplay achievements. Flag each instance with a specific replacement and a running count: "Hedging language detected [N] times in this interview. Pattern is [improving/stable/worsening] compared to interview-history.md average." If the count exceeds 3, escalate: "This pattern is actively hurting your interview performance. Drill: practice 'The right approach is X because Y' for every product sense answer."
12. **Unknown employer brand in answers.** If the user's answers reference employers not famous in the target market, check whether the user included contextualizing parentheticals when naming them. If the user said "at Rakuten" without context, flag: "You referenced Rakuten without context. The interviewer may not know the scale. Practice: 'at Rakuten Ichiba -- Japan's largest e-commerce marketplace, $15B GMV.'" Track whether employer contextualization is improving across interviews.
13. **Ageism probe detection (veteran / 15+ years experience).** If career-plan.md shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, Cisco, Dell, Accenture, Deloitte, etc.), or explicit mention of age-related concerns, add an "Ageism Signal Analysis" section to the debrief. Scan the transcript for questions that may be probing for age-related concerns:
    - **Direct probes:** "How do you stay current with technology?", "How do you feel about working with a younger manager?", "Are you comfortable in a fast-paced startup environment?", "What's your energy level like?", "How long do you plan to work?", "Where do you see yourself in 10 years?" (when asked of someone clearly 10+ years from retirement).
    - **Indirect probes:** "Tell me about a time you had to learn a new tool quickly", "How do you handle working with people who have a different communication style?", "What motivates you at this stage of your career?" (the phrase "at this stage" is the signal).
    - **Clustering analysis:** If 3+ age-related probes appear in one interview, flag: "PATTERN: [N] questions in this interview appear to probe age-related concerns. This clustering suggests the interviewer may have reservations about experience level or cultural fit. This is NOT a reflection of your performance -- it may indicate a company culture issue. Prepare stronger 'currency' and 'energy' signals for the next round."
    - **Grade age-probe responses:** For each detected age-related question, grade the user's response on: (a) Forward-looking framing (did they talk about the future or dwell on the past?), (b) Energy and curiosity signals (did they convey genuine enthusiasm or sound tired/cynical?), (c) Tech currency (did they reference modern tools/methods?), (d) Brevity (did they over-explain, which can signal defensiveness?).
    - **Rewrite age-probe answers:** For any age-probe response scoring below 7/10, generate a rewrite that: leads with recent learning or adoption, demonstrates curiosity about the company's current challenges, avoids referencing "decades of experience" as a credential, and ends on a forward-looking note.
    - **Track across interviews:** If age-related probes appear in multiple interviews (check interview-history.md), note the pattern: "Age-related questions have appeared in [N] of your last [M] interviews. This is [common for your profile / higher than expected]. Actions: (1) Strengthen your 'tech currency' stories -- add 2-3 more recent-tech examples to experience-library.md. (2) Review your LinkedIn and resume for unintentional age signals (graduation year, early career details, outdated tech listed). (3) Run `/linkedin-audit` for age-signal review."
14. **Military Jargon Detection (military-to-PM career changers).** If career-plan.md shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), add military jargon detection to the debrief analysis: (a) After each interview, flag any military jargon the candidate used. Scan the transcript for: AOR, OPORD, S2/S3/S4, battle rhythm, MDMP, IPB, CONOP, SIGINT, EEI, FRAGO, HUMINT, TOC, FOB, PCS, TDY, OER, NCOER, and any other military-specific terms. For each instance, provide the civilian translation and flag it: "MILITARY JARGON DETECTED: You said '[term]' at [timestamp/location]. Civilian equivalent: '[translation].' Practice the civilian version." (b) If the interviewer asked "Can you explain what you mean by [military term]?" -- that is a direct signal the jargon leaked. Flag as CRITICAL and add to the translation practice list with high priority. (c) Track jargon count across interviews. If the count is not decreasing over time, escalate: "You used [N] military jargon terms in this interview vs [M] in your last interview. The count is [increasing/stable/decreasing]. If not decreasing, schedule additional mock interview practice focused specifically on jargon elimination." (d) For defense tech interviews: jargon is acceptable but still track it to ensure the candidate can switch modes for general tech interviews.
15. **Career Returner Debrief Overlay.** Conditional on `career-plan.md` showing a career gap > 1 year:
    - Flag ALL gap-related questions from the interview: "Tell me about your break," "How have you stayed current?", "What concerns might a HM have?", "Why are you returning now?"
    - Grade gap answers on: brevity (target 30-45 seconds), forward-looking pivot present, no over-justification, no negative self-talk, currency bridge deployed
    - Track "gap handling score" across interviews as a separate dimension
    - If gap answer ran > 60 seconds, flag as "Compression needed — practice the 30-second version"
    - Generate recovery material if gap handling scored poorly (3/10 or below)
16. **Failed Founder Debrief Overlay.** Conditional on `career-plan.md` showing founder/CEO at a shut-down company:
    - Flag ALL founder/failure-related questions: "What happened to your startup?", "What did you learn from the failure?", "Can you take direction?", "Why did you try again at [second company]?", "How do you adjust from startup to big company?"
    - Grade founder answers on: ownership (no blame-shifting), brevity (target under 90 seconds for failure story), specific learnings (not generic "I learned to be resilient"), forward-looking pivot, no over-justification
    - Track "founder narrative score" across interviews as a separate dimension
    - If stability concern was raised: grade on whether the candidate's response addressed it directly or deflected
    - Flag if the candidate spent > 2 minutes total on startup history — signal to compress
    - For compound narrative ("two consecutive failures"): track separately whether the "Why did you go to Company B after Company A failed?" question was handled well
17. **Executive-Level Debrief Overlay.** If `career-plan.md` shows VP/Director/CPO/SVP level AND 12+ years experience:
    - Additional question categories for executive interviews: Board/Investor Communication, Org Design Philosophy, P&L Ownership, Executive Team Dynamics, "How would you structure the PM org?", "What's your product strategy framework?", Strategic Disagreement with CEO/CTO.
    - Grading adjustment: Law 3 (Skill Demonstration) at executive level tests strategic thinking, org-building judgment, executive communication, and stakeholder management -- not IC PM skills like user research methodology or A/B test design.
    - Executive red flag detection: Did the interviewer test for "doer vs. delegator"? Was there a "roll up your sleeves" concern? Flag these as executive-specific signals requiring specific prep.
    - Recovery doc format: executive-level recovery documents should be strategic memos (not tactical analyses) -- position papers on product org structure, market entry strategy, or platform vs. product trade-offs.
    - **Non-standard executive interview format handling.** Executive interviews include formats that do not follow typical Q&A. Detect the format and apply the appropriate rubric:
      - **Retained search firm intake:** Grade on mutual-fit assessment signals, not Q&A performance. Key criteria: Did the candidate convey clear role criteria? Did they ask strategic questions about the opportunity? Did the search firm indicate clear next steps? Standard Three Laws grading does not apply -- use: (1) Clarity of positioning, (2) Strategic curiosity about the role, (3) Mutual-fit signals exchanged.
      - **CEO chemistry conversation:** Grade on rapport, strategic alignment, and mutual evaluation. This is a "would we want to work together?" assessment, not a traditional interview. Rubric: (1) Did the conversation feel like a peer exchange or a one-sided evaluation? (2) Was there strategic alignment on company direction? (3) Did the candidate evaluate the CEO as much as the CEO evaluated them?
      - **Board presentation round:** Grade on strategic thesis clarity, question handling under pressure, and executive presence. Rubric: (1) Was the strategic narrative coherent and conviction-driven? (2) Did the candidate handle tough board-style questions without becoming defensive? (3) Did the candidate present as a peer (fellow executive) or as a candidate (seeking approval)?
18. **Remote-Only Debrief Overlay.** Conditional on `career-plan.md` showing remote-only preference:
    - Flag ALL remote-related questions/moments: "Would you consider hybrid?", "Why remote?", "Is there a personal reason?", "How do you collaborate with the team?", "What about occasional travel?"
    - Detect "remote friction signals": interviewer energy shift after remote discussion, follow-up probing on collaboration, "we're really looking for someone in-office for this" statements
    - Grade remote answers on: confidence (not defensive), substance (specific async wins cited), no personal disclosure
    - Privacy guardrail: if the candidate disclosed personal reasons for remote during the interview, flag it as a critical error for future avoidance
    - Track "remote conversation performance" across interviews to identify improvement
