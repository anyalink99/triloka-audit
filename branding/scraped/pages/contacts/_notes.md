# Contacts page — scrape notes

**URL:** https://triloka.ae/contacts  
**Scraped:** 2026-04-13  
**See also:** `branding/scraped/_notes.md` for site-level typography, palette, header comparison, known issues.

---

## CRITICAL BUGS (contacts-specific)

1. **Page `<title>` = "Контакты ONZE,"** — Russian text, wrong company name (ONZE). Live SEO + brand issue.
2. **Form submit button = "Отправить"** — Russian for "Send". An international English-language site with a Russian CTA button.
3. **Form accent colour = `#007bff` (bright blue)** — completely off-brand; all other CTAs on the site are either white or dark.
4. **Header is a blank black bar** — only element is a hamburger icon (=) at far right. No logo, no nav links. Confirmed by screenshot at `pages/contacts/element/header-over-hero/desktop-1440x900.png`.
5. **Yandex Maps embedded** — a Russian mapping service on a UAE studio's international site. Will not load for many international users.

---

## Floating elements / overlays

| Kind | Selector | Decision |
|------|----------|----------|
| Header | `#intw37gfc_0` (sticky, 133px — shortest of all pages) | Hide for sections |
| Side panel | `#i376bp8z5_0` (fixed, fullscreen) | Hide everywhere |
| Form image (sticky LPC widget) | `div.lpc-form-2__image` (sticky, 906x906) | Keep — real content |
| Form fields (sticky LPC widget) | `div.lpc-form-2__form` (sticky, 906x600) | Keep — real content |
| Contact info block | `#_lp_block_802721713` | Keep — phone/address/hours/email |

---

## Hide list used

```
--hide="#intw37gfc_0,#i376bp8z5_0"
--section-selector=".section"
```

---

## Header state (contacts-specific)

Near-solid-black bar, 133px tall. Only visible element: hamburger icon (=) in top-right corner. No TRILOKA logo. No navigation links. No social icons. No language toggle.  
This is the most broken header variant — a visitor arriving directly on `/contacts` has no visual brand marker and no navigation path except the hamburger.  
Evidence: `pages/contacts/element/header-over-hero/desktop-1440x900.png`.

---

## Sections inventory

| Index | Selector | Top | Height | Role | Heading | Notes |
|-------|----------|-----|--------|------|---------|-------|
| 0 | `#intw37gfc_0` | 0 | 114px | Header | — | Hidden |
| 1 | `#im6xjjey0_0` | -182 | 78px | Unknown | — | Negative top — above viewport |
| 2 | `#ihlqztuxs_0` | 23 | 36px | Header strip | — | Skipped |
| 3 | `#irz7t50pd_0` | 114 | 1542px | Main content | "Our contacts" | Breadcrumb + form + map + contact info. Same ID as home/portfolio main wrapper. |
| 4 | `#io9282k83_0` | 114 | 1542px | Main content duplicate | "Our contacts" | Identical coordinates as section 3 — another DOM ghost |
| 5 | `#itt01w9ig_0` | 1655 | 548px | Footer | — | Standard footer |
| 6 | `#i46ycyhqu_0` | 2203 | 0px | Footer ghost | — | height:0, collapsed — renders nothing |

---

## Page structure (contacts)

1. Header (blank bar + hamburger only)
2. Breadcrumb: "Home / CONTACT"
3. "Our contacts" heading (Title Case — inconsistent with rest of site ALL CAPS)
4. Two-column layout: left = interior photo (dining room with chandelier), right = "DISCUSS THE PROJECT" form
   - Form fields: Name, Telephone, E-Mail (3 fields — home/portfolio forms have only Name + Telephone)
   - Checkbox: "I agree to the processing of my personal data *"
   - Submit button: "Отправить" (Russian), styled bright blue (#007bff)
5. Contact info strip: Telephone +971 562510706 (WhatsApp + Telegram icons), Address, Opening hours (Mon–Fri 9:00–18:00, Sat–Sun Closed), email info@triloka.ae
6. Yandex Maps embed (full-width, shows Dubai)
7. Footer

---

## Form differences vs home/portfolio

| Field | Home form | Portfolio form | Contacts form |
|-------|-----------|---------------|---------------|
| Name | Yes | Yes | Yes |
| Telephone | Yes | Yes | Yes |
| E-Mail | No | No | **Yes** |
| Data consent checkbox | No | No | **Yes** |
| Submit label | "SEND" | "SEND" | **"Отправить"** (Russian) |
| Button style | Dark/text | Dark/text | **Bright blue** |

---

## Assets roles (contacts)

- `pages/contacts/images/` — 9 images saved, 0 failed
- Interior photo: modern dining room with statement chandelier (left column)
- Map: Yandex Maps screenshot

---

## Known issues (contacts-specific)

- Section 1 at `top: -182` — element positioned above viewport, will be visually invisible or cause layout shifts.
- Sections 3+4 at identical coordinates (DOM duplication of entire main content).
- Section 6 height:0 — collapsed footer ghost.
- Yandex Maps will fail to load or display abnormally for users outside CIS region.
- "Отправить" button text and blue styling are likely inherited from an ONZE template that was not fully localised.
