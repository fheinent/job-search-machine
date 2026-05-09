---
name: mock-interview
description: Interactive mock interview with one-question-at-a-time flow and Three Laws grading.
---

# /mock-interview - Interactive Mock Interview

**UNIVERSAL PRIVACY GUARDRAIL:** When reading career-plan.md, the following information is PRIVATE and must NEVER appear in any external-facing output (messages, documents, scripts, blurbs, or coaching visible to anyone other than the user): reasons for career gaps (caregiving, health, family), reasons for remote preference (caregiving, disability, family obligations), age or graduation year, personal financial constraints, immigration/visa details beyond what the user explicitly shares, relationship status, health conditions, pregnancy/family planning, and any information marked as "private" or "confidential" in career-plan.md. This information may inform INTERNAL analysis and recommendations but must never leak into generated content. In mock interview contexts, this means: never generate interviewer questions that probe for private information, never include private details in model answers or rewrites, and coach the user to deflect if real interviewers probe these areas.

## When to Use

Run this skill to practice for upcoming interviews. Best used after `/interview-prep` so questions can be tailored to the target company. Can also be used standalone for general practice. Voice mode (dictation) is strongly recommended for realistic practice.

**Trigger:** `/mock-interview [type]`

Types:
- `behavioral` -- Tell me about yourself, strengths/weaknesses, failure, conflict, accomplishment, etc.
- `product-sense` -- Design a product, improve a product, identify opportunities, prioritize features
- `execution` -- Metrics, debugging, root cause analysis, A/B testing, tradeoffs
- `technical` -- System design, technical tradeoffs, API design, data modeling (for technical PM roles)

### Function-Specific Mock Types [FUNCTION-ADAPTIVE]

In addition to the base types (behavioral, product-sense, execution, technical), detect the user's function and offer these types:

**SWE:** system-design (present a design prompt, evaluate requirements gathering, high-level design, component deep-dive, operational concerns), coding (present algorithmic problem, evaluate correctness, efficiency, code quality, communication)

**Design:** portfolio-review (walk through a case study, evaluate problem framing, process, outcome, reflection), design-challenge (present a design problem, evaluate structured approach, user consideration, feasibility, iteration)

**Data Science:** case-study (present a business problem requiring data analysis, evaluate metric definition, methodology, insight quality, recommendation), technical (SQL/statistics/ML questions)

**Marketing:** campaign-strategy (design a GTM or growth campaign, evaluate audience targeting, channel mix, measurement plan), analytics-case (analyze marketing data, evaluate analytical rigor and business recommendation)

**CS/Sales:** cs-strategy (design a health score or CS org, evaluate methodology, segmentation, playbook design), cs-roleplay (simulate a QBR, executive escalation, or account save -- the interviewer plays the customer VP)

Examples:
- `/mock-interview behavioral`
- `/mock-interview product-sense`
- `/mock-interview execution` (targets weakness areas from interview-history)
- `/mock-interview system-design` (SWE)
- `/mock-interview portfolio-review` (Design)
- `/mock-interview case-study` (Data Science)
- `/mock-interview cs-roleplay` (CS/Sales)

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
- Interview type (behavioral, product-sense, execution, technical)

**Optional:**
- Target company (if provided, pulls company-specific questions from interview-prep output or company-intel)
- Specific weakness to focus on (e.g., "I keep bombing prioritization questions")
- Number of questions (default: 5-8)

**Auto-read (do not ask the user for these -- read them directly):**
- `context-library/experience-library.md` -- for writing rewrites that use real experience
- `context-library/career-plan.md` -- for addressing-weaknesses context
- `context-library/interview-history.md` -- for weakness patterns to prioritize
- `context-library/qa-master.md` -- for pre-drafted common answers
- `insider-data/behavioral-interview-frameworks.md` -- for question frameworks and grading criteria
- Most recent interview-prep output in `briefings/` (if exists, for company-specific questions)

## Process

### Step 0: Session Setup
Display this message at the start of EVERY mock session:

```
MOCK INTERVIEW SESSION — [Type]: [behavioral/product-sense/execution/technical]
[Company-specific if applicable]

For best results, answer out loud using dictation instead of typing.
This simulates real interview conditions and gives you better feedback
on pacing and structure.

macOS: Press Fn twice to start dictation
Granola: Use Granola for automatic transcription
Speechify: Use speech-to-text mode

I'll ask one question at a time. Answer fully, then I'll grade and rewrite.
Ready? Here's your first question.
```

### Step 1: Question Selection
Build the question queue using this priority order:
1. **Critical weakness-first (below 5/10):** If `interview-history.md` shows any question type with an average score at or below 5/10, these are CRITICAL and must be the FIRST questions asked. Lead with the single lowest-scored question type. If "Walk me through a product you've built" is scored 4/10, ask that FIRST -- not third, not after warmup. The user needs to practice their worst area when they are fresh, not after they have warmed up on easier questions. For career changers: check if "PM narrative" (TMAY) or "product you built" are the lowest scores -- these two are almost always the career changer's weakest and must be drilled relentlessly.
2. **Weakness-next (at or below 6/10):** If `interview-history.md` shows question types with average scores at or below 6/10 but above 5/10, prioritize these after critical weaknesses. Also check the "Weaknesses" section in interview-history.md patterns -- any question type explicitly listed there (e.g., "product sense," "compensation questions," "why leaving") should be prioritized regardless of exact numeric score, as the user or the OS has already identified it as a development area. **If interview-history.md has zero entries** (new user or early in job search), skip weakness priorities and start with the foundational questions: "Tell me about yourself" (type 1), "Accomplishment" (type 8), "Biggest failure" (type 7), and "Why here" (type 4). These four form the core that every candidate must nail before practicing edge cases.
3. **Company-specific:** If interview-prep output exists or a company was specified, pull questions from company-intel or the prep package
4. **Gap coverage:** If the user has done prior mock sessions, avoid repeating the same questions. Cover new types.
5. **Standard bank:** Fall back to the standard question bank for the type

**Behavioral Question Bank (cover these types across sessions):**

| # | Type | What It Tests | Framework |
|---|------|---------------|-----------|
| 1 | Tell me about yourself | Positioning, weakness mitigation | Addressing-Weaknesses Framework (2 min max) |
| 2 | Compensation (current pay) | Negotiation awareness | Avoidance-and-flip strategy |
| 3 | Compensation (expectations) | Market knowledge | Range + data source |
| 4 | Why here / why this company | Authenticity, research | Mission + role fit + people |
| 5 | Why this job | Address level/function concerns | Enthusiasm + address concerns |
| 6 | Greatest weakness | Self-awareness, growth | Real weakness + performance feedback + growth |
| 7 | Biggest failure | Vulnerability, learning | Real work failure + context + growth |
| 8 | Accomplishment | Impact, storytelling | U-shaped arc (challenge, struggle, triumph) + metrics |
| 9 | Say no / push back | Judgment, courage | Genuinely hard no + texture + justification |
| 10 | Curveball / unconventional | Thinking on feet | Strategic use to reinforce strength or address weakness |
| 11 | Cross-functional conflict | Collaboration, influence | Specific conflict + empathy for other side + resolution |
| 12 | Prioritization / tradeoffs | PM judgment | Framework + specific example + what you cut and why |
| 13 | Leading without authority | Influence, leadership | Specific example + how you brought people along |
| 14 | Ambiguity / incomplete info | Comfort with uncertainty | How you structured the unknown + what you did first |
| 15 | Organizational design | Team building, org structure, scaling | Framework + specific org built + decisions and trade-offs |
| 16 | Board/executive communication | Upward management, exec presence | Specific board presentation + what you simplified + outcome |
| 17 | Strategic disagreement | Executive conflict resolution, influence | Specific disagreement with CEO/exec + data-driven resolution |
| 18 | Talent/hiring philosophy | People development, culture building | Specific PM developed + their trajectory + your approach |
| 19 | Domain Translation | Communication, abstraction | Explain your most impactful project to someone outside your industry in 60 seconds |
| 20 | Involuntary Departure | Composure, ownership, forward pivot | "Why did you leave your last role?" -- Grade on: composure, brevity (under 30 seconds), ownership without over-explaining, forward pivot to why this role is better. Red flags: blame, emotional charge, excessive detail, volunteering information not asked for. |
| 21 | Re-Application | Self-awareness, growth evidence | "You interviewed with us before. What's changed?" -- Grade on: specific growth evidence, self-awareness about prior gaps, genuine enthusiasm (not desperation). Red flag: vague "I've grown a lot" without specifics. |
| 22 | Background Context | Composure, brevity, ownership | "Tell me about [situation from background]." -- Grade on: brief factual acknowledgment, ownership, pivot to growth/lessons. Red flags: defensiveness, over-explaining, blame. Note: only include this question if career-plan.md indicates background check concerns. |

**[FUNCTION-ADAPTIVE]** When the detected function is NOT PM, replace PM-specific behavioral questions with function-appropriate ones. SWE behavioral: technical decision with tradeoffs, debugging a production incident, architecture review pushback, mentoring junior engineers, driving technical standards adoption. Design behavioral: design critique pushback, stakeholder alignment on design direction, accessibility advocacy, design system governance. Data Science: experiment design disagreement, communicating uncertainty to stakeholders, model deployment tradeoff. CS: balancing customer advocacy vs business needs, managing underperforming CSM, executive relationship rescue, cross-functional influence with Sales.

**UXR-to-PM mock questions:** If `career-plan.md` shows UXR/Research-to-PM career change (e.g., current title is UX Researcher, User Researcher, Research Lead, or similar), include at least ONE of these in every behavioral mock session:
- "You're a researcher -- can you actually make decisions with incomplete data?" -- Grade on: directness (no hedging), a specific example of deciding with <60% confidence, and a bridge showing research skill as an advantage, not a crutch.
- "Walk me through a time you drove a product decision, not just informed one." -- Grade on: ownership language ("I decided" not "I recommended"), clear outcome tied to the decision, and evidence the candidate went beyond presenting findings.
- "How would you handle disagreeing with your user research?" -- Grade on: ability to name when data should be overridden (business constraints, speed, strategic bets), a specific example, and comfort with the tension.

**DS-to-MLE-Manager hybrid mock mode:** If `career-plan.md` shows BOTH a Data Science background AND targeting ML Engineering Manager roles, run a combined mock session covering all three dimensions in a single session. Question sequencing: (1) ML system design first -- model serving, feature stores, monitoring (use system-design type with ML focus; this is typically the candidate's growth area), (2) DS case study second -- experimentation, statistical methodology (use case-study type; this validates existing strengths), (3) IC-to-Manager behavioral third -- 2-3 questions from the block below (this is the people-management growth area). Target 7-10 questions total, ~45-60 minutes. Grade each dimension independently, then provide cross-dimension feedback: "Your system design answer showed strong modeling intuition but missed the monitoring/alerting layer -- exactly the gap MLE interviews will probe."

**IC-to-Manager mock questions:** If `career-plan.md` shows IC-to-Manager transition (e.g., "first-time manager," targeting Manager/EM/Director without prior management experience), include 2-3 of these in every behavioral mock session:
- "You've never had direct reports. How would you handle a team disagreement?" -- Grade on: framework (not platitudes), specific approach to diagnosing the conflict, and evidence of informal conflict resolution from IC experience.
- "How would you balance your individual contributions with team management?" -- Grade on: realistic time allocation, willingness to let go of IC work, and a concrete plan for the first 90 days.
- "Describe how you would onboard a new hire on your team." -- Grade on: specificity of the onboarding plan (not generic "pair them with a buddy"), milestones, and how success is measured.
- "A senior engineer on your team disagrees with your technical direction. What do you do?" -- Grade on: empathy for the senior IC's perspective, structured escalation approach, and evidence the candidate can lead without pulling rank.

**VP/Director-level behavioral questions (types 15-18):** These question types are ONLY asked when career-plan.md shows the user is at Director level or above. They test executive competencies that are irrelevant for IC or early-manager candidates. When generating questions for Director+ candidates, include at least 2 of types 15-18 in every behavioral session. These questions probe for strategic judgment, organizational thinking, and executive presence -- the skills that differentiate a VP hire from a strong Senior PM.

### Step 2: Ask ONE Question
Present a single question. Do not explain what it tests. Do not give hints. Behave like a real interviewer.

Format:
```
**Question 1 of [N]:**
[The question, stated simply and directly, as an interviewer would ask it]
```

Then STOP. Wait for the user's answer.

### Step 3: Grade Using the Three Laws

After the user answers, grade immediately. Use the scoring anchors below (canonical source: `sub-agents/interview-grader.md`).

**Pre-grading check -- Word count:** Count the words in the user's answer. The word count threshold depends on input type:
- **Dictated/spoken answers (voice mode):** 400 words = ~2 minutes (spoken answers include filler words, restarts, and natural repetition that inflate word count vs. written text). Apply -2 penalty above 400 words.
- **Typed answers:** 250 words = ~2 minutes of polished spoken delivery (typed answers are denser than speech). Apply -2 penalty above 250 words.
- **Prepared/memorized answers (rewrites):** Target 200 words per the 200-Word Rule from `behavioral-interview-frameworks.md`. This is the gold standard for a practiced answer.

If the answer exceeds the threshold, apply an automatic -2 penalty to the Structure score and include this note: "This answer would run over 2 minutes in a real interview. Trim to the strongest 60 seconds."

**Solution-jumping detection (career changers):** If `interview-history.md` shows a pattern of "jumps to solutions" (common for engineers pivoting to PM), apply a -2 penalty to Law 3 (Skill Demonstration) if the user proposes a specific solution before identifying user segments, defining the problem space, or stating success metrics. The PM skill being tested in product sense questions is STRUCTURED THINKING, not solution quality. Flag: "You proposed a solution at word [N] of your answer, before defining users or success metrics. This is the #1 career-changer penalty in product interviews. Structure: users -> problems -> metrics -> solutions." Similarly, if `interview-history.md` shows "defaults to research" (common for UXR-to-PM changers), generate a conflicting-data question in every mock session: present two data sources that disagree and require a decision. Grade harshly if the user proposes more research instead of making a call.

**Under-length check (too short):** If the answer is under 75 words (typed) or 120 words (dictated), it is dangerously thin. Apply an automatic -1 penalty to Specificity and include this note: "This answer would be under 30 seconds in a real interview. The interviewer will assume you have nothing deeper. Expand with a specific example and at least one metric." A 30-second answer signals either lack of preparation or lack of experience -- both are red flags. Coach the user to hit the 200-word sweet spot.

**Verbal pattern check:** If the answer starts with "So..." or "Yeah, so..." -- note it as a common verbal tic but do not penalize. If the answer reads as stream-of-consciousness with no clear structure, flag it in Law 1: "In a real interview, the interviewer lost the thread here."

**English-as-second-language (ESL) considerations:** If `experience-library.md` or `career-plan.md` indicates the user's primary language is not English (e.g., languages listed with English as "fluent" but not "native," or international background):
- Grade on substance, structure, and specificity -- NOT on grammar, word choice sophistication, or idiomatic fluency. Minor grammatical errors, non-native phrasing, or accent-influenced word choices should be noted as coaching points but should NOT reduce the Three Laws scores. An answer with clear structure, strong metrics, and demonstrated skill is a 9/10 regardless of whether the phrasing is perfectly native.
- Flag patterns that could create misperceptions in real interviews: hedging language common in high-context cultures ("perhaps we could consider" instead of "the right approach is"), excessive use of "we" instead of "I" (common in Japanese and German professional culture where credit-sharing is valued), and understated conclusions that bury the recommendation. These are coaching points, not penalties.
- In rewrites, preserve the user's natural voice rather than converting to American-idiomatic English. The goal is the user's best self, not a different person.
- For users whose `interview-history.md` shows conciseness or assertiveness weaknesses, explicitly flag when the answer demonstrates those patterns: "This answer shows the hedging/length pattern from your interview history. Practice the 'conclusion first, evidence second' structure."

**Scoring Anchors (use these for consistent grading across sessions):**

**Law 1 -- Structure:**
- 9-10: Crystal clear structure. Interviewer knew where the answer was going at every point. Concise, well-paced.
- 7-8: Good structure with minor wandering. One section went long or lacked a signpost.
- 5-6: Recognizable structure but messy. Started organized, lost the thread partway through.
- 3-4: Stream of consciousness. The interviewer had to work to follow.
- 1-2: No discernible structure. Rambling. Multiple restarts.

**Law 2 -- Specificity:**
- 9-10: Vivid and believable. Metrics in context ("increased revenue 11%, $14M annually, from a single feature"). Named specific tools, constraints, people by role.
- 7-8: Good specifics. One or two areas where more detail would strengthen it.
- 5-6: Mix of specific and vague. Some good details buried in generic statements.
- 3-4: Mostly abstract. "We improved the metric" without which metric or by how much.
- 1-2: Entirely hypothetical or generic. No real example. Textbook answer.

**Law 3 -- Skill Demonstration:**
**[FUNCTION-ADAPTIVE]** The 'skill' being tested must match the function. PM: product judgment. SWE: engineering judgment, system design quality. Design: design thinking, user empathy. Data Science: analytical rigor, statistical correctness. CS: customer strategy, retention methodology.
- 9-10: Unambiguous demonstration. Interviewer would write "strong evidence of [skill]" on scorecard.
- 7-8: Good demonstration with one gap. Proved the skill but missed an opportunity to go deeper.
- 5-6: Partial demonstration. Answered the question but interviewer is not fully convinced.
- 3-4: Tangential. Story was fine but did not prove the skill being tested.
- 1-2: Missed entirely. Answered a different question or claimed the skill without evidence.

```markdown
## Grading: [Question]

### Law 1 — Structure [X/10]
Did you organize your answer? Signal where you were going?
Use rule of three? Stay under 2 minutes?
[Specific feedback on what worked or didn't in the structure]
[If over word count threshold: "OVER TIME: ~[estimated minutes] spoken. Automatic -2. Trim to strongest 60 seconds."]

### Law 2 — Specificity [X/10]
Did you use a real example with real metrics?
Or stay abstract? ("We improved revenue" vs "We increased
revenue 11%, $14M annually, with a single feature")
[Specific feedback pointing to vague vs concrete moments in the answer]

### Law 3 — Skill Demonstration [X/10]
Did the answer prove the PM skill this question targets?
Skill tested: [name the skill]
[Whether and how the user demonstrated it]
[Specific feedback]

### Overall: [X/10]
**Overall score = minimum of the three Law scores, not the average.** A chain-is-only-as-strong-as-weakest-link approach. An answer with Structure 9, Specificity 9, Skill Demo 3 is a 3/10 answer because it missed the point. This prevents high scores on well-structured, specific answers that fail to demonstrate the target skill (or vice versa). Display the calculation: "Overall = min(Law 1, Law 2, Law 3) = min([X], [Y], [Z]) = [result]"
[One sentence summary: what was strongest, what to fix]

### Rewrite
Using your experience library, here's how I'd restructure this answer:

[Full rewritten answer — not a summary, a complete answer the user could memorize and deliver]
[Pull specific bullets, metrics, and stories from experience-library.md]
[Note which experience-library entries were used: "Used: Story 3 (The Onboarding Overhaul) + Growth/Metrics bullet 2"]
[Keep the rewrite under 200 words (the gold standard for a prepared answer)]

**Voice matching:** The rewrite should sound like a polished version of the user's voice, not Claude's voice. If the user used humor, keep humor. If they are naturally concise, keep it short. If they use informal phrasing, preserve the informality while tightening the structure. Mark sections where you significantly changed the voice: "[restructured for clarity -- adjust to your natural phrasing]". The goal is the user's best self, not a different person.
```

### Step 4: Continue or Summarize
After grading, ask:
```
Ready for the next question? (or type "done" to end the session)
```

If the user says "done" or after 5-8 questions, proceed to the session summary.

### Step 5: Session Summary (after 5-8 questions or "done")

```markdown
## Mock Interview Summary

### Session Stats
- Questions asked: [N]
- Average score: [X/10]
- Best answer: Question [N] ([topic]) — [X/10]
- Weakest answer: Question [N] ([topic]) — [X/10]

### Score Breakdown
| Question | Structure | Specificity | Skill Demo | Overall |
|----------|-----------|-------------|------------|---------|
| Q1: [short name] | X/10 | X/10 | X/10 | X/10 |
| Q2: [short name] | X/10 | X/10 | X/10 | X/10 |
[...]

### Patterns
**Consistent strength:** [e.g., "You consistently use metrics well (Law 2 avg: 8/10). Your specificity is above average."]
**Consistent weakness:** [e.g., "Structure is your gap (Law 1 avg: 5/10). You tend to start talking before organizing. Try signposting: 'I'll cover three things: the context, my approach, and the result.'"]
**Pacing:** [e.g., "3 of 5 answers exceeded 400 words. Practice delivering the same content in half the words."]

### Recommended Practice
Based on this session and your interview-history patterns:
1. [Specific question type to practice] — Run: `/mock-interview behavioral` and ask me to focus on [type]
2. [Specific structural fix] — Practice: [concrete exercise]
3. [Specific story to develop] — Your experience library is missing a strong story for [type]. Add one.

### Interview History Update
Append a mock session entry to `context-library/interview-history.md` with the date, session type, questions asked, per-question scores, and overall average. This is required -- do not skip. Format:

```
### Mock Session — [Type] — [Date]
Questions: [N] | Avg Score: [X/10]
| Question | Structure | Specificity | Skill Demo | Overall |
|----------|-----------|-------------|------------|---------|
| Q1: [short name] | X/10 | X/10 | X/10 | X/10 |
[...]
Patterns: [1-sentence summary of strengths/weaknesses this session]
```

[After updating, confirm: "Session scores saved to interview-history.md."]
```

## Output

The output is interactive and delivered incrementally:
1. Session setup message (with voice mode recommendation)
2. One question at a time
3. Grade after each answer
4. Session summary after completion

All grading uses the exact Three Laws format specified above. No deviation.

## Example

**Input:** `/mock-interview behavioral`

**Session flow:**

1. Setup message with voice mode recommendation
2. "Question 1 of 6: Tell me about yourself."
3. [User answers via typing or dictation]
4. Grading: Structure 6/10 (went 2.5 minutes, no signposting), Specificity 8/10 (good metrics), Skill Demo 7/10 (showed PM skills but didn't address weakness). Rewrite pulls from experience-library Story 1 and Growth/Metrics bullets.
5. "Ready for the next question?"
6. "Question 2 of 6: Tell me about a time you had to push back on a stakeholder who wanted a feature you disagreed with."
7. [Continues through 6 questions]
8. Session summary showing patterns: strong on specificity, weak on structure and pacing.

## Quality Checks

1. **One question at a time.** Never ask multiple questions. Never preview upcoming questions. Behave like a real interviewer.
2. **Wait for the answer.** Do not grade until the user has responded. Do not provide hints or coaching before the answer.
3. **Honest grading.** Do not inflate scores. A 5/10 means average. A 7/10 means good. A 9/10 means exceptional. Most answers should land between 5-7. If every answer scores 8+, the grading is too lenient.
4. **Rewrites use real experience.** Every rewrite must pull from `experience-library.md`. If the experience library lacks relevant material, say so: "Your experience library doesn't have a strong story for this. The rewrite below is the best I can do with available material. Consider adding [type of experience] to your library."
5. **Word count enforcement.** Always count words. Always apply the -2 penalty for >400 words. This is the single most common interview mistake and the grading must catch it every time.
6. **No coaching before the answer.** The learning happens in the grading and rewrite, not in pre-answer hints. Keep the question clean and simple.
7. **Pattern detection.** The session summary must identify real patterns, not generic advice. If structure is consistently low, say so with specific evidence. If one Law is consistently strong, acknowledge it.
8. **Behavioral type coverage.** Across multiple sessions, ensure all 22 behavioral question types (listed above) get covered. Do not repeat the same types every session. Check interview-history.md for what has been practiced.
9. **Rewrite length.** Rewrites must be under 300 words. If a rewrite exceeds this, it fails the same pacing test as the user's answer.
10. **Voice mode reminder.** Always include the voice mode setup message. Spoken practice is materially better than typed practice.
11. **International/visa persona checks.** If career-plan.md indicates the user needs visa sponsorship or has non-US employers: (a) Include a visa logistics question ("Will you need sponsorship to work in the US?") in behavioral sessions -- this is a real question that causes friction and must be practiced. Grade the answer on confidence and brevity (target: 30 seconds, matter-of-fact tone). The rewrite must use the script from qa-master.md. (b) Include a comp expectations question ("What are your compensation expectations?") prioritized early in behavioral sessions if interview-history.md shows comp framing weakness. The rewrite must demonstrate the market-rate framing (never mention current non-US comp). (c) When rewriting TMAY answers, naturally embed employer brand context parentheticals and verify the rewrite fits within 2 minutes. (d) For ESL users whose interview-history.md shows assertiveness or conciseness weaknesses, the grading must explicitly call out hedging language and consensus-oriented framing as coaching points with specific replacement phrases.
12. **Career gap / returner mock question types.** If career-plan.md shows a career gap (e.g., gap_years > 0, or explicit mention of career break/return), add these gap-specific question types to the behavioral question bank and include at least 2 in every behavioral mock session for returners:
    - **"Tell me about your career break."** Grade based on: (a) Brevity -- answer must be under 45 seconds. If the candidate spends more than 60 seconds on the gap explanation, flag it: "OVER TIME ON GAP: You spent [N] seconds on the gap explanation. Target 45 seconds max. The gap answer is a bridge to your strengths, not the main event. Practice cutting it shorter." (b) No over-justification -- the candidate should not explain WHY they took a break. A brief factual acknowledgment is sufficient. (c) Forward-looking pivot -- the answer ends with enthusiasm for the role, not with the gap. (d) No negative self-talk -- ban phrases like "I know it's been a while," "I realize my skills may be rusty," "I hope you'll give me a chance."
    - **"How have you stayed current?"** Grade based on: (a) Specificity of activities -- vague answers ("I've been reading industry blogs") score low. Specific answers ("I completed Google's PM certification and advised a Series A startup on their onboarding flow") score high. (b) Genuine vs. performative -- the activities should feel real and substantive, not padding. If the candidate lists 5 activities but none have metrics or outcomes, flag it: "These activities feel performative. Pick the 1-2 most impactful and go deep with specifics."
    - **"What concerns might a hiring manager have about hiring someone returning from a break?"** Grade based on: (a) Ability to name the concern directly -- dodging the question scores low. "They might wonder if my skills are current" is direct and strong. (b) Evidence that mitigates the concern -- after naming it, the candidate must provide specific proof: "Here's how I've addressed that: [specific activity with metric]." (c) Confidence -- the tone should be "I understand the concern and here's why it shouldn't worry you" not "I know I have a lot to prove."
    - **Flag over-long gap answers.** If the candidate spends more than 60 seconds on ANY gap-related question, this is a signal to practice cutting it shorter. Add the coaching note: "Gap answers are a bridge, not a destination. The interviewer needs to hear enough to check the box, then wants to hear about your work. Practice the 30-second version until it's reflexive."
13. **Compound judgment questions (failed founder / shut-down company).** If career-plan.md shows founder/CEO/co-founder experience at a company that shut down, failed, or was acqui-hired at low value, add these question types to the behavioral bank:
    - "Tell me about a time your company/product failed. What did you learn?" -- Grade on: ownership (no blame-shifting), specific learnings (not generic "I learned to be resilient"), and BREVITY (under 90 seconds).
14. **Domain Jargon Detection (domain-locked career changers).** If career-plan.md shows 5+ years in a single industry AND the mock interview is simulating a company OUTSIDE the user's primary domain, apply a -1 penalty on Law 1 (Structure) for each untranslated domain-specific term. The system should maintain a running count of jargon incidents.

    Common domain jargon to flag (by industry):
    - **Healthcare:** FHIR, HL7, EMR/EHR, ICD-10, claims adjudication, formulary, prior authorization, HIPAA (OK to use but explain), meaningful use, interoperability (OK in tech contexts)
    - **Fintech:** ACH, KYC/AML, PCI compliance, issuing vs acquiring, BIN, interchange, float, ledger, reconciliation
    - **Defense/Government:** ITAR, FedRAMP, ATO, FISMA, CMMC, contracting officer, SBIR, program of record
    - **Real Estate:** MLS, escrow, title insurance, HOA, cap rate, NOI, LTV (different from fintech LTV)

    For in-domain mock interviews: jargon is acceptable and expected.

    Track jargon flag counts across sessions. If counts are not decreasing over time, recommend more translation practice.

15. **Military Jargon Detection (military-to-PM career changers).** If career-plan.md shows military background (active duty, veteran, reserves, or military titles like Captain, Major, Lieutenant, Colonel, etc.), apply these adjustments:
    - **Grade penalty (-2 on Law 1: Structure) any time the candidate uses untranslated military jargon in a general tech mock interview.** Examples of jargon to flag: "AOR" (should be "area of responsibility"), "OPORD" (should be "operational plan"), "S2/S3/S4" (should be "intelligence/operations/logistics"), "battle rhythm" (should be "operating cadence"), "MDMP" (should be "structured decision-making process"), "IPB" (should be "competitive analysis"), "CONOP" (should be "concept of operations" or "project plan"), "SIGINT" (should be "signals intelligence" or better: "data collection and analysis"), "EEI" (should be "key information requirements"), "FRAGO" (should be "updated plan" or "change order"). Flag each instance explicitly in the grading: "MILITARY JARGON DETECTED: You said '[jargon term]' -- translate to '[civilian equivalent]' for general tech interviews."
    - **For defense tech mocks:** Jargon is acceptable when the interviewer would understand it, but still flag if overused (more than 3 military terms in a single answer). The candidate should demonstrate they CAN speak civilian when needed.
    - **Add question type: "How does your military experience translate to product management?"** Grade on specificity, civilian language, and concrete PM skill mapping. A 9/10 answer names 2-3 specific PM skills, gives a translated military example for each, and connects each to the target role's requirements. A 5/10 answer says "leadership and discipline" without specifics. A 3/10 answer uses untranslated military jargon to describe military experience.
    - **Translation practice in rewrites:** Every rewrite for a military candidate must use fully translated civilian language. The rewrite should demonstrate what the answer sounds like with zero jargon. Include a note: "Compare your answer to this rewrite. Every military term has been translated. Practice until the civilian version feels natural."
    - "How would you handle disagreeing with your manager's product direction?" -- Grade on: ability to articulate following someone else's vision without resentment.
    - "Your startup had 15 people. We have 5,000. How do you adjust?" -- Grade on: specific operational awareness of how processes differ at scale.
16. **Remote-only question types.** If `career-plan.md` shows a remote-only preference, add these question types to the mock rotation (at least 2 per mock session for remote-only candidates):
    - **"Why do you prefer working remotely?"** -- Grade on: outcome-focused answer (not personal reasons), confidence (not defensive), specificity of async wins. A 9/10 answer leads with measurable output and collaboration wins. A 5/10 answer says "I just work better from home" without evidence. A 3/10 answer mentions personal reasons (caregiving, family, commute avoidance).
    - **"Would you consider coming into the office 2-3 days a week?"** -- Grade on: honest boundary-setting, positive framing, no waffling, no over-explaining. A 9/10 answer is direct and confident: "I do my best work in a distributed environment -- here's the evidence." A 5/10 answer hedges: "Maybe, it depends..." A 3/10 answer agrees to something the candidate does not want.
    - **"How do you build relationships with your team remotely?"** -- Grade on: specific examples, proactive approach described, not just "Slack and Zoom." A 9/10 answer names specific rituals, async practices, and relationship-building tactics with outcomes.
    - **"Our team really values in-person collaboration. How would you handle that?"** -- Grade on: reframe to distributed collaboration value, acknowledge their preference, offer compromise if genuine. A 9/10 answer validates their preference while presenting a compelling case for distributed work with evidence.
    - Flag if candidate over-explains (> 45 seconds on why remote) -- coaching note: "You spent [N] seconds explaining why remote. Target 30 seconds max. State the preference, give one piece of evidence, move on."
    - Flag if candidate discloses personal reasons for remote preference -- immediate coaching to reframe: "You mentioned [personal reason]. NEVER share personal reasons for remote preference in an interview. Reframe to outcomes: productivity, async collaboration wins, deep focus."
    - **Privacy guardrail:** The interviewer persona NEVER probes for personal reasons ("Is there a family reason?") -- but coach on how to deflect if it happens in real interviews: "If an interviewer asks WHY you prefer remote in a way that probes personal reasons, redirect: 'It's really about how I do my best work -- let me share some examples of what that looks like.'"

17. **Communication style overlay (veteran / 15+ years experience).** If career-plan.md shows 15+ years of experience, or experience at legacy/enterprise companies (Oracle, IBM, SAP, HP, etc.), or explicit mention of age-related concerns, add this check: Are they speaking in "executive broadcast" mode (long, authoritative monologues) vs. "collaborative conversation" mode? Many senior professionals default to the former in interviews, which younger interviewers may read as rigid or hierarchical. Grade on: conversational tone, ability to ask clarifying questions before answering, appropriate use of "I" vs. "we", and not over-referencing tenure ("In my 18 years..."). Flag if candidate name-drops too many past companies -- this can read as "living in the past." Flag if answers consistently reference experiences from 5+ years ago without connecting to current relevance.
