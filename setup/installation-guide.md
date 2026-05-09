# Installation Guide

Job Search Machine is designed to work with Claude Code and Cowork. Setup takes 5 minutes.

---

## Requirements

**You need a Claude subscription.** Claude Pro or Max at [claude.ai](https://claude.ai). The Job Search Machine is the system; Claude is the brain behind it and powers the whole thing.

**If you prefer to use the Terminal but haven't used one before,** no worries. See `terminal-basics.md` in this folder — it's a 2-minute read that covers everything you need. No coding required. You'll type plain English and paste job descriptions.

**On Windows?** Install WSL (Windows Subsystem for Linux) first. Open PowerShell as admin and run: `wsl --install`. Restart. Then follow all steps below inside your WSL terminal. Everything else works the same.

**The Job Search Machine zip file** (you have this)

---

## Step 1: Extract the Zip

Download the zip and extract to a folder on your computer:

```
~/Documents/job-search-machine/
```

Folder structure:
```
job-search-machine/
├── CLAUDE.md                # System guide
├── START-HERE.md            # First 30 minutes
├── README.md                # Product overview & FAQ
├── CHANGELOG.md             # Version history
├── .gitignore               # Technical file (ignore)
├── .claude/                 # Skills folder (18 skills — don't edit)
├── sub-agents/              # AI reviewers (ATS, recruiter, hiring manager, interviewer)
├── cowork-tasks/            # Daily morning briefing system
├── briefings/               # Where briefings are saved
├── context-library/         # Your personal data (edit these)
├── templates/               # Resume, work product templates
├── setup/                   # Setup guides (this file here)
└── insider-data/            # Interview frameworks & 250+ company intel profiles
```

---

## Step 2: Open in Claude Code

Choose the option that matches how you use Claude Code:

---

### **Option A: Terminal (Recommended)**

Open your terminal and paste this exactly:

```bash
cd ~/Documents/job-search-machine && claude
```

Press Enter.

**That's it.** Claude Code opens with Job Search Machine active.

---

### **Option B: VS Code or JetBrains IDE**

1. Open your IDE (VS Code, IntelliJ, PyCharm, etc.)
2. Open the `job-search-machine` folder:
   - **VS Code**: File → Open Folder → navigate to `~/Documents/job-search-machine`
   - **JetBrains**: File → Open → navigate to `~/Documents/job-search-machine`
3. Make sure the Claude Code extension is installed:
   - **VS Code**: Install the "Claude Code" extension from the marketplace
   - **JetBrains**: Install the "Claude Code" plugin from Jetbrains Marketplace
4. Open the Claude Code window (VS Code: click the Claude icon in the sidebar; JetBrains: Tools → Claude Code)
5. Type directly into Claude — Job Search Machine system is active

---

### **Option C: Claude Desktop**

1. Download Claude Desktop from [claude.ai](https://claude.ai) if you haven't already
2. Open Claude Desktop
3. Use the **Projects** feature (or drag-and-drop):
   - Drag the `job-search-machine` folder into Claude Desktop, or
   - Click "Add Project" and select `~/Documents/job-search-machine`
4. Claude detects the `.claude/` folder and activates Job Search Machine
5. You can now use `/[skill-name]` commands as normal

---

**Choose one. All three work exactly the same way.** Most users prefer Terminal (Option A) for speed.

---

## Step 3: Read START-HERE.md

Inside Claude, read the onboarding guide:

```
Read START-HERE.md
```

It walks you through the first 30 minutes.

---

## Step 4: Populate Your Context

The system draws from your experience library. First session priorities:

1. **Fill `context-library/experience-library.md`** (15 min)
   - Your work history
   - STAR stories
   - Key accomplishments with metrics

2. **Fill `context-library/career-plan.md`** (10 min)
   - What role are you targeting?
   - Company preferences
   - Salary range

3. **Try your first skill:** Run `/quick-start [JD]` with any job posting

---

## Step 5: Start Using Skills

Each skill is accessed via `/[skill-name]`. Examples:

```
/quick-start [paste a job description]
/resume-tailor [paste a JD]
/job-fit-scorer [paste a JD]
/interview-prep [Anthropic]
/weekly-retro
```

---

## Troubleshooting

**"I don't see the skills available"**
- Make sure you're in the `job-search-machine/` folder when you open Claude Code
- Check that `.claude/skills/` folder exists with skill subfolders

**"How do I know which skill to use?"**
- Read `CLAUDE.md` for the full skill list and when to use each
- Read `START-HERE.md` for the typical workflow

**"Can I modify the skills?"**
- Yes! They're prompts in Markdown. Edit them to make them yours.
- Each skill file is at `.claude/skills/[skill-name]/SKILL.md`

**"What if I don't have experience to fill the templates?"**
- Use the example templates in `setup/example-experience-library.md` as a starting point
- Start with what you have; fill in more as you remember

---

## First Week Checklist

- [ ] Extract zip to `~/Documents/job-search-machine/`
- [ ] Open in Claude Code (`cd` + `claude`)
- [ ] Read `START-HERE.md`
- [ ] Populate `experience-library.md` (15 min)
- [ ] Populate `career-plan.md` (10 min)
- [ ] Build `target-companies.md` with 20 companies (20 min)
- [ ] Run `/quick-start` on a real job
- [ ] Run `/job-fit-scorer` on another job
- [ ] Use `/resume-tailor` to customize a resume

You're ready to go.

---

## Support

This is v1. If you find bugs or have ideas for improvements, you can:
- Check `README.md` for FAQ
- Review the skill files themselves (they're well-documented)
- Iterate on the system (it's yours to adapt)

Happy hunting.