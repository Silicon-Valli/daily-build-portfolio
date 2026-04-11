# Blueprint: Tariff Margin Calculator

**Built:** Apr 3, 2026
**Time to build:** ~2 hours
**Stack:** Single HTML file — no backend, no framework, no database

---

## What it is

A free web calculator that shows importers and e-commerce founders exactly how US tariff changes hit their unit economics. Enter factory cost, shipping, old and new tariff rates, and target margin. Get: new landed cost, minimum retail price to maintain margin, old vs new gross margin comparison, color-coded verdict, and three price scenarios.

Live CTA captures emails for a supplier alternatives list (Vietnam, Mexico) — that's the monetization seed.

---

## Why this existed on April 3, 2026

US raised tariffs on Chinese imports to 125% on April 2. A $10 product from China now lands at $22.50 before shipping. Every Shopify founder, Amazon seller, and product company was manually running this math in spreadsheets. Search intent for "tariff calculator" and "tariff impact" was live and spiking. The URL you build today gets bookmarked today — not next week.

The demand signal: real, urgent, time-bound. This is not an evergreen idea. It's a news-cycle play. The window is roughly 2–3 weeks while the story is live. After that, it becomes a reference tool with slower SEO-driven traffic.

---

## Exact build steps

**Step 1: Build the file (4 hours or less)**

It's a single HTML file with embedded CSS and JavaScript. No dependencies, no build step.

Inputs: factory/supplier cost, shipping + duties per unit, old tariff %, new tariff %, target gross margin % (slider), current retail price (optional).

Outputs:
- Old landed cost = factory cost × (1 + old tariff %) + shipping
- New landed cost = factory cost × (1 + new tariff %) + shipping
- Tariff cost increase = new tariff amount − old tariff amount
- Minimum retail price = new landed cost ÷ (1 − target margin %)
- Old gross margin = (current price − old landed) ÷ current price
- New gross margin = (current price − new landed) ÷ current price
- Verdict: loss / critically thin (<15%) / manageable / holding — color-coded
- Three price scenarios: absorb (keep current price) / split (50/50) / full pass-through (hit target margin)

Add an email capture CTA at the bottom: "Need supplier alternatives in Vietnam or Mexico? Get notified."

**Step 2: Deploy (2 minutes)**

Drag the HTML file to vercel.com/new. No config needed. Get a live URL.

**Step 3: Post (today, not tomorrow)**

r/ecommerce, r/FulfillmentByAmazon, r/smallbusiness. Template:

> "US-China tariffs hit 125% this week. Built a free calculator to see exactly what it does to your unit margins. [link] — no sign-up, runs in 30 seconds."

Zero pitch. Just utility. These communities have people with this exact problem right now.

Also works as a tweet thread: open with the $10 → $22.50 example, give 3 tactical moves, end with the link.

---

## Monetization path

**Immediate:** Email capture → list of people who need supplier alternatives. That list is worth money to Vietnam/Mexico sourcing brokers. Charge for intros, or affiliate with a sourcing platform.

**Week 2:** Add a "Find supplier alternatives" paid tier ($49 one-time) that generates a short list of verified suppliers by product category. You're doing the research manually at first. Automate if it gets volume.

**Longer term:** The email list becomes an audience for any trade/sourcing-adjacent product. A newsletter, a directory, a paid supplier matching service.

The free calculator is the top of the funnel. The email is the asset.

---

## What to do differently next time

- Seed it faster. The calculator was ready same day the tariff news broke. The post should go up within hours, not days. News-cycle tools decay fast.
- Add a share button. "My margin dropped X% — calculate yours" is shareable. Build the social share copy into the result.
- Build the supplier CTA more specifically. "Vietnam/Mexico supplier alternatives" is vague. A dropdown by product category (electronics, apparel, home goods, etc.) would convert better.

---

## Steal this

The formula generalizes: **news event that changes a number people care about → calculator that does the math for them → email capture for the next step.**

Other versions of this exact play:
- Fed interest rate change → mortgage payment calculator
- Minimum wage increase by state → payroll impact calculator
- Platform fee change (Etsy, Amazon, Shopify) → margin calculator for sellers on that platform
- Currency fluctuation → international contractor pay calculator

Each one is a 4-hour build, a timely post, and an email list. None of them require a backend.
