# Recession Runway Planner — Blueprint

## What it is

A single-page HTML tool that models a startup's cash runway across three recession scenarios — soft landing, 2020-style shock, and 2008-style correction. Unlike generic runway calculators (which draw a straight line from current burn to zero), this one applies documented median SaaS outcomes from real downturns to your numbers: churn multipliers, growth collapses, and burn creep. Output is three colored runway timelines plus a decision-threshold checklist for when to act.

## The demand signal that justified it

April 7, 2026: US markets recorded their largest single-week drop since 2020 following the April 2 global tariff announcement. Founder communities (r/startups, X, IH) flooded with "what do I do with my runway" posts. Existing tools show a straight-line runway number — zero scenario modeling. The gap is founders don't need to know their base runway, they need to know how bad it gets if this is 2008 and not a blip.

Validated by: CB Insights data (38% of startup failures = cash depletion), SaaS Capital Q2 2020 survey (n=1,500+), Bessemer State of the Cloud data on 2008 churn patterns.

## Exact build steps

1. Single HTML file, no backend, no API calls
2. Inputs: current MRR, cash on hand, monthly burn, monthly churn %, monthly MRR growth ($), customer concentration (% from top 3 customers)
3. Scenarios hardcoded:
   - Soft: churnMultiplier 1.3x, growthMultiplier 0.6x, burnMultiplier 1.0x
   - Moderate (2020): churnMultiplier 1.65x, growthMultiplier 0.35x, burnMultiplier 1.05x
   - Hard (2008): churnMultiplier 2.1x, growthMultiplier 0.15x, burnMultiplier 1.08x
4. JS calculates month-by-month MRR decay (churn applied to current MRR each month) until cash hits zero, capped at 60 months
5. Output: 3 scenario cards (color-coded green/yellow/red) + summary box + decision threshold checklist with 3 action thresholds (now, 12 months, 6 months)
6. Concentration warning: if top 3 customers > 50% of MRR, append additional warning to summary
7. Deploy as static file: vercel.com/new → drag-and-drop

## Monetization path

**Immediate**: Free tool with no email gate. Goal is shares and inbound. Founders share calculator results screenshots — built-in viral loop.

**Near-term**: Add email capture after results are shown: "Get a weekly recession scenario update — we'll update the multipliers as new market data comes in." Builds list of founders who self-selected as worried about runway.

**Paid layer**: $19/month "CFO mode" — connects to Stripe or Quickbooks via OAuth to pull actual burn data instead of manual inputs. Updates monthly automatically. This is the paid version: same tool, real data.

## What to do differently next time

The scenario multipliers are static — they don't update. A second build should pull real-time churn data from publicly available SaaS benchmarks (SaaS Capital publishes quarterly). That would justify a recurring subscription.

The concentration warning is binary (>50%). Better: a slider that shows impact of losing the top customer, top 2, all 3. That's the actual question founders are asking.

## Steal this

The formula: **take a generic calculator that draws a straight line → add historically-anchored scenarios → add decision thresholds (not just numbers)**. This works for any domain:

- Ecommerce: "How does your profitability hold across 3 demand scenarios?"
- Hiring: "How long can you maintain headcount across 3 revenue scenarios?"
- Agency: "What does your utilization look like if you lose your top client?"

The key insight is that scenarios + historical anchors turn a calculator from a status check into a decision tool. That's why people share it — it answers "what do I do" not just "where am I."
