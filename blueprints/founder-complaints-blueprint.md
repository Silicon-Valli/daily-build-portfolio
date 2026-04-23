# Founder Complaints — Live feed of what builders are mad about right now

**Live:** https://daily-build-portfolio.vercel.app/founder-complaints.html
**Repo:** https://github.com/Silicon-Valli/daily-build-portfolio
**Built:** April 23, 2026 · single HTML file, no build step

## What it is

A single-page tool that pulls Reddit JSON for five builder subreddits (r/SideProject, r/Entrepreneur, r/SaaS, r/indiehackers, r/startups), filters posts from the last 24 hours, and classifies them as Wants ("anyone know a tool that…", "looking for", "wish there was") or Pains ("frustrated with", "hate that", "broken"). Top 30 ranked by engagement (upvotes + comments × 2). Filter chips, refresh button, email capture for the weekly digest.

The point: when someone Googles "what should I build," the existing answers are stale frameworks (Trends.vc, Exploding Topics) or paid lists. This is free, live, and shows actual posts you can reply to.

## The demand signal

"Building in Silence" megathreads and "what are you struggling with" weekly threads are perpetual top posts on r/SideProject and r/indiehackers. The behavior already exists — builders complain publicly, other builders look for things to build. The friction is that nobody wants to scroll five subreddits every morning.

Reddit's JSON endpoint is fully public (no auth, no API key) — `https://www.reddit.com/r/[name]/new.json?limit=50` returns clean JSON. The only catch: Reddit blocks browser CORS, so you need a proxy to fetch from a static page.

Q1 2026 saw multiple "AI agents that monitor Reddit" launches (Reddi.ai, ReactionPHP variants). All paid. None of them just give you the list.

## Build steps

1. **Single HTML file.** Dark theme (`#0f0f13` bg, `#ff6b3d` accent). One file under 30KB. No frameworks, no build pipeline.

2. **Subreddit list and patterns at the top of the script.** Five subreddits as a constant. Two regex pattern arrays — `WANT_PATTERNS` ("anyone know a", "looking for a", "wish there was a", "is there a tool", "any good", "recommend a", "alternative to") and `PAIN_PATTERNS` ("frustrated with", "hate that", "broken", "doesn't work", "annoying", "why does", "tired of"). Both case-insensitive.

3. **CORS proxy chain.** Reddit blocks browser CORS. Use `https://corsproxy.io/?` as primary and `https://api.allorigins.win/get?url=` as fallback. Wrap each fetch in a try/catch that walks the proxy list — if one is rate-limited or down, the next one runs.

4. **Fetch + parse loop.** For each subreddit, fetch new.json, parse `data.children`, keep only posts with `created_utc` in the last 24h. For each post, run the title and selftext through both regex arrays. If either pattern hits, classify accordingly. Store: title, subreddit, ups, num_comments, permalink, classification, engagement score (`ups + num_comments * 2`).

5. **Render.** Sort by engagement desc, take top 30. Render as cards: classification chip (Want / Pain), title with permalink, subreddit + age + engagement count. Filter chips at top: All / Wants / Pains.

6. **Refresh button.** Re-runs the whole fetch loop. Button shows a loading spinner while the proxy chain works.

7. **Email capture.** Form at bottom: "Want this every Monday morning? Drop your email." localStorage placeholder; swap for a real backend (Buttondown, ConvertKit, Mailerlite) when it justifies the work.

8. **Mobile responsive.** Cards stack, filter chips wrap, refresh button stays sticky. Text scales to 14px base on small screens.

9. **Deploy to Vercel.** Drop the HTML in the daily-build-portfolio repo, push, Vercel auto-builds.

## How to monetize

The free version is the wedge — five subreddits, last 24h, basic classification. Money lives one tier up:

- **Paid weekly digest.** $5/mo. Pulls from 20 subreddits + Hacker News "Ask HN" + Product Hunt comments + Indie Hackers forum + selected Twitter/X lists. Delivered as an email with the top 50 grouped by theme. Saves the user 30 minutes a Monday.
- **Topic alerts.** $10/mo. Pick keywords ("scheduling," "invoicing," "PM tool") and get pinged the moment a complaint matches. Useful for SaaS founders watching their own competitive space.
- **API access.** $29/mo. JSON feed of classified complaints. Useful for VC associates, accelerator scouts, content writers.
- **Sponsored "Built That" callouts.** Small box that says "Someone built this — here's the link." Charge $99/listing. Founders pay to put their answer in front of a stream of people literally asking for the thing.

Fastest path to first dollar: launch on r/SideProject and r/indiehackers, mention the weekly digest, hand-build the first 10 issues in a Google Doc, charge $5 for the next batch.

## Gotchas discovered during the build

- **Reddit CORS is the entire trick.** Fetching `https://www.reddit.com/r/SaaS/new.json` from a static HTML page returns a CORS error. Don't fight it — use a proxy. corsproxy.io works without rate-limiting up to 100 req/h. allorigins.win is the fallback. If both fail, the user sees a "Reddit's being slow, hit refresh in a minute" message.
- **Rate limits aren't published, but they exist.** Don't try to fetch 30 subreddits in one go. Five is the sweet spot.
- **Regex patterns need to bias toward false positives.** Better to show a few off-topic posts than to miss a real complaint. The user can ignore noise; they can't ignore a missing signal.
- **Engagement score weighting matters.** `ups + comments * 2` because comments mean people are actually engaging, not just hitting upvote. A post with 50 ups and 80 comments is much more valuable than 200 ups and 5 comments.
- **No personal info on the site.** No "built by," no founder name, no Twitter handle. The work speaks for itself.
- **Refresh button is a feature, not a hack.** Builders want to feel the freshness. The act of clicking refresh and watching new posts appear is part of the value.
- **24-hour window beats 7-day window.** A 7-day window dilutes signal — you see posts that already got responses. 24h means everything on the list is still actively unanswered.

## What ships next

- Hacker News "Ask HN" integration (single fetch, no proxy needed — HN allows CORS)
- Product Hunt comment scraping for the last 24h of launches
- "Mark as built" button — when someone replies to a complaint with a tool, the tool gets credited under that complaint
- Topic clustering — group similar complaints so the user sees "5 people want a calendar tool with X" instead of 5 separate posts
- Real email backend — Buttondown free tier handles the first 100 subscribers
