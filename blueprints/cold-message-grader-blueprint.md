# Cold Message Grader — Blueprint

## What it is

A single-page web tool that scores cold outreach messages (emails, DMs, LinkedIn messages) across 8 dimensions and gives specific, actionable fixes. Runs entirely client-side — no API, no signup, no backend. Takes 2 seconds to grade a message.

## The demand signal

The vibe coding backlash hit peak in April 2026. Amazon lost 6.3 million orders from an AI coding mandate gone wrong. "Vibe Coding Is Over" started trending. Builders are pivoting from "ship more" to "sell what you've shipped." The gap: technical builders can build products but can't do outreach. Cold messaging is the #1 distribution skill they're missing.

GTMnow's Cold Email Grader exists but requires signup and uses server-side AI. Indie builders want instant, free, no-friction tools. A client-side grader that works for ALL platforms (not just email) fills a specific hole.

## Exact build steps

1. Single HTML file with embedded CSS and JS. No framework, no build step.
2. Platform selector: Email, LinkedIn, X DM, Reddit, Slack. Each has different optimal word counts and scoring thresholds.
3. Textarea for the message. Character and word count displayed live.
4. 8 scoring dimensions, each 0-100:
   - **Length**: optimal range per platform (email 50-125 words, X DM 15-40, etc.)
   - **Personalization**: detect "you/your" vs "I/my" ratio, specific references, company mentions
   - **Value Proposition**: benefit language, specific numbers, social proof signals
   - **CTA Clarity**: question count (ideal: exactly 1), concrete next steps, weak qualifiers
   - **Spam Risk**: flagged words, ALL CAPS, excessive exclamation marks
   - **Reading Level**: Flesch-Kincaid grade level (sweet spot: grade 5-8)
   - **Opening Line**: weak opener detection vs. specific/personalized hooks
   - **Conciseness**: filler word count, paragraph density
5. Total score with color-coded ring (green/amber/red), verdict text, and "Fix these first" section highlighting the 3 weakest dimensions.
6. Shareable URL: message encoded in base64 URL param. Anyone with the link sees the same graded message.
7. X share button with pre-populated tweet including score.
8. Email capture: "Get weekly outreach teardowns" — converts tool users into an email list.

## Monetization path

**Immediate**: Email capture on the results page. Weekly "outreach teardown" newsletter converts tool users into subscribers. Sponsor slots in the newsletter ($50-200/week once list hits 500+).

**Medium-term**: Premium tier ($9/month) with: message history, team scoring (compare across your sales team), A/B message comparison, industry-specific benchmarks, Chrome extension that grades before you hit send.

**Longer-term**: The grading algorithm becomes an API. Charge per-call for CRM integrations (HubSpot, Pipedrive, Outreach.io). $0.01/grade at enterprise volume.

## What to do differently next time

The scoring algorithm is heuristic-based (regex + word counting). It's good enough for v1 but misses nuance — a well-placed filler word for tone isn't the same as lazy writing. V2 should incorporate a small LLM call for the personalization and value prop dimensions specifically. Keep the rest client-side for speed.

Platform-specific scoring thresholds were estimated from blog posts and outreach guides, not from actual A/B test data. If this gets traction, collect anonymized messages + reply rates from users who opt in, and retrain the thresholds on actual performance data.

## Steal this: the "Score Before You Send" pattern

The formula: take any skill where people are bad at self-assessment (outreach, resumes, landing pages, pitch decks, pricing pages). Build a client-side scorer with 6-10 dimensions. Show a total score + specific fixes. Add a shareable URL so scored results spread.

Why it works: people love quantifying themselves. A score is inherently shareable ("I got 73/100 on my cold email"). The URL with encoded content means every share is also distribution. And the "fix these first" section creates repeat usage — people come back to check their rewrite.

Other applications: Resume Grader, Landing Page Scorer, Pitch Deck Audit, Pricing Page Analyzer, README Scorer, Job Description Grader.
