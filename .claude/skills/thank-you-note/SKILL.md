---
name: thank-you-note
description: Generate a personalized thank-you note referencing specific conversation moments from the interview transcript.
---

# /thank-you-note - Personalized Post-Interview Thank-You

## When to Use

Run this skill within 24 hours of an interview. Provide the interview transcript and get a thank-you note that proves you were listening. The note references specific conversation moments, adds a new thought, and stays under 150 words. Never generic. Never "thanks for your time."

Also supports **recovery mode** -- if you fumbled a question during the interview, this skill generates a follow-up document to attach to the thank-you that reframes your answer.

**Trigger:** `/thank-you-note [transcript file path] [interviewer name]`

Examples:
- `/thank-you-note ~/Documents/granola/anthropic-round2.md Sarah Chen`
- `/thank-you-note` (then paste the transcript and provide the interviewer name)
- `/thank-you-note ~/Documents/granola/stripe-round1.md David Kim --recovery "I fumbled the prioritization question"`

**Take-Home Exercise Follow-Up Mode:**
If the input is not a live interview transcript but rather a take-home exercise completion (user says "I submitted a take-home" or "product exercise"), adapt the note:
- The recipient is typically the recruiter or the hiring team (not a specific interviewer who asked questions).
- Instead of referencing "conversation moments," reference specific aspects of the exercise: the problem you analyzed, a particular insight from your research, or a methodological choice you made and why.
- The value-add becomes sharing an ADDITIONAL thought you had after submitting: "After submitting, I kept thinking about the edge case of [X]. If I were building this, I'd also want to test [Y]." This shows continued engagement without undermining the submission.
- Do NOT apologize for or correct anything in the submission. If there are weaknesses, the recovery mode handles that separately. The thank-you note should be confident and forward-looking.
- Tone is slightly more professional than a post-conversation note (since there was no personal interaction to reference). But still avoid generic phrases.

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
- Interview transcript (file path or pasted text) OR take-home exercise context (the prompt, your submission summary, and any feedback received)
- Interviewer name(s) or recruiter name -- can be a single name or a list for panel interviews

**Optional:**
- Interviewer email(s) (if known, for formatting)
- Recovery flag: a question the user feels they fumbled
- Specific tone preference (default: professional-warm, not stiff)

**Panel interview handling:** If the user provides multiple interviewer names (or the transcript reveals a panel with 2+ interviewers), generate a SEPARATE thank-you note for EACH interviewer. Each note must:
- Reference a moment specific to THAT interviewer's questions or comments (not the same moment across all notes)
- Vary the opening hook and value-add so the notes do not read identically (panelists often compare notes)
- Tailor tone to the interviewer's apparent seniority and role (e.g., more strategic for a VP, more technical for an engineering lead)
- If the transcript does not clearly attribute questions to specific interviewers, ask the user: "I can see [N] interviewers in the transcript but cannot tell who asked which questions. Can you identify who asked what? This lets me personalize each note."
- Maintain the same 150-word limit PER NOTE (not combined)

**Auto-read (do not ask the user for these -- read them directly):**
- `context-library/experience-library.md` -- for recovery mode rewrites
- `context-library/career-plan.md` -- for role enthusiasm context
- Interview debrief output (if `/interview-debrief` was run first -- use the grading to identify fumbles automatically)

## Process

### Step 1: Transcript Mining
Read the full transcript. Identify candidate moments for the thank-you note:
- A question the interviewer seemed personally passionate about (asked follow-ups, shared their own opinion, leaned in)
- A specific product discussion, technical debate, or strategic topic you discussed together
- A moment where you and the interviewer connected on a shared insight or experience
- A topic where the interviewer shared something about the company's direction, challenges, or culture
- Any moment the interviewer said something revealing about what they care about

Rank moments by:
1. How personal/specific the moment was (the more unique to this conversation, the better)
2. Whether you can add a genuinely useful follow-up thought
3. Whether it reinforces your fit for the role

Select the top 2-3 moments.

### Step 2: Draft the Thank-You Note
Write the note following these rules:

**Structure:**
1. **Opening hook** (1 sentence): Reference the most specific conversation moment. Not "Thank you for your time" -- instead, lead with the substance. Example: "I've been thinking more about the latency tradeoff you mentioned in the caching discussion."
2. **Add value** (1-2 sentences): Contribute a new thought, resource, perspective, or data point related to that moment. This proves you are still thinking about the problem, not just going through the motions.
3. **Second moment** (1 sentence, optional): Brief reference to another specific moment that stood out.
4. **Enthusiasm close** (1 sentence): Genuine, specific enthusiasm for the role. Not "I'm excited about the opportunity" -- instead, reference something specific: "The [specific project/challenge/mission] you described is exactly the kind of problem I want to spend the next few years on."

**Hard rules:**
- Under 150 words. Count them. If over, cut.
- NEVER use: "Thank you for taking the time," "I enjoyed our conversation," "I look forward to hearing from you," or any other generic filler
- NEVER open with "Thank you" -- open with substance
- Every sentence must contain information specific to THIS conversation. A reader should be able to tell exactly which interview this note is about.
- Subject line: "[Specific topic from conversation] - [Your Name]" (not "Thank you for the interview")

### Step 3: Recovery Mode (if applicable)
If the user flagged a fumbled question, or if `/interview-debrief` scored any question below 4/10:

1. Identify the fumbled question and what went wrong
2. Generate a follow-up document (1 page max) that demonstrates the user's real capability:
   - Frame it naturally: "I realized I jumped to solutions on [question]. After reflecting, here's how I'd typically approach this:"
   - Write the proper answer using `experience-library.md` for real examples and metrics
   - Format it as a clean, professional mini-document (not an essay -- use headers, bullets, structure)
   - Keep it focused: address the specific fumble, do not re-answer every question
3. Integrate the recovery into the thank-you note:
   - Add one sentence referencing the topic: "I've been reflecting on your question about [topic] and put together a brief writeup of how I typically approach [the underlying problem]."
   - Attach the document as a follow-up

**Recovery document format:**
```markdown
# [Topic]: My Approach

After our conversation, I wanted to share my fuller thinking on [topic].

## Context
[1-2 sentences framing why this matters]

## My Typical Approach
1. [Step 1 with specific detail from experience-library]
2. [Step 2 with specific detail]
3. [Step 3 with specific detail]

## Example from My Experience
[Brief example pulling from experience-library -- real project, real metrics, real outcome]

## Key Takeaway
[1 sentence tying it back to the role]
```

## Output

### Standard Thank-You Note

```
Subject: [Specific conversation topic] - [Your Name]

Hi [Interviewer Name],

[Opening hook referencing specific conversation moment — 1 sentence]

[Value-add: new thought, resource, or perspective on that topic — 1-2 sentences]

[Optional: second specific moment reference — 1 sentence]

[Enthusiasm close tied to specific role/mission/challenge — 1 sentence]

Best,
[Your Name]
```

Word count: [X]/150

### Recovery Thank-You Note (when applicable)

```
Subject: [Topic from fumbled question] - [Your Name]

Hi [Interviewer Name],

[Opening hook referencing the conversation — 1 sentence]

[Value-add on a strong moment — 1 sentence]

[Recovery reference: "I've been reflecting on your question about [topic] and put together a brief writeup of my approach. Attached/linked below." — 1 sentence]

[Enthusiasm close — 1 sentence]

Best,
[Your Name]

---
[Attached: Recovery document]
```

## Example

**Input:** `/thank-you-note ~/Documents/granola/anthropic-round2.md Sarah Chen`

**Transcript contains:** Discussion about Claude Code's developer experience, a debate about whether to optimize for power users vs new developers, Sarah mentioned her team's internal metric for "time to first useful output," and the user shared a story about redesigning onboarding at their previous company.

**Output:**
```
Subject: Time to first useful output - [Your Name]

Hi Sarah,

Your "time to first useful output" metric stuck with me -- it's a cleaner frame
than the activation proxies I've typically used. I sketched out how that metric
might decompose differently for CLI power users vs GUI-first developers, and I
think the segmentation reveals where the real onboarding leverage is.

The tension you described between depth for power users and accessibility for
newcomers is exactly the kind of product problem I find most energizing -- it
reminds me of the onboarding tradeoffs I navigated at [Company], where we found
that the "power user path" and "new user path" actually converged sooner than
expected.

Building developer tools that make people feel capable on day one is the work I
want to do next.

Best,
[Your Name]
```

Word count: 131/150

**[FUNCTION-ADAPTIVE]** The example above is for a PM interview. For other functions, the conversation topics and value-adds would be function-specific (SWE: technical architecture discussion, system design tradeoff; Design: design process debate, user research methodology; Data Science: modeling approach, experiment design; CS: customer strategy, retention framework) but the structure is the same.

## Quality Checks

1. **Word count: 150 max.** Count every word. If the draft exceeds 150, cut until it does not. This is not a guideline -- it is a hard limit. Long thank-you notes are not read.
2. **Zero generic phrases.** Scan the output for: "thank you for your time," "I enjoyed our conversation," "I appreciate the opportunity," "I look forward to hearing." If any appear, rewrite. These phrases signal "template" to the interviewer.
3. **Conversation-specific proof.** Every sentence in the note must contain at least one detail that could ONLY come from this specific interview. If a sentence could apply to any interview at any company, it fails this test.
4. **Subject line is substance, not courtesy.** The subject line should reference a specific topic from the conversation. Never "Thank you" or "Following up" as the subject.
5. **Value-add is genuine.** The new thought, resource, or perspective must be genuinely useful, not filler. If you cannot add real value, keep the note shorter rather than padding with empty additions.
6. **Recovery mode auto-triggers.** If `/interview-debrief` was run and any question scored below 4/10, proactively suggest recovery mode even if the user did not flag it: "Your debrief shows you scored [X/10] on the [topic] question. Want me to generate a recovery document to attach to the thank-you?"
7. **Recovery document stays focused.** The recovery attachment addresses one question, not the whole interview. It should feel like a natural follow-up ("I kept thinking about this") not an apology or correction.
8. **Send timing reminder.** Always include at the end: "Send within 24 hours of the interview. Same-day is best."
9. **Panel interview deduplication.** When generating multiple notes for a panel interview, compare all notes before presenting them. No two notes should reference the same conversation moment as their primary hook. No two notes should open with a structurally identical sentence. If a panelist did not speak much or ask memorable questions, it is acceptable to write a shorter note (as few as 80 words) rather than fabricating substance.

---

## Persona-Specific Thank-You Rules

### Career Returner Thank-You Rule
Conditional on `career-plan.md` showing a career gap > 1 year:
- If the gap came up in the interview: include ONE subtle "currency signal" in the value-add section. Example: "After our conversation about [topic], I dug deeper into [current trend] — here's what I found compelling..." This signals current relevance without explicitly addressing the gap.
- If the interviewer probed the gap specifically and it went poorly: the value-add section should demonstrate current expertise WITHOUT referencing the gap. Show, don't tell.
- NEVER use the thank-you note to re-explain or justify the gap. Forward momentum only.
- Privacy guardrail: never reference caregiving, health, or personal reasons for the gap.

### Failed Founder Thank-You Rule
Conditional on `career-plan.md` showing founder/CEO at a shut-down company:
- If "stability concern" or "can you take direction?" surfaced in the interview: include a team-collaboration signal. Example: "I was particularly struck by [interviewer's] perspective on [topic] — that's exactly the kind of strategic depth I want to contribute to."
- If the failure narrative went long or poorly: use the value-add section to demonstrate FOCUSED depth (not breadth) — show you can go deep on one area, not run the whole company.
- NEVER use the thank-you to re-explain the failure or the startup's shutdown. Forward focus only.
- If the company is founder-friendly (startup, etc.): can lean slightly into the builder narrative. If enterprise: pure PM framing.

### Remote-Only Thank-You Rule
Conditional on `career-plan.md` showing remote-only preference:
- If remote work was discussed during the interview and received positively: reinforce with a brief mention: "I appreciated the team's embrace of distributed collaboration — it's where I do my strongest work."
- If remote was a friction point: do NOT over-address it. Include a subtle async competence signal: "I've been thinking about [specific problem discussed] and drafted some initial thoughts — would love to share async."
- Privacy guardrail: NEVER reference why the candidate needs/prefers remote (caregiving, health, family, location constraints).

### Veteran (15+ Years) Thank-You Rule
Conditional on `career-plan.md` showing 15+ years of experience or experience at legacy/enterprise companies:
- Tone check: the thank-you note must NOT read like a formal corporate memo. It should be conversational, direct, and relatively brief. Flag if the draft uses passive voice, "I would be remiss," "I appreciated the opportunity to discuss," or other formal enterprise phrasing.
- Include a tech currency signal: reference something modern/current from the interview conversation to combat the "not current" perception.
- Do NOT reference total years of experience or say "in my X years..."
- Legacy employer de-emphasis: if referencing past work, lead with WHAT not WHERE.

### Military-to-PM Thank-You Rule
Conditional on `career-plan.md` showing military background:
- Jargon recovery: if ANY military jargon leaked during the interview (check interview-debrief if available), the thank-you note is the place to deliver the civilian reframe. Example: if the candidate said "AOR" in the interview, the note could naturally reference the concept using civilian language: "I've been thinking more about defining scope boundaries for the initiative we discussed..."
- Bridge narrative reinforcement: include one line connecting military experience to PM relevance using fully civilian language.
- For defense tech: can reference shared military context warmly. For general tech: pure civilian framing.
- Do NOT lead with "As a veteran..." or "From my military experience..."

### Executive-Level Thank-You Rule
Conditional on `career-plan.md` showing VP/Director/CPO/SVP level AND 12+ years experience:
- Tone shift: peer follow-up, not candidate gratitude. Replace "Thank you for taking the time" with direct engagement: "Great conversation about [specific strategic topic]."
- Value-add upgrade: strategic observation, not operational insight. Instead of "Here's a metric I found," offer "Here's a perspective on the strategic challenge we discussed" -- the kind of insight a board member or executive peer would share.
- No over-qualification: do not re-prove credentials. At VP level, the thank-you note continues the strategic dialogue, not the interview evaluation.
- Keep 150-word limit but shift ratio: 60% strategic continuation, 30% enthusiasm for scope/team, 10% logistics.

### Board Member / Investor Thank-You Rule
Conditional on interviewer identified as board member, investor, PE/VC partner, or compensation committee member:
- **Shorter than standard:** 3-4 sentences max. Board members and investors evaluate judgment and signal quality, not thoroughness. A long note signals candidate-mode thinking.
- **Lead with investment-thesis alignment**, not product-specific detail. Frame around the strategic inflection point, not the feature roadmap.
- **Tone:** brief, high-conviction, no hedging. No detailed product analysis. Board members assess whether you think like an executive, not whether you can do the IC work.
- **Example framing:** "Our conversation confirmed my conviction that [Company] is at an inflection point where [strategic thesis]. I'd be energized to help navigate that transition."
- **No value-add attachment or recovery doc.** A follow-up document to a board member reads as over-eager. The note itself is the entire communication.
- Override the 150-word limit downward: target 60-80 words.
