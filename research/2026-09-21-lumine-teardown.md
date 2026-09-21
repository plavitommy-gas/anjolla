# Site Teardown: Lumine — Luxury Nail, Lash & Brow Studio

**URL:** https://pretty-delivers-191144.framer.app/
**Platform:** Framer (meta generator `Framer 7175f5c`; assets on framerusercontent.com)
**Date analyzed:** 2026-09-21
**Source:** Full rendered HTML + inline CSS + inline Framer appear-animation JSON (pasted by user — more complete than a fetch)

## Tech Stack (Confirmed from Source)

| Technology | Evidence | Purpose |
|---|---|---|
| Framer | `meta[name=generator]`, `framerusercontent.com` bundles, `data-framer-*` attrs | Whole-page builder/runtime |
| React + Framer Motion | `react.*.mjs`, `motion.*.mjs` modulepreload | Rendering + animation |
| Framer "appear" animations | inline `<script type="framer/appear" id="__framer__appearAnimationsContent">` JSON | Load/scroll reveal animations |
| Google Fonts (self-hosted woff2) | `@font-face` for Inter, Manrope, Nunito | Typography |

**Takeaway:** No GSAP / Lenis / ScrollTrigger / custom cursor. All motion is Framer's standard *appear* reveals (fade + translate, staggered). **Fully cloneable with plain HTML/CSS + one IntersectionObserver.**

## Design System

### Colors (from `body{--token-*}` + inline overrides)
| Usage | Value |
|---|---|
| Page background (cream) | `rgb(250,248,245)` `#faf8f5` |
| Primary text (warm charcoal) | `#4a4745` |
| Muted text (gray) | `#807f7e` |
| Primary accent (lilac/purple) | `#9483d2` |
| Button fill (light lavender) | `#ccc6ea` |
| Pale lilac surface | `#efe6f4` |
| Lavender-white card | `#f5f2f9` |
| Deep navy (CTA card) | `#132436` |
| Navy 2 | `#32404d` |
| White | `#ffffff` |
| (unused) terracotta | `#c9835c` |
| Hero gradient | `linear-gradient(139deg,#cac2ed 0%,#e5e5e7 100%)` |
| Card gradient | `linear-gradient(145deg,#f5f2f9 14%,#efebf7 49%,#ebe6f5 87%)` |

### Typography
| Role | Font | Weight | Size (desktop → mobile) | Notes |
|---|---|---|---|---|
| Big display H1 ("Nails & Lashes") | Inter | 200 | 147px → 45px | UPPERCASE, line-height ~0.73 |
| Section H2 ("Luxury Nail Care") | Inter | 300 | 72px → 35px | light, elegant |
| Card H2 ("Book in 60 seconds") | Manrope | 500 | 32px → 21px | |
| Body p | Manrope | 400–500 | 16px → 13px | text-wrap:balance |
| Label H3 ("Hygienic", "Hours") | Inter | 700 | 18px → 14px | |
| Service name H3 ("Gel Manicure") | Inter | 500 | 20px | UPPERCASE |
| Price H1 ("$35") | Inter | 600 | ~62px | |

Fonts: **Inter** (headings/UI/display) + **Manrope** (body). Nunito loaded but barely used.

### Spacing / Shape
- Corner radius: **20px** on almost everything (cards, images, nav pill, buttons); 10px on small icon chips.
- Max content width: **1200px**, 20px side gutters.
- Generous vertical rhythm; sections are tall rounded blocks.
- Nav pill uses `backdrop-filter: blur(10px)` on `rgba(255,255,255,.6)`.

### Responsive
Three breakpoints: desktop `≥1200`, tablet `810–1199`, phone `≤809`. Root font-size steps down (93.75% / 87.5% / 62.5%). Grids collapse 2-col → 1-col; the 3 side-by-side bottom blocks stack.

## Effects Breakdown

| Effect | Implementation | Complexity | Cloneable? |
|---|---|---|---|
| Load/scroll reveals | Framer appear: opacity 0.001→1 + translateY, staggered delays 0.2–0.8s, ease `cubic-bezier(0.44,0,0.56,1)` | Low | Yes (IntersectionObserver + CSS transition) |
| Hero gradient block | rounded-bottom 20px, lavender→grey linear gradient, portrait image absolutely centered at bottom | Low | Yes |
| Frosted nav pill | translucent white + backdrop-blur | Low | Yes |
| Gradient cards | 145deg lavender gradient, 20px radius | Low | Yes |
| Tinted line icons | inline SVG with `mask` + `background-color:#9483d2` | Low | Yes (inline SVG) |
| Circular arrow buttons | round chip, → SVG, on lilac/white | Low | Yes |

### Reveal values (confirmed from `__framer__appearAnimationsContent`)
- hero image: opacity 0→1, 0.8s
- left column: fade, delay 0.2s, 0.4s
- "love it" card: translateY(-20→0), delay 0.5s, 0.6s
- book card: translateY(200→0), delay 0.3s, 0.6s
- reviews card: translateY(20→0), delay 0.7s
- big H1: translateY(100→0), delay 0.8s, 0.4s
- All ease `cubic-bezier(0.44,0,0.56,1)`.

## Page Structure (top → bottom)
1. **Sticky nav** — wordmark "Lumine" + frosted pill (Services/About/New Clients/Contact) + lavender "Book Now".
2. **Hero** — gradient rounded block: left headline "Luxury Nail Care" + subcopy + tiny "Love it or we fix it" card; centered tall model photo; bottom cards ("Book in 60 seconds" + "4.9 ★ / 12K reviews"); huge display "Nails & Lashes".
3. **Highlights strip** — Hygienic / Best Products / Expert Artists (icon+title+sub) + lavender pill "Fast & On Time · 45 min".
4. **Featured** — left 2×2 image cards (services) with name overlay; right tall owner card (photo + name/role).
5. **Three blocks** — price/offer card ($35 + arrow), stat card ("10 years… 2,000+ guests"), testimonial card.
6. **Contact block** — "Hours" card (cream) + "Ready to glow?" card (navy) with arrow CTA.
7. Framer badge (remove for clone).

## Assets Needed to Recreate (Anjolla version)
1. Hero nail photo (portrait) — have: `nails-pink-chrome`, `nails-editorial-pearls`, `nails-nude`.
2. 4–6 service/gallery images — have 15+ real IG shots.
3. Owner image — have `owner-illustration` (branded) + `studio-working`.
4. Logo — have `logo-emblem` (cropped) + text wordmark.
5. Icons — inline SVG (sparkle, clock, hand/leaf, checkmark, arrow), tinted lilac.

## Build Plan (Anjolla adaptation)
**Stack:** single self-contained `index.html`, inline CSS, Google Fonts (Inter + Manrope), one IntersectionObserver for reveals. No framework — keeps it portable and fast for a one-page site.

**Adaptations requested by client:**
- **Nails only** — drop Lash & Brow. Services: Gel lak, Ojačavanje (rubber baza), Nail art, French/kombinovani, Manikir.
- **No prices** — remove `$35` price card; replace with a soft offer/quality card.
- **Longer homepage** — add a dedicated Gallery section + expanded About + services detail.
- **Language:** Serbian (Latin). Location: Čukarica, Beograd. Booking via Instagram DM (@anjolla_nails).
- **Palette:** keep cream `#faf8f5` + lilac `#9483d2`/lavender `#ccc6ea` (matches Anjolla's own logo + nail work); add warm taupe/gold `#b89b6e` from brand for elegant accents; navy `#132436` for final CTA.

**Section order (Anjolla):** Nav → Hero → Highlights strip → Usluge (services) → Galerija → O nama (Anja) → Recenzija → Radno vreme + CTA → Footer.
