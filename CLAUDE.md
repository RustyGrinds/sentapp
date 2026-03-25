# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Model setup

See global `~/.claude/CLAUDE.md` for the hybrid cloud/local model configuration. All work in this repo uses `claude-cloud`.

## Project

Sent is a pre-launch AI-powered occasion intelligence platform at sentapp.net. The repo is a GitHub Pages site — pushing to `main` deploys automatically. There is no build step, no bundler, no dependencies, and no package manager.

## Deployment

```bash
git add <file>
git commit -m "message"
git push origin main
```

GitHub Pages serves from the root of `main`. CNAME points to `sentapp.net`. Deploys take ~30 seconds after push.

## Architecture

Two standalone HTML files — no shared CSS, no shared JS, no imports between them:

- **`index.html`** — the public marketing/landing page at sentapp.net. Single file with all CSS in `<style>` and all JS in `<script>` at the bottom.
- **`sentapp.html`** — the working app prototype. Same single-file structure. Calls the Anthropic API directly from the browser to generate messages.

### Waitlist flow (`index.html`)
The `submitWaitlist()` function POSTs `{ email }` to a Cloudflare Worker proxy at `https://sent-waitlist.rustycranklive.workers.dev/`. The worker forwards the request to Kit's v4 API (`api.kit.com/v4/subscribers`) using `X-Kit-Api-Key` auth. The proxy exists to avoid ad-blocker blocking of `api.kit.com` in the browser. The Kit API key lives only in the Cloudflare Worker — not in `index.html`.

### Message generation (`sentapp.html`)
Calls `https://api.anthropic.com/v1/messages` directly from the browser with `claude-sonnet-4-20250514`. The API key is intentionally client-side for prototype/demo purposes — this is not production architecture.

## Design system

Both files use the same design language:

- **Fonts:** DM Serif Display (headings, italic S mark) + DM Sans (body) — loaded from Google Fonts
- **Colors:** `--ink` #1A1410 · `--amber` #C8832A · `--amber-lt` #F5A84B · `--cream` #FAF7F4
- **Motif:** Postage stamp (perforated edges, motion lines, italic S)
- **`index.html`** uses cream/light backgrounds for most sections, ink for hero/how-it-works/pricing/waitlist
- **`sentapp.html`** is fully dark-mode (ink background throughout)

## Key product context

See `sent_design_doc_alt.pdf` and `sent_cribnotes_alt.pdf` for full product vision. Short version:

- **Four-step pipeline:** Aggregate (OAuth from Facebook/LinkedIn/Google) → Research (real-time context on recipient) → Generate (AI message in user's voice archetype) → Deliver (SMS/email/LinkedIn/Instagram/WhatsApp)
- **Five voice archetypes:** The Nurturer, The Wit, The Sage, The Hype, The Minimalist
- **Three tiers:** Free · Sent+ $4.99/mo · Sent Pro $12.99/mo
- **Sent Gift:** Embedded cash gifts via Stripe — a second revenue stream separate from subscriptions
- **Digital Postcard Builder** (Sent+ and Pro): the organic growth engine — branded stamp postcards recipients share
- **Long-term vision:** "Sent Threads" → full relationship platform. The occasion app is the wedge.
- Fundraising: $750K pre-seed. Currently Phase 1 (story sharp, investor intros, accelerator applications).

## `index.html` section order

Nav → Hero → Problem → How It Works → The Magic (comparison) → Voices → Media Suite → Pricing → Waitlist → Footer

## Remaining items to build

1. Sent Gift section (currently only shown in media suite, needs its own featured section)
2. Digital Postcard Builder teaser section
3. Nav links wired to sections
