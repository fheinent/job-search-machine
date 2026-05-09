# Terminal Basics for Non-Technical Users

You don't need to be technical to use Job Search Machine. This file explains the basics so you can get up and running.

---

## What Is a Terminal?

A **terminal** is a text-based window where you type commands to your computer.

Think of it like texting your computer:
- You type a command (what you want to do)
- You press Enter
- Your computer does it

Instead of clicking icons, you use words.

---

## How to Open a Terminal

### On Mac

**Option 1: Spotlight (easiest)**
1. Press `Cmd + Space`
2. Type `terminal`
3. Press Enter
4. A window opens

**Option 2: Finder**
1. Open Finder
2. Go to Applications → Utilities
3. Double-click "Terminal"

### On Windows

**Option 1: Start Menu (easiest)**
1. Click the Windows start icon (bottom left)
2. Type `cmd`
3. Click "Command Prompt"

**Option 2: Keyboard shortcut**
1. Press `Windows Key + R`
2. Type `cmd`
3. Press Enter

### On Linux

Open your application menu and search for "Terminal" or press `Ctrl + Alt + T`

---

## What You'll See

When you open the terminal, you'll see something like:

```
user@computer ~ %
```

or 

```
C:\Users\username>
```

This is the **prompt**. It's waiting for you to type a command.

---

## Basic Commands You'll Use

### Navigate to a Folder

**Command:** `cd` (stands for "change directory")

**Example:**
```
cd Documents/job-search-machine
```

This moves you into the `job-search-machine` folder inside your `Documents` folder.

**If the path has spaces**, wrap it in quotes:
```
cd "Documents/My Work/job-search-machine"
```

### Starting Claude Code

**Command:** `claude`

**What it does:** Opens Job Search Machine in Claude Code

**Full example:**
```
cd Documents/job-search-machine
claude
```

This navigates to the folder, then opens Claude.

### List Files in a Folder

**Command:** `ls` (on Mac/Linux) or `dir` (on Windows)

**Example:**
```
ls
```

Shows you all files in your current folder.

---

## Step-by-Step: Getting Started

### Step 1: Open Terminal
- Mac: Press `Cmd + Space`, type `terminal`, press Enter
- Windows: Press `Windows + R`, type `cmd`, press Enter

### Step 2: Navigate to Job Search Machine

Type this exactly:

**Mac/Linux:**
```
cd ~/Documents/job-search-machine
```

**Windows:**
```
cd Documents\job-search-machine
```

Then press Enter.

### Step 3: Open Claude Code

Type:
```
claude
```

Press Enter.

**Claude Code will open in your browser or app.**

---

## Troubleshooting

### "Command not found: claude"

This means Claude Code isn't installed yet.

**Fix:**
1. Go to claude.com
2. Download Claude Code (or the VSCode extension)
3. Follow installation instructions
4. Close your terminal and open a new one
5. Try `claude` again

### "No such file or directory"

This means the folder path is wrong. 

**Fix:**
1. Make sure you extracted the job-search-machine zip correctly
2. Make sure the path is correct (double-check spelling)
3. Try typing just `ls` to see what folders are in your current location

### "cd doesn't work / It says 'cd' is not recognized"

You might be using PowerShell instead of Command Prompt on Windows.

**Fix:**
1. Close this terminal
2. Open Command Prompt (not PowerShell)
3. Try again

### "Claude is loading forever"

This is normal the first time. It's downloading and setting up. Give it 30 seconds.

If it's taking >2 minutes:
1. Check your internet connection
2. Try closing and re-opening the terminal

---

## Files You'll See

When you navigate to `job-search-machine`, you'll see:

```
CLAUDE.md                 ← Main system guide (how to use the OS)
START-HERE.md            ← Your first 30 minutes
README.md                ← Product description and FAQ
CHANGELOG.md             ← What changed in each version
.gitignore               ← Technical file (ignore it)
.claude/                 ← Skills folder (18 skills — don't edit manually)
sub-agents/              ← AI reviewers for resumes and interviews
cowork-tasks/            ← Daily morning briefing system
context-library/         ← Your personal data (edit these)
templates/               ← Templates for resumes, work products
setup/                   ← Setup guides and examples (this file is here)
briefings/               ← Where daily briefings are saved
insider-data/            ← Company interview intel (250+ companies)
```

**You only edit files in `context-library/`** (your experience library, career plan, target companies, etc.)

The rest of the system does the work.

---

## That's It

You now know enough terminal to use Job Search Machine. You don't need to memorize anything else.

**Remember:**
- `cd [folder]` = navigate to a folder
- `claude` = open Claude Code
- `ls` = see what's in your current folder

Now go back to START-HERE.md and start your first session.
