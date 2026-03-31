# CLAUDE.md — Sent Landing Page Rebuild
## For: Codebro (Claude Code)
## Task: Assemble all 8 slides into one index.html and push to sentapp.net

---

## YOUR ONE JOB

Replace the current `index.html` in `RustyGrinds/sentapp` with the fully assembled new landing page. Then `git add . && git commit -m "rebuild: full landing page v2" && git push`. That's it.

---

## REPO & DEPLOYMENT

- **Repo:** `C:\Users\natew\OneDrive\Documents\Sent` → `RustyGrinds/sentapp` on GitHub
- **Live URL:** sentapp.net (GitHub Pages — pushes to main go live automatically)
- **Waitlist:** Kit (ConvertKit) via Cloudflare Worker proxy at `https://sent-waitlist.rustycranklive.workers.dev/`
  - POST `{ email }` to the worker — it handles everything
  - Form ID: `9245595`

---

## DESIGN SYSTEM — DO NOT DEVIATE

```css
--n1: #06080F;   /* page bg */
--n2: #0C1220;   /* section bg */
--n3: #111A2E;   /* card bg */
--n4: #182038;   /* featured card bg */
--n5: #1F2A46;   /* borders */
--text-hi: #DCE4F0;
--text-mid: #7A8DAA;
--text-lo: #3A4A64;
```

**Fonts:** `DM Serif Display` (serif) + `DM Sans` (sans) — Google Fonts
**No white backgrounds. No amber/gold. Dark everywhere.**

### Steel gradient (used on logo, CTAs, labels, accents)
```css
/* Ping-pong animation — back and forth, this IS the brand motion */
background: linear-gradient(90deg,
  #0C0D10 0%, #1C2028 12%, #4A5568 28%, #9AAABB 42%,
  #D4E0EC 50%, #EEF4FA 54%, #C8D8E8 64%,
  #6A7A8E 78%, #1C2028 90%, #0C0D10 100%
);
background-size: 300% auto;
animation: steel-pingpong 4s ease-in-out infinite;

@keyframes steel-pingpong {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

### Motion rules
- **Only animate:** logo, CTAs (heartbeat), section labels, stamp (float), key card borders (crawl), pipeline energy
- **Never animate:** body text, card content, section backgrounds
- **All label animations:** 10s loop — action in first 25–30%, hold 30–82%, fade 82–92%, dark pause 92–100%

---

## PAGE STRUCTURE — 8 SECTIONS + NAV + FOOTER

```
NAV
├── Steel ping-pong logo "Sent"
└── Heartbeat CTA "Join the waitlist" → #waitlist

SECTION 1 — HERO (#hero)
SECTION 2 — THE PROBLEM (#problem)
SECTION 3 — HOW IT WORKS (#how)
SECTION 4 — THE MAGIC (#magic)
SECTION 5 — THE MEDIA STUDIO (#media)
SECTION 6 — YOUR VOICE (#voice)
SECTION 7 — PRICING (#pricing)
SECTION 8 — EARLY ACCESS (#waitlist)

FOOTER
```

---

## SECTION-BY-SECTION SPEC

### NAV
- Fixed, dark bg `rgba(6,8,15,0.97)`, animated steel bottom border line
- Logo: steel ping-pong "Sent" italic
- CTA: "Join the waitlist" — heartbeat pulse (two pumps, rest) — no shine, steel gradient fill
- CTA links to `#waitlist`

---

### SECTION 1 — HERO
**Label animation:** Twinkling ✦ star on badge (static steel gradient badge, no text animation)

**Layout:** Two column — left: accordion headline + sub, right: floating stamp

**Accordion headline:**
```
Every occasion.  [+ expands → 🎂 Birthdays, 🎓 Graduations, 👶 New babies, 🏆 Promotions, 🌅 Retirements, 🕊️ Condolences]
Every person.    [+ expands → 👨‍👩‍👧 Family, 🤝 Close friends, 💼 Colleagues, 🤙 Old friends, 🧑‍💻 Clients, 🏘️ Neighbors]
Every event.     [+ expands → 💍 Weddings, 🎉 Anniversaries, 🏠 New home, 🚀 New venture, 🎖️ Milestones, 🌍 Big moves]
```
- Tags pop in with stagger on expand. One panel open at a time.
- "Remembered. *Sent.*" fades in on FIRST open and STAYS for the rest of the session.

**Stamp (right side):**
- SVG stamp: steel gradient border, perforated edges (dark circles)
- Inner face: 7 horizontal tube rects (`<rect>` NOT `<line>`) with vertical cylinder gradients — descending thickness top to bottom
- Tube gradient (vertical): dark top → bright platinum center → dark bottom (cylindrical illusion)
- S drawn LAST (on top of tubes): `fill="url(#smokeGrad)"` + `stroke="url(#steelGrad)"` — smoky dark transparent fill
- Smoke S fill: `stop-opacity ~0.78–0.92` dark midnight blue, tubes ghost through
- Stamp floats: `translateY(0↔-10px) rotate(-5deg)`, 5s ease-in-out
- Drop shadow: `filter: drop-shadow(0 10px 32px rgba(154,170,187,0.25))`

**Demo button (centered below, full width of hero):**
- Text: "Try the demo today!"
- Hover: text hides, 3 double-chevron arrows appear left→center→right, staggered 0.22s, drop-and-fade animation
- Border: `1px solid #2A3650` → `#6A7A8E` on hover

---

### SECTION 2 — THE PROBLEM
**Label animation:** `THE PROBLEM`
- Starts static
- Math equation builds term by term: `∑(missed)` → `+ ∅` → `÷ time`
- Then `= S` pops in large, glowing, STAYS
- Then `O` `L` `V` `E` `D` appear letter by letter after the S
- Full equation `∑(missed) + ∅ ÷ time = SOLVED` holds
- Fades, reset

**Content:** 3 click-to-expand cards
```
😶 Generic messages — stat: 52× — "sent word for word by 52 other people"
⏰ Missed entirely  — stat: 67% — "admit forgetting an important occasion"
🕸️ Scattered data  — stat: 5+  — "platforms life moments are scattered across"
```
- Click to expand: steel border crawls around card, `+` rotates to `×`, stat number reveals with detail copy
- One card open at a time

**Callout bottom:**
> "Every person you love has moments worth celebrating. Sent makes sure you never miss another one."
> `Here's how →`

---

### SECTION 3 — HOW IT WORKS
**Label animation:** `HOW IT WORKS`
- Starts static
- Translucent cylindrical pipe materializes (same gradient DNA as stamp tubes)
- Pipe has window cut-away (SVG mask): emojis flow through the window left→right
- Emojis: 🎂 📸 👶 🎬 🏆 🎙️ — spawn and die INSIDE the solid end caps (not visible at edges)
- After last emoji exits: `Sent.` materializes in italic steel at pipe exit
- Fades, reset

**Pipe construction:**
```svg
<!-- Vertical cylinder gradient on rect — same as stamp tubes -->
<!-- SVG mask cuts window: solid caps at left/right (9px), open center -->
<!-- Emojis flow in emoji-track div behind the SVG overlay -->
<!-- Spawn: left:12px, Exit: calc(100% - 12px) — hidden behind caps -->
```

**Content:** 4 pipeline step cards — ALL OPEN AND LOCKED (no click needed)
```
01 Aggregate — OAuth from all platforms, one feed
02 Research  — real-time context on recipient's life right now
03 Generate  — your voice archetype, their actual life, not a template
04 Deliver   — right channel, right time, 365/24/7
```
- Pipes between steps: 3 stacked tube rects (same cylinder gradient), energy bolt flows L→R
- Energy bolt: `translateX(-110% → 110%)`, opacity 0→1→1→0
- Stagger: pipe 2 delay 0.65s, pipe 3 delay 1.3s — cascades across the full pipeline

**Callout bottom:**
> "Set it up once. Every moment handled. Every message personal. Every person remembered."
> `And it sounds like you →`

---

### SECTION 4 — THE MAGIC
**Label animation:** `THE MAGIC`
- Wand SVG slides in from left (fast)
- Iris blades snap closed
- Flash burst (radial gradient circle scales up)
- "The Magic" text materializes out of blur + letter-spacing
- Wand fades 0.5s before sweep ends
- Label HOLDS fully visible
- Sparks pop: 📸 🎬 🎙️ 🎭 fly off in different directions
- Fades, 10s loop

**Content:** Side-by-side comparison
- Left: "Without Sent" — generic message, `"sent by 52 other people"`
- Center: `V E R S U S` spelled vertically in muted dark letters — no line, no arrow
- Right: "With Sent" — steel border crawl, subtle glow pulse, interactive voice tags

**5 voice tags (click to swap message):**
```
😏 The Wit       — sharp, dry, playful
🤗 The Nurturer  — warm, expressive, big-hearted
🎉 The Hype      — ALL CAPS ENERGY
🌿 The Sage      — thoughtful, genuine, grounded
🎯 The Minimalist — six words, no fluff
```
Message fades out/in on swap. All use Marcus/Austin/Biscuit as the example.

**Callout bottom:**
> "This is what it feels like to be remembered. Not as a notification. As a person who actually knows you."
> `Now imagine doing this in your voice →`

---

### SECTION 5 — THE MEDIA STUDIO
**Label animation:** `THE MEDIA STUDIO`
- Camera SVG slides in
- Iris blades snap (6 thin rects rotate from center)
- Flash burst
- Label materializes
- Camera fades
- Media sparks pop off lens: 📸 🎬 🎙️ 🎭 in different directions
- Label holds, fades, 10s loop

**Content:** 2 featured hero cards (full width grid, 2-col) + 4 media cards below (4-col grid)

**Featured cards (steel border crawl on load):**
```
💸 Sent Gift       — badge: "Revenue model" — coin floats animation
   "Remember the birthday card your uncle slipped a $20 into?"
   Tiers: Free $25 / Sent+ $100 / Pro $500

💌 Postcard Builder — badge: "Growth engine" — stamp rocks animation
   "People screenshot these. People share these."
   Tiers: Free preset / Sent+ AI-generated / Pro + voice fingerprint
```

**Media cards (click to expand):**
```
📸 Photos      — Free: 3/msg, Sent+: 10/msg, Pro: unlimited + AI
🎭 GIFs/Memes  — Free: 1, Sent+: unlimited + AI, Pro: full suite
🎬 Video       — Free: 15s, Sent+: 60s, Pro: 3min
🎙️ Voice Notes — Pro only: AI-scripted, your voice
```

**Callout bottom:**
> "Every format. Every channel. All delivered in your voice, automatically, on time."
> `And it all starts with your voice →`

---

### SECTION 6 — YOUR VOICE
**Label animation:** `YOUR VOICE`
- Mic SVG slides in
- 7 sound wave bars pulse outward (heights: 6/10/16/20/16/10/6px)
- Label materializes
- Mic fades, bars settle
- Label holds, fades, 10s loop

**Content:** 5 voice archetype cards + interactive message stage + fingerprint teaser

**Voice cards (5-col grid):**
```
🤗 The Nurturer  — Warm, expressive, big-hearted
😏 The Wit       — Dry humor, sharp, playful
🌿 The Sage      — Thoughtful, genuine, grounded
🎉 The Hype      — Energetic, enthusiastic, loud
🎯 The Minimalist — Short, clean, no fluff
```
- Click: steel border crawls, glowing dot appears, card glows
- One active at a time

**Message stage:**
- Default: "Select a voice above to hear it in action →" prompt
- On select: context line (emoji + recipient + situation) + italic message + voice tag + note
- Different message for each archetype, all featuring different recipients/occasions

**Voice fingerprint teaser row:**
> "Over time, Sent learns your *actual* writing style — not just an archetype."
> Badge: `Pro feature` (steel gradient)

**Callout bottom:**
> "The archetype is where you start. *The voice fingerprint is where you end up.*"
> `Now let's talk about the plan →`

---

### SECTION 7 — PRICING
**Label:** `PRICING` — **STATIC. NO ANIMATION. Intentional silence. Do not add any animation here.**

**Content:** Trial banner + 3 tier cards + rollback row

**Trial banner (steel border crawl, subtle glow):**
> "30 days of *Pro*, on us."
> "No credit card. No commitment. Full access from day one."
> Heartbeat CTA: "Join the waitlist ✦" → `#waitlist`

**3 tier cards:**
```
Free     $0/forever  — 3 msgs/month, 10 contacts, preset messages, Gift $25
Sent+    $4.99/mo    — FEATURED (steel top line, "Most Popular" badge)
                       Unlimited msgs, AI-generated, all channels, Postcard, Gift $100
Pro      $12.99/mo   — Everything + voice fingerprinting, voice notes, analytics, CRM, Gift $500
```

**Rollback row:**
> "If you don't convert after the trial, you drop to free — but *you keep everything you made.*"

**Callout bottom:**
> "*The free tier isn't the product. It's the reminder of what you're missing.*"
> `Be the first in →`

---

### SECTION 8 — EARLY ACCESS (id="waitlist")
**Label animation:** `EARLY ACCESS → ticket tear → ACCESS GRANTED`

Sequence (10s loop):
1. "Early Access" holds (0–1s)
2. Two SVG ticket halves slide in from right as one unit, S glows in negative space gap between halves (1–2.8s)
3. Left half flies up-left rotate(-15deg), right half flies down-right rotate(15deg), S fades simultaneously (2.8–4s)
4. Checkmark materializes at EXACT same position S was — ring bursts, stroke draws (4–5s)
5. "Access Granted" slides in right of checkmark (5–8.2s)
6. Fade, dark pause, loop

Ticket halves are SVG shapes (not emoji):
- Left half: rounded left corners, curved notch on right edge (classic ticket half)
- Right half: matching notch left, rounded right corners
- Both: steel cylinder gradient fill, perforations top/bottom
- S: zero-width flex wrapper at gap point, `left:22px`, vertically centered via flex
- Checkmark: identical wrapper positioning as S — guaranteed same spot

**Content:** 2-col layout — ticket visual left, form right

**Ticket visual (floating, slight rotate -1deg):**
- Full ticket SVG — stub on left with smoke S + SENT + ADMIT ONE
- Main body: EARLY ACCESS in bloomed steel gradient (bright 8%→92% of width)
- DATE / WAITLIST / NO. fields, corner ornaments, "— DON'T MISS OUT —"

**Form (right):**
```
"Your ticket is waiting."
[email input] [Claim your spot ✦] ← heartbeat CTA
"One email when you're in. That's it."
• 30 days of Pro — free, no card required
• Keep everything you make, always
• Founding member pricing — locked in
• First access to every new feature
```
On submit → hide form, show: `"You're on the list. We'll be in touch. ✦"`
Wire to Kit proxy: `POST https://sent-waitlist.rustycranklive.workers.dev/ { email }`

**Closing section (below, dark bg #06080F):**
```
Relationships, remembered.
Sent.   ← steel ping-pong italic
[smoke stamp SVG — small, ~80px]
─────────────────────────────────
Sent — sentapp.net    © 2026 Sent    Privacy · Terms · Contact
```

---

## STAMP SVG SPEC (used in hero + closing)

```
Outer: steel gradient border rect, rx=6-7
Inner face: dark gradient rect, rx=4-5
Perforations: dark circles along all 4 edges (punch through border into page bg)

7 TUBE RECTS (inside inner face, behind S):
- <rect> elements with vertical linearGradient (NOT lines — gradients don't work on SVG lines)
- Heights descending: 14, 11, 8.5, 6.5, 5, 3.5, 2px
- All same width (inner face edge to edge)
- 80% of inner face height, vertically centered
- Each has own gradient ID (same cylinder formula, different opacity)

S TEXT (drawn LAST — renders on top of tubes):
- font: Georgia serif italic
- fill: smoke gradient (dark near-black, ~78% opacity, slight midnight blue at center)
- stroke: steel gradient
- text-anchor: middle, dominant-baseline: central
- Precisely centered in inner face

SENT label: Trebuchet MS, ~9px, muted steel color, letter-spacing 6-7
```

---

## KEY ANIMATIONS REFERENCE

```css
/* Heartbeat — CTA buttons */
@keyframes heartbeat {
  0%{transform:scale(1)} 8%{transform:scale(1.06)} 16%{transform:scale(1)}
  26%{transform:scale(1.04)} 34%{transform:scale(1)} 100%{transform:scale(1)}
}

/* Steel ping-pong — logo, labels, borders */
@keyframes steel-pingpong {
  0%{background-position:0% 50%} 50%{background-position:100% 50%} 100%{background-position:0% 50%}
}

/* Stamp float */
@keyframes float {
  0%,100%{transform:translateY(0) rotate(-5deg)} 50%{transform:translateY(-10px) rotate(-5deg)}
}

/* Pipeline energy bolt */
@keyframes energy-flow {
  0%{transform:translateX(-110%); opacity:0}
  5%{opacity:1} 95%{opacity:1}
  100%{transform:translateX(110%); opacity:0}
}

/* Steel border crawl on cards */
@keyframes border-crawl {
  0%{stroke-dashoffset:600} 100%{stroke-dashoffset:0}
}
```

---

## WAITLIST WIRING

```javascript
async function submitWaitlist(email) {
  await fetch('https://sent-waitlist.rustycranklive.workers.dev/', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ email })
  });
  // hide form, show success message
}
```

---

## GIT WORKFLOW

```bash
cd ~/OneDrive/Documents/Sent
git add .
git commit -m "rebuild: full landing page v2 — all 8 slides, new design system"
git push
```

GitHub Pages deploys automatically from main. Live at sentapp.net within ~60s.

---

## WHAT NOT TO DO

- Do NOT use `<line>` elements with gradient strokes — they collapse to zero height. Use `<rect>` instead.
- Do NOT animate section label text with the steel ping-pong — only specific labels per the map above.
- Do NOT add animations to Pricing label — intentionally static.
- Do NOT use white or amber/gold — the entire site is the dark steel palette.
- Do NOT deviate from the design system colors above.
- Do NOT touch the Cloudflare Worker URL or Kit form ID.

---

*Built in claude.ai — Nate + Claude, March 2026*
