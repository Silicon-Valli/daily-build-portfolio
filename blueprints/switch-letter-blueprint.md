# Switch Letter — Blueprint

A single-page tool that helps people write polished announcements when they leave an AI subscription. Pick the tool you're leaving, the alternative you're moving to, the audience (X, Slack, email, README, LinkedIn, blog), and the tone (professional / direct / spicy). Get back a 2–3 paragraph announcement, ready to copy. Free; $9 forever-license unlocks 200+ pre-written templates and a follow-up generator.

## What it is

One HTML file. No backend. No API calls. All template selection happens deterministically in the browser based on the user's picks. The "AI" piece is fake — it's a curated template library with smart variable substitution. The user thinks they're getting AI; they're getting better-than-AI: a hand-crafted message that says exactly what they meant.

Distribution mechanic: every generated letter has a "Tweet this" button and a share-link encoder. Each share is free promo for the tool.

## The demand signal

Three things hit the same week (Apr 22–26, 2026):

1. **Anthropic A/B-tested a $100/mo Claude Code paywall** for ~2% of new prosumers. HN: 402 points, 413 comments. Indie builders openly migrated to Cursor, Codex CLI, OpenCode + GLM-5.1.
2. **Sora shut down** (Apr 26). Disney's $1B partnership collapsed. Users had days to migrate prompts and content.
3. **DeepSeek V4 launched** (Apr 24) at ~10x lower output token cost than Claude Opus, with comparable code quality.

Result: thousands of indie builders, teams, and solo devs are leaving AI subscriptions this week. They have to explain it — to their team, their customers, their followers, their boss. Most don't write the post because it's awkward and time-consuming. The market for "nice cancel-and-switch announcement" is real, niche, and timed.

## Build steps

### Single HTML file (~700 lines)

Five inputs, all client-side:

1. **From tool dropdown** — Claude Code, Cursor, ChatGPT Plus, GitHub Copilot, Sora, Midjourney, Runway, Other
2. **To tool dropdown** — OpenCode + GLM-5.1, Codex CLI, Aider, Cursor, Claude Pro (downgrade), Gemini Pro, DeepSeek, Local model, Still deciding, Other
3. **Reason pills** — Pricing change, Deprecated, Cost-cut alternative, Quality gap, Reliability, Privacy, Vendor trust
4. **Audience pills** — X / Twitter, Slack, Customer email, README, LinkedIn, Blog
5. **Tone pills** — Professional, Direct, Spicy

Plus three personalization inputs: name, monthly spend, switch date.

### Template engine

Two lookup tables:

- `TEMPLATES[audience::tone]` — array of 1–2 variants per combination. Each variant uses `{{from}}`, `{{to}}`, `{{reasonClause}}`, `{{name}}`, `{{spend}}`/`{{spendClause}}`, `{{date}}`.
- `REASON_CLAUSE[reason][fromKey]` — context-specific phrasing for the reason. E.g. for `pricing × claude-code`, return "a quiet pricing test that pushed the entry tier from $20 to $100/mo"; for `deprecated × sora`, "the discontinuation announcement (web/app shut down April 26)".

Generation is deterministic substitution, not AI. The same inputs always produce the same letter — which is part of the trust play. You can re-generate after editing inputs and get the same result.

### Reroll button

Each `audience::tone` slot has multiple variants. The "Try a variant" button cycles through them. This makes the tool feel responsive without requiring an LLM call.

### Share URL

Inputs are encoded as JSON, base64-encoded, appended as `?s=<payload>`. Loading the URL pre-fills the form and auto-generates. Used by the "Copy share link" button. Anyone re-opening the link sees a banner explaining they got it from someone.

### Tweet integration

`https://twitter.com/intent/tweet?text=<letter or summary>&url=<share URL>`. For X audience, the full letter goes in. For other audiences, a short pitch goes in.

### Email capture for Pro

LocalStorage waitlist for the $9 Pro tier. No backend needed for v1.

## Monetization path

**Free tier**: 60+ template variants across 6 audiences × 3 tones × 7 reasons. Enough to cover the most common reshuffles.

**Pro tier ($9 lifetime)**:
- 200+ pre-written templates (board email, investor brief, press statement, vendor reply, migration thread, refund request)
- Follow-up generator: drafts the next message after the first one lands ("they replied with X — what do I send back?")
- Custom-letterhead PDF export
- Stripe Payment Link, no recurring billing

**Why $9 lifetime**: this is a 2026-specific play. Builders are tired of subscriptions. Lifetime licenses are a trust signal. Calibration from VV's portfolio: every recent $9 lifetime tool (Blueprint Vault, FormDraft Pro waitlist) has had email capture activity. The tool itself reinforces the positioning — "we help you leave subscriptions, so we don't subscribe you."

**Longer term**: 
- B2B "team license" at $99 covering all 200 templates + per-seat brand customization
- Affiliate links to alternative tools (OpenCode, Cursor, DeepSeek API) earning ~5% on signup
- Sponsored migration guides ("switching from X to Y? We wrote the playbook")

## What to do differently next time

1. **Test the share URL on day-1 traffic.** The single biggest distribution lever is the tweet button. If the share URL doesn't render correctly on first share, you've burned the launch viral coefficient.

2. **Don't over-engineer the template engine.** v1 should have ~30 strong templates, not 100 mediocre ones. Quality of output matters more than coverage.

3. **The "spicy" tone does the marketing.** Spicy versions are the ones that get screenshotted on Twitter. They're not for everyone but they're the format that travels. Make sure the spicy templates actually slap.

4. **Pre-fill from URL parameters even without share encoding.** Power users want `?from=claude-code&to=cursor&reason=pricing` to just work. Document this.

## Steal this

The formula generalizes to any moment where users have to publicly announce a decision they're slightly anxious about:

- **Cancellation Letters** — leaving a community, ending a contract, quitting a service
- **Hire/Fire announcements** — inverse direction, same emotional stakes
- **Pivot announcements** — "we're changing direction" templates by audience
- **Acquisition announcements** — "we got acquired/we acquired" templates
- **Layoff communications** — empathetic templates, hard problem
- **Roadmap kills** — "we're sunsetting feature X" with templates by user segment
- **Investor updates after bad quarters** — templates that don't lie but don't panic

The pattern: pick the situation, pick the audience, pick the tone, get back a deterministic message with smart variables. The "AI" feeling comes from coverage and quality, not from inference.

The wedge in every case is the same: people don't write the message because the activation energy is too high. Lower the activation energy from 30 minutes to 30 seconds and you have a paying tool.

## File map

```
Claude Cowork/
├── switch-letter.html          ← the tool (this build)
└── blueprints/
    └── switch-letter-blueprint.md   ← this file
```

## How to rebuild from scratch

1. Take the 5 inputs (from, to, reason, audience, tone) + 3 personalizations (name, spend, date).
2. Build a `TEMPLATES` object keyed `audience::tone` with 1–2 string variants each. Each string uses `{{var}}` placeholders.
3. Build a `REASON_CLAUSE` object keyed `reason` → `fromKey` → context-specific phrasing.
4. On generate: look up `TEMPLATES[audience::tone]`, pick a variant, substitute variables, render to a `<pre>` block.
5. Wire up: copy button, tweet button, share-URL encoder/decoder, reroll button, email capture for Pro.
6. Style: dark mode, amber accent, 720px breakpoint for mobile.
7. Ship. Free hosting via Vercel or GitHub Pages.

Total build time from scratch: 3–4 hours. The template-writing is 70% of the time. The code is 30%.
