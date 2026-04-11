# Blueprint: Skill Builder — AI Skill File Generator

## What it is

A single-page static HTML tool that generates properly structured skill files for Claude Code, obra/superpowers, and Hermes Agent. Users fill in a form — skill name, trigger condition, step-by-step behavior, output format, example, and constraints — and get a ready-to-copy or downloadable .md snippet in their chosen framework format.

No backend. No API calls. No login. Works in any browser, offline.

## The demand signal that justified it

Hermes Agent v0.7.0 ("Resilience Release") shipped April 3, 2026, introducing a self-evolution loop where the agent automatically writes reusable Markdown Skill files to SQLite after each complex task. This landed on GitHub Weekly Trending (week of April 8). Around the same time, obra/superpowers crossed 137,000 installs with Anthropic's official marketplace listing confirmed.

The gap: every obra and Hermes user is creating skill files by hand, guessing the format by reading example files. There's no tool for structured skill creation. The query "how to write a Claude Code skill file" has no good first result. This is the tool that fills that gap.

Secondary signal: this tool connects directly to skills-index.html (already built). Skills Index shows you the best community skills — Skill Builder shows you how to create your own. Two tools, one audience, one click apart.

## Exact build steps

1. Single HTML file with two-column layout: form on left, live preview on right.
2. Form fields: skill name (text), trigger condition (select + text detail), description, steps (textarea), output format, example, constraints.
3. Three framework tabs: CLAUDE.md, obra/superpowers, Hermes Agent. Each generates a different but compatible output format.
4. Live preview updates on every keystroke using vanilla JS — no libraries.
5. Copy button (navigator.clipboard) and Download .md button (Blob URL).
6. Sticky preview panel on desktop, stacked layout on mobile.
7. Email capture section at bottom — "Get the best community-submitted skill files weekly."
8. Footer links back to skills-index.html.

HTML, CSS, JavaScript — no dependencies, no build step, deployable via drag-and-drop at vercel.com/new in under 2 minutes.

## Monetization path

**Immediate:** Email capture. Every person who generates a skill file is someone who would pay for a curated weekly digest of the best community-submitted skill files. The bar is lower than a newsletter — it's "get the files that are working."

**Near-term ($9/month):** Weekly Skill Drops — the 5 most-copied skill files from community submissions, curated, tested, ready to use. Subscribers get formatted, opinionated packs (e.g. "The TDD Pack for Claude Code: 5 skills that enforce test-first workflow").

**Longer-term:** Skill Packs marketplace. Builders who create popular skills can submit them. Verified packs sell at $4–12 each. Skill Builder becomes the creation tool for the marketplace.

**B2B:** Teams standardizing their CLAUDE.md conventions. A "Team Skills" tier where an organization can build a shared library of internal skill files, share them via a private URL, and track which ones their devs are actually using. $49/month per team.

## What to do differently next time

- Add a "Test this skill" section that runs a simulated scenario and shows how the agent would interpret the skill file.
- Include a community gallery of the 10 most-copied skill files — makes the tool stickier and shows new users what good skills look like before they start writing.
- The "Where to use this" section (sidebar) should also include Cursor Rules and Windsurf configuration, which use similar formats. Broadens reach without adding complexity.
- Start with the framework selector visible above the fold — some users will want to pick the framework before filling in anything else.

## Steal this formula

**The pattern:** A category has a standard file format that practitioners create by hand. Most get it wrong or waste time. Build a form that generates the correct format and download it as the real file type.

**Applied elsewhere:**
- n8n workflow template generator: fill in trigger, steps, error handling → download the .json workflow file
- Cursor Rules generator: same form pattern → generates .cursorrules file in the correct format
- GitHub Actions generator: fill in trigger, steps, runners → generates the .yml workflow file
- .gitignore generator (exists, works well — proof the pattern converts)
- Dockerfile generator: fill in base image, ports, environment → generates valid Dockerfile

The formula: practitioners have a standard file → new entrants don't know the format → a generator removes the friction → demand already exists because people are googling the format.
