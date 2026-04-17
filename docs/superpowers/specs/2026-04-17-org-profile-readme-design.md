# Cacheplane Org Profile README — Design

**Date:** 2026-04-17
**Repo:** `cacheplane/.github`
**Output file:** `profile/README.md`

## Goal

Create the public landing page shown on `https://github.com/cacheplane`. Mirror the `cacheplane.ai` product story, surface the one public repo (`angular-agent-framework`), and give enterprise visitors a clear next step (Pilot Program) without turning the profile into a marketing page.

## Audience

Primary: developers landing on the org from the public `angular-agent-framework` repo or from a web search for LangGraph + Angular.

Secondary: enterprise evaluators scanning for maturity signals (clear products, docs link, pilot path).

## Scope

In scope:
- Single file: `profile/README.md` in the `cacheplane/.github` repo.
- Hero, tagline, positioning, products (3), resources, Pilot CTA.

Out of scope:
- Updating the repo's top-level `README.md` (it is not what GitHub renders on the org landing page; leaving it as-is).
- Any changes to `angular-agent-framework`, `dawnai`, or `pretable`.
- Hosted assets on `cacheplane.ai` (none required — hero is the GitHub org avatar).
- Shields.io badges (belong on individual repos, not the org profile).
- Social links (the org has none to advertise at this time).
- Mentions of `dawnai` or `pretable` (private; not part of the public product story on `cacheplane.ai`).

## Structure

Top to bottom:

1. **Hero**
   - Centered HTML block.
   - `<img>` pointing at `https://avatars.githubusercontent.com/u/269322961?s=200&v=4` (the Apple-style plane the org already uses as its avatar), linked to `https://cacheplane.ai`, width ~96px.
   - Centered `<h3>` tagline: *Production-grade LangGraph for enterprise Angular teams.*

2. **Positioning (2–3 sentences)**
   - Names the "last mile" problem (GenAI proofs-of-concept that don't ship).
   - Positions Cacheplane's answer: signal-native primitives, open standards, no lock-in.
   - Does not repeat the site headline verbatim, but echoes its motifs ("last mile", "no vendor lock-in, no black boxes").

3. **Products (3 items)**
   Each item is an H3 with a single-sentence description and a trailing link line.
   - `@cacheplane/angular` — signal-native LangGraph streaming for Angular 20+. Links: public repo (`angular-agent-framework`), npm, docs.
   - `@cacheplane/render` — generative UI on open standards (Vercel json-render, Google A2UI). Link: docs on `cacheplane.ai`. No public repo link.
   - `@cacheplane/chat` — accessible, production-ready chat components for Angular. Link: docs on `cacheplane.ai`. No public repo link.

4. **Resources**
   - Bullet list: Website, Documentation, Pricing, contact email (`hello@cacheplane.ai`).

5. **Pilot CTA**
   - One soft line near the bottom pointing at `https://cacheplane.ai/pilot` (or whatever the canonical pilot URL turns out to be — verified during implementation).

## Style

- Plain GitHub-flavored Markdown.
- One centered `<div>` block for the hero; everything else is pure Markdown.
- Matches the tone of `angular-agent-framework/README.md` (technical, calm, specific).
- No emoji in section headings. No hype language.
- Heading hierarchy: no `#` H1 at the top (GitHub renders the profile without one cleanly), H2 for major sections, H3 for product items.

## Visual assets

- Hero image: `https://avatars.githubusercontent.com/u/269322961?s=200&v=4` — GitHub's own CDN, already the org icon, guaranteed to be the Apple-style plane PNG the org uploaded. No asset to create or host.
- No other images.

## Links to verify during implementation

- `https://cacheplane.ai` — site root (confirmed 200 during brainstorming).
- `https://cacheplane.ai/docs/getting-started`, `https://cacheplane.ai/api-reference`, `https://cacheplane.ai/pricing` — referenced in `angular-agent-framework/README.md`; assume canonical.
- `https://cacheplane.ai/pilot` — referenced here for the Pilot CTA; will probe during implementation and fall back to the bare site root + contact email if it 404s.
- `https://github.com/cacheplane/angular-agent-framework` — confirmed public.
- `https://www.npmjs.com/package/@cacheplane/angular` — referenced in the public repo's README; assume canonical.

## Success criteria

- `profile/README.md` exists and renders correctly on `https://github.com/cacheplane` after merge.
- All outbound links return 200 (probed before committing).
- Tagline, positioning, and three products align with what's on `cacheplane.ai`.
- No broken references to private repos.
- PR is opened against `main`.
