# AGENTS.md - CorporateGifts.ID Agent Instructions

## Blog Migration Standard Architecture & Immutable Rules
All migrated blog detail articles MUST strictly follow the exact HTML blueprint and classes defined in `PANDUAN_MIGRASI_BLOG.md` and `.agents/rules/blog-migration-rules.md`.
The reference baseline implementation is `blog/souvenir-kantor-pajak.html` (Artikel #56) & `blog/tren-seminar-kit-korporat-terbaru-2026.html` (Artikel #57).

#### Key Standards & Component Specifications:

1. **Fonts & Preconnect**:
   - Google Fonts `Poppins` (500, 600, 700) and `Inter` (400, 500, 600, 700) with preload and print media onload fallback.

2. **Body Tag**:
   - `<body class="blog-detail-page">` (DILARANG menggunakan `blog-details-page`).

3. **Header & Navigation (Wajib Lengkap)**:
   - Logo: `<a href="/" class="logo d-flex align-items-center me-auto me-xl-0"><img src="../assets/img/logo-header.png" alt="CorporateGifts.ID - Vendor Corporate Gift &amp; Souvenir Perusahaan" style="max-height:40px;width:auto;" width="214" height="40" loading="lazy"></a>`
   - Menu Nav: `Beranda`, `Tentang Kami`, `Layanan`, `Katalog`, `Portofolio`, `<li class="dropdown"><a href="/produk"><span>Produk</span> <i class="bi bi-chevron-down toggle-dropdown"></i></a>...` (6 sub-menu produk: Souvenir Kantor, Souvenir Custom, Merchandise Perusahaan, Seminar Kit, Hampers & Parcel, Paket Souvenir Promosi), `Blog` (active), dan `Galeri`.
   - Header CTA: `<a class="btn-getstarted" href="https://wa.me/62895639068080?text=Halo%2C%20saya%20ingin%20konsultasi%20..." target="_blank" rel="noopener"><i class="bi bi-whatsapp me-1"></i> Hubungi Kami</a>`.

4. **Breadcrumbs Bar**:
   - `<div class="breadcrumbs-bar py-3 bg-white" style="border-bottom: 1px solid #f1f5f9;"><div class="container"><nav aria-label="breadcrumb" class="m-0 p-0" style="background: transparent;"><ol class="breadcrumb m-0 p-0" style="background: transparent; font-size: 0.88rem;"><li class="breadcrumb-item"><a href="/" style="color: var(--accent-color, #15803d); text-decoration: none; font-weight: 500;">Beranda</a></li><li class="breadcrumb-item"><a href="/blog" style="color: var(--accent-color, #15803d); text-decoration: none; font-weight: 500;">Blog</a></li><li class="breadcrumb-item active" aria-current="page" style="color: #64748b; font-weight: 500;">[Topik / Judul]</li></ol></nav></div></div>`.

5. **Article Wrap & Header**:
   - Wrap: `<section class="py-5"><div class="container" data-aos="fade-up"><div class="row g-5"><div class="col-lg-8"><article class="article-detail-wrap">`
   - Badge kategori: `<span class="badge px-3 py-2 rounded-pill fw-semibold" style="background: rgba(22, 163, 74, 0.1); color: var(--accent-color, #16a34a); font-size: 0.82rem;"><i class="[icon] me-1"></i> [Kategori]</span>`
   - Title: `<h1>[Judul Lengkap]</h1>`
   - Meta bar: Author thumbnail 44x44 (wajib dari `../assets/img/penulis/[slug].webp`), nama penulis link ke `/penulis#[slug]`, job title `Senior Corporate Gifting Specialist`, dan tanggal update + waktu baca rata kanan (`<div class="text-muted ms-auto">`).

6. **Featured Image**:
   - `.article-featured-img` dengan image WebP lokal (`width="1200" height="675" class="img-fluid"`) + caption paragraph italic di bawahnya.

7. **Table of Contents (TOC)**:
   - Container: `.table-of-contents`
   - Header: `<div class="d-flex justify-content-between align-items-center" id="toc-header" style="cursor: pointer; user-select: none;"><h2 class="m-0 d-flex align-items-center"><i class="bi bi-list-nested text-success me-2"></i> Daftar Isi Artikel</h2><button type="button" class="btn btn-sm btn-light border px-2 py-1 text-muted d-inline-flex align-items-center gap-1" id="toc-toggle-btn" aria-expanded="true" aria-controls="toc-list" style="border-radius: 6px;"><span id="toc-btn-text">Tutup</span><i class="bi bi-chevron-up" id="toc-btn-icon"></i></button></div>`
   - List: `<div id="toc-list" class="mt-2"><ol class="mb-0">...</ol></div>`

8. **Body Content, Callouts, & Tables**:
   - Paragraf pertama diawali: `<strong><a href="/" class="text-success text-decoration-none fw-bold">Corporate Gifts ID</a></strong> - ...`
   - **Poin Kunci / Highlight**: `<div class="article-key-points"><h3 class="h6 fw-bold text-dark mb-2"><i class="bi bi-lightbulb-fill text-success me-2"></i> Poin Kunci ...:</h3><ul class="mb-0 small text-muted ps-3" style="line-height: 1.7;"><li><strong>Label:</strong> Deskripsi.</li></ul></div>`
   - **Callout Baca Juga**: `<div class="article-baca-juga"><span class="badge bg-success text-white px-2 py-1 rounded-pill small fw-bold">Baca Juga</span><a href="/blog[slug]" class="hover-green">[Judul Artikel] <i class="bi bi-arrow-right ms-1"></i></a></div>`
   - **Tabel Responsif**: Wajib dibungkus `<div class="tbl-wrap"><table class="tbl-corporategifts"><thead>...</thead><tbody><tr><td data-label="Kolom">...</td></tr></tbody></table></div>`. DILARANG menyisipkan inline `<style>` untuk tabel di head.
   - **HTML Semantik Murni**: Dilarang meninggalkan karakter markdown `*` (*italic*) atau `**` (**bold**). Wajib dikonversi ke tag HTML `<em>...</em>` atau `<strong>...</strong>`.
   - **Zero Em-Dashes**: Dilarang menggunakan karakter em-dash (`—` / `&mdash;`), gunakan tanda strip `-`.
   - **Internal Links**: Wajib menyematkan tautan internal natural ke produk (`/produk...`), katalog (`/katalog`), RFQ (`/minta-penawaran`), atau artikel blog relevan (`/blog[slug]`).

9. **FAQ Accordion**:
   - `.article-faq-compact my-4` dengan container `#faq-section` dan `#blogFaqAccordion` (`.accordion.accordion-flush`), minimal 5 item FAQ relevan yang sinkron 1:1 dengan schema `FAQPage`.
   - Tombol item: `<button class="accordion-button collapsed py-2 px-3 fw-semibold text-dark bg-white" type="button" data-bs-toggle="collapse" ...>`

10. **Bottom RFQ CTA Banner**:
    - `.card.border-0.mt-5.shadow-sm.text-center.text-md-start.blog-cta-banner` dengan `.d-flex.flex-column.flex-md-row.align-items-center.justify-content-between.gap-3` dan `.blog-cta-actions` (tombol hijau Minta Penawaran & outline hijau WhatsApp CS).

11. **Author Box**:
    - `.article-author-box.mt-4` dengan foto 90x90 dari `../assets/img/penulis/[slug].webp`, nama penulis link ke `/penulis#[slug]`, badge spesialisasi berwarna, bio penulis, dan link profil lengkap.

12. **Share Bar**:
    - `.article-share-bar` dengan tombol share WhatsApp, LinkedIn, Facebook, dan Copy Link dengan alert JS.

13. **Sidebar Kanan (3 Widget Standar Wajib)**:
    - Widget 1: Kategori Produk Kami (6 link produk ke `/produk...`).
    - Widget 2: Bantuan Konsultasi Kilat (+62 895-6390-68080 & Chat WhatsApp Sekarang).
    - Widget 3: Unduh E-Katalog PDF Resmi 2026 (`../assets/docs/katalog-corporategifts-id.pdf`).

14. **Section Artikel Terkait (3 Rekomendasi)**:
    - `<section class="py-5 bg-light border-top"><div class="container" data-aos="fade-up">`
    - Section header dengan baris "Rekomendasi Wawasan" + "Artikel Terkait Lainnya" + tombol "Lihat Semua Artikel" (`/blog`).
    - 3 Kartu rekomendasi artikel terkait ber-badge kategori pojok kiri atas, excerpt, author footer, dan tautan ke `/blog[slug]`. Verifikasi ketat bahwa file gambar di `assets/img/blog` benar-benar ada di disk.

15. **Footer & Scripts**:
    - Footer 4 kolom standar + Partner Network baris bawah + script auto-update tahun copyright.
    - Floating WhatsApp button + Scroll-Top.
    - Skrip TOC toggle standar (`toggleTOC`) yang menangani `#toc-header` dan `e.stopPropagation()` pada `#toc-toggle-btn`.

16. **Schemas (5 JSON-LD Blocks)**:
    - `LocalBusiness & Organization`: `@id: "https://corporategifts.id/#localbusiness"`
    - `Article (Utama)`: `@id` berakhiran `#article` (`https://corporategifts.id/blog/<slug>#article`), `mainEntityOfPage` bernilai `https://corporategifts.id/blog/<slug>`
    - `Article (Ringkasan Eksekutif)`: `@id` berakhiran `#summary` (`https://corporategifts.id/blog/<slug>#summary`), `about` bernilai `https://corporategifts.id/blog/<slug>#article`
    - `BreadcrumbList`: 3 tingkat (Beranda `https://corporategifts.id/` > Blog `https://corporategifts.id/blog` > Judul `https://corporategifts.id/blog/<slug>`)
    - `FAQPage`: Array Question/Answer yang sinkron 1:1 dengan accordion.

17. **Full 5-Step Sync Checklist**:
    - `blog/<slug>.html` (artikel detail dengan Clean URLs tanpa .html dan tanpa trailing slash).
    - `blog.html` (disisipkan sesuai urutan tanggal update kronologis menurun, link kartu ke `/blog/<slug>`, kapasitas 30 kartu per halaman).
    - `sitemap.xml` (`<loc>https://corporategifts.id/blog/<slug></loc>` dan `<lastmod>YYYY-MM-DD</lastmod>`).
    - `_redirects` (WAJIB update di 3 bagian setiap kali migrasi 1 artikel):
      1. **Bagian Blogger 301 Redirects** (bagian atas file):
         ```
         # [Judul Artikel]
         /<YYYY>/<MM>/<slug>.html /blog/<slug> 301
         /<slug> /blog/<slug> 301
         /<slug>/* /blog/<slug> 301
         ```
      2. **Bagian `# Legacy .html to Clean URLs (Non-Trailing Slash) 301 Redirects`** (di bawah header `# Blog Detail Pages Legacy .html 301`):
         ```
         /blog/<slug>.html /blog/<slug> 301
         ```
      3. **Bagian `# Trailing Slash to Non-Trailing Slash 301 Redirects`** (di bawah header `# Trailing Slash to Non-Trailing Slash 301 Redirects`):
         ```
         /blog/<slug>/ /blog/<slug> 301
         ```
    - `llms.txt` (ringkasan 1 baris di bawah `Blog & Artikel` dengan URL `https://corporategifts.id/blog/<slug>`).

18. **Date Source of Truth**:
    - Selalu gunakan nilai dari kolom Excel **Tanggal Update** (kolom kanan) untuk tanggal artikel, meta bar, schema JSON-LD, kartu `blog.html`, dan `sitemap.xml`.
