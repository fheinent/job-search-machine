# START HERE

Welcome to Job Search Machine. This is a Claude Code system that helps you land interviews through precision targeting, strategy, and compounding effort over 8-12 weeks. This is not intended to be an automated, massive application tool that hits on every open role like if you were playing Whac-a-Mole.

**First session: 30 minutes. No setup required.**

---

## What This System Does

1. **Vets jobs** → Tells you in 60 seconds if a Job Description (JD) is worth your time based on your experience, what you are looking for and other preferences.
2. **Customizes resumes** → ATS-optimized, tailored to each role from your real experience. Not generic information, useless buzzwords, nor fabricated achievements.
3. **Preps interviews** → Combines web research, insider company data (when available in context, otherwise does a search), and your past patterns.
4. **Creates differentiation** → Work products that show insight, not just tell it.
5. **Finds referrals** → Activates your network with precision messaging.
6. **Negotiates offers** → Analyzes leverage, structures counter-offers, sets walkaway numbers.

**Core principle:** 20-30 minutes per day, 50-100 quality applications, 8-12 week window.

---

## Your First 30 Minutes

### Step 1: Populate Your Experience Library (15 min)

Open `context-library/experience-library.md`. Fill in:

1. **Your current level & target level** (Senior PM applying for Director? IC PM for the first time?)
2. **Your work history** — every role, company, years (no gaps)
3. **5-10 concrete accomplishments** with metrics:
   - "Led checkout redesign, increasing conversion 8%"
   - "Built and shipped feature to 2M daily users"
   - "Doubled engagement through A/B test framework"
4. **STAR stories** — 3-5 stories that illustrate how you solve problems

Don't overthink it. Rough notes are fine. The system will structure and surface them later. **Even better, dictate it. Humans speak much faster than typing**, and usually give better context and detail. In case you need it, **here's a link the Wispr Flow** https://wisprflow.ai/r?FEDERICO167 (it includes a referral bonus of **1 free PRO Plan month** for you). If you take notes with AI, **Granola** is the best tool for interview transcription: https://join.granola.ai/t/r7x3292aj5 (referral bonus included).

**IMPORTANTE** This will be your personal OS during your job search journey. You can do with it whatever you want. But let me give you some advice: **skipping Step 1 is not in your best interest**. If you do, every skill output will be generic. Blank library = blank resume.

### Step 2: Define Your Target (10 min)

Open `context-library/career-plan.md`. Answer:

1. What level are you targeting? (IC PM, Senior PM, Director, VP?)
2. What function? (Core Product, AI/ML, Growth, Platform?)
3. What company types? (Startups, scaleups, FAANG, deep tech?)
4. What's your ideal offer? (Salary range, equity, remote, impact?)
5. What's a deal-breaker? (Legacy tech stack, travel, bad culture, slow-moving?)

In some cases, the system will already have enough information from your experience library to answer these questions. If that's the case, you can skip this step.

### Step 3: Try Your First Vet (5 min)

Find any job posting (Linkedin, Glassdoor, Indeed, Infojobs, HN, Angel List — anywhere).

Copy the JD and run:

```
/quick-start [paste the JD here]
```

The system will give you:
- Red flags in 10 seconds
- Salary estimate for that market/level (if publicly available)
- Interview intel for that company
- Verdict: pursue, pursue with referral only, or skip

---

## Next: Build Your Target List

Once your experience library is decent, run:

```
/company-research [company name]
```

to research companies. Build your target list of 50-100 companies ranked by:
1. **Mission fit** (do you believe in what they do?)
2. **Role fit** (do they have roles that match your target?)
3. **Network fit** (do you have connections inside?)

Save your ranked list to `context-library/target-companies.md`.

---

## Then: Start the Rhythm

**Weekly rhythm (20-30 min per day, 5 days/week):**

- **Day 1:** Review target list, identify 3-5 to pursue this week
- **Day 2-4:** For each role:
  - Run `/job-fit-scorer` (5 min) → decide
  - Run `/resume-tailor` (15 min) → customize
  - Run `/hiring-manager-msg` (10 min) → find HM contact
  - Send application + message
- **Day 5:** Run `/weekly-retro` (20 min) → assess pipeline, patterns, next week

---

## Available Commands

See `CLAUDE.md` for the full skill list. Key ones:

| Command | When | Time |
|---------|------|------|
| `/quick-start [JD]` | Found a posting, vet it fast | 2 min |
| `/job-fit-scorer [JD]` | Want a score before investing | 5 min |
| `/resume-tailor [JD]` | Ready to apply | 15 min |
| `/interview-prep [company]` | Interview scheduled | 20 min |
| `/work-product [role]` | Show insight before applying | 30 min |
| `/weekly-retro` | End of week checkpoint | 20 min |

---

## Common Mistakes

**Blank experience library → Generic output.** You get what you put in. Spend 15 min populating it. Or whatever amount of time you want until you feel comfortable with it.

**Pursuing everything.** Vet first with `/quick-start` or `/job-fit-scorer`. Not every role is worth your time.

**Skipping the referral path.** Cold resumes get lost. Referrals get reviewed. Use `/referral-request` early.

**Waiting for perfection.** First application won't be your best. 5th application will be better. 20th will be tight.

---

## How Long?

**Please keep in mind that the timeline below is based on a typical job search, but you can adjust it to your needs.**

- **Weeks 1-2:** Setup, library building, first 5-10 applications
- **Weeks 3-6:** Pipeline filling, interview prep, pattern spotting
- **Weeks 7-10:** Interviews advancing, work products sharpening, negotiation prep
- **Week 11+:** Offer(s) land, negotiation

Based on my experience, most people see first interviews in week 3-4, offers in week 8-12.

---

## You're Ready

Go fill `context-library/experience-library.md` for 15 minutes. When you feel ready with it, run `/quick-start` on any job you find to get a sense of how the system works.

Questions? Check `CLAUDE.md` for skill details or the `/` command hints.

Live long and prosper 🖖