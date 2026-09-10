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
7. **Body Content**:
   - Struktur heading teratur (`h2`, `p`, highlight boxes).
   - Selipkan callout `.article-baca-juga` dengan link artikel terkait.
   - **Internal Links**: Wajib menyematkan tautan internal kontekstual ke produk (`../produk/...`), katalog (`../katalog.html`), RFQ (`../minta-penawaran.html`), atau artikel blog relevan.
   - **HTML Semantik Murni**: Dilarang meninggalkan karakter markdown `*` (*italic*) atau `**` (**bold**). Wajib dikonversi ke tag HTML resmi `<em>...</em>` atau `<strong>...</strong>`.
   - **Zero Em-Dashes**: Dilarang menggunakan karakter em-dash (`—` / `&mdash;`), gunakan tanda strip `-`.
8. **FAQ Accordion**: `.article-faq-compact my-4` dengan container `#faq-section` dan `#blogFaqAccordion` (Bootstrap accordion-flush), minimal 5-6 item FAQ relevan yang sinkron 1:1 dengan schema `FAQPage`.
9. **Bottom RFQ CTA**: White card `.card.border-0.mt-5.shadow-sm.text-center.text-md-start.blog-cta-banner` dengan `.blog-cta-actions` (tombol hijau Minta Penawaran & outline hijau WhatsApp CS).
10. **Author Box**: `.article-author-box` dengan foto 90x90, nama, badge spesialisasi berwarna, bio penulis lengkap, dan tautan ke `penulis.html#[author-anchor]`.
11. **Share Bar**: `.article-share-bar` dengan tombol share WhatsApp, LinkedIn, Facebook, dan Copy Link.
12. **Sidebar**: `.sidebar` sticky dengan 3 widget standar resmi:
    - Widget 1: Kategori Produk Kami (6 link produk).
    - Widget 2: Bantuan Konsultasi Kilat (+62 895-6390-68080 & Chat WhatsApp).
    - Widget 3: Unduh E-Katalog PDF Resmi 2026.
13. **Related Section**: Grid 3 kartu rekomendasi artikel terkait dengan verifikasi ketat bahwa file gambar di `assets/img/blog/` benar-benar ada di disk.
14. **Footer**: 4-column footer standar + Partner Network baris bawah.
15. **Schemas (5 JSON-LD Blocks)**:
    - `LocalBusiness & Organization`: Comprehensive fields (`name`, `alternateName`, `url`, `logo`, `image`, `description`, `telephone`, `email`, `priceRange: "Rp15.000 - Rp750.000"`, `paymentAccepted: "Cash, Bank Transfer, Invoice B2B"`, `currenciesAccepted: "IDR"`, `address`, `geo`, `openingHoursSpecification`, `areaServed`, `sameAs`).
    - `Article (Utama)`: `@id` with `#article`, headline, image array, published/modified dates, author Person link, publisher Org `#localbusiness`.
    - `Article (Ringkasan Eksekutif)`: `@id` with `#summary`, paired summary article schema for Google rich snippets and AI Overview.
    - `BreadcrumbList`: 3 hierarchical levels (`Beranda` -> `Blog` -> `{Article Title}`).
    - `FAQPage`: Array of `Question` & `Answer` mirroring the body accordion FAQ 1:1.
16. **Full 5-Step Sync**: Secara simultan wajib memperbarui:
    - `blog/<slug>.html` (artikel detail).
    - `blog.html` (disisipkan sesuai urutan tanggal update kronologis menurun, kapasitas 30 kartu per halaman).
    - `sitemap.xml` (`<loc>` dan `<lastmod>YYYY-MM-DD</lastmod>`).
    - `_redirects` (rule 301 Blogger url dan clean url).
    - `llms.txt` (ringkasan 1 baris di bawah `Blog & Artikel`).
17. **Date Source**: Selalu gunakan nilai dari kolom Excel **Tanggal Update** (kolom kanan) untuk tanggal artikel, meta bar, schema JSON-LD, kartu `blog.html`, dan `sitemap.xml`.
