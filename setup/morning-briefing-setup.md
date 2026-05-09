# Setting Up Your Daily Morning Briefing

The **morning briefing** is an optional automation that gives you a daily 5-minute intelligence report on new roles, networking opportunities, and pipeline coaching.

---

## What the Morning Briefing Does

Every weekday at 7:00 AM, Claude analyzes:
- **Part 1 (7:00 AM):** New roles that match your target companies + initial scoring
- **Part 2 (7:15 AM):** New LinkedIn connection requests you should make + referral nudges
- **Part 3 (7:30 AM):** Pipeline summary + coaching on your biggest bottleneck

**Time commitment:** 5-10 minutes to review + act on (optional; you control the pace)

---

## How to Set It Up

### Option 1: Claude Desktop Cowork (Easiest)

**Requirements:** Claude Desktop app + Claude Pro or Claude Max subscription

**Steps:**

1. Open Claude Desktop app (or go to claude.ai)
2. Look for **"Cowork"** tab in the upper part of the left sidebar (it's the second tab from the top)
3. Click **"Schedule"** and then **New task**
4. Set up a new schedule:
   - **Name:** "Daily Job Search Briefing"
   - **Description:** "Daily job search briefing"
   - **Prompt:** [Copy the full text from `cowork-tasks/daily-morning-briefing.md`]
   - **Permissions:** "Ask before acting" or "Act without asking" (Optional - it is set to Ask by default)
   - **Model:** Claude Haiku 4.5 (Optional - it is set to Default model)
   - **Frequency:** Weekdays (Mon–Fri)
   - **Time:** 7:00 AM (your timezone - available for daily or weekly scheduling)
   
5. Click **"Create"** and confirm

**It will run automatically every weekday at 7:00 AM.**

---

### Option 2: Manual Run (No Automation)

If you don't have Claude Pro/Max or don't want automation:

1. Every morning, open Claude Code in your `job-search-machine/` folder
2. Read the prompt: `cowork-tasks/daily-morning-briefing.md`
3. Copy the full prompt
4. Paste it into a new Claude conversation
5. Claude will generate your 3-part briefing
6. Takes ~3 minutes

---

## What to Do With the Output

The briefing generates **3 sections** across ~2,000 words total:

### Part 1: New Roles Found (7:00 AM)

**What you get:**
- Top 3 roles ranked by fit (0-100 score)
- Job title, company, fit reasoning
- Resume readiness check (do you have tailored resume ready?)
- Recruiter feedback score (would a recruiter advance this?)
- ATS score (will ATS parse your resume correctly?)

**Action:** 
- ✅ Score >75? Run `/resume-tailor` and apply today
- ⏳ Score 60-74? Add to your list; prepare resume for later
- ❌ Score <60? Likely skip (or investigate why fit is weak)

---

### Part 2: Networking Requests (7:15 AM)

**What you get:**
- 5-10 people you should reach out to (based on target-companies.md)
- Personalized LinkedIn message (~300 chars)
- Connection strength indicator (first-degree, mutual connection, cold)
- Referral nudge if someone accepted your request in last 48h

**Action:**
- Copy the drafted message
- Paste into LinkedIn message / cold email
- Follow up 5-7 days later if no response

---

### Part 3: Pipeline Coaching (7:30 AM)

**What you get:**
- Pipeline summary table (# apps sent, # interviews, # rejections, etc.)
- Bottleneck analysis: where your funnel is broken
- Coaching message specific to your situation
- Today's 3-4 action items (with time estimates)

**Action:**
- Read the coaching message (honest, real feedback)
- Pick 1-2 actions from the priority stack
- Do them today (you have time)

---

## Keeping the Briefing Updated

For the briefing to stay relevant, update these files **weekly:**

1. **`connection-tracker.md`** — When you reach out to someone new, add them
2. **`target-companies.md`** — Add new companies you discover, remove ones no longer relevant
3. **`interview-history.md`** — Log every interview immediately after it happens
4. **`app-tracker.md`** (if using `/app-tracker` skill) — Log every application

**How often:** Spend 10 min on Friday to update context files. Briefing gets better with better data.

---

## Troubleshooting

### "The briefing isn't running"

Check:
- Is Cowork actually enabled? (Look for toggle in Claude settings)
- Is your schedule set for weekdays + correct timezone?
- Try running manually first: does it work when you paste the prompt?

### "The briefing is recommending bad roles"

This means your `target-companies.md` or `career-plan.md` isn't clear enough. Rebuild it:
1. Read the instructions in `career-plan.md`
2. Be more specific about what you want (not just "PM roles")
3. Run briefing again

### "The connection requests aren't personalized"

The briefing needs info to personalize. Make sure:
1. `target-companies.md` has company details (not just names)
2. `connection-tracker.md` is kept up-to-date
3. You've run `/company-research` on at least 5 of your top companies

### "Networking recommendations feel generic"

Cowork briefing uses what you give it. To get better recommendations:
1. Add more detail to your target-companies notes
2. Log past interviews and outcomes in `interview-history.md`
3. Update `career-plan.md` with weaknesses you're addressing

---

## When to Turn It Off

The briefing is optional. **Turn it off if:**
- You're only passively job searching (not actively applying)
- You prefer to control your own pace
- You don't check messages regularly enough to act on it

**Keep it on if:**
- You want daily accountability
- You like having a "briefing" framing (structure, not endless todo)
- You're actively job searching (applying 2+ roles/week)

---

## Advanced: Customizing the Briefing

**Don't like the current approach?** You can customize the prompts. Each part lives here:

- `cowork-tasks/briefing-part1-roles.md` — Role discovery and scoring
- `cowork-tasks/briefing-part2-networking.md` — Connection requests and follow-ups
- `cowork-tasks/briefing-part3-coaching.md` — Pipeline analysis and coaching

Edit them to match your style. The briefing will adapt.

**Examples of customizations:**
- "Only show roles at companies I've explicitly starred in target-companies.md"
- "Don't recommend connection requests to companies I already have contacts at"
- "Focus coaching on my specific bottleneck (e.g., I'm getting interviews but not advancing)"

---

## Connect Google Calendar

1. Open Claude Desktop app
2. Go to Settings > Connectors
3. Click 'Google Calendar'
4. A Google sign-in window will appear. Sign in with the Google account that has your interview calendar.
5. Click 'Allow' to grant access
6. You should see a green checkmark confirming the connection

**This lets the briefing check for scheduled interviews and include prep reminders in your daily output.**

---

## What's Next?

Once your briefing is running:

1. **Week 1:** Let it run, see what it recommends
2. **Week 2:** Start acting on recommendations (apply to top roles, reach out to suggested contacts)
3. **Week 3+:** Update context files weekly, adjust briefing prompts if needed
4. **Weekly:** Sunday night, spend 10 min reviewing the briefing and planning your week


You now have a job search operating system. Use it well.