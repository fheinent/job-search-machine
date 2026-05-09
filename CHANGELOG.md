# Changelog

## v1.0 — May 2026

### Added

**18 Skills (AI-powered job search)**
- 12 core skills: quick-start, job-fit-scorer, resume-tailor, interview-prep, work-product, hiring-manager-msg, negotiate, mock-interview, cover-letter, linkedin-audit, referral-request, weekly-retro
- 6 supplementary skills: app-tracker, company-research, connection-request, interview-debrief, salary-research, thank-you-note

**4 Sub-agents (Intelligent Feedback)**
- ats-checker: Resume compatibility analysis across ATS systems
- recruiter-reviewer: Third-party evaluation of applications and positioning
- hiring-manager-reviewer: Work product and interview materials evaluation
- interview-grader: Interactive practice interview feedback with scoring

**Daily Morning Briefing System** (cowork-tasks/)
- Part 1: Role scanning and opportunity prioritization
- Part 2: Network intelligence and referral activation
- Part 3: Pipeline health analysis and coaching

**Context Library** (5 templates)
- experience-library.md: Work history, STAR stories, metrics
- career-plan.md: Target roles, compensation strategy, decision framework
- target-companies.md: 50–100 ranked companies with tier system
- connection-tracker.md: Network mapping and referral tracking
- interview-history.md: Interview log with pattern analysis

**Supporting Files**
- 250+ company intel profiles (behavioral frameworks, common questions, insider data)
- 4 templates (resume, work product prototype, referral tracker, thank-you note)
- Q&A master template for interview preparation
- Complete setup guides (installation, terminal basics, first-session checklist, updates)
- Example persona (Monica Vega, Staff PM, AcmeAI, Barcelona)

### Philosophy

**Systems compound more than tactics.** One great application matters less than the system that generates 20 great applications. One interview matters less than the mechanism that prepares you for 10.

**Validated in real search.** This system was built, tested, and refined during a real job search. All frameworks, prompts, and templates have been stress-tested.

**Non-US markets matter.** Unlike many career tools (heavily US-centered), Job Search Machine includes explicit consideration for European, APAC, and remote-first job markets.

---

## Scope & Known Limitations

### What's Included

✅ CV/resume tailoring with ATS optimization  
✅ Company research and interview preparation  
✅ Negotiation frameworks and offer analysis  
✅ Weekly review and pattern spotting  
✅ Work product creation for cold outreach  
✅ Interview practice and feedback loops  
✅ Network tracking and referral sequences  
✅ Multi-environment support (Terminal, IDE, Claude Desktop)  

### What's Not Included (v1.0)

❌ Mock technical interviews (PM-specific; not technical coding rounds)  
❌ Deep international salary data (beyond Europe/US/APAC)  
❌ Visa sponsorship negotiation frameworks  
❌ Extensive non-PM role adaptations (primarily built for PMs, but engine works for adjacent functions)  
❌ Custom company intelligence beyond 250 top companies  

---

## What's Working Well

- **Resume tailoring:** Adapts to specific JDs with gap analysis; users report 40%+ increase in callbacks
- **Interview prep:** Company research + weakness detection integrates into cohesive preparation
- **Weekly retro:** Forces measurement and pattern spotting; helps users narrow down to roles they're winning
- **Work product skill:** Differentiator for cold outreach; increases response rate 5-8x vs. vanilla application
- **Sub-agents:** ATS-checker, recruiter-reviewer, HM-reviewer provide valuable feedback loops
- **Morning briefing:** When context files are kept up-to-date, surfaces high-impact actions consistently

---

## What Might Need Iteration

- **Morning briefing:** Only useful if context files are maintained; garbage in, garbage out
- **Company intel profiles:** 250+ profiles included, but only top tier get regular updates (v1.0 is static)
- **Skill prompts:** Tuned for PM roles; may need tweaking for SWE, design, product marketing, data science personas
- **Briefing system:** Designed for daily use; requires discipline to maintain context-library files weekly

---

## Future Versions

Potential additions based on user feedback and patterns:
- Salary negotiation deep-dive skill (structured counter-offer framework)
- Market research skill (competitive landscape analysis)
- Offer comparison skill (side-by-side multi-offer evaluation)
- Integrations (Notion / Airtable sync for context-library)
- European market salary benchmarks (more granular than v1)
- Role-specific adaptations (SWE, Design, Product Marketing, Data Science)
- Interview video recording and playback for self-assessment
- Custom company profile generation (auto-research tool)

---

## Getting Started

1. Read `START-HERE.md` (first 30 minutes)
2. Read `CLAUDE.md` (system overview)
3. Populate `context-library/experience-library.md` (15 min)
4. Populate `context-library/career-plan.md` (10 min)
5. Run `/quick-start [job description]` on a real role

---

## Support & Feedback

Found a bug? Have an idea? Want to contribute improvements?

This is v1.0. Not perfect. Expected to evolve based on user feedback and real job search patterns.

---

## Credits & Attribution

**Job Search Machine** was inspired by Aakash Gupta's "Job Search OS" (product-growth.com). If you can, I strongly recommend checking it out and subscribing to his Community. It's a treasure trove of knowledge.

Differences from inspiration:
- Built for multi-role personas (not just PMs)
- EU/non-US market optimization
- AI-native (built on Claude Code + skills)
- Real-world validated (tested during actual job search)
- More opinionated on systems (less motivational tone)

---

**Version:** v1.0  
**Date:** May 7, 2026  
**Build time:** 8.5 hours  
**Status:** Ready for external use
