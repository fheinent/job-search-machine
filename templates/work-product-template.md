# Work Product Template

A **work product** is a 1-2 page document that showcases your thinking on a company's product. It's a way to stand out and get meetings or referrals.

This template gives you **3 approaches** — pick the one that fits your situation.

---

## How to Choose Your Type

| Situation | Type | Goal |
|---|---|---|
| You found a role and want to stand out before applying | **get-interview** | Earn the interview by showing unique insight |
| You're already in the process and want to impress | **in-process** | Prove you can do the job by doing a piece of it |
| You fumbled a specific interview question | **specific-interview** | Recover by showing your real process |

---

## Template 1: Get-Interview (Pre-Application / Cold Outreach)

**Purpose:** Attached to your application or sent directly to the hiring manager. Earns you an interview by proving you understand their product and have a differentiated perspective.

**Length:** 1 page. Max 2.

**Research required before writing (the hooks):**
- [ ] Most recent earnings call or funding announcement (CEO priorities)
- [ ] Product reviews: App Store, Play Store, G2, TrustRadius (real user complaints), Trustpilot
- [ ] Recent product/engineering blog posts (what they're publicly building)
- [ ] Public user complaints: Twitter/X, Reddit, Hacker News (known pain points)
- [ ] Recent feature launches or changes (product direction signals)

Pull 3-5 specific hooks from this research. Better to choose those with the highest relevance to the role you're applying to. These make the document impossible to dismiss as generic.

### Structure

```markdown
# [Specific Title, e.g., "Reducing Checkout Abandonment in Stripe's New Billing Flow"]
[Your Name] | [Date] | For: [Role Title] at [Company]

## Why Listen to Me
[2-3 sentences connecting YOUR specific experience to THEIR specific problem.
Draw directly from experience-library.md. Not "I'm a PM with 8 years of experience"
but "At [Company], I reduced checkout abandonment by 34% across a payment flow
handling $2B annually -- a problem structurally similar to what I see in
[Target Company]'s billing experience."]

## The Observation
[1-2 paragraphs. Start with a specific, data-backed observation about their product.
Reference a real user complaint, a public metric, or something you noticed using
the product yourself. This proves you did the work.]

[Example hook: "In Q3 earnings, [CEO] mentioned checkout conversion as a key
initiative. Looking at 127 recent App Store reviews mentioning 'checkout,'
three patterns emerge..."]

## Analysis
[Break down the problem. 3-5 specific points. Each grounded in data or
observation, not theory. Show your product thinking, not a framework.]

1. **[Specific point]:** [Evidence from research hooks + your interpretation]
2. **[Specific point]:** [Evidence + interpretation]
3. **[Specific point]:** [Evidence + interpretation]

## Recommendations
[2-3 specific, actionable recommendations. Each should be:]
- Non-obvious (not "improve onboarding")
- Grounded in your research hooks
- Connected to your unique experience
- Acknowledging tradeoffs (every recommendation has a cost)

### 1. [Recommendation Title]
[What to do, why it works, what tradeoff to accept, what metric to watch]

### 2. [Recommendation Title]
[Same structure]

### 3. [Recommendation Title]
[Same structure]

## What I'd Want to Explore Together
[1-2 sentences framing the next conversation. Signal that you know you're
missing internal context and want to learn, not just pitch.]
```

---

## Template 2: In-Process (During Interview Loops)

**Purpose:** Sent between rounds or as a take-home. Proves you can do the actual work of the role. This is a mini-PRD or product proposal scoped to the hiring manager's charter.

**Length:** 1-2 pages. Dense. No filler.

**Research required before writing:**
- [ ] Everything from get-interview research, PLUS:
- [ ] The HM's LinkedIn (what are they responsible for?)
- [ ] Recent product changes in the HM's area specifically
- [ ] Competitive landscape for this specific product area
- [ ] Any internal signals from your interviews (what problems did interviewers mention?)

### Structure

```markdown
# [Proposal Title, e.g., "Feature Proposal: Smart Invoice Reminders for Stripe Billing"]
[Your Name] | [Date] | For: [Role Title] at [Company]

## Why Listen to Me
[Same format as get-interview. 2-3 sentences connecting your experience
to this specific proposal. Be precise about the parallel.]

## Problem Statement
[Define the problem from the USER's perspective, not the company's. Include:]
- Who has this problem (specific user segment)
- How painful it is (data: support tickets, reviews, churn correlation)
- Why it matters now (market pressure, competitive threat, CEO priority)

## Current State
[What the product does today. Be specific enough that the HM knows you've
actually used the product. Screenshot descriptions or flow descriptions welcome.]

## Proposed Solution

### User Stories
- As a [user type], I want to [action] so that [outcome]
- As a [user type], I want to [action] so that [outcome]
- As a [user type], I want to [action] so that [outcome]

### Key Flows
[Describe the 2-3 most important user flows. If you built a prototype
using the prototype-prompt-template, reference or link it here.]

1. **[Flow name]:** [Step-by-step description]
2. **[Flow name]:** [Step-by-step description]

### What I'm NOT Proposing (Scope Boundaries)
[Explicitly state what's out of scope and why. This demonstrates prioritization
and prevents the HM from thinking you're naive about complexity.]

## Competitive Context
[What competitors do here. Not a feature matrix -- an insight about
different strategic choices and their tradeoffs.]

## Success Metrics
- **Primary:** [metric + target, e.g., "Reduce late payments by 20% within 6 months"]
- **Secondary:** [metric + target]
- **Guardrail:** [metric that must NOT degrade, e.g., "Support ticket volume stays flat"]

## Phased Approach
| Phase | Scope | Timeline Estimate | Key Risk |
|---|---|---|---|
| 1 (MVP) | [minimum viable version] | [weeks] | [biggest risk] |
| 2 | [iteration based on Phase 1 data] | [weeks] | [risk] |
| 3 | [full vision] | [weeks] | [risk] |

## Open Questions
[3-5 questions you'd need internal data to answer. Shows intellectual
honesty and sets up the next conversation.]
```

---

## Template 3: Specific-Interview (Post-Interview Recovery)

**Purpose:** Sent as a follow-up attachment when you fumbled a specific question in an interview. Proves that your real process is stronger than your improvised answer.

**Length:** 1 page.

**When to use:**
- You jumped to a solution without exploring the problem
- You blanked on metrics or structure
- You gave a surface-level answer to a deep question
- The interviewer probed an area where your answer was weak

### Structure

```markdown
# [Title, e.g., "How I'd Actually Approach: Prioritizing Stripe's SMB Feature Roadmap"]
[Your Name] | [Date] | Follow-up to [Round/Interviewer Name] Interview

## Context
[1-2 sentences. Name the question. Own that your live answer was incomplete.]

[Example: "In our conversation, you asked how I'd prioritize the SMB feature
roadmap. I jumped to a framework answer. Here's what my actual process looks
like when I have time to do it right."]

## My Process

### Step 1: Define the Decision
[What exactly are we deciding? Frame the prioritization question precisely.
Show that you start by clarifying scope, not jumping to solutions.]

### Step 2: Gather Signal
[Where would I look for data? Be specific to this company:]
- **Usage data:** [what I'd query and why]
- **User research:** [what questions I'd ask which segments]
- **Competitive analysis:** [what I'd look at and what I'd learn]
- **Stakeholder input:** [who I'd talk to and what I'd ask]
- **Business constraints:** [what I'd need to understand about the business model]

### Step 3: Synthesize
[How I'd combine these inputs into a decision framework. Not a generic
RICE score -- a framework specific to this problem that weighs the
dimensions that actually matter here.]

### Step 4: The Recommendation
[Given what I know publicly, here's my best hypothesis for how I'd
prioritize. Include specific features/initiatives with reasoning.
Acknowledge what would change with internal data.]

## Why Listen to Me
[Connect to a parallel experience where you ran exactly this process.
Draw from experience-library. Include the specific outcome.]

## What I'd Explore Next
[Frame the conversation you'd want to have with the HM.
2-3 specific questions that demonstrate your depth.]
```

---

## Quality Checklist (All Types)

Before submitting any work product, verify:

- [ ] **Company-specific hooks:** At least 3 references to specific, recent company data (earnings, reviews, launches)
- [ ] **"Why Listen to Me" is grounded:** Every claim traces back to experience-library.md
- [ ] **No generic sentences:** Read each sentence and ask "could this apply to any company?" If yes, rewrite.
- [ ] **No AI-sounding language:** No "delve," "landscape," "leverage," "robust," "synergy," "streamline," "cutting-edge"
- [ ] **Tradeoffs acknowledged:** Every recommendation has a cost or risk mentioned
- [ ] **Under 2 pages:** Shorter is always better. If you can cut a paragraph without losing the argument, cut it.
- [ ] **Real metrics:** At least 2-3 data points from public sources
- [ ] **Actionable:** A PM on their team could take this into a planning meeting
- [ ] **Prototype included (optional):** If you used prototype-prompt-template.md, link it

## After Writing

1. Run `/review-as-hiring-manager` to get the HM perspective score
2. Address all "generic content" and "AI-sounding content" flags
3. Score target: Specificity 8+, Product Sense 7+, Unique Insight 7+, Actionability 7+
4. If the meeting test answer is "No" or "Maybe," revise before sending


## How to Send

**Email template:**

```
Subject: [Quick thought on X at Company]

Hi [Hiring Manager],

I've been thinking about [specific problem at company] since our interview. 
Wanted to share a structured analysis.

[Paste your 1-pager here, or attach as PDF]

Curious what your team's seen on this. Happy to discuss.

—[Your name]
```

---

## After You Send

Wait 5-7 days. If no response, don't follow up on the work product itself. Follow up with something else (use `/hiring-manager-msg` skill for general follow-up).
