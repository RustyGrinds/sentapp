# CLAUDE.md — Sent Codebase Guide
> Read this before touching any file. These decisions are locked.

---

## Project
**Sent** — AI-powered occasion intelligence platform  
Live: sentapp.net (GitHub Pages) | Repo: RustyGrinds/sentapp, branch: main  
Waitlist: Kit/ConvertKit via Cloudflare Worker at `sent-waitlist.rustycranklive.workers.dev` (form ID 9245595)  
Payments: Stripe (Sent Gift feature)

---

## Canonical Design System (LOCKED — April 2026)

### CSS Variables
```css
:root {
  --bg:       #06080F;
  --bg-2:     #0C1220;
  --bg-3:     #111A2E;
  --bg-4:     #182038;
  --surface:  #1F2A46;
  --text:     #DCE4F0;
  --text-mid: #7A8DAA;
  --text-lo:  #3A4A64;
  --serif:    'DM Serif Display', Georgia, serif;
  --sans:     'DM Sans', 'Trebuchet MS', sans-serif;
}
```

### Fonts
- **DM Serif Display** — headings, brand moments
- **DM Sans** — UI, body, labels
- Load via Google Fonts. Do NOT use Palatino or Trebuchet MS as primary fonts.

### Steel Gradient (brand motion identity)
```css
background: linear-gradient(90deg,
  #0C0D10 0%, #1C2028 12%, #4A5568 28%, #9AAABB 42%,
  #D4E0EC 50%, #EEF4FA 54%, #C8D8E8 64%,
  #6A7A8E 78%, #1C2028 90%, #0C0D10 100%);
background-size: 300% auto;
animation: steel-pingpong 4s ease-in-out infinite;
```
```css
@keyframes steel-pingpong {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

### Color Rules
- **No amber, no gold, no cream, no white backgrounds. Ever.**
- Dark backgrounds on everything — all pages, all states.
- Borders: use `rgba` of `--text-lo` or `--surface`.

---

## Files

| File | Purpose |
|------|---------|
| `index.html` | Landing page — 8 slides, all locked |
| `sent-app.html` | Working AI prototype — occasion selector + media suite |
| `sent-postcard.html` | Digital postcard builder |
| `sent-welcome.html` | Onboarding / welcome screen |
| `sw.js` | Service worker |
| `manifest.json` | PWA manifest |

---

## Stamp Logo (SVG Rules — LOCKED)

- Perforated border edges
- 7 cylindrical tube `rect` elements (NEVER use SVG `line` — always `rect` with vertical gradients)
- Tubes descend in thickness
- Smoke-fill S drawn last, on top
- Steel gradient border
- Stamp tubes = pipeline tubes = brand easter egg

---

## index.html — 8 Slides (ALL LOCKED)

### Section Label Animation System (all 10s loops, action in first ~30%)
| Slide | Animation |
|-------|-----------|
| 1 | Twinkling star badge |
| 2 | Math equation building → `=S` → `=SOLVED` |
| 3 | Cylindrical pipe + emoji data flow → `Sent.` |
| 4 | Wand sweep |
| 5 | Camera shutter + iris blades + media sparks |
| 6 | Mic + sound wave ripple |
| **7** | **INTENTIONALLY STATIC — no animation, ever** |
| 8 | Ticket tear → S glows → checkmark → Access Granted |

### Slide 8 — Early Access
Vintage ticket SVG (stub with smoke S + ADMIT ONE / EARLY ACCESS in bloomed steel gradient).  
Waitlist wired to Kit/ConvertKit via Cloudflare Worker.

---

## Hybrid AI Workflow

- **Claude.ai** — planning, logic, QC, generating precise instructions
- **Codebro (Claude Code)** — all file edits, git commits, git push
- Local Ollama on MSI GL65 at `192.168.1.207:11434`
- Git Bash aliases: `claude-local` / `claude-cloud` in `.bashrc`
- **If `ANTHROPIC_BASE_URL` is set:** run `unset ANTHROPIC_BASE_URL` before launching Claude Code to hit real Anthropic API

---

## Hard Rules

1. Never use SVG `line` elements with gradients — always use `rect` with vertical gradients.
2. Slide 7 (Pricing) label is permanently static. Do not add animation.
3. No amber, gold, cream, or white anywhere.
4. Do not change layout, visual logic, or functionality during var migrations — CSS names/values only.
5. Read this file before touching `index.html` or any other file.
