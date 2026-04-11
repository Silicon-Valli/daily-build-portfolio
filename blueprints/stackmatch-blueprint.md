# StackMatch Blueprint
**A vibe coding stack recommender quiz — steal this and adapt it to any crowded tool category**

---

## What it is

StackMatch is a 5-question quiz that recommends the right combination of AI coding tools for your specific project. You answer questions about what you're building, your technical background, your timeline, and your budget — and get back a named stack (e.g., "The Developer Stack" or "The Zero Budget Stack") with 3 specific tool recommendations, price estimates, and time-to-ship per tool.

It runs entirely as a static HTML file. No backend, no API calls, no user accounts. One file, open in browser, fully functional.

---

## The demand signal that justified it (why this, why now)

Three new AI coding tools launched in the first week of April 2026: flock (parallel agent orchestration), Baton (branch-isolated agent runs), and Antigravity (Google's agentic IDE). This added to an already noisy field. Indie Hackers published a thread listing 29 top vibe coding tools. New builders entering the space can't figure out where to start.

The specific frustration: every resource either lists all tools (overwhelming) or recommends one tool for everyone (useless). There's no opinionated, branching recommendation that accounts for your actual situation.

Search demand is real: "best vibe coding tools," "lovable vs cursor," "how to build a web app without coding," "what tools should I use to build a SaaS" — these are live queries with no clean answer.

---

## Exact build steps

This is genuinely replicable in one sitting.

**Step 1: Define your decision tree (30 minutes of thinking, not building)**

Before touching code, write out 5 questions that actually differentiate users. For a stack recommender:
- What type of project? (determines the entire framework category)
- What's their coding level? (determines AI vs human coding tools)
- How fast? (determines Cursor vs Windsurf, or Lovable vs Bolt)
- Do they need a backend? (determines Supabase vs nothing)
- What's their budget? (determines which paid tools to include)

The output: a 2D matrix of ~8 profiles. Each profile is a named stack. Write the names and the "why this stack" paragraph before writing any code.

**Step 2: Write the HTML (60-90 minutes)**

Structure:
- Progress bar (CSS transition on a `div` width)
- One question visible at a time (innerHTML swap via JS)
- Each option is a clickable div that pushes a value into an `answers[]` array
- After 5 clicks, `getStackKey(answers)` picks a profile from a lookup object
- Results render: stack name + explanation paragraph + 3 tool cards

All state lives in two variables: `answers` (array) and `current` (integer). No framework needed. The entire quiz is ~200 lines of vanilla JS.

**Step 3: Write the content (1-2 hours)**

This is the actual work. Each stack profile needs:
- A memorable name ("The Lovable Stack" not "Recommended Stack #4")
- A 2-sentence "why this" explanation that would make someone nod
- 3 specific tools with: name, role (Build/Host/Database), honest description, real price, realistic time estimate

Do not write vague descriptions. "Lovable handles auth and UI" is worse than "Lovable is the most capable no-code AI builder in 2026 — it ships actual apps, not mockups." The opinionated specificity is the product.

**Step 4: Test every path (15 minutes)**

With 5 questions averaging 4 options each, there are ~1024 possible paths. You only need to handle ~8 actual profiles, but test the edge cases: "free + no code + landing page" should give the landing stack, not a $25/month recommendation.

**Step 5: Deploy to Vercel (2 minutes)**

Go to vercel.com/new → drag the .html file → click Deploy → rename the project. Done. Single-file HTML deploys to Vercel's CDN instantly.

---

## Monetization path

**Immediate (day 1):**
There's no paid CTA in the current version. That's intentional — the tool's job is to get shared. Distribution first.

**Week 1 monetization:**
Add an email capture at the end of the results: "Get notified when the tool list updates (happens weekly)." Email list is the monetization seed.

**Month 1:**
Tool makers will notice you're sending them traffic. Reach out to Lovable, Cursor, Windsurf — offer a "Featured Tool" placement for $49/month. You're not selling ads, you're selling placement in a recommendation engine. Totally different positioning.

**Month 3+:**
If the tool gets traffic: "Get the extended stack guide — 10 additional tools, 3 real project examples, and a decision tree for edge cases." Sell as a $19 PDF or Notion template. The quiz drives it.

The pattern: free quiz → email list → sponsored placement or paid extended resource. Zero infrastructure cost throughout.

---

## What to do differently next time

**Be more opinionated about specific version differences.** The quiz currently treats Cursor and Windsurf as interchangeable except for speed. In practice, they have different strengths for different project types. Sharper differentiation = more trust in the recommendation.

**Add a "results share" mechanism.** After the result, a "Share your stack →" button that generates a URL like `stackmatch.html?stack=developer` would let people share their result on social. The quiz validates itself when someone posts "got The Developer Stack, and that's exactly what I'm running."

**Validate the content before shipping.** The tool claims to know what's best. Make sure every recommendation survives 5 minutes of Googling — no deprecated tools, no wildly off pricing. If anything in the tool is wrong, it poisons trust in everything.

---

## Steal this formula for other contexts

The "crowded tool category → opinionated quiz recommender" is a formula that works anywhere there are too many options.

Direct analogies:
- **"Email tool recommender"**: 5 questions → Mailchimp vs ConvertKit vs Beehiiv vs Substack vs Loops
- **"AI writing tool finder"**: budget + use case → Claude vs GPT vs Jasper vs Copy.ai vs Perplexity
- **"Project management recommender"**: team size + workflow → Linear vs Notion vs Asana vs ClickUp
- **"Payment processor picker"**: volume + country + product type → Stripe vs Lemon Squeezy vs Paddle vs Gumroad

In every case: the market is noisy, every "comparison" article is biased toward affiliate links, and there's no tool that takes your actual situation into account and gives you a direct answer. That gap is always there. This is the template.

The formula: pick a crowded category → identify the 4-5 real differentiators → define 6-10 coherent user profiles → build the quiz → deploy → reach out to tool makers.

Distribution is always the same: post in the communities where confused people congregate, let the tool validate itself when someone's recommendation matches their setup, collect emails.

---

*Built: Apr 04, 2026 | Demand signal: flock, Baton, Antigravity launches + Indie Hackers "29 vibe coding tools" thread | Build time: ~3 hours*
