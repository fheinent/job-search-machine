---
name: interview-prep
description: Generate comprehensive interview prep combining web research, insider company data, and your past patterns. Includes likely questions, weakness heatmap, and practice talking points.
---

# /interview-prep — Complete Interview Preparation

## When to Use

An interview is scheduled at a specific company for a specific role. You need complete preparation covering: what they ask, what they care about, and where your weaknesses show up.

Input: Company name + role title (and round number if you know it: screening, technical, design, culture fit, etc.)

Output: Web research intel + company-specific question bank + your weakness heatmap + practice talking points

---

## Role

You are an interview coach who combines:
1. Public research on the company (web, LinkedIn, Glassdoor, blind, product)
2. Insider data on their interview patterns (from `insider-data/`)
3. Your past interview history (from `interview-history.md`) to surface patterns
4. Your experience library to craft specific examples

Goal: Walk into the interview feeling prepared, not surprised.

---

## Process

### Step 1: Research the Company (5 min)

**Load:** `insider-data/company-intel/[company].md` (if it exists)

**Also research:**
- **Company stage & financials:** Funded how much? What's the burn rate? Public or private?
- **Product focus:** What's their flagship product? What are they launching?
- **Recent news:** Funding rounds, leadership changes, layoffs, partnerships?
- **Culture signals:** What do employees on Blind/Glassdoor say? What's the vibe?
- **Market position:** Are they winning or struggling relative to competitors?
- **Your take:** Why did you apply to THIS company, THIS role?

**Red flags to note:**
- Recent layoffs (company might be contracting)
- Rapid executive turnover (unstable leadership)
- Negative Blind/Glassdoor patterns (burnout, politics, poor product direction)
- Missing leadership in your function (e.g., no CPO for a PM role — concerning)

---

### Step 2: Load Interview Patterns (3 min)

**Load:** `insider-data/behavioral-interview-frameworks.md` or company-specific interview docs

Extract:
- **Interview structure:** Phone screen → take-home → technical → culture fit → final
- **Round breakdown:** What's assessed in each round?
- **Question types:** Behavioral, technical, product case, design, architecture?
- **What they emphasize:** Culture fit, technical depth, speed to impact?
- **Red flags during interviews:** What kills candidates (arrogance, vagueness, lack of curiosity)?
- **Time limits per round:** 30 min screening, 60 min technical, etc.?

---

### Step 3: Surface Your Weakness Heatmap (5 min)

**Load:** `context-library/interview-history.md` + `context-library/career-plan.md`

**Questions to surface patterns:**

From interview history:
- Which question types do you struggle with? (e.g., "behavioral questions about conflict resolution")
- Which company types ask you the hardest questions? (e.g., "FAANG always emphasizes scale")
- Which of your stories resonate? (e.g., "People love my founder story but glaze over my analytics background")
- Which domains do you need to study more for? (e.g., "Always asked about mobile strategy, don't have good answer")

From career plan:
- What weaknesses are you addressing? (e.g., "Limited AI experience but targeting AI PM roles")
- What deal-breakers do you care about? (e.g., "Won't work in fast-moving startup without good process")

**Create a heatmap:**

| Question Type | Your Strength | Your Weakness | How to Prepare |
|---|---|---|---|
| Behavioral (leadership, teamwork, conflict) | ✅ Strong storyteller | ⚠️ Weak on conflict resolution examples | Prepare 2 conflict stories with outcomes |
| Product case study (design a feature) | ✅ Strong at spec and tradeoffs | ❌ Tend to over-design without constraints | Practice saying "I'd ask X questions first before designing" |
| Technical depth (APIs, data, architecture) | ⚠️ Adequate but not expert | ❌ Can't code or build | Be honest about depth; ask great questions instead |
| Scale & metrics (billion-user problems) | ⚠️ Have scale experience but at smaller companies | ⚠️ Haven't experienced billion-user growth | Frame: "Scaled to X million; would love to see how Y billion is different" |
| Startup speed vs. process | ✅ Shipped fast | ⚠️ Sometimes miss process consequences | Ask about their process trade-offs explicitly in interviews |

---

### Step 4: Build Your Question Bank (5 min)

Compile likely questions for THIS company + THIS role:

**Standard Behavioral Questions (Asked everywhere):**
- Tell me about a product you shipped that failed. What did you learn?
- Tell me about a time you disagreed with your manager/team.
- Tell me about a time you had to work with a difficult engineer/designer.
- Tell me about your biggest product impact and how you measured it.
- Why are you interested in this company/role?

**Role-Specific Questions:**

*For Product Manager roles:*
- Design a feature for [Company's product].
- How would you measure success for [specific feature]?
- How would you prioritize between three conflicting stakeholder asks?
- Walk me through your approach to competitive analysis.

*For Growth/Analytics PMs:*
- Design a growth experiment for [Company's product].
- You have a 20% drop in [key metric]. Walk me through diagnosis.
- How would you build a growth roadmap?

*For PM roles at AI companies:*
- How do you think about capability vs. safety trade-offs?
- Tell me about your approach to building products with LLMs.
- Design a feature using AI. What are the failure modes?

**Company-Specific Curveballs (from insider data):**
- [What did their last round of interviews emphasize?]
- [Have they asked about domains you're weak in?]
- [Do they ask process questions? Vision questions? Tactical questions?]

---

### Step 5: Craft Your Stories (8 min)

For each weakness, prepare a STAR story that addresses it.

**STAR = Situation → Task → Action → Result**

Keep each to 3-4 sentences. Be specific. Use numbers.

**Example:**
- **Weakness:** "I don't have leadership experience"
- **Story to prepare:** "I led cross-functional roadmap planning with 20+ engineers, no direct authority. Situation: Product was fragmented across 3 teams. Task: Align on shared roadmap. Action: I ran weekly sync where each team presented their priorities, we scored them together on impact/effort, and decided jointly. Result: All three teams shipped coordinated features for the first time; velocity improved 15%."

---

### Step 6: Prepare Your Questions Back (3 min)

At the end of every interview, you ask questions. This signals:
- You're genuinely interested (not desperate)
- You're thinking strategically (not just taking any job)
- You care about culture/process fit (not just paycheck)

**Prep 5-7 questions to ask:**

| Category | Example Question |
|---|---|
| **On the role** | "What does success look like for this role in year 1? What does year 2 look like?" |
| **On the team** | "Walk me through the team structure. Who do I report to? Who are my key collaborators?" |
| **On the product** | "What's the biggest product challenge the team faces right now?" |
| **On the company** | "How does the company approach [process you care about]? e.g., how do you think about tech debt, process vs. speed, etc.?" |
| **On career** | "What's the career progression path for PMs at this level? What skills are valued most?" |
| **On decision-making** | "Tell me about a time the company pivoted strategy. How was that decision made?" |

**Never ask:**
- Anything Googleable ("What does your company do?")
- Anything about salary (wait for them to bring it up, or HR in later rounds)
- Anything negative ("Why is your retention so low?")

---

### Step 7: Assemble Your Prep Document (Output)

---

## Output Format

```markdown
## Interview Prep: [Company Name] — [Role Title]

**Round:** [Screening / Technical / Design / Culture Fit / Final — if known]
**Interview Date:** [Date & Time]
**Interviewer:** [Name & Title — if known]

---

## Company Intel

### Business Context
- **Stage:** [Series X / Public / etc.]
- **Funding:** [Raised $YM to date]
- **Burn rate:** [If available — is the company stable?]
- **Recent news:** [Major announcements, hires, layoffs?]

### Product & Market
- **Core product:** [What do they sell/do?]
- **Main competitor:** [Who are they competing against?]
- **Market position:** [Winning? Struggling? Growing?]
- **Your assessment:** [Why is this an interesting role?]

### Culture Signals
- **From insider data:** [What do employees on Blind say?]
- **From your network:** [What have people told you about working there?]
- **Red flags:** [Any concerns? Or: No red flags detected]

---

## Interview Structure for [Company]

**Typical process for [role title]:**
1. [Round 1: Phone screen — 30 min, recruiter, culture fit questions]
2. [Round 2: Product case study — 60 min, hiring manager, real-world problem]
3. [Round 3: Technical depth — 60 min, senior PM, architecture & trade-offs]
4. [Final round: Team lunch — 90 min, culture fit & executive alignment]

**Emphasis:** [What do they care most about? Speed, technical depth, culture fit, scale experience?]

---

## Your Weakness Heatmap

| Question Type | Strength ✅ | Weakness ⚠️ | Prep Strategy |
|---|---|---|---|
| Behavioral (teamwork, conflict) | Strong storyteller | Struggle with conflict resolution | Prepare: "Time I disagreed with manager and how we resolved it" |
| Product case study | Fast ideation, good specs | Over-design without constraints | Prepare: "I'd ask about [constraints/users/metrics] first" |
| Technical depth | Understand architecture | Can't code from scratch | Prepare: Be honest; ask great clarifying questions instead |
| Scale & metrics | Shipped at scale | Haven't done billion-user problems | Prepare: "Scaled to X; love to learn from billion-user context" |

**Plan:** Focus prep on weaknesses. This company will ask about X, Y, Z. Have stories ready.

---

## Question Bank for This Interview

### Behavioral (Asked everywhere)
1. Tell me about a product you shipped that failed. What did you learn?
2. Tell me about a time you disagreed with your manager.
3. Tell me about your biggest product impact. How did you measure it?
4. Why are you interested in [Company] specifically?

### Role-Specific for [PM / Growth / AI Product]
1. [Design a product problem specific to their company]
2. [Walk through how you'd prioritize something relevant to them]
3. [How would you measure success for X?]

### Company-Specific (from insider data)
1. [Curveball they've asked others]
2. [Domain they emphasize — be ready]

---

## Your Stories (STAR Format)

### Story 1: [Challenge/Achievement title]
*Situation:* [Context — what was the problem?]
*Task:* [What were you asked to do?]
*Action:* [What did you specifically do? Numbers, decisions, approach]
*Result:* [What happened? Metrics, outcomes, learning]

**Use when asked about:** [Behavioral type that this addresses]

**Key phrases to remember:** [Specific language you want to land]

---

### Story 2: [Impact/Scale story]
...

### Story 3: [Failure/Learning story]
...

---

## Your Questions to Ask Them

1. **On the role:** "What does success look like in year 1 for this role?"
2. **On the team:** "Walk me through who I'd be working most closely with."
3. **On the company:** "Tell me about a time the company changed strategy. How was that decided?"
4. **On product:** "What's the biggest product challenge you're facing right now?"
5. **On career:** "What's the growth path for PMs at this level?"

**Remember:** Ask from genuine curiosity, not to impress. They should feel you're evaluating them too.

---

## Pre-Interview Checklist

- [ ] You've read all company intel
- [ ] You've prepped 3 STAR stories specific to this company/role
- [ ] You know 5-7 questions to ask them
- [ ] You've reviewed your weakness heatmap and prepped for hard topics
- [ ] You know the interviewer's name and title
- [ ] You know what round this is
- [ ] You've researched the interviewer (LinkedIn, Blind, their product work)
- [ ] You know your talking points (don't ramble; be concise)

---

## During the Interview

**Mindset:**
- You're interviewing THEM as much as they're interviewing you
- Confidence > perfection (a good question is better than a perfect answer)
- Honesty > BS (if you don't know something, say so and ask about it)

**Communication:**
- Listen fully before answering (don't interrupt)
- Be specific (numbers, concrete examples, not vague philosophy)
- Ask clarifying questions (shows intellectual curiosity)
- Keep answers to 2-3 minutes max (don't ramble)

**Red flags to avoid:**
- Talking negatively about past managers/companies
- Arrogance or defensiveness
- Lack of curiosity (not asking questions back)
- Vagueness (not using numbers or specifics)

---

## Post-Interview Action

1. **Within 1 hour:** Log the interview in `interview-history.md` with score, strengths, weaknesses
2. **Note patterns:** What went well? What would you do differently?
3. **Update career-plan.md:** Did they emphasize anything you didn't expect?
4. **Wait for next round signal**
```

---

## Example Output

```markdown
## Interview Prep: Anthropic — Senior Product Manager, Claude

**Round:** Technical Deep Dive (Round 2 of 3)
**Interview Date:** 2024-05-15 at 2pm CEST
**Interviewer:** Dario Amodei, CEO (per email — likely abbreviated, expect VP Product instead)

---

## Company Intel

### Business Context
- **Stage:** Post-Series A, Series C funding anticipated
- **Funding:** Raised ~$160M to date
- **Burn rate:** High (research-heavy). Company is profitable on inference revenue.
- **Recent news:** Claude 3 family launched (Opus, Sonnet, Haiku). Announced partnership with Stripe. Expanding product offerings.

### Product & Market
- **Core product:** Claude API + web chat interface. LLM-as-a-service competing with OpenAI.
- **Main competitor:** OpenAI (ChatGPT), Google (Gemini), Mistral
- **Market position:** Winning — Claude 3.5 Sonnet is fastest/most capable as of 2024
- **Your assessment:** This is an exciting moment. They're moving from research-first to product-first. First PM hire for Claude product = building the product org from scratch. High impact.

### Culture Signals
- **From Blind:** People love the mission focus. Strong respect for Dario. Smart team. Can be academic (slow on some product decisions).
- **From your network:** Alex at Stripe worked with Anthropic PM on integration. Says: "they care deeply about capability/safety trade-offs, not just shipping fast."
- **Red flags:** Being founded by former OpenAI people = might have high expectations. Academic culture = slower on product iteration than you expect.

---

## Interview Structure for Anthropic

**Typical process for PM roles:**
1. **Initial phone screen (30 min, recruiter)** — culture fit, background, why Anthropic [ALREADY DONE]
2. **This round: Technical deep dive (60 min, VP Product or Dario)** — dive into capability/safety trade-offs, approach to product strategy, how you'd prioritize
3. **Case study (90 min, live design session)** — design a new Claude feature given constraints
4. **Final round (60 min, culture/values)** — team lunch, meet other PMs, assess fit

**Emphasis:** Technical depth + philosophy alignment on safety/capability + ability to ship in academic environment

---

## Your Weakness Heatmap

| Question Type | Strength ✅ | Weakness ⚠️ | Prep Strategy |
|---|---|---|---|
| Capability vs. safety trade-offs | ✅ Shipped in regulated envs (Stripe compliance) | ⚠️ Never worked on alignment/safety | Prepare: "I haven't done alignment research, but here's how I translate constraints into product..." |
| AI/LLM product design | ⚠️ Understand LLM fundamentals | ❌ Limited hands-on LLM product work | Prepare: Use Claude daily. Observe features you like/dislike. Ask great questions about their approach. |
| Academic vs. startup pace | ✅ Can operate in both | ⚠️ Might push too hard for speed | Prepare: Ask about their tempo. Show you respect the research/product cadence trade-off. |
| Scale at this level | ✅ Built to scale | ✅ No weakness here — emphasize |

**Plan:** You'll be asked about aligning safety & capability. Have 2 stories ready (Stripe compliance example + one about unclear constraints). Expect questions about your approach to research partnerships.

---

## Question Bank for This Interview

### Behavioral (Asked everywhere)
1. Tell me about a product decision where you had to balance multiple competing concerns.
2. Tell me about a time you shipped something complex (regulatory, technical, or otherwise).
3. Tell me about your biggest product impact.
4. Why Claude? Why Anthropic specifically?

### Role-Specific for AI Product PM
1. "Imagine we want to expand Claude's capabilities in [domain]. Walk me through how you'd approach this given safety concerns."
2. "Design a new Claude feature. What constraints would you need to understand first?"
3. "How do you think about the relationship between product speed and research velocity?"

### Company-Specific (from Anthropic context)
1. "Tell me about a time you worked with technical/research teams. How did you navigate differences in culture or pace?"
2. "What's your philosophy on safety as a product feature vs. safety as a requirement?"
3. "Anthropic is founded by former OpenAI people. What's your take on the difference between their approach and ours?" [They care about this]

---

## Your Stories (STAR Format)

### Story 1: Shipping with Competing Constraints (Stripe Compliance)

*Situation:* At Stripe, we were building new payment features that had to comply with PCI, state money transmitter laws, and partner API limitations. Engineering wanted to move fast; compliance had guardrails. The core question: how to ship without cutting corners on safety.

*Task:* I was assigned to lead the roadmap for Q3, which required both speed (competitor pressure) and zero safety regressions.

*Action:* I did three things: (1) I worked with legal to categorize requirements into hard blocks vs. nice-to-haves, converting vague "compliance" into specific product constraints. (2) I ran weekly syncs where legal, eng, and I discussed upcoming launches and identified constraint conflicts early. (3) I designed feature specs that built constraints INTO the product, rather than treating compliance as a post-hoc review. Example: instead of "validate for PCI," the system had hard limits on what data could be logged.

*Result:* We shipped 8 features that quarter with zero compliance issues, and velocity actually improved because we built constraints in upfront (60% faster reviews vs. previous quarter).

**Use when asked about:** Capability/safety trade-offs, working with constraints, shipping fast safely

**Key phrases:** "Turn vague requirements into product constraints," "Work with specialists early, not late," "Design with guardrails baked in"

---

### Story 2: Shipping in Ambiguous Territory

*Situation:* At an AI startup, we were building an AI product where the capabilities were genuinely uncertain — we didn't know what the model could do reliably. The business pressure was: launch ASAP. The technical reality: we don't know safe boundaries yet.

*Task:* Define what to ship in v1 without causing user harm or regulatory risk.

*Action:* I proposed we ship a narrow use case where we had 100% confidence in reliability, rather than a broad one we were uncertain about. It meant less revenue initially, but I modeled two scenarios: (A) Ship broad, find issues in production, lose trust; (B) Ship narrow, build reputation, expand safely. I presented both to leadership with forecast. We chose B. I then worked with the ML team on continuous evaluation — we monitored real user sessions to expand boundaries safely over time.

*Result:* Took 3 months to expand beyond the initial narrow use case, but when we did, we had user trust and zero reputation damage. By month 6, we had 2x the initial forecasted capability scope.

**Use when asked about:** Working with uncertain constraints, shipping safely, research/product collaboration

**Key phrases:** "Ship narrow with confidence vs. broad with risk," "Continuous evaluation unlocks safe expansion," "Trust is the constraint, not capability"

---

### Story 3: Learning from Disagreement

*Situation:* My PM partner wanted to launch a feature without sufficient testing. I worried it would fail in production and hurt users.

*Task:* Disagreement management. We both wanted the right thing, but disagreed on risk tolerance.

*Action:* Instead of debating, I asked: "What would make you confident?" Turns out, 5 hours of testing would have been enough for them. I worked with QA to create a targeted test plan that answered their specific concerns (not just generic testing). We shipped 2 weeks later, with both of us aligned.

*Result:* Feature shipped cleanly. More importantly, we learned that transparent disagreement + digging into root concerns beats hierarchy.

**Use when asked about:** Working through disagreement, humility, collaboration

---

## Your Questions to Ask Them

1. **On the product strategy:** "Walk me through how you're thinking about breadth vs. depth for Claude's capabilities over the next 12 months. How do you prioritize?"
2. **On research partnership:** "Tell me about a time product and research had different priorities. How did you navigate that?"
3. **On pace:** "How do you think about the trade-off between research velocity and product shipping speed?"
4. **On the team:** "What's the team structure for Claude product? Who do PMs work with most closely?"
5. **On success:** "What does year 1 look like for success in this role?"
6. **On the company:** "Anthropic was founded by former OpenAI people. What's the core difference in how you approach product compared to them?" [Shows you're thinking strategically]

---

## Pre-Interview Checklist

- [x] Read company intel
- [x] Prepped 3 STAR stories (compliance, ambiguity, disagreement)
- [x] Know 6 questions to ask
- [x] Reviewed weakness areas (AI product experience)
- [x] Know the interviewer (VP Product or Dario — likely VP Product)
- [x] Know this is round 2 of 3 (technical deep dive)
- [x] Used Claude daily for past week (understand the product)
- [ ] Set a reminder 30 min before to settle

---

## During Interview Notes

- **Tone:** Conversational, curious, not defensive
- **On AI/safety:** Ask great questions. You don't need to have all the answers.
- **On pace:** Show you respect academic rigor. Don't try to convince them to move faster.
- **Energy:** This is a conversation, not an interrogation. Be yourself.

---

## Post-Interview (After the call)

- [ ] Log in `interview-history.md` with score out of 10
- [ ] Note: What went well? What surprised you?
- [ ] Update `career-plan.md` if you learned something about company/role that changes your thinking
- [ ] If advancing: schedule next round and prep accordingly
```

---

## Quality Checks

**Good prep:**
- Company intel is specific to THIS company (not generic)
- Your weakness heatmap identifies real gaps and prep strategies
- Stories are detailed and memorable, not generic
- Questions show genuine curiosity, not just "good interview questions"
- Pre-interview checklist is actually actionable

**Bad prep:**
- Generic company research (copy-paste from their website)
- No personalization to your weaknesses
- Stories are vague ("I shipped a feature")
- Questions are canned ("What's the team structure?")
