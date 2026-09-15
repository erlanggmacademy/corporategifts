# Standard Operating Procedure & Immutable Rules: Blog Migration

## 1. Golden Rule
**Setiap artikel blog yang dimigrasikan WAJIB 100% identik strukturnya dengan baseline referensi (`blog/souvenir-kantor-pajak.html` & `blog/tren-seminar-kit-korporat-terbaru-2026.html`).**
Dilarang memodifikasi class name, menghapus wrapper, mengganti format font, menyederhanakan navbar/sidebar/related posts, atau mengubah format komponen HTML.

---

## 2. Standard HTML Blueprint Components (Wajib Diikuti Tanpa Deviasi)

### A. `<head>` & Fonts
- Wajib memuat Google Fonts **Poppins (500, 600, 700)** dan **Inter (400, 500, 600, 700)**.
- Preload stylesheet & Vendor CSS standar (`bootstrap.min.css`, `main.min.css`, `bootstrap-icons.css`, `aos.css`, `glightbox.min.css`).

### B. JSON-LD Schemas (5 Blok Wajib & Komprehensif)
1. **`LocalBusiness & Organization`**: Lengkap dengan `@id: "https://corporategifts.id/#localbusiness"`, `priceRange`, `openingHoursSpecification`, `areaServed`, dan `sameAs`.
2. **`Article (Utama)`**: `@id` berakhiran `/#article`, `mainEntityOfPage` berakhiran `/`, `headline`, `image` array absolut, `datePublished`, `dateModified`, `author` (Person dengan URL profil penulis `/penulis#[slug]`), `publisher` (Organization link `#localbusiness`), dan `inLanguage: "id-ID"`.
3. **`Article (Ringkasan Eksekutif)`**: `@id` berakhiran `/#summary`, `about` berakhiran `/#article`, headline diawali `Ringkasan Eksekutif: ...`, rangkuman deskripsi artikel untuk rich snippet Google & AI Overview.
4. **`BreadcrumbList`**: 3 tingkat: Beranda (`https://corporategifts.id/`) -> Blog (`https://corporategifts.id/blog`) -> Judul Artikel (`https://corporategifts.id/blog<slug>/`).
5. **`FAQPage`**: Array `Question` dan `Answer` yang sinkron 1:1 dengan konten Accordion FAQ pada body artikel.

### C. Body, Header Nav & Breadcrumbs
- Tag Body: `<body class="blog-detail-page">` (Jangan gunakan `blog-details-page`).
- Header Nav: Memuat logo standard, dropdown produk (6 link ke `/produk...`), link Galeri (`/galeri`), dan tombol WhatsApp CS "Hubungi Kami".
- Breadcrumbs Bar: Bar putih ramping ber-border bottom `#f1f5f9` (Beranda > Blog > Judul) dengan link ke `/` dan `/blog`.

### D. Main Article Layout & Elements
1. **Section Layout**: `<section class="py-5"><div class="container" data-aos="fade-up"><div class="row g-5"><div class="col-lg-8"><article class="article-detail-wrap">`
2. **Article Header & Meta Bar**: 
   - Badge kategori hijau soft (`background: rgba(22, 163, 74, 0.1); color: #16a34a`).
   - Title `<h1>`.
   - Meta bar: Thumbnail penulis 44x44 (wajib path `../assets/img/penulis/[slug].webp`), nama penulis link ke `/penulis#[author-anchor]`, jabatan penulis, tanggal update dari Excel, dan estimasi waktu baca rata kanan.
3. **Featured Image**: Gambar cover utama 1200x675 (`.article-featured-img`) dengan caption paragraph italic.
4. **Table of Contents (TOC)**: Menggunakan `#toc-header`, `#toc-toggle-btn`, `#toc-btn-text` ("Tutup"), `#toc-btn-icon` (`bi-chevron-up`), dan `#toc-list` dengan toggle script `toggleTOC` di bawah.
5. **Body Content & Typography**:
   - Paragraf pertama diawali: `<strong><a href="/" class="text-success text-decoration-none fw-bold">Corporate Gifts ID</a></strong> - ...`
   - **HTML Semantik Murni**: Dilarang menyisakan karakter markdown `*` (*italic*) atau `**` (**bold**). Wajib dikonversi ke tag HTML semantik `<em>...</em>` atau `<strong>...</strong>`.
   - **Internal Links**: Wajib menyematkan tautan internal natural ke produk (`/produk...`), katalog (`/katalog`), RFQ (`/minta-penawaran`), atau artikel blog relevan (`/blog[slug]`).
   - **Zero Em-Dashes**: Dilarang menggunakan em-dash (`—` / `&mdash;`), gunakan tanda strip `-`.
   - **Kotak Poin Kunci**: `.article-key-points` (multi-line highlight box berlatar hijau lembut dengan ikon dan bullet list).
   - **Kotak Baca Juga**: `.article-baca-juga` (single-line flex strip dengan badge hijau dan panah link ke `/blog[slug]`).
   - **Tabel Responsif**: Wajib dibungkus `<div class="tbl-wrap"><table class="tbl-corporategifts">...`.
6. **FAQ Accordion**: `.article-faq-compact my-4` dengan `#faq-section` dan `#blogFaqAccordion` (Bootstrap flush accordion minimal 5 item).
7. **Bottom RFQ CTA**: `.card.border-0.mt-5.shadow-sm.text-center.text-md-start.blog-cta-banner` dengan tombol hijau Minta Penawaran (`/minta-penawaran`) dan outline WhatsApp CS.
8. **Author Box**: `.article-author-box.mt-4` dengan foto 90x90 dari `../assets/img/penulis/[slug].webp`, nama link ke `/penulis#[slug]`, badge spesialisasi berwarna, bio penulis, dan link profil lengkap.
9. **Share Bar**: `.article-share-bar` (WhatsApp, LinkedIn, Facebook, Copy Link dengan alert).
10. **Sidebar Sticky**: 3 widget wajib:
    - Widget 1: Kategori Produk Kami (6 link produk ke `/produk...`).
    - Widget 2: Bantuan Konsultasi Kilat (+62 895-6390-68080 & Chat WhatsApp).
    - Widget 3: Unduh E-Katalog PDF Resmi 2026 (`../assets/docs/katalog-corporategifts-id.pdf`).
11. **Section Artikel Terkait (3 Rekomendasi)**: Header bar "Rekomendasi Wawasan" + grid 3 kartu artikel rekomendasi ber-badge, excerpt, author footer, dan link ke `/blog[slug]`. Verifikasi ketat file gambar di `assets/img/blog` benar-benar ada di disk.
12. **Footer**: 4-column footer standar + Partner Network baris bawah + script auto-update tahun copyright + Floating WhatsApp.

---

## 3. Mandatory 5-Step Synchronization Checklist
Setiap kali artikel baru dibuat:
1. `blog/<slug>.html` dibuat sesuai blueprint lengkap di atas.
2. `blog.html` disisipkan card artikel di grid dengan badge, thumbnail, excerpt, dan metadata (urut kronologis menurun berdasarkan kolom Tanggal Update, link ke `/blog<slug>/`, kapasitas 30 artikel per halaman).
3. `sitemap.xml` ditambahkan URL artikel `<loc>https://corporategifts.id/blog<slug>/</loc>` lengkap dengan `<lastmod>` dan `<priority>0.8</priority>`.
4. `_redirects` ditambahkan rule 301 redirect dari URL Blogger lama dan clean URL.
5. `llms.txt` ditambahkan rangkuman 1 baris di bawah seksi `Blog & Artikel` dengan URL `https://corporategifts.id/blog<slug>/`.

---

## 4. Author Mapping Reference
| Nama Penulis di Excel | Target Anchor di `penulis.html` | Jabatan Standar | Avatar Lokal |
| :--- | :--- | :--- | :--- |
| **Arinda Zakia** | `/penulis#arinda-zakia` | Senior Corporate Gifting Specialist & Content Strategist | `../assets/img/penulis/arinda-zakia.webp` |
| **Amelia** | `/penulis#amelia` | Creative Product Designer & Bespoke Packaging Consultant | `../assets/img/penulis/amelia.webp` |
| **Vendor Souvenir Kantor** | `/penulis#vendor-souvenir-kantor` | Editorial Team & Merchandise Production Specialist | `../assets/img/penulis/vendor-souvenir-kantor.png` |
