# Vibe Code Trust Score — Blueprint

## What it is

A 10-question self-audit tool for non-technical founders who built their app with AI tools (Lovable, Bolt, Cursor, etc.). Outputs a Trust Score from 1–10 plus a specific list of what to fix before shipping. Takes 3 minutes. No backend, no API, no login. Pure static HTML.

---

## The demand signal that justified it

**Fortune, April 2, 2026:** "In the age of vibe coding, trust is the real bottleneck." The article argues the differentiator in 2026 isn't whether your team uses AI — it's whether you test what AI produces.

**AppSec Santa 2026 study:** 1 in 4 AI-generated code samples contains a confirmed security vulnerability. Testing 534 samples across six major LLMs against OWASP Top 10.

**Armis benchmark, April 2026:** Systemic security gaps in AI-generated code across all leading models.

**The gap:** Every explainer article about vibe coding quality problems targets developers. The founders who built with Lovable/Bolt and can't read code have no accessible way to self-assess before shipping. This fills that gap with plain English.

---

## Exact build steps

Paste this prompt into Claude (claude.ai or any Claude API interface). It will generate the complete working HTML file in one shot.

---

```
Build a single-file HTML tool called "Vibe Code Trust Score". Dark background (#0a0a0e), green accent (#22c55e). No external dependencies.

The tool is a 10-question self-audit for founders who built their app with AI tools (Lovable, Bolt, Cursor, etc.). Each question has 3–4 options. Every option is pre-tagged with a visible risk label shown BEFORE the user picks: "✓ OK" (green), "⚠ Risk" (amber), or "✗ Flag" (red). This is important — the risk label is visible upfront, not revealed after.

Scoring: safe = 2 pts, warn = 1 pt, bad = 0 pts. Max score = questions × 2. Normalize to 1–10.

The 10 questions and their options:

Q1: How was this app primarily built?
- Lovable, Bolt, or similar full-stack AI builder [warn] → issue: "AI-builder apps often have untested edge cases. Auth and payment flows need manual verification."
- Cursor, Windsurf, or vibe coding IDE with my own review [safe]
- Claude/ChatGPT prompts pasted directly into files [bad] → issue: "Directly pasted AI output without review is the highest-risk pattern. Logic errors and missed edge cases are common."
- Mostly written by hand, AI-assisted [safe]

Q2: Does it process payments?
- No payments at all [safe]
- Yes — Stripe handles everything [warn] → issue: "Stripe webhook handling is the most common failure point in AI-built apps. Verify failed payment, refund, and cancellation flows."
- Yes — multiple payment providers or custom billing [bad] → issue: "Multi-provider payment logic built by AI has a high error rate on edge cases. Get this reviewed before real volume."

Q3: What user data do you store?
- Nothing — fully anonymous [safe]
- Email address only [safe]
- Name, usage data, preferences [warn] → issue: "User profile data requires a privacy policy and a clear deletion path. Make sure both exist before launch."
- Health, financial, or other sensitive data [bad] → issue: "Sensitive data in an AI-built app without a security review is high risk. Do not launch to real users without an external audit."

Q4: Are API keys and secrets stored properly?
- I'm not sure / I haven't checked [bad] → issue: "Check this before anything else. Search your codebase for strings that look like API keys. Hardcoded secrets are the #1 cause of data breaches in AI-built apps."
- Some might be in the code, some in env vars [warn] → issue: "Inconsistent secret management is risky. Move all keys to environment variables and rotate anything that was ever in the codebase."
- All in environment variables, nothing hardcoded [safe]
- Using a proper secrets manager [safe]

Q5: Has anyone tried to break it?
- I've only tested the main flow [bad] → issue: "Untested failure paths are where real damage happens. Test at minimum: bad inputs, failed auth, failed payments, and slow/no network."
- I've manually tested edge cases [warn] → issue: "Self-testing catches some issues. Consider asking a technical friend to try to break it before you market it."
- External person tested it [safe]
- Proper QA or bug bounty in place [safe]

Q6: Is there error monitoring?
- No — I'd find out when a user complains [bad] → issue: "Set up Sentry (free tier) before launch. Knowing about errors the moment they happen vs finding out from a bad review is the difference between fixable and reputation damage."
- I check logs manually sometimes [warn] → issue: "Manual log checks miss most errors. Add Sentry or a similar tool. Takes 15 minutes."
- Sentry or similar monitoring in place [safe]

Q7: What happens when your app is down or broken?
- There's no way for users to contact me [bad] → issue: "Add a visible contact email before launch. Users who can't reach you leave a bad review instead."
- There's an email on the site [warn] → issue: "An email is fine for now. A status page builds trust as you grow."
- Support email + I'm reachable within a few hours [safe]

Q8: Is there rate limiting on public endpoints?
- Not applicable — no public endpoints [safe]
- I don't know / probably not [bad] → issue: "Unprotected endpoints can be abused to run up your API bills or spam your database. Lovable/Bolt apps often leave this unprotected. Check with your platform."
- Yes — rate limiting is in place [safe]

Q9: Have you tested what happens when a payment fails?
- No payments — doesn't apply [safe]
- No — only tested successful payments [bad] → issue: "Use Stripe's test card 4000000000000002 to simulate a declined payment. Verify the user sees the right message and their account isn't left in a broken state."
- Yes — failed payments show a useful error [warn] → issue: "Good. Also verify subscription cancellation and refund flows before going beyond 10 paying customers."
- Yes — including cancellations and refunds [safe]

Q10: Who else has used this app?
- Just me [bad] → issue: "Share it with 3 people before launch. Watch how they use it — where they get confused is where real users will churn."
- A friend or two tried it [warn] → issue: "Good start. Watch someone unfamiliar use it without help — that session surfaces more issues than hours of solo testing."
- 5+ people outside my immediate circle [safe]
- Beta users are already using it regularly [safe]

Results logic:
- Score 8–10: "Ship-ready" — green — verdict: "You're doing the basics right. Launch to a small group first, watch what breaks, fix it, then open it up."
- Score 5–7: "Soft launch only" — amber — verdict: "Share with 10–20 people you trust before any public announcement. Fix the flagged items below first."
- Score 1–4: "Not ready" — red — verdict: "Don't market this yet. Fix the specific things listed below, in order."

After results, show all flagged issues (from non-safe answers) as a list with red/amber dots. Red dot for bad answers, amber for warn.

Add a share button that copies the current page URL with ?score=X appended. Use a textarea-based clipboard fallback so it works on file:// (not just HTTPS):
- If navigator.clipboard and window.isSecureContext: use navigator.clipboard.writeText
- Otherwise: create a hidden textarea, select it, execCommand('copy'), remove it

When the page loads with ?score=X in the URL, show a simplified result view with that score and a "Run your own audit" button that restarts the quiz.

Add a footer note: "Based on the AppSec Santa 2026 study finding 1 in 4 AI-generated code samples contains a confirmed security vulnerability. This is a self-assessment — not a substitute for a professional security review."

Progress bar at top fills as questions are answered. Smooth fade-up animation on each question. Mobile responsive.
```

---

Paste that, get a working file. Total build time from prompt to deployed: under 30 minutes if you drag-drop to Vercel immediately after.

---

## Monetization path

**Immediate:** Free tool drives awareness. The CTA at the bottom is "share your score" — viral loop among builders.

**Near-term:** When a founder scores 1–4, add a CTA: "Book a 1-hour vibe code audit — $99." This is a productized consultation. The tool pre-qualifies the customer (they know they have problems, they've listed them).

**Longer-term:** Bundle of services: Trust Score (free) → Audit Call ($99) → Fix Engagement ($500–2000 depending on complexity). The free tool is the top of the funnel.

**Alternative:** A $9/month "Trust Score Pro" version that generates a downloadable PDF report formatted for enterprise vendor security questionnaires. The non-technical founder who's about to sell to a hospital or bank will pay for this.

---

## What to do differently next time

- Add a mailto CTA on low scores immediately (book audit) rather than just "share your score"
- Consider a second tier with 5 additional questions that go deeper into GDPR and SOC 2 compliance — those are the real enterprise blockers
- The "skip" UX pattern on the shared link view could drive more conversion: show the score, then require audit completion to unlock the full issue list

---

## Steal this

**The formula:** Take a topic where non-technical people have real risk but can't read technical documentation → translate that risk into 10 plain-English questions with visible risk labels → show a score + specific fixes. The score is shareable (social proof). The fixes are specific (utility). The failure state creates a service opportunity.

Works for: Lovable app security, SaaS pricing sanity-check, cold email deliverability, landing page conversion readiness, team hiring process audit.

The key is making the risk labels visible *before* the user picks an option (not after). Seeing "✗ Flag" next to an option they know describes them creates cognitive dissonance that makes the issue memorable.
