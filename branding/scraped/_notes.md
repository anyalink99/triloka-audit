# TRILOKA — Site-level scrape notes

**URL:** https://triloka.ae/  
**Scraped:** 2026-04-13  
**Platform:** MegaGroup website builder (megagroup.ru)  
**Pages scraped:** home (`/`), portfolio (`/portfolio`), contacts (`/contacts`)  
**Description:** UAE-based architecture & interior design studio. Multi-page site with a dark premium aesthetic (near-black backgrounds, gold/copper accent tones, serif + sans typography). 5–12 `.section` divs per page; no semantic `<section>` elements.

---

## Pages

| Slug | URL | Role |
|------|-----|------|
| `home` | https://triloka.ae/ | Landing — hero video, services overview, portfolio preview, Panorama block, CTA form, footer |
| `portfolio` | https://triloka.ae/portfolio | Portfolio hub — 3 category tiles (Residences, Interiors, Joinery). "Commercial" category NOT linked here; only accessible from header. |
| `contacts` | https://triloka.ae/contacts | Contact page — form (Name/Telephone/E-Mail), Yandex Maps, address/hours/phone/email, footer |

---

## Site-wide floating elements / overlays

| Kind | Selector | Position | Behaviour | Decision |
|------|----------|----------|-----------|----------|
| Header | `#intw37gfc_0` | sticky top:0 | **Different on every page** (see header section) | hide for sections |
| Side panel (mobile menu) | `#i376bp8z5_0` | fixed, full-screen, z:10 | Slides in on hamburger click; empty when closed | hide everywhere |
| Discuss form (home/portfolio) | `#i6zrvjgsj_0` | sticky mid-page | Contact form widget; actual page content | keep visible |

---

## Hide list (for sections re-scrape)

```
--hide="#intw37gfc_0,#i376bp8z5_0"
```

---

## Header structure — CRITICAL: three distinct layouts

The constructor generates a **different header for each page** despite sharing the same `#intw37gfc_0` ID:

| Page | Height | Layout | Logo | Nav links | Social icons | Hamburger |
|------|--------|--------|------|-----------|--------------|-----------|
| Home | 157px | 1 row | Yes, left, medium | Yes, center-right, tiny | Yes, tiny, right (Instagram, YouTube, Telegram, WhatsApp, Facebook) | No |
| Portfolio | 177px | 2 rows | Yes, left, **~3× larger** | Yes, center, row 1 | Yes, own row (Instagram, YouTube, Telegram, Pinterest) | **Yes — on desktop** |
| Contacts | 133px | 1 row | **Absent** | **Absent** | **Absent** | **Only element** |

- No consistent sticky-vs-transparent transition: home header is transparent over hero, portfolio and contacts are solid black.
- The same `#intw37gfc_0` ID used across all pages — any CSS/JS targeting this ID affects all three simultaneously.
- Evidence file: `pages/portfolio/element/header-over-hero/desktop-1440x900.png` (two-row), `pages/contacts/element/header-over-hero/desktop-1440x900.png` (blank bar + hamburger only).

---

## Typography

| Family | Weights saved | Style | Likely usage |
|--------|--------------|-------|--------------|
| Cormorant Infant | 300–700 regular + italic | Luxury serif | H1/H2 display headings |
| Cormorant SC | 300–700 | Serif small-caps | Section labels, eyebrow text |
| Onest | 100–900 (all 9) | Modern sans | Body, nav, UI labels |
| Montserrat | various | Geometric sans | Subheadings, captions |
| Inter | various | Neutral sans | UI / form labels |

All `.woff2` files saved. `.woff` fallbacks for Onest all return HTTP 404 (server-side missing file) — modern browsers unaffected, IE11 would break.  
`lg.woff` / `lg.ttf` (LightGallery icon font) also 404 — gallery icons may render as squares in the lightbox.

Font file: `branding/scraped/fonts/_fonts.json` — 94 entries (93 saved, 12 failed).

---

## Palette (sampled from PNGs)

| Role | Value | Notes |
|------|-------|-------|
| Background (primary) | `#0a0a0a` / `#111` | Near-black, used on all pages |
| Background (footer) | `#0d0d0d` | Very dark, photo overlay |
| Text (primary) | `#ffffff` / `#f5f5f5` | White on dark |
| Text (secondary) | `#999` / `#aaa` | Labels, captions |
| Accent / CTA button | `#007bff` (blue) | **Wrong** — only on contacts "Отправить" button; off-brand |
| Gold/copper tones | `#b8956a` approx | Photo content, not in UI |
| Section dividers | transparent / dark | No visible rule lines |

---

## Known issues / TODO for build

1. **`<title>` of `/contacts` = "Контакты ONZE,"** — Russian text, wrong brand (ONZE ≠ TRILOKA). Live SEO/brand bug.
2. **Onest `.woff` 404** — 9 font weight variants return 404 for the old-format fallback. `.woff2` works.
3. **LightGallery icon font 404** — `lg.woff` and `lg.ttf` not found; gallery icons may be missing.
4. **DOM ID namespace shared across pages** — same IDs (`#irz7t50pd_0`, `#io9282k83_0`, `#i46ycyhqu_0`, `#itt01w9ig_0`) appear on home, portfolio, and contacts. Any global CSS/JS targeting these IDs modifies all pages at once.
5. **Footer duplicated on every page** — two elements at identical coordinates (`#i46ycyhqu_0` + `#itt01w9ig_0`). On contacts, `#i46ycyhqu_0` collapses to `height: 0`.
6. **Sections wrapper `#irz7t50pd_0` is 6386px tall on home** — the entire page content is inside a single `.section` with no meaningful subdivisions. Same wrapper duplicated as `#io9282k83_0` at same coordinates.
7. **Image dedup: 0 removed on all pages** — site uses `/thumb/...` CDN path pattern, not Framer's `?scale-down-to=`. Dedup didn't fire. One image 403 on home.
8. **`counter.megagroup.ru/loader.js`** — MegaGroup tracker loaded on every page (visible in source).
9. **Animations not captured in static PNGs** — preloader, scroll-triggered reveals, the 30-second image-stretch timer.
10. **360° Panorama block** — section 8 on home shows a static photo. No interactive viewer loaded.

---

## Source capture

Not performed. The site is a MegaGroup SPA: obfuscated class names (`section--u-intw37gfc`, `div--u-izc9qwtju`), constructor-generated IDs, logic injected via `$ite.start()`. Source is unreadable — screenshots remain ground truth.
