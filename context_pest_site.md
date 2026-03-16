# ZeroBite Pest Control — Site Context

## Overview

Static HTML/CSS/JS pest control website for **ZeroBite Pest Control**, serving Ontario (Kitchener-Waterloo and Toronto/GTA). No frameworks, no build tools, no server-side rendering — pure static files hosted on Netlify/Cloudflare. Clean URLs via directory-based structure (`page/index.html` served as `/page/`).

- **Domain:** `https://www.zerobitepest.ca`
- **Brand:** ZeroBite Pest Control (single brand across all regions)
- **Total pages:** 60

---

## URL Architecture

Multi-region subdirectory structure:

```
/                                            Brand-level homepage (region-neutral)
/kitchener-waterloo/                         KW regional hub
/kitchener-waterloo/bed-bug-control/         KW service page (14 services)
/kitchener-waterloo/pest-control-kitchener/  KW city page (8 cities)
/toronto/                                    Toronto regional hub
/toronto/bed-bug-control/                    Toronto service page (14 services)
/toronto/pest-control-scarborough/           Toronto city page (10 cities)
/services/                                   Brand-level services overview
/about/                                      Brand-level about
/contact/                                    Brand-level contact (both offices)
/blog/                                       Blog index
/blog/[post-slug]/                           Blog posts (3 KW + 3 Toronto)
/thank-you/                                  Form submission confirmation
```

---

## Page Count

| Section | Pages |
|---------|-------|
| KW region (hub + 14 services + 8 cities) | 23 |
| Toronto region (hub + 14 services + 10 cities) | 25 |
| Blog (index + 3 KW posts + 3 Toronto posts) | 7 |
| Global (homepage, services, about, contact, thank-you) | 5 |
| **Total** | **60** |

---

## KW Service Pages (14)

All under `/kitchener-waterloo/`:
`bed-bug-control`, `rodent-control`, `ant-control`, `cockroach-control`, `wildlife-removal`, `termite-control`, `wasp-removal`, `tick-control`, `moth-control`, `spider-control`, `flea-control`, `silverfish-control`, `earwig-control`, `commercial-pest-control`

Toronto has the same 14 service slugs under `/toronto/`.

## KW City Pages (8)

Under `/kitchener-waterloo/`:
`pest-control-kitchener`, `pest-control-waterloo`, `pest-control-cambridge`, `pest-control-guelph`, `pest-control-brantford`, `pest-control-elmira`, `pest-control-stratford`, `pest-control-new-hamburg`

## Toronto City Pages (10)

Under `/toronto/`:
`pest-control-downtown-toronto`, `pest-control-scarborough`, `pest-control-north-york`, `pest-control-etobicoke`, `pest-control-mississauga`, `pest-control-brampton`, `pest-control-markham`, `pest-control-vaughan`, `pest-control-richmond-hill`, `pest-control-oakville`

## Blog Posts (6)

KW posts:
- `/blog/bed-bug-treatment-kw-guide/`
- `/blog/mice-invasion-waterloo-fall/`
- `/blog/spot-termites-kitchener-waterloo/`

Toronto posts:
- `/blog/raccoon-removal-toronto-guide/`
- `/blog/bed-bugs-toronto-condos/`
- `/blog/carpenter-ants-gta-prevention/`

---

## Contact Info

- Phone: (647) 787-2244 / `+16477872244` (single number for all regions)
- Email: `info@zerobitepest.ca`
- No physical address displayed on site

---

## Header/Footer Variants

### Variant A — Brand-level pages (`/`, `/about/`, `/contact/`, `/services/`, `/blog/`, `/blog/*`, `/thank-you/`)
- Nav Home link: `/`
- Mega-menu service links: all point to `/services/`
- Header phone: (647) 787-2244
- Footer: no address, all 18 city links in Service Areas
- Footer copyright: "Serving Ontario"

### Variant B — Region-scoped pages (`/kitchener-waterloo/*`, `/toronto/*`)
- Nav Home link: `/kitchener-waterloo/` or `/toronto/` (regional hub)
- Mega-menu service links: point to regional service pages (e.g., `/toronto/bed-bug-control/`)
- Header phone: (647) 787-2244
- Footer: no address, all 18 city links in Service Areas (same as Variant A)
- Footer copyright: "Serving Ontario"

### Footer Notes
- No physical addresses anywhere on site
- Single phone number (647) 787-2244 on all pages
- Single email info@zerobitepest.ca on all pages
- All 18 city page links in every footer (8 KW + 10 Toronto) for SEO

---

## Tech Stack

- **HTML:** Static HTML5, `lang="en-CA"`
- **CSS:** `/assets/css/style.css` — custom properties design system, glassmorphism (`glass-bg`, `glass-border`), fully responsive, no CSS framework
- **JS:** `/assets/js/main.js` — vanilla JS IIFE, IntersectionObserver for reveal animations, carousel, FAQ accordion, mobile menu, honeypot spam protection, form pre-fill via `data-prefill-city` attribute
- **Fonts:** Google Fonts — Sora (headings), DM Sans (body), preloaded
- **Icons:** Font Awesome 6.5.1 CDN
- **Images:** `.webp` format in `/assets/img/`, OG image at `/assets/img/og-default.webp`

---

## Schema.org JSON-LD Structure

Every page has `<script type="application/ld+json">` in `<head>` with an `@graph` array.

### Brand homepage (`/`)
- `Organization` with `@id: /#organization`
- `subOrganization` references: `/kitchener-waterloo/#business` and `/toronto/#business`

### Regional hubs (`/kitchener-waterloo/`, `/toronto/`)
- `LocalBusiness` + `PestControlService` with `@id: /[region]/#business`
- `parentOrganization` → `/#organization`
- `BreadcrumbList`: Home > [Region]
- `FAQPage`

### Service pages (`/[region]/[service]/`)
- `Service` with `provider.@id` → `/[region]/#business`
- `BreadcrumbList`: Home > [Region] > [Service Name]
- `FAQPage`

### City pages (`/[region]/pest-control-[city]/`)
- `LocalBusiness` + `PestControlService` with `@id: /[region]/#business`
- `areaServed` set to specific city
- `BreadcrumbList`: Home > [Region] > [City] Pest Control
- `FAQPage`

### Blog posts
- `Article` with `datePublished`, `dateModified`, `author`, `publisher`
- `FAQPage` with 5 questions per post

---

## Sitemap Architecture

`robots.txt` points to `sitemap-index.xml`.

- **`sitemap-index.xml`** — references 4 child sitemaps
- **`sitemap-global.xml`** — 5 URLs (homepage, services, about, contact, blog)
- **`sitemap-kw.xml`** — 23 URLs (hub + 14 services + 8 cities)
- **`sitemap-toronto.xml`** — 25 URLs (hub + 14 services + 10 cities)
- **`sitemap-blog.xml`** — 7 URLs (blog index + 6 posts)

---

## Redirects

`_redirects` file (Netlify format) contains 22 × 301 redirects from old flat KW URLs to new `/kitchener-waterloo/` paths:

```
/bed-bug-control-kitchener/    → /kitchener-waterloo/bed-bug-control/
/rodent-control-kw/            → /kitchener-waterloo/rodent-control/
/pest-control-kitchener/       → /kitchener-waterloo/pest-control-kitchener/
... (22 total)
```

---

## Internal Linking Strategy

- **Within region (primary):** regional hub ↔ service pages ↔ city pages (fully cross-linked within same region)
- **Between regions (secondary):** footer "Also Serving: [other region]" link only — do NOT cross-link individual service pages between regions
- **Global → regions:** `/services/` links to both regional variants; `/about/` and `/contact/` reference both hubs
- **Blog → services:** KW blog posts link to KW service pages; Toronto posts link to Toronto service pages

---

## Key CSS Classes

- `.hero`, `.page-hero` — hero sections
- `.trust-strip`, `.trust-ticker` — scrolling credentials bar
- `.section-pad` — standard section padding
- `.container` — max-width content wrapper
- `.grid-auto`, `.grid-4` — responsive grid layouts
- `.service-card`, `.card-white`, `.card-glow` — service/blog cards
- `.faq-list`, `.faq-item`, `.faq-question`, `.faq-answer` — FAQ accordion
- `.cta-banner` — call-to-action sections
- `.breadcrumb` — breadcrumb navigation
- `.local-context-grid`, `.neighbourhood-card` — city page local content
- `.article-wrap` — service page article layout with sidebar
- `.callout-box` — highlighted info boxes in blog posts
- `.section-label` — small uppercase label above headings
- `.text-gradient` — gradient text effect
- `.reveal`, `.stagger` — scroll-triggered animation classes
- `.mobile-overlay` — mobile menu panel
- `.floating-phone` — fixed mobile phone button
- `.btn-primary`, `.btn-outline`, `.btn-sm` — button variants

---

## File Structure

```
pestcontrolsite/
├── index.html                          # Brand homepage
├── _redirects                          # 22 × 301 redirects (Netlify)
├── robots.txt                          # Points to sitemap-index.xml
├── sitemap-index.xml                   # Sitemap index
├── sitemap-global.xml                  # Global pages sitemap
├── sitemap-kw.xml                      # KW region sitemap
├── sitemap-toronto.xml                 # Toronto region sitemap
├── sitemap-blog.xml                    # Blog sitemap
├── assets/
│   ├── css/style.css                   # All styles (no changes needed for new regions)
│   ├── js/main.js                      # All JS (no changes needed for new regions)
│   └── img/                            # Images (.webp)
├── kitchener-waterloo/
│   ├── index.html                      # KW regional hub
│   ├── bed-bug-control/index.html      # 14 service pages...
│   ├── rodent-control/index.html
│   ├── ...
│   ├── pest-control-kitchener/index.html  # 8 city pages...
│   ├── pest-control-waterloo/index.html
│   └── ...
├── toronto/
│   ├── index.html                      # Toronto regional hub
│   ├── bed-bug-control/index.html      # 14 service pages...
│   ├── ...
│   ├── pest-control-downtown-toronto/index.html  # 10 city pages...
│   ├── pest-control-scarborough/index.html
│   └── ...
├── services/index.html                 # Brand-level services
├── about/index.html                    # Brand-level about
├── contact/index.html                  # Brand-level contact
├── thank-you/index.html                # Form confirmation
└── blog/
    ├── index.html                      # Blog index (6 post cards)
    ├── bed-bug-treatment-kw-guide/index.html
    ├── mice-invasion-waterloo-fall/index.html
    ├── spot-termites-kitchener-waterloo/index.html
    ├── raccoon-removal-toronto-guide/index.html
    ├── bed-bugs-toronto-condos/index.html
    └── carpenter-ants-gta-prevention/index.html
```

---

## Adding a New Region

To add a future region (e.g., Ottawa):

1. Create `/ottawa/` directory with hub `index.html`
2. Create 14 service subdirectories with unique local content
3. Create city subdirectories with unique local content
4. Use Variant B header/footer with Ottawa phone/address
5. Add `sitemap-ottawa.xml` and reference it in `sitemap-index.xml`
6. Update brand homepage region selector cards
7. Update `/services/`, `/about/`, `/contact/` to mention new region
8. Add "Also Serving" links in other regional footers
9. Create Ottawa-focused blog posts
10. Each region adds ~25 pages

---

## Important Notes

- All content is unique per region — Toronto pages are NOT find-and-replace copies of KW
- CSS and JS are 100% generic — no region-specific code, no changes needed for new regions
- `data-prefill-city` attribute on `<body>` pre-fills the contact form city field via JS
- Honeypot field in contact form for spam protection
- All pages use `lang="en-CA"` with `hreflang="en-CA"` and `hreflang="x-default"`
- Hours: Mon-Fri 7am-8pm, Sat-Sun 8am-6pm, 24/7 Emergency Line
