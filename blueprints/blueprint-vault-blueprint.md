# Blueprint Vault — Blueprint

**What it is:** A one-page site that packages 12 existing build blueprints behind a $9 lifetime paywall, with one blueprint fully unlocked as the free preview. A single-file HTML landing page with a Stripe Payment Link CTA, an email capture for the free tier, locked content rendered with a blur + overlay pattern, and a social-proof bar showing the shipped count.

No backend. The "paywall" is purely presentational — the content is gated by rendering locked sections blurred, and the real delivery happens after Stripe checkout via a download link in the confirmation email.

---

## The demand signal

Build-in-public accounts on X have been growing audiences for two years but struggling to monetize the audience. The pattern most people run: ship cool stuff → grow followers → never charge anyone → burn out.

The tight constraint: a builder has already produced the asset. Blueprints, templates, SKILL.md files, landing page patterns — these already exist as by-products of shipping. Turning them into a bundle is marginal cost ≈ zero.

What's missing is the packaging layer. Notion docs don't convert. Gumroad pages look the same as everyone else's. A custom landing page that treats the blueprints like a product — not a portfolio artifact — is the gap.

Signal source: this project itself. Five consecutive days of ⭐ 1 ratings on build outputs forced the question "what would someone actually pay for?" The answer was: not more calculators, not more AI graders. The asset that already exists — the blueprints themselves — is what survives the "would someone pay for this?" test. That's what went into the vault.

---

## Exact build steps

1. **Single-file HTML landing page.** No framework. No build step. Deploys to Vercel via drag-and-drop.

2. **Section layout (top to bottom):**
   - Sticky header with logo + pricing CTA
   - Hero with headline, subhead, two CTAs ("Unlock" + "Read the free one"), trust line, proof bar (4 stats)
   - Vault grid — 12 cards, 1 free (fully expanded), 11 locked
   - Pricing card ($9, features list, Stripe button)
   - Email capture for the free tier
   - FAQ (5 common objections)
   - Footer

3. **Lock pattern.** Each locked card shows: title + one-liner (visible) + meta chips (visible) + a 140px-tall preview section where content is rendered with `filter: blur(6px)` + opacity 0.5. On top: a gradient fade to surface color + a centered button that says "🔓 Unlock all 12 — $9" linking to `#pricing`. The blur is purely cosmetic — the real content isn't on this page at all.

4. **Free preview content.** One card is rendered fully open with the complete blueprint text: demand signal, exact build steps, monetization path, and "steal this" variations. This is the proof the other 11 are equally detailed. Pick the blueprint that's most representative of what buyers would value — ideally one with a clear demand signal and a monetization angle that isn't obvious.

5. **Stripe Payment Link.** Create a one-time $9 product in Stripe Dashboard → Payment Links. Toggle "Collect email." Under "After payment" set redirect to a thank-you page that has the blueprint download link (or host blueprints as markdown files in a private GitHub Gist and email the link via Stripe's automated receipt customization).

6. **Email capture (free tier).** Form posts to an email service or, as a placeholder, writes to localStorage. The real hookup happens later — ConvertKit, Buttondown, or just Loops.so. Show a green success message on submit.

7. **FAQ as disclosure widget.** Accordion pattern: `.faq-item.open` class toggled on click. No JS library — just `classList.toggle('open')`. FAQ questions should address: who this is for, commercial use rights, why only $9, delivery mechanism, refund policy.

8. **Proof bar.** Four tiles in a CSS grid: blueprint count, apps shipped, days building, price. Uses accent color for numbers, muted text for labels. Stacks to 2×2 on mobile.

9. **Responsive everywhere.** Mobile: hero padding reduces, card flex wraps, price card goes full width, proof bar collapses to 2 columns.

10. **Animation restraint.** Just one: a pulsing dot in the hero badge (CSS `@keyframes pulse`). No scroll reveals, no parallax, no sliders. Price-card gets a subtle gradient-border treatment using the CSS `mask-composite: exclude` trick for a premium feel.

---

## Monetization path

**The core sale.** $9 one-time for all 12 blueprints. Conversion target: 2-3% of landing page visitors. At 1,000 visits/month, that's ~$180-270. Not life-changing. It's validation.

**Price ladder plan.**
- First 100 buyers: $9 (founder pricing)
- Next 400: $19
- After 500: $29 or move to $9/month with access to all new blueprints

**Email list compound.** The free tier grows a list of builders who aren't ready to buy. Ship 1 new blueprint per month to the list with a soft pitch at the end ("see the other 12 here"). Over 6 months a list of 1,000+ builders becomes the actual asset.

**Upsell tier — Blueprint Vault Pro ($49).**
- The 12 blueprints + a "build-along" Loom video for each one walking through the decisions
- Voice notes on what went wrong and what I'd change
- Access to a private Discord/Slack for buyers
- This tier doesn't exist yet — ship the $9 first, validate, then build the $49 layer

**B2B angle ($299+).** Teams running internal "hack weeks" or indie studios want inspiration + structure. A team license unlocks the vault for up to 10 people. No product changes needed — just a different Stripe product and a license note.

**Distribution tactic.** Post the free blueprint directly on Hacker News ("Show HN: Repo Decoder — a pattern for non-technical founders to parse GitHub repos"). The free blueprint is the lead magnet. If someone reads it and likes it, the vault link is at the bottom.

---

## Gotchas and what to do differently next time

- **Stripe Payment Link is placeholder.** The initial deploy ships with `href="https://buy.stripe.com/REPLACE_ME"`. The real Stripe setup (product creation, redirect URL, webhook for delivery) is a 10-minute task after launch. Don't let it block publishing.

- **The blur pattern is a trust signal, not real protection.** Anyone can disable CSS in devtools and read the blurred text. But — and this matters — the blurred text is intentionally a short generic summary, not the actual blueprint. The full blueprint lives in a GitHub Gist or Notion doc accessed only via the post-payment email. Don't put real content on the public page even blurred.

- **Free blueprint needs to carry the vault.** It has to be good enough that readers believe the other 11 are equally detailed. If the free one feels thin, conversion tanks. Pick the blueprint with the clearest "steal this" variations section — that's what proves the vault's value.

- **Social proof is thin at launch.** The proof bar says "12 blueprints · 27 apps shipped · 30 days building · $9" — no testimonials. That's honest for day 1. Week 2, add a live tweet embed of the first buyer + a metric ("18 builders bought in week one"). Week 4, add a named testimonial if someone writes in unprompted.

- **The FAQ handles the $9 objection head-on.** "Why only $9?" is there because it's the question skeptical buyers ask first. Answering it preempts the doubt. Same for "what if I don't like them?" — the refund is so cheap it removes friction entirely.

- **Email capture without a real backend = lost leads.** The localStorage placeholder is fine for day 1 but leaves money on the table. Wire up ConvertKit or Buttondown in week 1. Don't let "I'll add it later" become "I forgot."

- **Don't gate more than you should.** The locked content blur pattern is a trust exercise. If it feels spammy or over-the-top (full-page blurs, aggressive CTAs popping up), it breaks the product's vibe. Restrained gating = more trust = more conversions.

---

## Steal this pattern

**The formula:** existing content asset + product landing page + cheap paywall.

Works anywhere there's a by-product of shipping that someone would pay a small amount to access without searching for it:

- **Course notes** — every creator has scattered docs. Bundle them, put a $9 gate on, ship.
- **Spreadsheet templates** — financial models, hiring plans, OKR sheets. $9 for the bundle.
- **Newsletter archives** — paywalled back-catalog of a free newsletter. Search + filter as the real value-add.
- **Prompt library** — 50 prompts that work for a specific niche (marketing, customer research, sales ops). $9.
- **Design assets** — social post templates, pitch deck frames, email signatures. $9.
- **Lessons learned** — "Things I wish I knew when starting [X]" as a structured PDF. $9.

The move: take something that already exists, wrap it in a product-grade landing page, let the landing page carry the perceived value. Most builders underprice their by-products because they've spent so much time with them they've lost the ability to see what they're worth.

$9 is the price where buying requires zero thought. That's the point.
