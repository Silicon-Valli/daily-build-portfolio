# Agent KYA — Open spec for verifying AI agent identity

**Live:** https://daily-build-portfolio.vercel.app/agent-kya.html
**Repo:** https://github.com/Silicon-Valli/daily-build-portfolio
**Built:** April 22, 2026 · single HTML file, no build step

## What it is

A public-domain JSON spec for declaring who an AI agent is, who it works for, what it's allowed to do, and who's accountable when it does something it shouldn't. Think of it as KYC for software that moves money, books trades, sends emails, or signs contracts.

The site itself is the spec doc plus three ready-to-copy sample agents (research, sales, dev) and a list of who should adopt the format and why.

## The demand signal

On April 21, 2026, MetaComp launched StableX KYA — the first commercial Know-Your-Agent framework, integrated with Eclipse, Plume, and Bind. That's the validation. A real company built a paid version, which means the problem is real and the timing is now.

McKinsey's 2026 State of AI report: 78% of execs say they couldn't pass an AI governance audit within 90 days. SOC 2 compliance for "non-human identities" is starting to show up in enterprise procurement checklists. Banks issuing agent-controlled cards (Meow, Bank of Bots) have no shared way to attest that the agent on the other side is the one its principal claims it is.

Every standard wins by being free, open, and adopted before someone forces permission. HTTP, OAuth, OpenTelemetry — same playbook.

## Build steps

1. **Single HTML file.** Dark theme, indigo+teal accent. No build pipeline, no React, no Next.js. The whole site loads from one file under 30KB.

2. **Spec section first.** Eight fields with one-line descriptions: `agent_id`, `principal`, `scope` (allowed actions), `vendor_allowlist`, `limits` (per-txn + daily caps), `escalation` (who to alert), `attestation` (signed by whom), `version`. Show a copy-to-clipboard button next to a code block of the JSON.

3. **Three sample agents.** ResearchBot, OutreachBot, DevBot. Match the agent names from Agent Ledger so the two tools tell the same story.

4. **Adoption paths.** Four cards: solo builders publish their agent KYA on a `/.well-known/kya.json` endpoint; SaaS vendors publish per-customer-agent specs; audit tools (like Agent Ledger) read the spec and flag violations; banks/fintechs require a KYA before issuing an agent card.

5. **FAQ.** Why JSON not YAML. Why open. How is this different from MetaComp's commercial version. What happens if you lie in your spec.

6. **Cross-link.** Footer + adoption section both point to Agent Ledger as the existing audit tool that already reads the format.

7. **Deploy to Vercel.** Static drop. Add to the same monorepo as the rest of the portfolio.

## How to monetize

The spec itself is free forever — that's the point. Money lives in the layer above:

- **Hosted attestation registry.** Charge agent operators to sign and publish their KYA at a stable URL with a verifiable signature chain. Pricing: per agent per month, similar to how SSL cert authorities work.
- **Audit tooling.** The Agent Ledger product reads the spec and charges for the dashboard. Same play as Datadog reading OpenTelemetry — the standard is free, the observability product isn't.
- **Compliance certification.** Sell a "KYA-Verified" badge that enterprises can require in their procurement contracts. The badge fee funds maintenance of the open spec.
- **Bank/fintech partnerships.** Agent banking platforms (Meow, Bank of Bots) need a way to verify agent identity before issuing a card. Partner with one, take a per-card fee.

The fastest path to first dollar: publish the spec, get one or two real adopters (probably a YC company building agents), then sell either the audit tool or the registry service.

## Gotchas discovered during the build

- **Don't position it as competing with MetaComp.** They built a commercial framework; the open spec is the layer below theirs. Frame it as "the open thing MetaComp's product complies with" — that way you're additive, not adversarial.
- **Cross-tool consistency matters.** Both the KYA site and Agent Ledger use the same agent names and same JSON shape. Anyone who looks at both should immediately see they're the same format. That's the flywheel — each tool makes the other more credible.
- **Keep the spec tiny.** Eight fields is enough. Resist the urge to add scope versioning, signature algorithms, attestation chains, etc. on day one. Ship the v1, let real adopters tell you what's missing.
- **No personal info anywhere.** No author names, no organizations, no email addresses. The spec speaks for itself.
- **Sample agents must match the audit tool.** If the sample agents don't pass verification in Agent Ledger, the whole story breaks. Test the integration: paste the sample KYA into Agent Ledger's KYA verifier and confirm it produces a clean pass for the matching seeded transactions.

## What ships next

- A `/.well-known/kya.json` validator endpoint at daily-build-portfolio.vercel.app/agent-kya.html/validate
- A reference implementation in TypeScript (npm package: `@agent-kya/spec`)
- Outreach to MetaComp suggesting their commercial product list which version of the open spec it's compatible with
- A directory at daily-build-portfolio.vercel.app/agent-kya.html/registry where adopters can list themselves
