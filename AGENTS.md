# AGENTS.md - CorporateGifts.ID Agent Instructions

## Blog Migration Standard Architecture
All migrated blog detail articles MUST strictly follow the exact HTML blueprint and classes defined in `PANDUAN_MIGRASI_BLOG.md` and `.agents/rules/blog-migration-rules.md`.
The reference baseline implementation is `blog/cara-mengukur-efektivitas-program-recognition.html`.

### Key Standards:
1. **Fonts**: Google Fonts `Poppins` (500, 600, 700) and `Inter` (400, 500, 600, 700).
2. **Body**: `<body class="blog-detail-page">`.
3. **Article Wrap**: `<article class="article-detail-wrap">`.
4. **Header**: `.article-header` + `.article-meta-bar` (Author thumbnail 44x44, name, jobTitle, date, reading time).
5. **Featured Image**: `.article-featured-img` with image + caption paragraph.
6. **TOC**: `.table-of-contents` with `#toc-header`, `#toc-toggle-btn`, `#toc-btn-text`, `#toc-btn-icon`, and `#toc-list`.
7. **Body**: `.article-body` containing `h2`, `p`, highlight boxes, `.article-baca-juga`, and `.article-faq-compact my-4` with `#blogFaqAccordion`.
8. **Bottom CTA**: `.blog-cta-banner` card with `.blog-cta-actions`.
9. **Author Box**: `.article-author-box` with 90x90 photo and bio.
10. **Share Bar**: `.article-share-bar` with WhatsApp, LinkedIn, Facebook, Copy link.
11. **Sidebar**: `.sidebar` with 3 standard widgets (Categories, WA quick chat, PDF Catalog).
12. **Related Section**: Standard recommendations grid with 3 cards.
13. **Footer**: 4-column layout + Partner Network.
14. **Schemas (5 JSON-LD Blocks)**:
    - `LocalBusiness & Organization`: Comprehensive fields (`name`, `alternateName`, `url`, `logo`, `image`, `description`, `telephone`, `email`, `priceRange: "Rp15.000 - Rp750.000"`, `paymentAccepted: "Cash, Bank Transfer, Invoice B2B"`, `currenciesAccepted: "IDR"`, `address`, `geo`, `openingHoursSpecification`, `areaServed`, `sameAs`).
    - `Article (Utama)`: `@id` with `#article`, headline, image array, published/modified dates, author Person link, publisher Org `#localbusiness`.
    - `Article (Ringkasan Eksekutif)`: `@id` with `#summary`, paired summary article schema for Google rich snippets and AI Overview.
    - `BreadcrumbList`: 3 hierarchical levels (`Beranda` -> `Blog` -> `{Article Title}`).
    - `FAQPage`: Array of `Question` & `Answer` mirroring the body accordion FAQ.
15. **Full 5-Step Sync**: Simultaneously update `blog/<slug>.html`, `blog.html` (30 articles per page capacity), `sitemap.xml`, `_redirects`, and `llms.txt`.
16. **Pagination Standard**: `blog.html` uses 3-column grid layout with 30 articles per page (10 rows × 3 columns) before pagination triggers.
