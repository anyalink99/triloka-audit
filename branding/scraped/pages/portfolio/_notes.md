# Portfolio page — scrape notes

**URL:** https://triloka.ae/portfolio  
**Scraped:** 2026-04-13  
**See also:** `branding/scraped/_notes.md` for site-level typography, palette, header comparison, known issues.

---

## Floating elements / overlays

| Kind | Selector | Decision |
|------|----------|----------|
| Header | `#intw37gfc_0` (sticky, 177px — tallest of all pages) | Hide for sections |
| Side panel | `#i376bp8z5_0` (fixed, fullscreen) | Hide everywhere |
| Discuss form | `#i6zrvjgsj_0` (sticky, 553px) | Keep — real content |

---

## Hide list used

```
--hide="#intw37gfc_0,#i376bp8z5_0"
--section-selector=".section"
```

---

## Header state (portfolio-specific)

Two-row solid black header. Row 1: TRILOKA logo (approx 3x larger than on home) left; nav links (HOME, PORTFOLIO, ABOUT US, GET A QUOTE, CONTACT, BLOG) center; EN toggle right. Row 2: social icons (Instagram, YouTube, Telegram, Pinterest) + hamburger icon (=) far right.  
Hamburger icon visible on desktop — unusual, should be mobile-only.  
Social set different from home: no WhatsApp, has Pinterest; home has WhatsApp + Facebook, no Pinterest.  
Evidence: `pages/portfolio/element/header-over-hero/desktop-1440x900.png`.

---

## Sections inventory

| Index | Selector | Top | Height | Role | Heading | Notes |
|-------|----------|-----|--------|------|---------|-------|
| 0 | `#intw37gfc_0` | 0 | 158px | Header | — | Hidden |
| 1 | `#im6xjjey0_0` | 0 | 78px | Header sub-element | — | Skipped |
| 2 | `#ieprlv22u_0` | 78 | 80px | Header sub-element | — | Skipped |
| 3 | `#irz7t50pd_0` | 158 | 1612px | Main content | "Portfolio" | 3 category tiles: RESIDENCES, INTERIORS, JOINERY. No "Commercial" tile. |
| 4 | `#io9282k83_0` | 833 | 937px | Discuss the project | — | Same block ID as on home (shared ID namespace) |
| 5 | `#i46ycyhqu_0` | 1770 | 548px | Footer | — | Standard footer |
| 6 | `#itt01w9ig_0` | 1770 | 548px | Footer duplicate | — | Same position as section 5 |

---

## Assets roles (portfolio)

- `pages/portfolio/images/` — 12 images saved, 0 failed
- 3 category tiles: interior (warm chandeliers), villa exterior (pool + garden), staircase/joinery details
- Footer background: same two-tower dusk photo as home

---

## Known issues (portfolio-specific)

- Portfolio page shows only 3 of 4 service categories. "Office design and commercial" is accessible only via the header nav dropdown, not from this page.
- 3 tiles link to sub-pages (`/portfolio/architecture`, `/portfolio/interiors`, `/portfolio/joinery`). These sub-pages were not scraped.
- Desktop hamburger icon in header is visible but should be mobile-only — a constructor layout error at this page's header variant.
- Footer duplicate (sections 5+6) same as home.
