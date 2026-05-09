# Updates & Changelog

---

## v1.0 (May 2026)

### Initial Release

**New:**
- 12 core skills for PM job search (quick-start, job-fit-scorer, resume-tailor, interview-prep, work-product, hiring-manager-msg, negotiate, mock-interview, cover-letter, linkedin-audit, referral-request, weekly-retro)
- 6 supplementary skills (app-tracker, company-research, connection-request, interview-debrief, salary-research, thank-you-note)
- 4 sub-agents for intelligent feedback (ats-checker, recruiter-reviewer, hiring-manager-reviewer, interview-grader)
- 5 context templates to populate once, use everywhere (experience-library, career-plan, target-companies, connection-tracker, interview-history)
- Q&A master template for interview prep
- 3-part morning briefing system (cowork-tasks) for daily job search accountability
- 251+ company interview profiles (behavioral frameworks, common questions, insider data)
- Complete setup guides (installation, first-session checklist, terminal basics)
- Example experience library and career plan (Alex Chen profile)
- Resume, work product, and referral templates

**For:**
- Product Managers, Software Engineers, Data Scientists, Product Designers, Product Marketing Managers (IC through Director)
- Job searchers with 20–30 min/day available for 8–12 weeks
- Users in US, Europe, APAC, or remote-first markets (with emphasis on non-US job markets)
- Knowledge workers who value systems over tactics and precision over volume

**Scope:** v1.0 is a complete, functional system. Not perfect. Expected to evolve based on user feedback.

---

## Known Limitations

**v1.0 doesn't include:**
- Mock technical interviews (PM-specific, not technical coding rounds)
- International market salary data beyond Europe
- Visa sponsorship negotiation frameworks (country-specific complexity)
- Non-PM role adaptations (primarily built for PMs)
- Custom company intelligence beyond top 250 companies

---

## What's Working Well in v1.0

- Resume tailoring (adapts to specific JDs with gap analysis)
- Interview prep (company research + weakness detection)
- Weekly retro (forces measurement and pattern spotting)
- Work product skill (differentiator for cold outreach)
- Subagents (ats-checker, recruiter-reviewer, HM-reviewer are strong feedback loops)

---

## What Might Need Iteration

- Morning briefing (only useful if context files are kept up-to-date; garbage in, garbage out)
- Company intel profiles (251+ profiles, but only top tier get regular updates)
- Skill prompts (tuned for PM roles; may need tweaking for adjacent functions)

---

## How to Get the Most Out of v1.0

1. **Populate once, use everywhere:** Spend 30 minutes filling experience-library and career-plan. Everything else feeds off these.
2. **Use weekly retro religiously:** Friday EOD, run `/weekly-retro`. Measure conversion rates. You'll spot patterns.
3. **Log interviews:** After every interview, update interview-history.md with feedback. This feeds interview-prep and weekly-retro.
4. **Keep target-companies updated:** As you learn about companies, add notes. This powers the morning briefing and research suggestions.
5. **Iterate on skills:** The prompts are yours. Edit them. Make them sound like you.

---

## Reporting Feedback

Have feedback? Found a bug? Missing something? Find me on linkedin @federicoheinen and send me a message!

---

## Future Versions (Post-v1)

Potential additions based on user patterns:
- `salary-negotiation-deep-dive` skill (more structured counter-offer framework)
- `market-research` skill (competitive landscape for roles)
- `offer-comparison` skill (compare multiple offers side-by-side)
- Integrations with Notion / Airtable (sync your data)
- European market salary benchmarks (more granular than v1)
- Non-PM role adaptations (SWE, Design, Operations)

---

## Release Notes

**v1.0 (May 7, 2026)**
- System designed, built, tested, and packaged
- Tested on 1 user (Fede) in real job search scenario
- Ready for external use
- Scope: 8.5 hours of initial build
- Philosophy: systems compound more than tactics

---

## Version History

This section shows system updates over time:

| Version | Date | What Changed | Why |
|---------|------|--------------|-----|
| v1.0 | May 2026 | Initial release | First product launch |
| | | | |

---

## Updating the Job Search Machine

When a new version is released, follow these steps to update without losing your personal data.

### Update Process

1. **Download the new version** from the distribution source.
2. **Copy these folders and files** from the new version into your existing job-search-machine folder, replacing the old versions:
   - `.claude/skills/` (all skill files)
   - `sub-agents/` (all sub-agent files)
   - `insider-data/` (company intel profiles and frameworks)
   - `cowork-tasks/` (scheduled task prompts)
   - `templates/` (template files)
   - `CLAUDE.md` (root config file)
3. **Do NOT overwrite `context-library/`.** This folder contains your personal data (experience library, career plan, target companies, connection tracker, interview history, etc.). It stays untouched during updates.
4. **Check `CLAUDE.md` for the version number** after copying to confirm the update applied correctly.

### What Gets Updated vs. What Stays

| Updated (replace with new version) | Preserved (never overwrite) |
|-------------------------------------|-----------------------------|
| `.claude/skills/` | `context-library/` |
| `sub-agents/` | `briefings/` |
| `insider-data/` | Any personal notes or files you added |
| `cowork-tasks/` | |
| `templates/` | |
| `CLAUDE.md` | |

### If Something Breaks

If an update causes issues, check the `CHANGELOG.md` at the project root for what changed in each version. If a skill behaves differently, the changelog will note breaking changes.