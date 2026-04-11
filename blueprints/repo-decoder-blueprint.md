# Repo Decoder — Blueprint

**What it is:** A browser-based tool that takes any public GitHub repository URL and returns a plain-English breakdown: what the project does, who it's for, key stats (stars, forks, last updated, language), a README excerpt, and a copyable pitch sentence. No backend, no API key, no signup — it calls GitHub's public API directly from the browser.

---

## The demand signal

The vibe coding wave put GitHub at the center of how builders discover tools. But GitHub is built for developers. Non-technical founders, PMs, investors, and product builders constantly encounter repos they can't quickly parse. "What does this actually do?" is a real question that wastes real time.

Additionally: indie builders who want to evaluate a trending repo as a business opportunity — to fork, compete with, or build on top of — need a fast signal layer. Currently that means reading hundreds of lines of README, which most people skip.

The GitHub Trending page gets heavy traffic from builders every day. Making that content digestible is a consistently needed filter.

---

## Exact build steps

1. **Single HTML file** — no build step, no npm install, deploys to Vercel by drag-and-drop.

2. **Input parsing** — extract `owner` and `repo` from any GitHub URL variant using regex: `github.com/([^/]+)/([^/\s?#]+)`. Strip `.git` suffix.

3. **Two parallel API calls** (via `Promise.allSettled` — fail gracefully if either errors):
   - `GET https://api.github.com/repos/{owner}/{repo}` — returns name, description, stars, forks, watchers, language, topics, updated_at, html_url.
   - `GET https://api.github.com/repos/{owner}/{repo}/readme` — returns base64-encoded README content.

4. **README parsing** — decode the base64 content with `atob()`. Strip: code blocks (between ``` markers), Markdown headings (`# ## ###`), image/badge lines (`![`, `[![`), HTML tags, and lines under 30 chars. Take the first 2–3 clean paragraphs and cap at 500 chars.

5. **Audience inference** — run regex patterns against the description + topics string to classify the repo's target users (e.g., `/\bai\b|\bllm\b/` → "AI builders and product teams"). Return up to 3 inferred audience types. Fall back to the repo's primary language if no patterns match.

6. **Render** — four cards: (a) repo header with stats and topic chips, (b) "What it does" with README excerpt, (c) "Who it's for" as labeled chips, (d) a copyable plain-English pitch string.

7. **Copy button** — uses `navigator.clipboard.writeText()` with a brief "✓ Copied" confirmation state. Fallback: `document.createRange()` + `window.getSelection()` for older browsers.

8. **Example links** — preload the input field with popular repos (supabase, langchain, next.js, llama.cpp) so first-time visitors see working output immediately.

9. **Error states** — 404 (repo not found), 403 (rate limited, common after ~60 requests/hour from one IP), and generic network failure. All shown inline, never break the page.

10. **Mobile** — flex input row stacks vertically on small screens. Result cards stay readable at 320px wide.

---

## Monetization path

**Immediate (free):** Deploy, post in r/SideProject and r/vibecoding. "Paste any GitHub URL, get a plain-English breakdown. For non-technical founders." Use it as a distribution tool — people share repo links with their teams using the generated pitch text.

**Short-term:** Add an email capture gate for the "Copy pitch" button after 3 uses per session (localStorage counter). Grow an email list of non-technical founders who regularly evaluate GitHub repos.

**Medium-term:** "Repo Radar" paid tier — a weekly digest of the 10 most-starred repos from the past 7 days, each with the plain-English breakdown auto-generated. $9/month. The audience is: investors, PMs, and founders who want to stay on top of what's building in AI/dev tools without being developers themselves.

**Longer-term:** B2B angle — teams evaluating open-source dependencies for their stack. A "repo audit" for procurement or security teams. "Here's what this library does, who maintains it, how active it is." $49/month per team.

---

## What to do differently next time

- **Pre-populate with fresh data.** The example repos should change weekly to surface trending tools. Either update the HTML manually or add a lightweight "trending" tab that calls the GitHub Trending API (unofficial but stable: `gh-trending.deno.dev/repositories`).

- **Rate limit handling.** GitHub's public API allows 60 requests/hour per IP. For high-traffic scenarios, add a note: "GitHub limits public API requests. If you hit a limit, try again in an hour or sign in." A GitHub OAuth flow could push the limit to 5,000/hour — worth adding if traffic is real.

- **Smarter README parsing.** The current heuristic strips aggressively. A better version would extract the first meaningful `##` section (often "What is this?" or "Overview") rather than just the first N non-empty lines.

- **Structured pitch format options.** Instead of one auto-generated pitch, offer three variants: one-liner (tweet-length), paragraph (LinkedIn), and bullet list (internal Slack message). Same data, three output formats.

---

## Steal this

The formula: **public API + context-stripping + non-technical output.**

The pattern works anywhere there's a data source built for experts that non-experts need to consume:

- **Arxiv Decoder** — paste an arXiv paper URL, get a plain-English breakdown. Same structure, calls arXiv's API.
- **npm Decoder** — paste an npm package URL, get "what this does, who uses it, how healthy it is" without reading the docs.
- **App Store Decoder** — paste an App Store URL, get a competitive analysis framed for non-technical product managers.
- **Patent Decoder** — paste a Google Patents URL, get the core claim in plain English.

Pick any expert-facing repository with a public API, build the context-stripping + re-rendering layer, and you have a tool for the adjacent non-expert audience that's 10x larger.
