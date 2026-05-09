# Prototype Prompt Template

You've written a great 1-pager work product. Now, create a **clickable prototype** to go with it and blow the interviewer's mind away.

A working UI makes your idea tangible. Takes ~30 minutes to build, and will make you stand out from other candidates.

---

## When to Use This

- **You have a work product that proposes a new feature or flow**
- **You want to show, not tell** (prototype > description every time)
- **You have 30 minutes** to build something quick (not 8 hours)

**Tools that work:**
- Claude Code (free, most flexible)
- Lovable (v0.dev, free tier)
- Vercel v0 (free tier)
- Replit (free)
- Figma Make Prototype (free tier)

---

## The Prompt Template

Copy everything between the `---` markers. Fill in the bracketed sections.

---

Build a clickable prototype for [Company Name]'s [product area].

Context: I'm interviewing for [role title] at [Company Name] and created a product analysis with these recommendations:
1. [Recommendation 1 - the one to prototype. Be specific: what does it do, who is it for, what problem does it solve?]
2. [Recommendation 2 - brief description]
3. [Recommendation 3 - brief description]

Build an interactive prototype of recommendation #1.

**User flow:**
- [Step 1: What the user sees first, e.g., "Dashboard showing invoice status with a new 'Smart Reminders' panel"]
- [Step 2: What the user clicks/does, e.g., "User clicks 'Configure Reminders' and sees a setup wizard"]
- [Step 3: The key interaction, e.g., "User sets reminder rules based on invoice age and amount, sees preview of reminder email"]
- [Step 4: The outcome, e.g., "Confirmation screen showing projected impact: '34% fewer late payments based on your invoice history'"]

**Screens needed:**
1. [Screen 1 name and what it shows]
2. [Screen 2 name and what it shows]
3. [Screen 3 name and what it shows]

**Design requirements:**
- Match [Company Name]'s design language. Their brand colors are [colors if known, or "look up their website"]. Their UI style is [clean/dense/playful/enterprise -- describe what you see on their product].
- Use their typography style (serif/sans-serif, weight, spacing)
- Navigation should feel like it belongs inside their existing product
- Include realistic dummy data that matches their domain (e.g., real-sounding company names for a B2B product, realistic dollar amounts for a fintech product)

**Tech stack:** Use React and Tailwind CSS.

**Priority:** Looking real > being complete. This is for a job application, not production. Focus on:
1. The main happy path working end-to-end
2. Realistic-looking data and UI polish
3. One or two micro-interactions that feel premium (hover states, transitions)

Do NOT build, unless the chosen recommendation makes it a MUST:
- Authentication or login flows
- Backend logic (mock all data)
- Edge cases or error states
- Mobile responsiveness (desktop only is fine)

---

## Real Example

```
Build a clickable prototype for Stripe's payables product.

Context: I'm interviewing for Senior PM at Stripe and created a product analysis with these recommendations:
1. Smart Invoice Reminder feature - AI-drafts personalized payment reminders, user approves before sending. Reduces manual chasing time by 60%.
2. Invoice status dashboard - Real-time visibility into overdue invoices, categorized by risk level
3. Automated escalation workflow - Triggers reminder sequences based on invoice age and customer history

Build an interactive prototype of recommendation #1.

**User flow:**
- Step 1: Payables admin opens Stripe dashboard and sees "3 overdue invoices" alert in the sidebar
- Step 2: Admin clicks alert and sees list of overdue invoices (Acme Corp $5,200 due 3 days ago, TechCorp $12,000 due 7 days ago, etc.)
- Step 3: Admin clicks Acme Corp invoice and sees AI-drafted reminder message: "Hi Acme, just checking in on invoice #INV-2024-567 for $5,200 from March 1st..."
- Step 4: Admin can edit the message, toggle "use this template for future reminders," and click "Send Now" or "Schedule for tomorrow"

**Screens needed:**
1. Dashboard alert / sidebar - Shows "3 overdue invoices" summary
2. Overdue invoices list - Table showing company, amount, days overdue, status
3. Single invoice detail - Suggested message draft, edit field, send/schedule buttons
4. Confirmation screen - "Reminder sent to Acme Corp" with link to audit history

**Design requirements:**
- Match Stripe's design language (clean, minimal, blue/gray palette)
- Use Stripe's primary color (#635BFF) for CTAs
- Include realistic invoice data (real company names, realistic amounts like $5,200, $12,000, not round numbers)
- Use Inter font or reasonable sans-serif fallback
- Navigation should feel like an extension of Stripe's existing dashboard

**Tech stack:** React and Tailwind CSS.

**Priority:** Looking real > being complete. Focus on:
1. The main happy path (see overdue → view suggestion → send message)
2. Realistic-looking invoice data and message drafts
3. One micro-interaction (e.g., smooth transition when editing message, or hover state on invoice row)

Do NOT build, unless needed:
- Actually sending emails (mock the send action)
- Email template editor interface (just show a text field with pre-filled message)
- Full audit history (show last 2-3 reminders, that's enough)
- Mobile responsiveness (desktop-only is fine)

```

---

## After Generation

### Checklist

- [ ] **Looks real** — could you show this to a customer?
- [ ] **Matches company branding** — colors, typography, spacing feel right?
- [ ] **Main flow works** — user can click through the happy path
- [ ] **Dummy data is realistic** — not Lorem ipsum, actual names/numbers
- [ ] **One design pass** — not pixel-perfect, but polished enough to screenshot

### How to Share It

**Option A: Live link** (best)
- Deploy to Vercel or Netlify (free tier)
- Share link in email
- Interviewer can click and play

**Option B: Screenshots** (good)
- Take 3-5 screenshots showing the flow
- Paste into your work product document
- Include captions ("User sees suggested reminder and can edit before sending")

**Option C: Screen recording** (okay)
- Record a 30-second video of the flow
- Narrate: "Click to see the suggested message. Edit if needed. Send or skip."
- Share link or embed in document

---

## Pro Tips

**Timeboxing:** Don't build for more than 30 minutes. If it's not done, good enough is good enough.

**Realistic data:** Make dummy data realistic. Instead of "Product A," use "Slack," "Notion," "Vercel." Instead of "$100," use "$4,250" (realistic invoice amount).

**Focus on ONE flow:** Don't try to show settings, admin, reporting. Just show the core user action.

**Match their design:** Spend 5 minutes in their app / website. Grab their color codes. Use their typeface (or a reasonable match). This signals you understand their brand.

**No backend:** You're not building a production app. Just the UI. No APIs, no database, no auth.

---

## If You Get Stuck

If you can't build the prototype:
- **Share the design brief instead** (the prompt you wrote)
- **Link to a competitor's flow** (e.g., "Here's how Bill.com does smart reminders — I'd adapt this for Stripe's design")
- **Do wireframes in Figma** (sketches are fine; working prototype is better but not mandatory)

The prototype is nice to have. The idea is what matters. Don't spend 3 hours building if 1 idea sketch gets the point across.
