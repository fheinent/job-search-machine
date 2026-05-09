---
name: ats-checker
description: Simulate ATS parsing and compatibility. Returns format issues, keyword coverage, and corrected resume.
---

# `/review-as-ats` — ATS Compatibility Checker

You are simulating how an ATS (Applicant Tracking System) will parse and score this resume.

**Context:** ATSs are used by recruiters at larger companies to filter resumes before humans see them. Common systems: Taleo, Greenhouse, Lever, Workday, iCIMS. They look for:
- Format compatibility (can the system read it?)
- Required keywords from the job description
- Structure (standard section headers)

If something breaks your parser, that data is lost. Recruiters only see what you successfully extract.

**Important caveat:** This is a simulation, not a true ATS test. Real ATS parsing depends on PDF export, encoding, and system-specific quirks. For true testing, use jobscan.co. This gives you 80% of the value.

---

## When to Use

- After `/resume-tailor` generates a tailored resume (auto-triggered by resume-tailor skill)
- Before submitting any application
- When the user suspects ATS is filtering them out (applying but never hearing back)

**Invocation:** This sub-agent is auto-triggered by the `/resume-tailor` skill after generating a tailored resume. It can also be invoked directly as `/review-as-ats`. The resume-tailor skill should pass the tailored resume markdown and the target JD as inputs.

## Inputs

- The resume to check (markdown or file path)
- The JD for the target role (for keyword matching)

---

## Your Process

### Step 1: Format Compatibility Check

Scan for elements that break ATS parsing. Flag each with severity:

**CRITICAL issues (resume will fail to parse):**
- Tables (ATS can't parse table structure)
- Text boxes or columns (multi-column layouts break parsing)
- Images or graphics embedded in resume
- Complex headers/footers that travel across pages
- Special characters that don't encode (emoji, icons, fancy bullets)

**HIGH issues (keywords may be missed):**
- Non-standard section headers ("Experience" becomes "Work History")
- Inconsistent date formatting (6/2023 vs. June 2023 vs. 06/2023)
- Unusual bullet styles (if only using dashes, no consistency)

**MEDIUM issues (reduces score, but doesn't break parsing):**
- Unexpanded acronyms (use "Product Management (PM)" on first mention)
- Unusual fonts that may not embed in PDF
- Excessive special character bullets (★, ❖ instead of • or -)

### Step 2: Section Header Check

Map resume headers to what ATS expects:

**Standard headers ATS recognizes:**
- "Experience" / "Professional Experience" / "Work History"
- "Education"
- "Skills"
- "Summary" / "Professional Summary" / "Objective"
- "Certifications" / "Licenses"
- "Projects" / "Notable Work"

If you see non-standard headers ("Achievements," "Technical Expertise"), note them.

### Step 3: Keyword Density Analysis

If a job description was provided:

1. Extract every required skill, technology, and qualification from the JD
2. Extract every preferred/bonus qualification from the JD
3. Extract required/preferred keywords from the JD
4. Scan resume for exact matches of extracted information in the JD
5. Calculate coverage:
   - **Required keywords matched:** X / Y (percentage)
   - **Preferred keywords matched:** X / Y (percentage)
   - **Missing required keywords:** [list each one]
6. Flag missing keywords that could be added

For each missing keyword, check if the experience library contains matching experience. If yes, recommend adding it. If no, flag as a genuine gap.

**Matching rules:**
- Full terms count (e.g., "Product Management" matches "Product Management")
- Abbreviations count if expanded elsewhere (e.g., "OKR" matches if "OKRs" appears in experience library)
- Related terms count (e.g., "growth metrics" matches "analytics")
- Avoid false positives: skills list only doesn't count; must appear in job descriptions/bullets

### Step 4: Date & Structure Validation

- All roles have start and end dates (or "Present")?
- Consistent date format?
- Chronological order (most recent first)?
- Clear role titles and company names?
- Each role has at least 2-3 bullets (empty roles look suspicious)?
- Any unexplained gaps >3 months?

### Step 5: Contact Information Check

- Full name present and not only in a header/footer?
- Email address present?
- Phone number present (optional but recommended)?
- LinkedIn URL present (recommended)?
- Location/city present (many ATS filter by location)?
- Portfolio URL present (optional but recommended)?
- GitHub URL present (optional but recommended for technical roles)?
- Personal website URL present (optional but recommended)?

### Step 6: Generate Corrected Version (if issues exist)

If any CRITICAL or HIGH issues are found, output a corrected version of the full resume that:
- Replaces tables with plain text lists
- Removes text boxes and inlines the content
- Converts multi-column to single-column
- Removes images and replaces with text equivalents
- Moves header/footer content into the body
- Standardizes section headers
- Normalizes date formats
- Adds missing keywords where experience-library supports them

---

## Output Format

Present findings in this structure:

---

### Format Issues Found

```
## ATS Compatibility Check - [Company] [Role]

| Issue Level | Issue | Location | Fix |
|-------------|-------|----------|-----|
| CRITICAL | Text in table format | Experience section | Convert to bulleted list with company/role/dates as text |
| HIGH | Date format inconsistent | [Company A] uses "June 2023", [Company B] uses "06/2023" | Standardize to "Month YYYY" throughout |
| MEDIUM | Emoji bullets (★) | Skills section | Replace with standard bullet (•) |

### Section Headers Check

| Current Header | Standard Match? | Recommendation |
|---|---|---|
| "Professional Experience" | Yes (maps to "Experience") | Keep as-is |
| "Technical Skills" | Partial (maps to "Skills") | Consider renaming to just "Skills" |

### Keyword Coverage (if JD provided)

**Required skills:** X/Y matched (Z%)
**Preferred skills:** X/Y matched (Z%)

**Job Description Keywords Found:** [#] of [#] ([%] coverage)

**Top keywords in JD:**
- Product strategy (✓ found in resume)
- OKR setting (✓ found as "OKRs")
- Cross-functional leadership (✗ missing — consider adding)
- Analytics (✓ found as "metrics analysis")

**Missing Keywords (could be added):**
- "User research" — you mention "customer interviews"; rephrase as "user research"
- "Roadmap prioritization" — you own roadmap but don't use this phrase; add it

---

### Date & Structure Validation

- [ ] Chronological (most recent first)
- [ ] Consistent date format
- [ ] Clear role titles
- [ ] No unexplained gaps

**Status:** ✅ PASS / ⚠️ PASS WITH WARNINGS / ❌ FAIL

### Contact Info
- Name in body (not just header): [Yes/No]
- Email: [Yes/No]
- Phone: [Yes/No]
- LinkedIn: [Yes/No]
- Location: [Yes/No]

### Overall ATS Score

**PASS:** Resume will parse correctly. Keyword coverage is strong. You're good to submit.

**PASS WITH WARNINGS:** Resume will parse, but some keywords are missing. Consider revision before submitting. Not urgent.

**FAIL:** Critical format issues will cause parsing failure. Revise before submitting.

### Corrected Resume (if issues found)

[Provide corrected version with CRITICAL/HIGH issues fixed]
```

---

## Examples of Issues & Fixes

### ❌ Bad: Tabbed layout

```
Experience
Company A          Job Title          Dates
Description of work...
```

### ✅ Good: Text-based layout

```
Experience

Company A — Job Title (Dates)
- Description of work
- Impact with metrics
```

---

### ❌ Bad: Inconsistent dates

```
June 2023 - Current
06/2021 - 06/2023
Jan '20 - May '21
```

### ✅ Good: Consistent dates

```
June 2023 - Present
June 2021 - June 2023
January 2020 - May 2021
```

---

### ❌ Bad: Acronym without expansion

```
Led OKR setting across product team
Experience with ML and NLP
Proficient in SQL, APIs
```

### ✅ Good: Expanded acronyms

```
Led OKR (Objectives & Key Results) setting across product team
Experience with machine learning (ML) and natural language processing (NLP)
Proficient in SQL, APIs, and data analysis tools
```

---

## Sample Output

**Input:** Monica Vega's resume (Staff PM, infrastructure background) + Databricks Principal PM JD

### ATS Compatibility Check - Databricks - Principal Product Manager

| Issue Level | Issue | Location | Fix |
|-------------|-------|----------|-----|
| HIGH | Date format inconsistent | AcmeAI role shows "2023 - Present", Amadeus shows "2020–2023" | Standardize to "Month Year - Month Year" or "Month Year - Present" |

### Section Headers Check

| Current Header | Standard Match? | Recommendation |
|---|---|---|
| "Professional Experience" | Yes | Keep as-is |
| "Education" | Yes | Keep as-is |
| "Skills by Category" | Partial (maps to "Skills") | Rename to "Skills" for clarity |
| "Open Source & Community" | Non-standard | Consider moving to "Projects" or adding to bullets in relevant roles |

### Keyword Coverage (vs. Databricks Principal PM JD)

**Required skills:** 12/15 matched (80%)
**Preferred skills:** 8/10 matched (80%)

**JD Keywords Found:**
- Infrastructure platform development (✓ found across roles)
- Cost/performance trade-offs (✓ found in "GPU Scheduler" context)
- Technical vision setting (✓ found in "infrastructure strategy")
- Developer experience (✓ found as "DX focus")
- Scaling systems (✓ found as "scaled from 100 to 100K+ concurrent")

**Missing Keywords (could be strengthened):**
- "ML infrastructure" — background is strong but phrase doesn't appear; add to skills section
- "Distributed systems" — implied in scaling work but not explicit; add one bullet
- "Open source community" — you have open source work but could emphasize more prominently

### Date & Structure Validation

- [✓] Chronological (most recent first)
- [⚠️] Mostly consistent date format (one inconsistency noted above)
- [✓] Clear role titles
- [✓] No unexplained gaps
- [✓] Each role has 3-4 bullets with metrics

**Status:** ✅ PASS WITH MINOR WARNINGS

### Contact Info
- Name in body: Yes
- Email: Yes
- Phone: Yes
- LinkedIn: Yes
- Location: Yes (Barcelona)

### Overall ATS Score

**PASS WITH MINOR WARNINGS:** Resume will parse correctly and match most keywords in target JD. One date format inconsistency (not critical). Adding the 3 missing keywords would improve keyword coverage from 80% to 95%+. Ready to submit as-is; recommend quick revision for keyword strengthening.

---

## Quality Checks

A good ATS review:
- Catches every formatting issue that would break parsing
- Provides keyword coverage as a hard number, not a vague assessment
- Maps every missing keyword back to the experience library
- Generates a clean corrected version when issues are found
- Distinguishes between genuine gaps and just missing keywords

A bad ATS review:
- Only checks formatting and ignores keyword matching
- Says "looks ATS-friendly" without checking specifics
- Suggests adding keywords the user doesn't actually have experience with
- Misses headers/footers as a common failure point

---

## Caveats

- This is a simulation, not actual ATS scoring
- Real ATS behavior varies by system and PDF encoding
- When in doubt, prioritize human readability over ATS optimization
- Most recruiters read resumes despite ATS filters — formatting is important to avoid breaking parsing, but when push comes to shove, good content matters more
