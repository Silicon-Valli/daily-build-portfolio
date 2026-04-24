# Compute Dividend Pricing — a protocol for AI that doesn't burn itself alive

**Date:** Apr 24, 2026
**Status:** Open spec, v0.1

---

## The thing that keeps happening

Sora shuts down on April 26, 2026. Public record: around $15M/day in compute at peak, roughly $2.1M lifetime revenue. The math was never going to close.

This isn't a Sora story. It's the default shape of an AI consumer product in 2026:

- Flat monthly fee (or free tier subsidized by hope).
- Compute cost per user is invisible to the user.
- Heavy users burn the economics. Light users subsidize them. Nobody is happy when the shutdown email arrives.

Stripe, Linear, Notion all priced per seat or per action. Those units map cleanly to value. "Infinite video generation" doesn't map to anything. Neither does "unlimited agent runs."

## The spec: Compute Dividend Pricing

A user-facing pricing object that every AI product can publish. Three fields, no fine print.

```json
{
  "product": "forms-50-runner",
  "period": "2026-04",
  "user_id": "sha256:...",
  "compute": {
    "input_tokens": 182430,
    "output_tokens": 64210,
    "tool_calls": 117,
    "gpu_seconds": 0,
    "raw_cost_usd": 2.38
  },
  "price": {
    "charged_usd": 4.00,
    "margin_usd": 1.62,
    "margin_pct": 40.5
  },
  "dividend": {
    "returned_usd": 0.00,
    "rule": "if monthly margin > 60%, return 50% of overage to user as credit"
  }
}
```

Three things it forces:

1. **Raw cost is visible.** The user sees what their usage actually cost the provider. Not a fake "credits" currency — real dollars.
2. **Margin is visible.** You know what you're paying for the compute vs. paying for the company.
3. **Dividend rule is a constraint.** If the company makes too much margin on you in a period, you get credit back. Aligns the provider's incentive with yours: if they make you more efficient, both sides win.

## Why this beats what exists

- **"Usage-based pricing"** (what OpenAI does for API): transparent cost, but no margin disclosure, no cap on how much you can burn in a bad prompt.
- **"Unlimited tier"** (what ChatGPT Plus did until it couldn't): hides the cost, works until it doesn't, then breaks trust loudly.
- **"Credits"** (what most AI SaaS does): arbitrary exchange rate, changes without notice, never converts back to dollars.

Compute Dividend Pricing is the only model where a user can look at the bill and know whether they're being gouged.

## The 48h demand signal

- Sora shutdown announcement (public): April 26, 2026. Thread traffic spiking on X around "why do AI products keep dying after launch."
- Humane AI Pin returned in waves through Q1 2026 — same pattern.
- Rabbit R1 — same.
- Developer discourse on Hacker News this week: recurring theme is "I can't tell what my agent runs cost." That's the product gap.

## How a provider implements it in an afternoon

1. Meter input tokens, output tokens, and tool calls per user per month. (If you're on Anthropic/OpenAI/etc., these are already in the response.)
2. Multiply by posted per-unit costs. That's raw cost.
3. Subtract from what you charged. That's margin.
4. Set a dividend threshold (suggestion: 60% margin triggers a 50% rebate of the overage).
5. Publish the JSON at `/pricing/{user_id}.json`. Link it from settings.

Total work: a day. The hard part isn't the code — it's deciding to show the number.

## Who would adopt this first

Small AI SaaS products that want trust as a wedge against incumbents. If you're competing with ChatGPT, Cursor, or Perplexity, you can't win on model quality. You can win on "we will never burn your money behind a black box."

## How someone monetizes the spec itself

- A hosted meter: you point your product at it, it computes and publishes the JSON. $19/mo per product.
- A badge: "Compute Dividend Pricing ✓" — small SaaS products display it the way they display SOC 2.
- An audit API: users can verify their bill against the published spec. Free for users, paid for providers.

## Gotchas

- **Margin is not the same as profit.** Raw compute cost excludes payroll, R&D, customer support. Providers need a column for "other operating costs" or this reads as gouging when it isn't.
- **Tool calls vary in cost.** A GPT-4 call and a GPT-nano call look the same in JSON; the spec needs per-model cost breakdown or it misleads.
- **Dividend rule is the hardest part.** If the threshold is too tight, providers can't invest. If too loose, it's cosmetic. 60%/50% is a starting anchor, not a rule.

## What I'd test first

Fork one existing AI SaaS (any small one with API access) and build a Compute Dividend dashboard for it. Publish the dashboard as a third-party site. If users start forwarding it to each other, the spec has legs. If nobody shares it, nobody wanted transparency enough to switch.

## Why this is actually surprising

Every pricing post-mortem after Sora/Humane/Rabbit says "they should have charged more." Nobody says "they should have shown users exactly what they were burning and made them a partner in the economics." That's the gap.

The weird thing is this doesn't require regulation. It just requires one provider to publish the JSON first and the rest look ugly by comparison.

---

**Distribution:** This spec, the forms-50 benchmark, and the saas-graveyard page are three ways of asking the same question: where does "agentic AI" actually lose money, and can we price it honestly? The engine will revisit this after one provider ships a version.
