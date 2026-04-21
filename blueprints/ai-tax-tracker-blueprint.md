# AI Tax Tracker — Build Blueprint

A single-page tool that quantifies how much AI capex is costing normal buyers on consumer hardware. You pick what you're buying (headset, RAM, SSD, GPU, laptop, console, phone), and it shows the AI tax — the dollar gap between today's price and what the same thing cost 12 months ago.

## What it is

A free, single-file HTML tool. No backend. No sign-up. Client-side JavaScript does all the math. Ships as one file, deploys anywhere static.

Users pick a product category, see three tiles (headline "AI tax" number, price a year ago, price today), and get a short plain-language explanation of what's driving the hike. A "copy shareable result" button encourages viral distribution.

## The demand signal this is built on

Three things happening simultaneously in April 2026:

1. Meta raised the Quest 3 price by $100 effective April 19, 2026 — citing "macroeconomic conditions" but every analyst attributed it to the DRAM/NAND crunch from AI buildout.
2. 32GB DDR5 kits that were ~$100 in September 2025 are trading at ~$320-360 right now. That's 3x in six months, and consumers are talking about it on X, r/hardware, r/buildapc, and in tech press headlines daily.
3. $600B+ in 2026 AI capex (Microsoft, Meta, Google, Amazon combined guidance) is the underlying driver — hyperscalers locking up 2026 HBM and DDR5 supply, squeezing consumer allocation.

The conversation online is "why is everything so expensive?" — but nobody's put a clean number on what an individual is paying. That's the gap.

## Exact build steps

1. Create a single `.html` file. No framework.
2. Use CSS custom properties for the dark theme (ink, panel, accent colors).
3. Ship a `const ITEMS = [...]` array at the top of the script. Each item has: id, emoji, label, sub-label, oldPrice, newPrice, driver text. 8 items is the sweet spot — enough variety to feel comprehensive, few enough that the grid stays clean.
4. Render the picker as a CSS grid of cards. Click → sets `selected` id → calls `calc()` and re-renders.
5. `calc()` does the math: applies optional country markup, multiplies by quantity, computes `diff`, `pct`, and picks one of 4 framing strings based on magnitude.
6. Three result tiles: headline "AI tax" (big orange number), old price, new price. Plus a story paragraph below that reads like a sentence, not a data dump.
7. "Copy shareable result" button writes a tweet-sized string to clipboard.
8. Methodology section at the bottom with every price source spelled out. This is where credibility lives — don't skip it.

## How to monetize

Three plausible paths, in order of how fast each can be tested:

1. **Affiliate links on the methodology section.** When you mention specific SKUs (Meta Quest 3, specific RAM kits, SSD models), link them to Amazon with affiliate tags. Non-intrusive. Someone reading methodology is already high-intent.
2. **Email capture with a monthly "AI tax report."** Once a month, send an update: which prices moved, what the new delta is, where the hyperscaler capex is pointing supply next. This builds a list of people who already care about this angle.
3. **Sponsored "timing" advisor.** Partner with price-tracking services (Camelcamelcamel, Slickdeals) — when someone picks an item, offer to notify them when the price drops. Revenue share on conversions.

Don't launch with all three. Launch with just the shareable copy button, watch what people do with it, then pick.

## Gotchas found during the build

- Memory pricing moves weekly. If you ship this and walk away, it's stale in a month. Either commit to a monthly refresh or put a visible "last updated" date so users calibrate.
- Markup % input is there because non-US buyers asked first when I tested the concept. VAT in Europe is 19-25%, import duties in India push some SKUs 40%+, so the same dollar figure lands very differently.
- Tempting to add more categories (cameras, drones, smart home). Resist until you know which of the 8 gets the most clicks. Add two more of the same type, not random new ones.
- The framing paragraph matters more than the numbers. People share the sentence, not the table. Write 4-5 variations tuned to the size of the hit.
- Don't call it "inflation calculator" — that's the wrong frame. "AI tax" is the share-worthy hook. The whole premise falls apart if the name is generic.

## What makes this worth shipping

Every other "AI impact" tool is about using AI — prompt libraries, workflow helpers, model comparisons. Nothing quantifies what AI is costing people who aren't using it. That's the contrarian angle and it's share-native. If someone on X posts "spent $340 on RAM that was $100 last year" there's now a single-page tool they can link to that explains exactly what happened and gives them a number to share.
