# Base Resume Template

This is your **master resume**. It contains all possible bullets from your entire career. Use this as a source document — when you apply to a specific role, use `/resume-tailor` to extract the right bullets for that job.

**Instructions:**
1. Fill in your contact info, summary, and all experience bullets. Or you can run "Help me organize my base resume using the experience library" and Claude will fill in the information for you
2. Review, add anything missing, remove anything outdated
3. This file should have MORE bullets than any single tailored resume (tailored resumes select the best 3-5 per role)
4. Take especial care with the tag section
5. When applying to a role, run `/resume-tailor [job description]` — it will pull from this template and customize it
6. Update this template quarterly as you learn new things

---

## Contact Block

**Your Name**  
Email: [your.email@example.com]  
Phone: +[country code] [phone]  
LinkedIn: linkedin.com/in/[profile]  
Location: [City, State/Country] | Open to [geographic preference]

---

## Summary / Professional Headline

**Choose one (or rotate between them depending on the role):**

### Version A: Growth-Focused
Senior Product Manager with 5+ years of PM experience scaling B2B SaaS products. Proven track record: $300k → $1.2M MRR in 18 months through data-driven onboarding, expansion, and monetization. Seeking roles where I can apply growth mechanics to [specific problem].

### Version B: Strategy-Focused
Product leader who builds products through customer discovery, rigorous prioritization, and cross-functional execution. 5 years building at startups from early growth to Series B. Most proud of work that ships fast and proves or kills hypotheses within weeks, not months.

### Version C: Technical-Focused
Senior PM with deep technical literacy and metrics-driven mindset. Built analytics infrastructure, experimented with pricing models, and executed cross-functional projects with engineering and design. Comfortable in both product strategy and hands-on execution.

---

## Experience

### [Most Recent Role]

**Company:** [Name], [Stage] ([ARR/Funding if known])  
**Title:** [Your Title]  
**Dates:** [Month Year] – [Month Year]  
**Team Size:** [# engineers], [# designers], [# analysts]  
**Scope:** [1-2 sentence description of what you owned]

#### Bullets (pick the 5-8 most relevant based on the job you're applying to):

- **[GROWTH]** Redesigned onboarding flow, reducing time-to-activation from X to Y. Increased user activation by Z%, resulting in $[M]M incremental ARR.

- **[STRATEGY]** Set product strategy for [area]; defined 2-year roadmap with clear OKRs. Prioritized across [# of requests], shipping [# features] that drove [specific metric].

- **[EXECUTION]** Led cross-functional initiative across [eng/design/sales]; owned scope, timeline, stakeholder alignment. Shipped in [timeframe] with [outcome metric].

- **[TECHNICAL]** Built data infrastructure for [type]; enabled real-time [metric type] tracking. Identified [key insight] that led to [decision/action].

- **[LEADERSHIP]** Mentored [# people] on [skill]; [outcome]. Ran [# meetings/reviews] to build alignment across [teams].

- **[CUSTOMER]** Conducted [# interviews] with [user type]; synthesized into [artifact]. Drove [decision] based on research, which resulted in [outcome].

- **[DOMAIN]** Established [domain expertise/framework]; now [impact/usage by team]. Interviewed [# customers] to validate [hypothesis].

- **[METRICS]** Tracked cohort analysis, churn drivers, and expansion metrics. Identified [pattern]; recommended [action]; execution resulted in [outcome].

---

### [Second Recent Role]

**Company:** [Name]  
**Title:** [Your Title]  
**Dates:** [Month Year] – [Month Year]  
**Scope:** [Brief description]

#### Bullets (5-8, most recent roles get more bullets):

- **[GROWTH]** [Describe]
- **[STRATEGY]** [Describe]
- **[TECHNICAL]** [Describe]
- **[EXECUTION]** [Describe]

---

### [Third Role]

**Company:** [Name]  
**Title:** [Your Title]  
**Dates:** [Month Year] – [Month Year]  
**Scope:** [Brief description]

#### Bullets (3-5):

- **[GROWTH]** [Describe]
- **[EXECUTION]** [Describe]
- **[LEADERSHIP]** [Describe]

---

### [Earlier Roles]

List with 2-3 bullets each (not 5-8):

**[Company] — [Title] ([Dates])**
- **[TAG]** [Bullet]
- **[TAG]** [Bullet]

---

## Education

**[University Name]**  
[Degree], [Major] | Graduated [Year]  
Relevant coursework: [if applicable]  
Awards: [if impressive]

---

## Skills / Technical

**Product Management:**
- Product strategy & positioning
- Metrics & analytics (cohort analysis, funnel analysis, experimentation)
- Customer discovery & research
- Roadmap prioritization & stakeholder management
- [Add your specialties]

**Technical / Tools:**
- [Programming languages you know, if relevant]
- [Data tools: SQL, Tableau, Mixpanel, etc.]
- [Design tools: Figma, etc.]
- [CRM / Data platforms]

**Domain Expertise:**
- [Industry]: [specific knowledge]
- [Problem area]: [specific knowledge]
- [Market]: [geographic or segment expertise]

---

## Certifications / Additional (Optional)

- [Certification name] ([Year])
- [Speaking]: ProductCon 2024, "How to Scale Onboarding"
- [Writing]: Substack, 2,400 subscribers, writing on product strategy
- [Open source / side projects]: [if relevant]

---

## Bullet Tag Reference

Use these tags to mark what each bullet demonstrates:

| Tag | What It Demonstrates | When JD Asks For |
|-----|----------------------|------------------|
| **GROWTH** | Revenue impact, user acquisition, expansion, metrics | "Experience driving growth," "Scaling," "North Star metrics" |
| **TECHNICAL** | Infrastructure, systems thinking, technical literacy | "Strong technical sense," "Works well with engineers," "Data analysis" |
| **LEADERSHIP** | Team building, mentorship, influence, cross-functional work | "Influence without authority," "Leadership," "Team player" |
| **STRATEGY** | Long-term thinking, prioritization, frameworks, positioning | "Strategy," "Roadmap," "Vision," "0-1 thinking" |
| **EXECUTION** | Shipping, project management, deadline delivery, iteration | "Execution," "Ship it," "Fast delivery," "Bias toward action" |
| **CUSTOMER** | User research, interviews, empathy, customer obsession | "Customer-focused," "User research," "Customer interviews" |
| **DOMAIN** | Market knowledge, competitive understanding, depth in area | "Domain expertise," "Industry knowledge," "Market understanding" |

---

## Feeling unease about an agent deciding what to include in your resume?

Ypu might find the idea of an agent analysing a JD and deciding what to include and what to leave out of your resume unsettling. Rest assured that the agent is only using the information that you provide it. So if you don't like what the agent decides to include or leave out, you can simply edit the .md file that you have generated and edit it to your liking.

That being said, you can be extra extra careful and do the following:

1. **Review the job description:** What skills are they asking for?
2. **Highlight the top 3 asks:** (e.g., "Growth experience," "Analytics," "Cross-functional leadership")
3. **Run `/resume-tailor [JD]`:** Claude will extract the right bullets from this template
4. **Get 2-3 bullets per "ask":** Tailor your bullets to emphasize what the JD is looking for
5. **Review for ATS compatibility:** `/resume-tailor` will check this, but scan for PDF-unfriendly elements (tables, images)

The Job Search Machine is designed to do this exact playbook and more, but you always have the final say.

### Quarterly Maintenance

Every 3 months:
1. Add new wins from your current role (if employed)
2. Remove bullets that feel dated
3. Rewrite bullets with new metrics if numbers have changed
4. Test `/resume-tailor` on a few old job descriptions to make sure bullets still land

---

## Dos and Don'ts

### ✅ Do

- Use specific numbers (not "increased," use "increased 34%")
- Lead with impact (what happened as a result?)
- Match the job description language (use their words)
- Show progression (recent roles have more bullets, older roles have fewer)
- Mention scope / team size for context (1 engineer vs. 10)

### ❌ Don't

- Use AI language ("leverage," "synergize," "robust," "cutting-edge")
- Make claims you can't back up with data
- List responsibilities (everyone had meetings; say what you shipped)
- Use acronyms without expanding (first mention: "ARR (Annual Recurring Revenue)", then "ARR" is fine)
- Pad with weak bullets (if you did 6 things, but 1 is weak, cut it)

---

## Example Bullets by Category

### GROWTH Examples
- "Redesigned signup flow; reduced friction by 40%. New users → first action in 2 hours (vs. 3 days). +34% activation rate YoY."
- "Led expansion into enterprise segment; built sales-assisted pilot motion. Closed 3 deals in 6 months; $500k ARR from new vertical."
- "Owned pricing strategy; tested value-based model vs. usage-based. Migrated 50 customers; +22% ACV without churn."

### TECHNICAL Examples
- "Built data infrastructure for real-time analytics; enabled weekly metric tracking vs. monthly. Discovered churn driver that informed 3 product decisions."
- "Fluent in SQL and Tableau; analyze cohorts to inform prioritization. Identified high-value customer segments; drove [specific action]."

### LEADERSHIP Examples
- "Mentored 2 APMs on storytelling and OKR-setting; both promoted to PM within 12 months."
- "Ran cross-functional initiative across eng/design/sales; owned scope, timeline, and communication. Shipped [feature] in [timeframe]."

### STRATEGY Examples
- "Defined 2-year product strategy for growth team; prioritized across 40+ requests. Shipped 8 features that collectively drove [metric] improvement."
- "Repositioned product from [old positioning] to [new positioning]. Messaging test improved sales qualified leads 2.1x."

### EXECUTION Examples
- "Shipped [feature] in 6 weeks; managed scope with engineering, design, and sales input. Launched with [go-to-market motion]; [outcome]."

### CUSTOMER Examples
- "Conducted 20 customer interviews; uncovered top 5 feature requests. Prioritized 2; both shipped and drove retention improvements."

### DOMAIN Examples
- "Deep expertise in SaaS metrics (CAC, LTV, NRR, churn). Advise sales on pricing sensitivity; inform finance on annual contract modeling."

---

## Next Steps

1. **Fill this template completely** — don't leave it half-done
2. **Save it** — this becomes your resume source document
3. **Use it with `/resume-tailor`** — every time you apply to a new role, tailor it
4. **Update quarterly** — add wins, remove old bullets, keep it fresh
