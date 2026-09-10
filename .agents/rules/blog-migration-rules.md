# Standard Operating Procedure & Immutable Rules: Blog Migration

## 1. Golden Rule
**Setiap artikel blog yang dimigrasikan WAJIB 100% identik strukturnya dengan baseline referensi (`blog/cara-mengukur-efektivitas-program-recognition.html`).**
Dilarang memodifikasi class name, menghapus wrapper, mengganti format font, atau mengubah komponen HTML.

---

## 2. Standard HTML Blueprint Components

### A. `<head>` & Fonts
- Wajib memuat Google Fonts **Poppins (500, 600, 700)** dan **Inter (400, 500, 600, 700)**.
- Preload stylesheet & Vendor CSS standar.

### B. JSON-LD Schemas (5 Blok Wajib & Komprehensif)
1. **`LocalBusiness & Organization`**: Lengkap dengan `@id: "https://corporategifts.id/#localbusiness"`, `priceRange`, `openingHoursSpecification`, `areaServed`, dan `sameAs`.
2. **`Article (Utama)`**: `@id` berakhiran `#article`, `headline`, `image` array absolut, `datePublished`, `dateModified`, `author` (Person dengan URL profil penulis), `publisher` (Organization link `#localbusiness`), dan `inLanguage: "id-ID"`.
3. **`Article (Ringkasan Eksekutif)`**: `@id` berakhiran `#summary`, headline diawali `Ringkasan: ...`, rangkuman deskripsi artikel untuk rich snippet Google & AI Overview.
4. **`BreadcrumbList`**: 3 tingkat: Beranda (`https://corporategifts.id/`) -> Blog (`https://corporategifts.id/blog.html`) -> Judul Artikel (`https://corporategifts.id/blog/<slug>.html`).
5. **`FAQPage`**: Array `Question` dan `Answer` yang sinkron 1:1 dengan konten Accordion FAQ pada body artikel.

### C. Body & Breadcrumbs
- Tag Body: `<body class="blog-detail-page">`
- Breadcrumbs Bar: Beranda > Blog > Judul Artikel

### D. Main Article Layout & Elements
1. **Article Header & Meta Bar**: Thumbnail penulis 44x44, nama penulis link ke `penulis.html#[author-anchor]`, jabatan penulis, tanggal update, estimasi waktu baca.
2. **Featured Image**: Gambar cover utama dengan caption paragraph.
3. **Table of Contents (TOC)**: Menggunakan `#toc-header`, `#toc-toggle-btn`, `#toc-btn-text`, `#toc-btn-icon`, dan `#toc-list` dengan toggle script di footer.
4. **Body Content & Typography**:
   - **HTML Semantik Murni**: Dilarang menyisakan karakter markdown `*` (*italic*) atau `**` (**bold**). Wajib dikonversi ke tag HTML `<em>...</em>` atau `<strong>...</strong>`.
   - **Internal Links**: Wajib menyematkan tautan internal natural ke produk (`../produk/...`), katalog (`../katalog.html`), RFQ (`../minta-penawaran.html`), atau artikel blog relevan.
   - **Zero Em-Dashes**: Dilarang menggunakan em-dash (`—` / `&mdash;`), gunakan tanda strip `-`.
   - **Callout Baca Juga**: `.article-baca-juga` di sela-sela pembahasan artikel.
5. **FAQ Accordion**: `.article-faq-compact my-4` dengan `#faq-section` dan `#blogFaqAccordion` (Bootstrap flush accordion 5-6 item).
6. **Bottom RFQ CTA**: `.card.border-0.mt-5.shadow-sm.text-center.text-md-start.blog-cta-banner` dengan tombol hijau Minta Penawaran dan outline WhatsApp CS.
7. **Author Box**: `.article-author-box` dengan foto 90x90, nama, badge spesialisasi berwarna, bio penulis, dan link profil lengkap.
8. **Share Bar**: `.article-share-bar` (WhatsApp, LinkedIn, Facebook, Copy Link).
9. **Sidebar Sticky**: 3 widget wajib:
   - Widget 1: Kategori Produk Kami.
   - Widget 2: Bantuan Konsultasi Kilat (+62 895-6390-68080 & Chat WhatsApp).
   - Widget 3: Unduh E-Katalog PDF Resmi 2026.
10. **Related Section**: Grid 3 kartu rekomendasi artikel terkait dengan verifikasi ketat bahwa file gambar di `assets/img/blog/` benar-benar ada di disk.

---

## 3. Mandatory 5-Step Synchronization Checklist
Setiap kali artikel baru dibuat:
1. `blog/<slug>.html` dibuat sesuai blueprint di atas.
2. `blog.html` disisipkan card artikel di grid dengan badge, thumbnail, excerpt, dan metadata (urut kronologis menurun berdasarkan kolom Tanggal Update, kapasitas 30 artikel per halaman).
3. `sitemap.xml` ditambahkan URL artikel lengkap dengan `<lastmod>` dan `<priority>0.8</priority>`.
4. `_redirects` ditambahkan rule 301 redirect dari URL Blogger lama dan clean URL.
5. `llms.txt` ditambahkan rangkuman 1 baris di bawah seksi `Blog & Artikel`.
