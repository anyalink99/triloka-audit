# Home page — scrape notes

**URL:** https://triloka.ae/  
**Scraped:** 2026-04-13  
**See also:** `branding/scraped/_notes.md` for site-level typography, palette, header comparison, known issues.

---

## Floating elements / overlays

| Kind | Selector | Decision |
|------|----------|----------|
| Header | `#intw37gfc_0` (sticky, 157px) | Hide for sections |
| Side panel | `#i376bp8z5_0` (fixed, fullscreen) | Hide everywhere |
| Discuss form (mid-page) | `#i6zrvjgsj_0` (sticky, 557px) | Keep — it is real content |
| Second header strip | `#ihlqztuxs_0` (sticky, 60px, top:-20) | Part of header group, hidden with header |

---

## Hide list used

```
--hide="#intw37gfc_0,#i376bp8z5_0"
--section-selector=".section"
```

---

## Header state (home-specific)

Single-row transparent header over hero video. TRILOKA logo (medium size) left; nav links (HOME, PORTFOLIO, ABOUT US, GET A QUOTE, CONTACT, BLOG) center-right; social icons (Instagram, YouTube, Telegram, WhatsApp, Facebook) tiny at right; EN language toggle boxed.  
No visible state change on scroll — header stays transparent against dark backgrounds. Low contrast issue across all scroll positions.  
Mobile: social icons displayed prominently left side (6 icons), TRILOKA centered, EN right. No hamburger visible in element crop — hamburger must be part of `#i376bp8z5_0` side panel trigger.

---

## Sections inventory

| Index | Selector | Top | Height | Role | Heading | Notes |
|-------|----------|-----|--------|------|---------|-------|
| 0 | `#intw37gfc_0` | 0 | 143px | Header | — | Hidden |
| 1 | `#ihlqztuxs_0` | -6 | 65px | Header strip | — | Skipped (hidden) |
| 2 | `#im6xjjey0_0` | 42 | 78px | Unknown small | — | Skipped |
| 3 | `#ipihj2r1y_0` | 143 | 694px | Hero | — | Video background; photo fallback shown in static |
| 4 | `#i1iyp8kit_0` | -27 | 864px | Hero overlay | — | Negative top, overlaps hero |
| 5 | `#irz7t50pd_0` | 837 | 6386px | Main content wrapper | "20 YEARS..." | Entire below-hero content in one section |
| 6 | `#ivp12fhsw_0` | 837 | 860px | Intro text | "20 YEARS OF EXPERIENCE IN DESIGN, ARCHITECTURE AND CONSTRUCTION IN DUBAI" | Sub-element of section 5 |
| 7 | `#io5zdpis9_0` | 1697 | 3696px | Portfolio grid | — | INTERIORS, ARCHITECTURE OF THE VILLA RESIDENCE, JOINERY, OFFICE DESIGN AND COMMERCIAL FINISHING IN DUBAI — 4 service blocks with "Learn more" CTAs |
| 8 | `#ilqzhou7h_0` | 5392 | 849px | Panorama | "PANORAMA / 360" | Static photo only; no 360-degree viewer loaded |
| 9 | `#io9282k83_0` | 6242 | 981px | Discuss the project | "FEEDBACK / REQUEST / DISCUSS THE PROJECT" | Form: Name + Telephone + SEND; people photos right; "ORDER A PROJECT / +971 562510706" |
| 10 | `#i46ycyhqu_0` | 7222 | 548px | Footer | — | Nav left, TRILOKA centered, address right |
| 11 | `#itt01w9ig_0` | 7222 | 548px | Footer duplicate | — | Identical element at same coordinates |

---

## Assets roles (home)

- `pages/home/images/` — 30 images saved (1 x 403 fail)
- Hero background: video (not captured in static); fallback = `pages/home/element/hero-with-header/` shows luxury villa exterior
- Section 7 images: interior renders (chandelier dining room, villa exterior pool, wooden staircase, office/commercial space)
- Section 9 images: B&W portraits (3 people in business attire)
- Footer background: dramatic dusk photo of two glass towers (Dubai skyline)

---

## Known issues (home-specific)

- Hero section contains a background video — static screenshots capture the poster frame only; actual animation/video not represented.
- Section 5 (`#irz7t50pd_0`) 6386px height means the sections pass captures an extremely tall crop — not useful as an isolated block reference.
- The 30-second auto-animation that stretches images (audit issue #9) is not visible in static PNGs.
- "Learn more" buttons in section 7: some open a modal ("Book a consultation now!"), some navigate to sub-pages. Behaviour inconsistent and not differentiable in static screenshots.
- Scroll-triggered reveal animations frozen at their initial/visible state in static capture.
- Footer duplicate (sections 10+11) at identical coordinates — only one renders visually; DOM has two elements.
