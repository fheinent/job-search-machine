# Job Search Machine

A Claude Code system that lands interviews through precision targeting, not volume.

---

## The Problem

You can apply to 50 roles. Or 500. You'll likely get 2-5 interviews either way. The bottleneck isn't luck... it's **strategy**.

Most job search advice is generic: "Tailor your resume. Network more. Practice interviews." All true. All insufficient.

**What's missing:** A system that adapts to *your* specific constraints (career gap, seniority level, visa status, location), *your* actual experience (not buzzwords), and *your* target companies (not every role that's hiring). And a system that compounds—each week gets better because you're learning patterns, not just grinding applications.

This is that system.

---

## What This Does

Run Claude Code skills to:

1. **Vet jobs in 60 seconds** (`/quick-start`) — Red flags, salary estimate, interview intel, verdict
2. **Tailor resumes** (`/resume-tailor`) — ATS-optimized, grounded in your real experience
3. **Prep interviews** (`/interview-prep`) — Company research + your past patterns + role-specific questions
4. **Create differentiation** (`/work-product`) — Work products that show insight, not tell it
5. **Find referrals** (`/referral-request`, `/connection-request`) — Activate your network with precision messaging
6. **Negotiate offers** (`/negotiate`) — Analyze leverage, structure counter-offers, walkaway numbers
7. **Track pipeline health** (`/app-tracker`, `/weekly-retro`) — See bottlenecks, adjust strategy weekly

**All 18 skills adapt to your function.** This works for PMs, engineers, designers, data scientists, marketers, CS/sales. Not just PM-focused.

---

## How It Works (5 Minutes)

### Setup (Your First 30 Minutes)

1. **Extract and open** this folder in Claude Code
2. **Fill `context-library/experience-library.md`** — Copy your resume + LinkedIn. Add 5-10 STAR stories with metrics. (Rough notes are fine; Claude structures them.)
3. **Fill `context-library/career-plan.md`** — Target role, company types, salary range, deal-breakers
4. **Run `/quick-start [any job posting]`** — Get a vet in 90 seconds
5. **That's it.** You've used the system.

See `setup/first-session-checklist.md` for the full 30-min walkthrough.

All with examples so you always know how to use the system. After installing, take a look at `setup/example-experience-library.md` and `setup/example-career-plan.md`.

### Weekly Rhythm

- **Day 1:** Review your target list, pick 3-5 to pursue
- **Days 2-4:** For each role, run `/job-fit-scorer`, `/resume-tailor`, `/hiring-manager-msg`, apply
- **Day 5:** Run `/weekly-retro` — See patterns, adjust strategy for next week

**Time:** 20-30 minutes per day, 5 days a week. Not 40 hours grinding.

---

## What's Included

### 18 Skills

| Skill | When | Time |
|-------|------|------|
| `/quick-start` | Found a posting, vet it fast | 2 min |
| `/job-fit-scorer` | Want a score before investing | 5 min |
| `/resume-tailor` | Ready to apply | 15 min |
| `/interview-prep` | Interview scheduled | 20 min |
| `/work-product` | Show insight before applying | 30 min |
| `/mock-interview` | Practice a specific question type | 10-20 min |
| `/interview-debrief` | Just finished an interview | 15 min |
| `/thank-you-note` | Post-interview follow-up | 5 min |
| `/negotiate` | Offer on the table | 30 min |
| `/weekly-retro` | End of week checkpoint | 20 min |
| + 8 more | Connection requests, cover letters, salary research, company research, etc. | 5-15 min each |

All skills adapt to your **function** (PM, SWE, Design, Data Science, Marketing, CS/Sales), **seniority**, and **special cases** (career returner, visa, founded a company, military background, executive-level, remote-only, etc.).

### 4 Sub-Agents

- **interview-grader** — Grades your answers using Three Laws framework (Structure, Specificity, Skill Demonstration)
- **hiring-manager-reviewer** — Reviews your work products; tells you if a HM would take a meeting
- **ats-checker** — Scans resumes for ATS blockers
- **recruiter-reviewer** — First-impression feedback on resumes

### Context Library (You Fill These with Claude's help)

- `experience-library.md` — Your work history, stories, accomplishments
- `career-plan.md` — Target role, companies, constraints, compensation
- `target-companies.md` — 50-100 companies ranked by fit
- `qa-master.md` — Comp strategy, common questions, logistics
- `app-tracker.md` — All applications (auto-logs from skills)
- `connection-tracker.md` — Your network + outreach status
- `interview-history.md` — Interview debriefs (builds patterns)
- `referral-tracker.md` — Who referred you where, status

### Templates

- **Prototype Prompt Template** — How to structure work products
- **Referral Tracker Template** — How to track warm intros
- **Example Experience Library** — Monica Vega's real profile (use as guide)
- **Example Career Plan** — Monica Vega's targets (use as guide)

### Automation (Optional)

- **Morning Briefing System** — Runs at 7am via Cowork. Three parts: scan for new roles, network intel, pipeline coaching. See `cowork-tasks/` for the system.
- **Google Calendar Integration** — Logs interview dates, alerts you for prep
- **Granola Integration** — Auto-transcribes interviews, saves to transcript folder

None of this is required. All skills work manually in Claude Code. Automation just removes friction.

---

## Constraints & Honesty

### You Must Fill Your Context Library

Blank library = blank output. No system compensates for that. Spend 15 minutes populating `experience-library.md` or the system will be generic.

### This Is Not a Guarantee

This system increases your interview rate and offer conversion rate *if you use it consistently*. If you apply to everything without vetting, skip the referral path, or don't prep for interviews, the system doesn't help. It's leverage, not magic.

### The Timeline

Based on 50-100 quality applications across 8-12 weeks:
- **Weeks 1-2:** Setup, library building, first 5-10 applications
- **Weeks 3-6:** Pipeline filling, first interviews (week 3-4 typical), pattern spotting
- **Weeks 7-10:** Interviews advancing, work products sharpening
- **Week 11+:** Offer(s) land

Most people see their first interview by week 3-4, offers by week 8-12. Your timeline depends on market fit, visa constraints, level, and how consistent you are.

---

## Getting Started

1. **Clone/Download** this repository and **open** in Claude Code
2. **Read** `START-HERE.md` — 5 minutes for the full orientation
3. **Do** `setup/first-session-checklist.md` — 30 minutes for setup
4. **Run** `/quick-start [any job posting]` — 2 minutes for your first vet
5. **Then** follow the weekly rhythm above

Questions? Each skill file has detailed documentation. Check `CLAUDE.md` for a full skill reference.

---

## How This Was Built

This system was built by combining:
- **20+ years of product leadership** across hiring loops (as candidate and interviewer)
- **200+ interviews conducted** as interviewer
- **Hundreds of job search patterns** from candidates across functions
- **Claude AI** for research, tailoring, interviewing, and analysis
- **Amazing contributions from other AI developers and content creators** such as Aakash Gupta (main inspiration), Pawel Huryn, Lenny Rachitsky, and others.


The skills are not boilerplate templates. They're specific rules, guardrails, and patterns extracted from real hiring. Example: the `/negotiate` skill encodes compensation strategy, equity analysis, and walkaway number methodology. The `/interview-prep` skill encodes company research + your past patterns + role-specific question types.

---

## License

MIT. Use it, modify it, build on it. Make it better. Just include the license in your copy.

---

## Feedback

If you find bugs, have ideas, or discover gaps, open an issue. This is a living system—it gets better as more people use it.

---

**Start with `START-HERE.md`. You'll be vetting your first job in 10 minutes.**
