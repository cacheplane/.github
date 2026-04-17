# Cacheplane Org Profile README — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ship `profile/README.md` in `cacheplane/.github` so the GitHub org landing page at `https://github.com/cacheplane` presents a clean, product-accurate face.

**Architecture:** One static Markdown file with a single centered HTML `<div>` for the hero (Apple-style plane avatar hosted on GitHub's CDN + tagline). Positioning paragraph, three product sections, resources, and a soft Pilot CTA. No assets to host; all outbound links resolved before commit.

**Tech Stack:** GitHub-flavored Markdown. `curl` for link probing. `gh` CLI for the PR.

**Spec:** `docs/superpowers/specs/2026-04-17-org-profile-readme-design.md`

**Working directory:** `/Users/blove/repos/.github` (already the repo root).

---

## File Structure

- **Create:** `profile/README.md` — the org profile content GitHub renders on the org landing page.
- **Create:** `docs/superpowers/plans/2026-04-17-org-profile-readme-plan.md` — this file.
- **Already in working tree (uncommitted):** `docs/superpowers/specs/2026-04-17-org-profile-readme-design.md` — the approved spec, committed in Task 2.
- **Do not touch:** top-level `README.md` — not what GitHub renders for the org profile; leaving as-is.

---

## Task 1: Create the feature branch

**Files:** None modified yet.

- [ ] **Step 1: Confirm clean starting state on `main`**

Run:
```bash
cd /Users/blove/repos/.github && git status --short && git rev-parse --abbrev-ref HEAD
```

Expected: output lists only the two untracked files under `docs/superpowers/` (the spec and this plan). Branch is `main`.

- [ ] **Step 2: Create and switch to feature branch**

Run:
```bash
git checkout -b org-profile-readme
```

Expected: `Switched to a new branch 'org-profile-readme'`.

---

## Task 2: Commit the design spec and the plan

**Files:**
- Add: `docs/superpowers/specs/2026-04-17-org-profile-readme-design.md`
- Add: `docs/superpowers/plans/2026-04-17-org-profile-readme-plan.md`

- [ ] **Step 1: Stage the spec and plan**

Run:
```bash
git add docs/superpowers/specs/2026-04-17-org-profile-readme-design.md docs/superpowers/plans/2026-04-17-org-profile-readme-plan.md
```

Expected: no output. `git status --short` now shows both files with `A` status.

- [ ] **Step 2: Commit**

Run:
```bash
git commit -m "$(cat <<'EOF'
docs: add org profile README design and plan

Design spec and implementation plan for the Cacheplane GitHub
org profile landing page at https://github.com/cacheplane.
EOF
)"
```

Expected: commit succeeds, summary shows 2 files changed.

---

## Task 3: Probe all outbound URLs

**Files:** None modified. This task decides the final URL set for Task 4.

- [ ] **Step 1: Probe every URL that will appear in the README**

Run:
```bash
for url in \
  https://cacheplane.ai \
  https://cacheplane.ai/docs/getting-started \
  https://cacheplane.ai/docs/render \
  https://cacheplane.ai/docs/chat \
  https://cacheplane.ai/pricing \
  https://cacheplane.ai/pilot \
  https://github.com/cacheplane/angular-agent-framework \
  https://www.npmjs.com/package/@cacheplane/angular \
  'https://avatars.githubusercontent.com/u/269322961?s=200&v=4'; do
  code=$(curl -sSL -o /dev/null -w "%{http_code}" "$url")
  echo "$code  $url"
done
```

Expected: each URL prints a status code. `200` is a pass. Record the output.

- [ ] **Step 2: Decide fallbacks for any non-200 URL**

Apply this substitution table when writing the README in Task 4:

| URL | If non-200, substitute with |
|---|---|
| `https://cacheplane.ai/docs/render` | `https://cacheplane.ai` (drop to site root) |
| `https://cacheplane.ai/docs/chat` | `https://cacheplane.ai` (drop to site root) |
| `https://cacheplane.ai/pilot` | Replace the entire Pilot CTA sentence with: *Evaluating LangGraph on Angular? Email us at [hello@cacheplane.ai](mailto:hello@cacheplane.ai) about the Pilot Program — we'll get your team from proof-of-concept to production in 90 days.* |
| `https://cacheplane.ai/docs/getting-started` | `https://cacheplane.ai` |
| `https://cacheplane.ai/pricing` | Omit the Pricing bullet from Resources |
| `https://www.npmjs.com/package/@cacheplane/angular` | Omit the npm link from the `@cacheplane/angular` product line |
| Any of the last three (angular-agent-framework repo, the avatar, or `cacheplane.ai` root) | **Stop.** These are load-bearing; investigate before continuing. |

Write down each substitution applied (if any) so the PR description can note them.

---

## Task 4: Write `profile/README.md`

**Files:**
- Create: `profile/README.md`

- [ ] **Step 1: Create the `profile/` directory**

Run:
```bash
mkdir -p /Users/blove/repos/.github/profile
```

Expected: no output.

- [ ] **Step 2: Write the file with the exact content below**

Apply any substitutions from Task 3 Step 2 before writing. Otherwise use this content verbatim:

```markdown
<div align="center">
  <a href="https://cacheplane.ai">
    <img src="https://avatars.githubusercontent.com/u/269322961?s=200&v=4" alt="Cacheplane" width="96" height="96" />
  </a>
  <h3>Production-grade LangGraph for enterprise Angular teams.</h3>
</div>

---

Half of enterprise GenAI pilots never reach production. The gap isn't ambition — it's the missing primitives: streaming state that behaves like the rest of your app, UI your agents can actually render, and chat surfaces accessible enough to ship. Cacheplane closes that last mile with signal-native, standards-based libraries for Angular teams building on LangGraph — no vendor lock-in, no black boxes.

## Products

### `@cacheplane/angular`

Signal-native streaming bridge to LangGraph — the Angular 20+ equivalent of `useStream()`. Drop it into a component, bind `messages()` directly in the template, get reactive access to tool calls, interrupts, and thread history.

[Repository](https://github.com/cacheplane/angular-agent-framework) · [npm](https://www.npmjs.com/package/@cacheplane/angular) · [Docs](https://cacheplane.ai/docs/getting-started)

### `@cacheplane/render`

Generative UI on open standards. Your agents render interactive UI through Vercel's json-render and Google's A2UI — one library, no proprietary schema.

[Docs](https://cacheplane.ai/docs/render)

### `@cacheplane/chat`

Accessible, production-ready Angular chat components. The surface enterprise teams keep rebuilding — shipped once, done right.

[Docs](https://cacheplane.ai/docs/chat)

## Resources

- [Website](https://cacheplane.ai)
- [Documentation](https://cacheplane.ai/docs/getting-started)
- [Pricing](https://cacheplane.ai/pricing)
- Contact: [hello@cacheplane.ai](mailto:hello@cacheplane.ai)

---

Evaluating LangGraph on Angular? Our [Pilot Program](https://cacheplane.ai/pilot) gets enterprise teams from proof-of-concept to production in 90 days.
```

Use the Write tool to create `/Users/blove/repos/.github/profile/README.md` with that exact content (after applying any Task 3 substitutions).

- [ ] **Step 3: Verify the file written**

Run:
```bash
wc -l /Users/blove/repos/.github/profile/README.md && head -5 /Users/blove/repos/.github/profile/README.md
```

Expected: line count between 30 and 50; first line is `<div align="center">`.

---

## Task 5: Render-preview the file

**Files:** None modified.

- [ ] **Step 1: Run GitHub's own Markdown renderer against the file**

This uses the public GitHub Markdown API so the preview is identical to how GitHub will render it in production. No auth required for small payloads.

Run:
```bash
jq -Rs '{text: ., mode: "gfm"}' /Users/blove/repos/.github/profile/README.md \
  | curl -sS -X POST -H "Content-Type: application/json" \
      --data @- https://api.github.com/markdown \
  | head -60
```

Expected: well-formed HTML output starting with the centered `<div>`, an `<img>` tag with the GitHub avatars URL, and the `<h3>` tagline. No raw `<` brackets or unparsed Markdown. If the output contains an HTTP error JSON instead, stop and investigate (likely: `jq` not installed, or network issue).

- [ ] **Step 2: Confirm no broken Markdown**

Visual check of the HTML head: the `<h3>` must appear inside the `<div>`, the three product headings must be `<h3>`s, and the `## Products` and `## Resources` lines must be `<h2>`s. If any look wrong, fix the Markdown in `profile/README.md` and re-run Step 1.

---

## Task 6: Commit the README

**Files:**
- Add: `profile/README.md`

- [ ] **Step 1: Stage and review**

Run:
```bash
git add profile/README.md && git diff --cached --stat
```

Expected: exactly one file — `profile/README.md` — shown as added.

- [ ] **Step 2: Commit**

Run:
```bash
git commit -m "$(cat <<'EOF'
docs: add org profile README landing page

Adds profile/README.md so the Cacheplane GitHub org page at
https://github.com/cacheplane shows a tagline, the three
@cacheplane products, and a pilot CTA.

Design: docs/superpowers/specs/2026-04-17-org-profile-readme-design.md
Plan: docs/superpowers/plans/2026-04-17-org-profile-readme-plan.md
EOF
)"
```

Expected: commit succeeds with one file added.

---

## Task 7: Push and open the pull request

**Files:** None modified.

- [ ] **Step 1: Push the branch**

Run:
```bash
git push -u origin org-profile-readme
```

Expected: push succeeds, upstream tracking set.

- [ ] **Step 2: Open the PR against `main`**

Run:
```bash
gh pr create --base main --head org-profile-readme \
  --title "Add org profile README landing page" \
  --body "$(cat <<'EOF'
## Summary

- Adds `profile/README.md`, which GitHub renders on the [cacheplane org landing page](https://github.com/cacheplane).
- Mirrors the `cacheplane.ai` product story: tagline, positioning, three products (`@cacheplane/angular`, `@cacheplane/render`, `@cacheplane/chat`), resources, and a soft Pilot CTA.
- Uses the GitHub-hosted org avatar (`https://avatars.githubusercontent.com/u/269322961?s=200&v=4`) as the hero, so no additional assets are required.
- Design spec and implementation plan committed under `docs/superpowers/`.

## Test plan

- [ ] All outbound links in `profile/README.md` return 200 (probed during Task 3).
- [ ] `profile/README.md` renders correctly via the GitHub Markdown API (`api.github.com/markdown`) during Task 5.
- [ ] After merge, confirm `https://github.com/cacheplane` shows the new landing page with the centered avatar, tagline, and three product sections.
EOF
)"
```

Expected: PR URL printed to stdout.

- [ ] **Step 3: Record the PR URL**

Note the URL in the final response to the user so they can click through.

---

## Self-Review

**Spec coverage:**
- Goal (publish org landing page) → Tasks 4 + 6 + 7.
- Audience (devs + enterprise) → README has both a dev-facing product list and an enterprise Pilot CTA.
- Structure (hero, positioning, 3 products, resources, Pilot CTA) → all present in Task 4 Step 2.
- Style (no H1, centered hero div, plain GFM, tone matching `angular-agent-framework`) → matched in Task 4 Step 2.
- Visual assets (GitHub avatar only) → Task 4 Step 2.
- Links to verify → Task 3.
- Success criteria (links 200, PR opened, renders on org page) → Tasks 3, 5, 7.

**Placeholder scan:** No TBDs. Every code block is complete. Every command has an expected output. Substitution table (Task 3 Step 2) is explicit, not "handle edge cases".

**Type consistency:** Branch name `org-profile-readme` is referenced consistently across Tasks 1, 7. Spec filename referenced consistently across Tasks 2, 6. Plan filename referenced consistently across Tasks 2, 6. Avatar URL identical in Tasks 3 and 4.

No gaps found.
