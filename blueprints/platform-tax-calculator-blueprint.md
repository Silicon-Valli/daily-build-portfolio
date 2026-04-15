# Platform Tax Calculator — Blueprint

## What it is

A single-file HTML calculator that compares what you actually keep when distributing through Apple App Store, Google Play, or the open web. Input your monthly revenue, app type, and developer size. Get instant breakdowns: platform commissions, payment processing fees, hosting costs, annual comparison table, and a total savings figure for going web-only. Shareable URLs with pre-filled inputs.

## The demand signal

Apple removed the vibe coding app "Anything" from the App Store for the second time on April 14, 2026 (TechCrunch, 9to5Mac, MacRumors all covered it). The Anything team says "the number of people who can build apps is about to go from millions to everyone." Meanwhile, 92% of developers now use AI coding tools daily (Stack Overflow). The question everyone's asking: do I even need the App Store?

The timing: this is a 48-72 hour narrative window. Apple's enforcement story is at peak attention. Every builder reading TechCrunch today is doing the mental math on what the App Store costs them. This calculator does it for them.

## Exact build steps

1. Single HTML file, zero dependencies. Dark mode, mobile-first layout.
2. Input section: monthly revenue (number field), app type (subscription / one-time / IAP / free+ads toggle buttons), developer size (under $1M / over $1M toggle).
3. Three platform comparison cards: Open Web (Stripe 2.9%+$0.30, Vercel free tier, $12/yr domain), Apple (15% small dev / 30% large dev), Google Play (same rate structure).
4. Savings banner: annual difference between web and highest-cost platform.
5. Annual comparison table: gross revenue, platform commission, payment processing, hosting, developer account fees, net revenue. Side-by-side.
6. "The $0 web stack" section: Vercel, Stripe, domain, PWA support, no review process, ship same day, no 30% tax, no removal risk.
7. Share button with Web Share API + clipboard fallback. URL params encode revenue/type/size for shareable links.
8. Context banner citing the Apple/Anything story with TechCrunch link.

## Monetization path

**Immediate:** Email capture for "Get notified when platform fee rates change" (add in iteration 2). The audience that uses this calculator is the exact audience for every other tool in the portfolio.

**Medium-term:** Affiliate partnerships with web deployment platforms (Vercel, Netlify, Railway) and payment processors (Stripe, Lemon Squeezy). The calculator naturally surfaces "here's the cheaper alternative."

**Longer-term:** Expand into a full "Platform Migration Guide" — paid resource ($19-$29) that walks through moving from App Store to web distribution. Legal considerations, PWA setup, payment integration, ASO-to-SEO transition.

## What to do differently next time

The Apple/Anything story has a 48-72 hour window of peak relevance. The calculator should have been built and deployed within hours of the TechCrunch article, not the next day. For time-sensitive builds, the engine should detect the signal and build in the same cycle.

The "free + ads" app type returns $0 in platform fees, which makes the comparison less dramatic. Could add an "effective tax" calculation that accounts for the reduced discoverability premium you pay by being on the App Store.

## Steal this formula

**The pattern:** Find a platform that just made a controversial change or enforcement action → build a calculator that quantifies the cost of staying on that platform vs. alternatives → distribute in the threads where people are already angry.

**Apply it to:** Shopify fee increases (Shopify vs. self-hosted), YouTube monetization changes (YouTube vs. own platform), Twitter/X API pricing (Twitter distribution vs. newsletter), any platform where the "tax" is a growing pain point for creators and builders.

The calculator format works because it makes the abstract (platform fees) concrete (exact dollar amounts). People share their results. The share URL brings traffic. The tool becomes the reference every time the platform debate resurfaces.
