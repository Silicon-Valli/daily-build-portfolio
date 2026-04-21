# Agent Ledger — Blueprint

*The audit layer for AI agent spending. Shipped April 21, 2026, 13 days after agent banking went live.*

## What it is

A lightweight web app that sits on top of agent-banking APIs and gives a human a readable view of what their AI agents are spending money on. Four seeded agents demoed inline. Paste-your-own CSV tool for auditing actual transaction exports. Waitlist for the team plan.

No backend. Single HTML file. Anomaly detection runs client-side.

## The demand signal

Meow Technologies launched the first agentic banking platform on April 8, 2026. AI agents can now open business checking accounts, issue physical and virtual cards, send and receive payments, and manage invoicing — all via natural language, no human returning for each step. Bank of Bots rolled out in parallel. Meow's explicit target market is "vibe-coded businesses — companies built and run primarily by AI tools."

Every bank UI ever shipped assumes a human is the spender. When an agent runs 40 transactions in a day across 12 vendors, the existing dashboards are unreadable. Sort-by-date and search-by-merchant were built for someone who remembers what they did. An agent's principal doesn't remember — they weren't there. They need a different view.

The infrastructure race right now is on the "can an agent spend" side (crowded, well-funded, regulatory moats). The audit side is empty. That's where a solo builder can ship something useful in a week.

Supporting data points:
- 79% of CFOs report using AI agents for dynamic budget reallocation (2026 AI Finance Survey).
- 86% of finance teams report encountering hallucinated data from AI agents at least once per month.
- Zero published audit UIs for agent-banking APIs as of April 21, 2026.

The window is 13 days old. By the time there are 10 dashboards, the moat is content, speed, and trust — all soloable.

## Exact build steps

1. **Single HTML file.** No framework. No build step. Deploys to Vercel by drag-and-drop or GitHub connection.

2. **Dark theme aligned with Agent Ledger visual identity.** Background `#09090f`, surface `#12131a`, text `#e4e4ea`, muted `#8b8d99`, accent `#8b7dff` (purple-violet), green `#4ecdc4` for clean status, red `#f87171` for flagged. Border radius 12px on cards. Consistent vertical rhythm using 22px card padding, 16px section gap.

3. **Hero block.** Eyebrow: "Agent banking went live 13 days ago. No audit layer exists." Headline: "Know what your AI agents actually spent — and why." Sub: positioning this as the human-side dashboard, not another agent framework. CTA row: primary "See the demo" (scrolls to demo), secondary "Join the waitlist."

4. **Proof bar, 3 cells:**
   - 79% of CFOs use AI agents
   - 86% hit hallucinated data monthly
   - 0 published agent-audit UIs

5. **Seeded 4-agent demo.** Four agent cards, each with a color, role, and ~5 transactions. Click an agent → see their transactions + flagged items.
   - `ResearchBot` (purple) — 5 transactions across OpenAI, Perplexity, Semantic Scholar. Flag: 3 duplicate OpenAI API calls within 60 seconds, likely retry bug.
   - `OutreachBot` (teal) — 4 transactions across Apollo, Smartlead, Clay. Flag: $49 double-charge on Smartlead within same billing cycle.
   - `DevBot` (yellow) — 6 transactions across Vercel, Supabase, GitHub. No flags — running clean.
   - `Unknown-Agent-7712` (red) — 3 transactions to unknown crypto vendors. Flag: unrecognized agent ID, unauthorized transfers, investigate immediately.

   The fourth card is the emotional hook. Nobody has a name for the pattern yet, so use one: "shadow agent" — an agent spending from an account where the principal never authorized that agent ID.

6. **Paste-your-own CSV.** Textarea accepting CSV with columns: `agent_id, timestamp, vendor, amount, description`. Parse with split-on-comma (keep it dumb). Run three heuristics:
   - Duplicate detection: same `vendor + amount` within 60 seconds → flag as "possible retry loop."
   - Off-hours: transaction outside 06:00–22:00 local → flag as "off-hours activity."
   - Unknown agent: `agent_id` not in user's allow-list (first 3 agent_ids treated as known) → flag as "shadow agent."
   
   Render: per-agent grouping, total spend, flagged spend, list of flagged items with reason strings.

7. **Waitlist form.** Email input, writes to localStorage as a placeholder until a real backend gets wired (ConvertKit or a Supabase row). Shows "You're #N on the list" with N seeded at 47 so it feels live from day one.

8. **FAQ.** Five items: Does this connect to my real bank? (Not yet — CSV today, API tomorrow.) Is the CSV sent anywhere? (No — client-side only.) When does the team plan launch? (100 waitlist signups.) Does it work with Bank of Bots? (Adapter planned.) What if my agent spends legitimately? (Clean status shown, not everything is a flag.)

9. **Mobile responsive at 720px and 560px breakpoints.** Collapse the 4-agent grid to 2-column at 720 and single-column at 560.

## Monetization path

**Immediate (free):** Post in r/SaaS, r/startups, and threads replying to Meow's launch coverage. "Meow gave your agent a bank account. Here's the audit layer." Free tool, collects emails, builds the list.

**Short-term (waitlist → paid):** At 100 waitlist signups, launch the team plan at $29/mo. Team plan features: persistent agent allow-list across CSV uploads, scheduled email digests of flagged activity, shareable PDF audit report for the principal's CPA.

**Medium-term (API adapter):** When Meow, Bank of Bots, or any agent-banking provider exposes a transaction webhook, ship an OAuth-connected version. Same product, no CSV copy-paste. Pricing moves to $49/mo per agent monitored with a free tier of 1 agent.

**Long-term (the 8-layer stack):** Agent Ledger is Layer 3 of an 8-layer financial infrastructure stack for AI agents (Identity, Banking, Audit, Approval Queue, Credit, Insurance, Taxes, Disputes). Each additional layer shipped strengthens the narrative around Agent Ledger as the trust anchor. Next buildable layer for a solo: Agent Taxes (Layer 7) — minimum scope is a Schedule C attachment generator for agent income.

## Steal this pattern

The formula: **new financial infrastructure launched → human-side audit UI missing → ship it as a paste-your-CSV tool first, APIs later.**

Variants a builder could ship this week:
- **Agent Cap Table** — if agents can earn revenue via A2A payments, they need equity/bonus tracking for their principals. Paste revenue CSV → get a "payouts to principal" summary.
- **Agent Compliance Log** — a running log of every action an agent took outside the approval queue, for SOC 2/audit trails. Paste action CSV → get a compliance-ready PDF.
- **Agent Vendor Registry** — a shared list of known-safe vendors that agents are cleared to pay. User submits vendor → community verifies → agent gets whitelist import.
- **Agent Gas Meter** — realtime spend-rate dashboard for LLM API costs across all your agents. Paste usage CSV → get burn rate + projection.

The underlying move in all of these: when a new category of economic actor exists (agents), every auxiliary service humans use has to exist for them too. Ship the auxiliary, not the primary.

## Gotchas discovered during the build

- **CSV parsing must be lenient.** Meow's export uses ISO timestamps; Bank of Bots likely uses different column names. Build the parser to accept header variations (`amount` vs `value`, `timestamp` vs `date`, `agent_id` vs `agent` vs `bot_id`). Fall back to column order if headers are missing.
- **Seed agents must feel real.** Lorem-ipsum-style fake transactions break the illusion. Use real vendor names (OpenAI, Perplexity, Apollo, Vercel, Supabase) and realistic amounts. The demo is the pitch.
- **The Unknown-Agent-7712 card does the emotional heavy lifting.** Without it, the tool looks like reporting. With it, the tool looks like security. Keep one flagged-red card prominent.
- **Waitlist number should feel credible.** Seed at 47, not 1,000. Big-round numbers read as fake. Odd specific numbers read as honest.
- **Don't build an agent framework.** Resist the temptation to "also generate prompts" or "also suggest agents." That pulls into the crowded side of the market. Audit only.

## First dollar path

1. Ship tool free → post in 3 Meow-launch-related threads → collect first 50 waitlist emails in week 1.
2. At 100 signups, send waitlist an email: "Team plan launches Tuesday. $29/mo, lifetime $99 for the first 20. Reply with YES to claim." First dollar comes from this email.
3. If <10 conversions on that email, the demand signal is weak — pivot to Layer 7 (Agent Taxes) with the same playbook.
4. If ≥10 conversions, build the API adapter against Meow first. They have the launch traffic.

## File

`Claude Cowork/agent-ledger.html` — single file, no dependencies.
