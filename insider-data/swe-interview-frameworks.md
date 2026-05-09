# SWE Interview Frameworks

Comprehensive guide for software engineering interviews. Use alongside `experience-library.md` and company-specific intel in `company-intel/`.

---

## System Design Interviews

### The Framework (use this structure every time)

1. **Requirements gathering** (3-5 min) — Clarify functional and non-functional requirements. Ask about scale, latency, consistency, availability. This is where senior candidates separate themselves.
2. **High-level design** (5-8 min) — Draw the major components: clients, load balancers, services, databases, caches, queues. Establish data flow.
3. **Component deep-dive** (10-15 min) — Pick 1-2 components the interviewer cares about. Go deep on data model, API design, algorithms, storage choices.
4. **Scaling & reliability** (5-8 min) — Horizontal scaling, replication, partitioning, caching layers, CDN. Discuss failure modes and recovery.
5. **Trade-offs & wrap-up** (3-5 min) — Articulate what you traded off and why. Consistency vs availability. Cost vs performance. Simplicity vs flexibility.

### Common Topics

- URL shortener (hashing, collision handling, analytics)
- Chat system (WebSockets, message ordering, presence, fan-out)
- News feed (push vs pull, ranking, fan-out-on-write vs fan-out-on-read)
- Rate limiter (token bucket, sliding window, distributed rate limiting)
- Distributed cache (consistent hashing, eviction policies, cache invalidation)
- Notification system (multi-channel delivery, templating, deduplication)
- Search autocomplete (trie, precomputation, ranking by popularity)
- File storage / Google Drive (chunking, sync, conflict resolution)
- Metrics / monitoring system (time-series DB, aggregation, alerting)
- Ride-sharing matching (geospatial indexing, real-time matching, ETA)

### What Interviewers Evaluate

| Signal | What they're looking for |
|--------|--------------------------|
| Requirement gathering | Do you ask clarifying questions or jump to drawing boxes? |
| API design | Clean, RESTful, versioned. Correct HTTP semantics. |
| Data modeling | Appropriate schema. Understands SQL vs NoSQL trade-offs. |
| Scalability reasoning | Can you reason about bottlenecks and calculate back-of-envelope numbers? |
| Trade-off articulation | Every decision has a cost. Do you name it? |
| Communication | Are you driving the conversation or waiting for prompts? |

### Level Expectations

- **E3-E4 (Junior/Mid):** Focus on functional requirements and basic component design. Show you understand client-server, databases, and caching.
- **E5 (Senior):** Own the full framework. Drive the conversation. Deep-dive with confidence. Calculate throughput and storage.
- **E6 (Staff):** System-level trade-offs, operational concerns (deployment, monitoring, rollback), multi-region, cost optimization. Discuss evolution over time.
- **E7+ (Principal/Distinguished):** Organizational impact. How the system design affects team structure, on-call, and cross-team dependencies. Technology strategy.

---

## Coding Interviews

### Pattern Categories

**Arrays & Strings:** Two pointers, sliding window, prefix sums, sorting + binary search, hash maps for O(1) lookup.

**Trees & Graphs:** BFS, DFS, topological sort, shortest path (Dijkstra, BFS on unweighted), union-find, tree traversals (inorder, preorder, postorder, level-order).

**Dynamic Programming:** Recognize overlapping subproblems. Start with brute-force recursion, add memoization, then convert to bottom-up if time allows. Common patterns: knapsack, LCS, interval DP, digit DP.

**System Simulation:** Design and implement components (LRU cache, file system, iterator, task scheduler). Tests OOP and clean API design.

**Concurrency:** Producer-consumer, reader-writer locks, thread-safe data structures. Mostly relevant at senior+ or for infra roles.

### What Matters Beyond Correctness

1. **Communication.** Talk through your approach before coding. Explain WHY, not just WHAT.
2. **Test case thinking.** Before writing code, identify edge cases: empty input, single element, duplicates, overflow, negative numbers.
3. **Time/space complexity.** State it unprompted after solving. Know when your solution is optimal and when it's not.
4. **Iterative refinement.** Start with brute force, articulate why it's slow, then optimize. This shows problem-solving process.
5. **Code quality.** Meaningful variable names, helper functions, clean structure. Interviewers read your code.

### Level Expectations

- **E3-E4 (Junior/Mid):** Solve medium problems cleanly with clear communication. Correctness and basic complexity analysis matter most.
- **E5 (Senior):** Solve hard problems, discuss trade-offs between approaches, and optimize iteratively. Expect follow-up extensions.
- **E6+ (Staff+):** Code quality, testing strategy, and system-level thinking matter as much as the solution. Interviewers assess whether you write production-grade code under pressure.

### Common Mistakes

- Jumping to code without clarifying the problem or discussing approach
- Not testing with examples before submitting
- Over-engineering (using a segment tree when a hash map works)
- Silent coding — interviewer can't evaluate what they can't see
- Ignoring edge cases until the interviewer asks
- Giving up instead of breaking the problem into smaller parts

---

## Behavioral Interviews for Engineers

### Top 10 SWE-Specific Behavioral Questions

1. **Tell me about a technical decision you disagreed with.** — Tests: engineering judgment, influence without authority, ability to disagree and commit.
2. **Describe a production incident you resolved.** — Tests: calm under pressure, systematic debugging, incident communication, blameless postmortem thinking.
3. **How do you handle technical debt?** — Tests: prioritization, pragmatism vs perfectionism, ability to make the business case for refactoring.
4. **Tell me about a time you mentored a junior engineer.** — Tests: teaching ability, patience, investment in team growth. Critical for senior+ levels.
5. **Describe a project where requirements changed significantly.** — Tests: adaptability, stakeholder management, ability to re-plan without losing momentum.
6. **How do you approach code reviews?** — Tests: collaboration, communication style, quality standards. Do you nitpick or focus on what matters?
7. **Tell me about a time you had to learn a new technology quickly.** — Tests: learning agility, resourcefulness, comfort with ambiguity.
8. **Describe your most complex debugging experience.** — Tests: systematic thinking, tool knowledge, persistence, root cause analysis.
9. **How do you prioritize competing technical demands?** — Tests: judgment, stakeholder communication, ability to say no with rationale.
10. **Tell me about a time you pushed back on a product requirement.** — Tests: cross-functional collaboration, technical advocacy, outcome orientation (not ego).

### Grading: Three Laws for Engineers

The Three Laws (Structure, Specificity, Skill Demonstration) apply to SWE behavioral answers with these adjustments:

| Law | Standard | SWE-Specific Emphasis |
|-----|----------|----------------------|
| Structure | STAR or similar framework | Include technical context without over-explaining. Non-technical interviewers should follow; technical interviewers should see depth. |
| Specificity | Concrete details, metrics | Name technologies, quantify scale (requests/sec, data volume, team size), describe the actual technical approach. |
| Skill Demonstration | Shows the competency asked about | Evaluate for: technical depth, system thinking, engineering judgment, collaboration. Not just "I did X." |

**Common failure mode:** Engineers over-index on technical detail and forget to explain the impact, the decision-making, and the collaboration. The best answers balance technical depth with business context.

---

## Company-Specific SWE Interview Formats (Top 20)

### Google
- **Rounds:** 5 on-site (2 coding, 1 system design, 1 behavioral/Googleyness, 1 flex). Phone screen first.
- **Unique:** Hiring committee review after interviews. Team matching happens AFTER offer. Googleyness = collaboration, humility, doing the right thing.
- **Levels:** L3-L4 coding-heavy. L5+ system design carries more weight. L6+ requires demonstrated cross-team influence.

### Meta (Facebook)
- **Rounds:** Phone screen, then 4-5 on-site (2 coding, 1 system design, 1 behavioral, sometimes 1 product sense for full-stack).
- **Unique:** "Move fast" culture signal matters. They look for speed and pragmatism, not just correctness. Team matching before final offer.
- **Levels:** E3-E4 coding-focused. E5+ system design weight increases. E6 requires demonstrated tech leadership.

### Amazon
- **Rounds:** Phone screen + loop of 4-5 (coding, system design, behavioral). Every round includes Leadership Principles.
- **Unique:** LP-heavy. Every behavioral answer should map to 1-2 Leadership Principles. Bar raiser in the loop (independent evaluator). "Hire and Develop the Best" and "Dive Deep" are common engineer LPs.
- **Levels:** SDE1-SDE2 coding-heavy. SDE3/Principal require design and LP depth.

### Apple
- **Rounds:** Phone screen, then 5-6 on-site. Mix of coding, system design, domain-specific, and team-fit.
- **Unique:** Team-specific hiring (you interview for a specific team). Secrecy culture — they may not tell you much about the project until later. Focus on craftsmanship and attention to detail.

### Microsoft
- **Rounds:** Phone screen, then 4-5 on-site. Final round is often with a senior leader ("as appropriate" interview).
- **Unique:** "As appropriate" interview is pass/fail and heavily behavioral. Growth mindset is a core value. Team matching during the process.

### Netflix
- **Rounds:** Multiple phone screens (often 3-4), then on-site panel.
- **Unique:** Culture fit is paramount. "Freedom and Responsibility" memo is required reading. Expect questions about judgment, candor, and self-direction. Senior-only hiring (no junior roles). High comp, no RSUs.

### Stripe
- **Rounds:** Phone screen, then 4-5 on-site (coding, system design, collaboration, manager/leadership).
- **Unique:** "Collaboration" round — pair programming or working through a problem together. They want to see how you think WITH someone. Bug bash round (debug existing code) is common.

### Airbnb
- **Rounds:** Phone screen, then 4-5 on-site including cross-functional and core values.
- **Unique:** Core values interview is a full round. "Belong Anywhere" culture. Expect questions about inclusivity, community, and mission alignment. Architecture round uses Airbnb-relevant scenarios.

### Uber
- **Rounds:** Phone screen, then 4-5 on-site (coding, system design, behavioral, domain).
- **Unique:** System design often involves real-time, geospatial, or high-throughput scenarios relevant to ride-sharing and delivery. Senior roles test cross-team influence.

### Coinbase
- **Rounds:** Phone screen, coding, system design, behavioral, culture.
- **Unique:** Crypto/blockchain domain knowledge is a plus but not required for most roles. "Clear communication" is a core cultural value. Remote-first.

### Databricks
- **Rounds:** Phone screen, then 4-5 on-site (coding, system design, behavioral).
- **Unique:** Data engineering and distributed systems depth expected. Spark knowledge helpful. System design often involves data pipeline or query engine scenarios.

### Snowflake
- **Rounds:** Phone screen, coding, system design, behavioral, team fit.
- **Unique:** Database and cloud infrastructure knowledge valued. Expect questions about query optimization, distributed storage, and multi-tenancy.

### Figma
- **Rounds:** Phone screen, then 4-5 on-site (coding, system design, collaboration, values).
- **Unique:** Product sense matters even for engineers. Real-time collaboration systems and CRDT knowledge relevant. Design tool domain helpful.

### Notion
- **Rounds:** Phone screen, then 4-5 on-site (coding, system design, values, collaboration).
- **Unique:** Full-stack generalists preferred. Expect product thinking alongside technical depth. Small team culture — they hire slowly.

### Vercel
- **Rounds:** Take-home or async coding, then interviews (system design, behavioral, team fit).
- **Unique:** Frontend and developer tooling expertise expected. Open-source contributions noticed. Next.js ecosystem knowledge is a strong signal.

### Shopify
- **Rounds:** Phone screen, coding (often in Ruby/Rails context), system design, life story, technical leadership.
- **Unique:** "Life story" interview — they want to understand your full arc. Commerce domain knowledge helps. Remote-first.

### Square (Block)
- **Rounds:** Phone screen, then 4-5 on-site (coding, system design, behavioral, domain).
- **Unique:** Payments and fintech domain helps. Clean code and testing emphasis. Java/Kotlin common.

### Plaid
- **Rounds:** Phone screen, coding, system design, behavioral.
- **Unique:** Fintech/API design depth valued. Security awareness matters. System design often involves banking integrations and data aggregation.

### Ramp
- **Rounds:** Phone screen, coding, system design, behavioral, culture.
- **Unique:** Fast-moving startup culture. Expect speed and pragmatism. Fintech domain. Full-stack generalists preferred.

### Anthropic
- **Rounds:** Phone screen, coding, system design, research/technical depth, values/mission.
- **Unique:** AI safety mission alignment matters. Expect deep technical discussions about ML systems, scaling, and safety. Research-oriented culture even in engineering. Thoughtfulness and intellectual humility valued.

---

## Staff+ / EM-Specific Interviews

### Architecture Review Rounds
- You'll be given an existing system (often the company's actual architecture, simplified) and asked to critique, improve, or extend it.
- **What they evaluate:** Do you ask about constraints first? Can you identify the real bottleneck vs cosmetic issues? Do you propose incremental improvements or only big rewrites?
- **Preparation:** Practice reviewing open-source system architectures. Read engineering blog posts from your target companies. Develop a checklist: reliability, scalability, operability, security, cost, developer experience.

### Cross-Team Influence Scenarios
- "Two teams disagree on the API contract. How do you resolve it?"
- "Your team's project depends on another team that has different priorities. What do you do?"
- **What they evaluate:** Influence without authority, empathy for other teams' constraints, ability to find win-win solutions, escalation judgment.

### Technical Strategy / Roadmap Questions
- "You have 6 engineers and 12 months. Here's the product vision. What do you build and in what order?"
- "Our system handles 10K req/sec today. We need to support 1M. What's your migration strategy?"
- **What they evaluate:** Prioritization frameworks, sequencing logic, risk management, ability to connect technical work to business outcomes, communication of technical strategy to non-technical stakeholders.

### "How Would You Improve Our System?" Questions
- Requires pre-interview research: read engineering blog posts, analyze the product as a user, look at job postings for architectural hints.
- **Structure your answer:** (1) What I observed as a user, (2) What I'd hypothesize about the architecture, (3) Where I'd investigate first, (4) Potential improvements with trade-offs.
- **What they evaluate:** Product sense, curiosity, humility (you don't know their system — acknowledge that), ability to reason about systems you haven't built.

### EM-Specific Additions
- **Team building:** How do you hire? How do you handle underperformers? How do you retain top talent?
- **Process design:** How do you run sprints/planning? How do you balance tech debt vs features? How do you handle on-call?
- **Stakeholder management:** How do you communicate technical concepts to PMs and executives? How do you push back on unrealistic timelines?
- **Delivery:** Tell me about a project that was at risk. How did you get it back on track?
