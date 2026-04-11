# Skills Index — Blueprint

## What it is

A browsable, curated directory of the best skills, system prompts, and workflows for Claude Code, Cursor, and AI coding agents. 20 real, copyable skills across 6 categories. Works fully in the browser with no backend, no API calls, no accounts. Search, filter by framework and category, copy a skill in one click, submit your own.

The product insight: there are now hundreds of thousands of people using Claude Code, Cursor, and similar agentic frameworks. Almost all of them write their own system prompts from scratch, every time. There's no central, curated place to find the best ones. Skills Index is that place.

## The demand signal that justified it

On April 9, 2026, three GitHub repos were trending simultaneously — all representing the same pattern:

- **obra/superpowers**: 141,921 stars, 2,028 stars added today. An agentic skills framework for Claude Code. Skills activate automatically, guiding agents through structured workflows (design → plan → TDD → review → branch).
- **forrestchang/andrej-karpathy-skills**: 9,230 stars, 702 today. Educational AI skill collection.
- **TheCraigHewitt/seomachine**: 4,713 stars, 649 today. A specialized Claude workspace for SEO.

Three repos. Same day. Same pattern: skill files for AI coding agents are a distributable product category. The aggregation layer — a curated index — doesn't exist yet.

## Exact build steps

1. Create a single HTML file. No framework, no build step, no dependencies.
2. Store all skills as a JavaScript array of objects with: `id`, `name`, `framework` (claude/cursor/both), `cat` (coding/writing/research/marketing/ops/data), `stars`, `trending`, `desc`, `tags`, `source` URL, `prompt`.
3. Render cards dynamically from the array. Each card shows: framework badge, category badge, star count, trending indicator, description, tags, copy button, source link.
4. Filter system: framework pills (All / Claude Code / Cursor / Universal / Trending) + category sidebar buttons. All client-side.
5. Search: simple `includes()` across name, description, and tags on every keystroke.
6. Copy button: `navigator.clipboard.writeText(skill.prompt)` — works in any modern browser.
7. Submit form: captures name, framework, category, prompt text, GitHub source, email. No backend — the form acknowledges submission without actually sending (hook up Formspree or similar for $0).
8. Email capture: same pattern — validate format, show success state.
9. Deploy as a single file to Vercel (drag-and-drop, 2 minutes).

Pre-populate with at least 15 real skills. Prioritize skills that:
- Are grounded in real, trending repos (direct credibility)
- Solve problems that come up in every project (code review, PR description, TDD)
- Work with both frameworks (broadest audience)

## Monetization path

**Immediate**: Email capture list. Skills Index becomes a weekly newsletter ("5 new skills indexed this week"). Build the list, then monetize the list.

**Short-term**: "Submit and get listed" for teams. A team at a company wants their Cursor rules to be the standard used across the org — they submit, we curate, they get a branded listing. $29/month for a verified team skill.

**Medium-term**: "Skills Pack" downloads. $9 one-time for a curated .cursorrules pack for specific stacks (Next.js + TypeScript + shadcn, Django + Postgres, etc.). Static files, pure margin.

**Longer-term**: The index becomes a search-indexed destination for "best Claude Code skills for X" queries. Affiliate or sponsored listing model once traffic exists.

## What to do differently next time

- Start with 5–7 skills, not 20. More skills means longer load and harder curation. Prove quality before quantity.
- Add shareable URLs for individual skills immediately. `?skill=5` loads with that card highlighted — every copy becomes a distribution event.
- Add a "last updated" timestamp per skill. Freshness matters — Claude Code and Cursor update frequently, and stale prompts lose credibility fast.
- Build the GitHub Awesome list in parallel. A `awesome-claude-skills` repo on GitHub captures organic search traffic that the HTML page won't.

## Steal this

The formula: **trending distribution channel + missing aggregation layer = first-mover directory product.**

Every new platform that enables user-generated content (skills, workflows, extensions, templates) eventually needs a curated index. The window to be that index is roughly 6–18 months after the platform hits critical mass. After that, the platform builds it themselves or a VC-funded startup does.

Apply this to:
- Windsurf rules directory (Windsurf is growing fast, no curated rules hub)
- n8n workflow library (n8n has templates but curation is poor)
- Lovable prompt library (millions of Lovable users, no indexed prompt collection)
- MCP server directory (thousands of MCPs, discovery is a mess)
- Dify workflow index (same pattern, growing fast in Asia)

Same build: single HTML file, curated content array, copy button, submit form, email capture. Different domain, different audience, same monetization path.
