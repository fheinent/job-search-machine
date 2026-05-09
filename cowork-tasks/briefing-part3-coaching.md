---
name: briefing-part3-coaching
description: Part 3 of daily briefing. Pipeline health, bottleneck detection, skill coaching.
---

# Morning Briefing — Part 3: Coaching
# Pipeline health, interview coaching, priority stack

**Time:** 7:20 AM (runs 10 min after Part 2) | **Duration:** 5-7 min | **Output:** `briefings/briefing-{DATE}-part3-coaching.md`
> This part reads today's Part 1 and Part 2 outputs for full context.

---

Read all files in the job-search-os/context-library/ folder. Also read job-search-os/CLAUDE.md for system rules. Read today's outputs: `briefings/[YYYY-MM-DD]-part1-roles.md` and `briefings/[YYYY-MM-DD]-part2-networking.md`.

## Quality Gate

Verify these files contain real data (not template placeholders):
1. **career-plan.md** -- Required for persona detection and coaching. If empty, STOP.
2. **interview-history.md** -- Needed for weakness coaching. If empty, skip that section.
3. **app-tracker.md** or alternative sources (`target-companies.md`, `connection-tracker.md`) -- Needed for pipeline summary.

Read `career-plan.md` to detect the user's target function. Pipeline benchmarks and drills adapt to function.

---

## Pipeline Summary

Build from app-tracker.md (or assemble from target-companies.md, connection-tracker.md, interview-history.md, briefings/).

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

Analyze the pipeline and flag the single biggest bottleneck:

- **High volume, no referrals** (apps > 10, referrals = 0): "YOUR BOTTLENECK: Referrals. Cold apps have 3-5% callback vs 15-25% with referrals. Focus on networking. No more cold applications without a referral path."
- **Referrals not converting** (referrals > 5, interviews = 0): "YOUR BOTTLENECK: Resume/Positioning. Referrals not converting. Check coverage scores. Run `/linkedin-audit`."
- **Interviews without prep** (interviews > 2 this week, no `/interview-prep` run): "YOUR BOTTLENECK: Preparation. [N] interviews without prep. Run `/interview-prep` for each before anything else."
- **Zero volume** (0 apps this week): "YOUR BOTTLENECK: Volume. Submit at least 2 today. If no 70+ roles, expand target list or adjust career-plan.md."
- **Early career, early weeks** (< 3yr exp AND weeks 1-4): "EARLY-CAREER PACING: Prioritize referral coverage over volume. 3-5 quality apps/week with referral paths. Create 1 work product this week."
- **Healthy pipeline** (steady apps, referral rate > 40%, interviews converting): "Pipeline healthy. [N] apps, [X]% referral rate, [N] interviews. Focus: [most impactful single action]."
- **Visa + weak US network** (visa needs AND near-zero US connections): "YOUR BOTTLENECK: US Network. Prioritize networking. Target alumni and diaspora connections."
- **Comp framing weakness** (comp score < 7/10 AND interviews scheduled): "PREP ALERT: Comp framing scored [X/10]. Rehearse: never state current non-US comp, cite levels.fyi market rate. Run `/mock-interview behavioral` for comp drill."
- **Career changer translation gap** (career changer AND translation < 6/10): "TRANSLATION BOTTLENECK: [question type] scored [X/10]. Run `/mock-interview behavioral` 5 times. Experience is strong -- problem is translation."
- **Dual-track interviews** (split strategy AND different-domain interviews this week): "DUAL-TRACK PREP: Run `/interview-prep` for EACH separately. Do not use same TMAY for both."
- **Relocating + weak target-location network**: "RELOCATION NETWORKING: Allocate 40%+ of connection requests to [target location]. Mention relocation in follow-ups."
- **Unknown employer brands**: "BRAND AWARENESS: Employers not household names. Verify LinkedIn About includes parentheticals. Practice TMAY with embedded employer context."

---

## Persona-Specific Coaching

### Remote-Only Candidate
If career-plan.md shows remote-only or caregiver/family constraints: review Part 1 role scan for hybrid/onsite warnings. Confirm Part 2 prioritized remote-friendly companies.

### Career Returner
If career-plan.md shows a career gap:
- **Return-to-work programs:** Search for active returnship programs at target companies (Path Forward, iRelaunch, company-specific). Report findings or suggest companies with known programs.
- **Gap narrative tracking:** If interview-history.md shows gap questions were asked, report scores and coaching: "If improving: 'Gap answer is tightening.' If not: 'Run `/mock-interview behavioral` -- target under 45 seconds, forward-looking, no over-justification.'"

### Senior-Level / Employed
If Director+ AND currently employed:
- Condense priority stack to 60-90 minute morning block: (1) respond to active conversations, (2) send 3-5 high-quality requests, (3) review new roles at top 10, (4) advance one work product. Everything else to weekend.
- Confidentiality note at top of output.

### Founder-to-Employee
If founder/CEO at shut-down company:
- **Founder narrative drill:** "Practice 30-second founder story. Lead with [Strong Brand], then: what you built, what you learned, why THIS role. Time yourself -- cut the middle if over 30 seconds."
- **Comp anchor warning:** "Your founder salary was $[X]. Market rate is $[Y]. Do NOT disclose founder comp. Use market-rate framing from qa-master.md."
- **Stability signal prep:** "Rehearse one story where you deferred to someone else's judgment or supported another leader's vision."

### Veteran / 15+ Years Experience
If 15+ years or legacy/enterprise employers:
- **Resume-stage rejection monitoring:** If rejection rate > 70% at resume stage, surface warning with actions: run resume-tailor with veteran compression, run linkedin-audit for age-signal review, increase referral coverage to 80%+.
- **Interview energy reminder:** "Lead with curiosity, not authority. Reference recent work (last 2-3 years) first. Avoid 'back in my day' framing."

### Military Background
If military background detected:
- **Dual-track split** (if both defense and general tech): Defense track uses mission-context framing, clearance emphasized. General track uses fully translated civilian language.
- **Translation drill:** "Today's story: [story from experience-library.md]. Practice in 90 seconds with zero military jargon. Record yourself. Flag terms a civilian recruiter would not understand."

---

## Interview Weakness Coaching

Read `interview-history.md` for documented weakness patterns. If any question type averages 6/10 or below:

- "SKILL GAP: [Question type] averaging [X]/10. Today's drill: Run `/mock-interview [type]` and practice [specific question] until you score 7+. Estimated time: 30 minutes."

- If interviews scheduled this week match a weakness: "URGENT PREP: [interview type] at [Company] this week, and [weakness] score is [X]/10. Run `/interview-prep [Company]` and `/mock-interview [type]` before the interview. Highest-priority action today."

- If fewer than 3 interviews logged, skip this section.

---

## Today's Priority Stack

Based on pipeline health check, persona coaching, and interview weakness coaching, generate the priority order:

1. [Highest priority action with specific instruction]
2. [Second priority]
3. [Third priority]
4. [If time permits]

Estimated time: [X] minutes total

**SENIOR-LEVEL / EMPLOYED MODE:** Cap at 60-90 minutes. Structure for a focused morning block.

---

## Output

Save everything to `job-search-os/briefings/[YYYY-MM-DD]-part3-coaching.md` using this format:

```markdown
# Part 3: Pipeline & Coaching - [Full Date]

## Pipeline Summary
[Pipeline table]

## Pipeline Health Check
[Bottleneck analysis]

## Persona Coaching
[Any applicable persona sections]

## Interview Weakness Coaching
[Drills and urgent prep]

## Today's Priority Stack
1. [Action]
2. [Action]
3. [Action]
4. [If time permits]

Estimated time: [X] minutes
```

---

## Sample Output

**Example output from May 8, 2026 for Monica Vega (Staff PM, infrastructure focus):**

```markdown
# Part 3: Pipeline & Coaching - Wednesday, May 8, 2026

## Pipeline Summary

| Stage | Count | Details |
|---|---|---|
| Applied (waiting) | 3 | Oldest: Company A (6 days) |
| Referral requested | 1 | Databricks Vector DB PM (requested May 6) |
| Interview scheduled | 1 | Lodgify (May 11, 2:00 PM) |
| Interviewed (awaiting result) | 0 | -- |
| Offer stage | 0 | -- |
| Rejected this week | 0 | -- |

**Active applications total:** 4
**Interviews this week:** 1

---

## Pipeline Health Check

**YOUR BOTTLENECK: Volume & Referrals**

You have only 3 active applications and 1 referral in flight. At this pace (1 week, 3 apps), you're tracking toward ~12 applications in a 12-week search — below the 20-30 you need. Even stronger: only 1 of 4 has a referral path activated.

**Action:** Today's Part 1 delivered 3 strong new roles (Databricks 88, Vercel 82, Anthropic 79). ALL THREE have referral paths identified (Sarah Chen is warm; others need light networking). Submit all 3 tailored resumes + send referral messages today.

**Secondary pattern:** You've done good company research (Databricks, Vercel are both top-tier fits). Quality is high. Problem is quantity + referral activation.

---

## Persona Coaching

### Staff-Level + Infrastructure Focus

Your positioning is strong (11 years, Staff PM, infrastructure depth). No early-career pacing needed. Focus on:
1. **Tier 1 company access:** You have warm connection to Databricks (Sarah Chen). Prioritize that first.
2. **Referral velocity:** Part 2 identified good cold contacts across Databricks, Vercel, Anthropic. Start with warm (Sarah), then cold (the 12 connection requests in Part 2).
3. **Compressed timeline:** You're employed at AcmeAI and presumably need to give notice (3 months). This means you should have an offer by early August at latest. 12-week window is tight for Staff-level hiring cycles (typically 8-12 weeks per company). Start the serious applications now.

---

## Interview Weakness Coaching

You have 1 interview scheduled (Lodgify, May 11). Before that interview, run:

1. **Company research:** `/company-research Lodgify` (5 min) — understand their product gaps, infrastructure challenges
2. **Interview prep:** `/interview-prep Lodgify "Senior PM"` (10 min) — likely questions for PM role
3. **Mock practice:** If you're weak on any pattern from interview-history.md, run `/mock-interview [type]` (20 min)

*Note: interview-history.md is empty. After this Lodgify interview, log results there so coaching can identify patterns.*

---

## Today's Priority Stack

1. **[URGENT] Send Databricks referral message to Sarah Chen** (2 min)
   - Use draft from Part 2 output
   - Goal: Get warm intro to hiring manager by end of week
   - If Sarah responds within 24h, you're in the top 10 candidates

2. **[URGENT] Submit tailored resumes for Databricks, Vercel, Anthropic** (5 min)
   - Part 1 already generated these. Copy into application forms.
   - Verify resume keyword coverage one more time before submitting

3. **[HIGH] Send 5 cold connection requests to Databricks + Vercel team members** (5 min)
   - From Part 2 list: Alex Torres, Sam Reyes (Databricks), Priya Sharma (Vercel)
   - Goal: Build backup intro paths in case Sarah doesn't deliver

4. **[MEDIUM] Prep for Lodgify interview (May 11)** (30 min)
   - Run `/company-research Lodgify` (what are they building, what problems do they have)
   - Run `/interview-prep Lodgify "Senior PM"` (typical PM questions, company context)
   - Review your STAR story about [infrastructure scaling] to fit their context

5. **[IF TIME] Work on work product for strongest role** (30 min optional)
   - Databricks is your #1 target. Create a strong work product to send alongside referral
   - Prompt: `/work-product Databricks "Principal PM Vector DB" get-interview`

---

**Estimated time:** 47 minutes (4-5 core actions) + 30 min optional (work product)

**If you do nothing else today, do #1-3.** Those three actions move the needle on your #1 bottleneck (referral activation).

---

## Mid-Week Checkpoint

By Friday (May 10):
- ✓ Did Sarah respond to the Databricks referral message?
- ✓ Were the 3 tailored resumes submitted?
- ✓ Did any of the 5 cold connections accept?
- ✓ How did the Lodgify interview go (May 11 afternoon)?

If all 4 are true, your pipeline will be in much healthier shape by Monday.
```

---

This briefing is your morning compass. Use it.
