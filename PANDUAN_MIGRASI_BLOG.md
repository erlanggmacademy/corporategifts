# SOP & Panduan Lengkap Migrasi Artikel Blog
**Project**: CorporateGifts.ID  
**Target Hosting**: Cloudflare Pages  
**Template Acuan**: `blog/souvenir-dosen-penguji-skripsi-hemat.html` / `blog/cara-memilih-souvenir-dosen-penguji-skripsi.html` / `blog/new-year-souvenir-kantor.html`

---

## Standar Desain, Font, dan Komponen Resmi

Sebelum memulai migrasi, wajib mengikuti standar teknis berikut:

### 1. Standar Font Google
Seluruh halaman wajib memuat kombinasi resmi **Poppins** (untuk Judul/Headings) dan **Inter** (untuk Teks Body/Navigasi/Meta):
```html
  <!-- Fonts Preconnect & DNS-Prefetch -->
  <link rel="dns-prefetch" href="https://fonts.googleapis.com">
  <link rel="dns-prefetch" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com" rel="preconnect">
  <link href="https://fonts.gstatic.com" rel="preconnect" crossorigin>
  <link rel="preload" as="style" href="https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700&family=Inter:wght@400;500;600;700&display=swap">
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" media="print" onload="this.media='all'">
  <noscript>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  </noscript>
```

### 2. Tag Body
Tag body wajib menggunakan class:
```html
<body class="blog-detail-page">
```
*(Catatan: Jangan gunakan `blog-details-page` agar styling CSS `.blog-detail-page` di `main.min.css` aktif dengan sempurna).*

### 3. Breadcrumbs Bar Standar
```html
<div class="breadcrumbs-bar py-3 bg-white" style="border-bottom: 1px solid #f1f5f9;">
  <div class="container">
    <nav aria-label="breadcrumb" class="m-0 p-0" style="background: transparent;">
      <ol class="breadcrumb m-0 p-0" style="background: transparent; font-size: 0.88rem;">
        <li class="breadcrumb-item"><a href="/" style="color: var(--accent-color, #15803d); text-decoration: none; font-weight: 500;">Beranda</a></li>
        <li class="breadcrumb-item"><a href="../blog.html" style="color: var(--accent-color, #15803d); text-decoration: none; font-weight: 500;">Blog</a></li>
        <li class="breadcrumb-item active" aria-current="page" style="color: #64748b; font-weight: 500;">[Topik / Judul Singkat]</li>
      </ol>
    </nav>
  </div>
</div>
```

### 4. Article Header & Meta Bar Standar
```html
<div class="article-header">
  <span class="badge px-3 py-2 rounded-pill fw-semibold" style="background: rgba(22, 163, 74, 0.1); color: var(--accent-color, #16a34a); font-size: 0.82rem;">
    <i class="bi bi-tag-fill me-1"></i> [Kategori Artikel]
  </span>
  <h1>[Judul Lengkap H1 Artikel]</h1>
  
  <div class="article-meta-bar">
    <div class="d-flex align-items-center">
      <a href="../penulis.html#[slug-penulis]" class="d-inline-flex me-2">
        <img src="../assets/img/penulis/[penulis].webp" alt="[Penulis] | CorporateGifts.ID" class="rounded-circle" width="44" height="44" loading="lazy" style="object-fit:cover;">
      </a>
      <div>
        <a href="../penulis.html#[slug-penulis]" class="text-dark d-block fw-bold text-decoration-none" style="font-size: 0.88rem;">[Nama Penulis]</a>
        <span class="text-muted" style="font-size: 0.76rem;">[Jabatan / Spesialisasi Penulis]</span>
      </div>
    </div>
    <div class="text-muted ms-auto">
      <i class="bi bi-calendar3 me-1"></i> [Tanggal Publikasi] &nbsp;|&nbsp; 
      <i class="bi bi-clock me-1"></i> [N] Menit Baca
    </div>
  </div>
</div>
```

### 5. Table of Contents (TOC) Standar
```html
<div class="table-of-contents">
  <div class="d-flex justify-content-between align-items-center" id="toc-header" style="cursor: pointer; user-select: none;">
    <h2 class="m-0 d-flex align-items-center">
      <i class="bi bi-list-nested text-success me-2"></i> Daftar Isi Artikel
    </h2>
    <button type="button" class="btn btn-sm btn-light border px-2 py-1 text-muted d-inline-flex align-items-center gap-1" id="toc-toggle-btn" aria-expanded="true" aria-controls="toc-list" style="border-radius: 6px;">
      <span id="toc-btn-text">Tutup</span>
      <i class="bi bi-chevron-up" id="toc-btn-icon"></i>
    </button>
  </div>
  <div id="toc-list" class="mt-2">
    <ol class="mb-0">
      <li><a href="#section-1">Sub Judul 1</a></li>
      <li><a href="#section-2">Sub Judul 2</a></li>
    </ol>
  </div>
</div>
```

### 6. Komponen FAQ Standar (Bootstrap Accordion)
Jika artikel memuat pertanyaan/jawaban (FAQ), letakkan di atas Author Box menggunakan format resmi Bootstrap Accordion flush:
```html
<!-- ══ FAQ SECTION (Bootstrap Accordion Standard) ═══════════════════ -->
<div class="article-faq-compact my-4" id="faq-section">
  <h3 class="h6 fw-bold text-dark mb-3 d-flex align-items-center">
    <i class="bi bi-question-circle-fill text-success me-2"></i> FAQ Seputar [Topik Artikel]
  </h3>
  
  <div class="accordion accordion-flush border rounded-3 overflow-hidden bg-white shadow-sm" id="blogFaqAccordion">
    
    <div class="accordion-item border-bottom">
      <h4 class="accordion-header" id="faqHead1">
        <button class="accordion-button collapsed py-2 px-3 fw-semibold text-dark bg-white" type="button" data-bs-toggle="collapse" data-bs-target="#faqCollapse1" aria-expanded="false" aria-controls="faqCollapse1" style="font-size: 0.88rem;">
          1. [Pertanyaan 1]
        </button>
      </h4>
      <div id="faqCollapse1" class="accordion-collapse collapse" aria-labelledby="faqHead1" data-bs-parent="#blogFaqAccordion">
        <div class="accordion-body py-2 px-3 text-muted" style="line-height: 1.6; font-size: 0.84rem;">
          [Jawaban 1]
        </div>
      </div>
    </div>

    <!-- Item FAQ selanjutnya (border-bottom pada semua item kecuali item terakhir) -->

  </div>
</div>
```

---

## Alur Kerja Setiap Migrasi Artikel (Checklist 7 Langkah)

Setiap kali data artikel (baris Excel + HTML Blogger) dikirimkan, proses migrasi wajib menjalankan 7 langkah berikut secara berurutan:

```
[1. Buat blog/slug.html] 
       ↓
[2. Update blog.html] 
       ↓
[3. Update penulis.html] 
       ↓
[4. Update sitemap.xml] 
       ↓
[5. Update _redirects] 
       ↓
[6. Update llms.txt] 
       ↓
[7. Validasi & Quality Check]
```

---

### 1. Pembuatan Halaman Artikel Baru (`blog/[slug-baru].html`)

* **Lokasi File**: Selalu di dalam folder `blog/` (contoh: `blog/new-year-souvenir-kantor.html`). **DILARANG** membuat folder tanggal fisik seperti `2025/10/`.
* **Cetak Biru Desain**: 100% identik dengan standar di atas:
  1. **Breadcrumbs Bar**: Bar putih ramping (`breadcrumbs-bar py-3 bg-white`).
  2. **Article Header**: Badge kategori, judul `<h1>`, meta-bar avatar penulis bulat, tanggal, dan waktu baca.
  3. **Featured Image**: Gambar cover WEBP lokal dari `assets/img/blog/` dengan caption teks miring di bawahnya.
  4. **Table of Contents (TOC)**: Komponen TOC interaktif dengan tombol toggle Buka/Tutup.
  5. **Article Body**:
     - **Teks 100% Asli**: Menggunakan redaksi kata demi kata dari HTML Blogger tanpa parafrase.
     - **Bebas Em Dash**: Ganti semua simbol em dash (`—` dan `&mdash;`) menjadi tanda hubung standar (`-`) atau koma.
     - **Internal Linking**: Pasang tautan internal natural sesuai angka di kolom Excel `Jumlah Link` menuju halaman `../produk/*.html`, `../layanan/*.html`, atau `../index.html`.
  6. **Kotak "Baca Juga" (In-Article Callout)**: Pasang boks rekomendasi artikel internal di tengah naskah (`article-baca-juga`) dengan badge hijau.
  7. **Blog CTA Banner**: Banner RFQ standar artikel (`blog-cta-banner`) dengan tombol formulir penawaran dan WhatsApp.
  8. **FAQ Section (Bootstrap Accordion)**: Menggunakan accordion flush sesuai standar di atas.
  9. **Author Box**: Kotak profil penulis (`article-author-box`) dengan avatar bulat, jabatan, ringkasan keahlian, dan tombol menuju `../penulis.html#[slug-penulis]`.
  10. **Share Bar**: Tombol share ke WhatsApp, LinkedIn, Facebook, dan Salin Link.
  11. **Sidebar Kanan**: 3 widget standar (Kategori Produk Kami, Bantuan Pengadaan Cepat via WA, dan Unduh E-Katalog PDF).
  12. **Section Artikel Terkait (3 Rekomendasi)**: Menampilkan grid 3 kartu artikel rekomendasi sebelum `</main>`.
  13. **Footer 4 Kolom**: `footer-about`, `<h3>Halaman</h3>` (8 links), `<h3>Produk</h3>` (6 links), `<h3>Hubungi Kami</h3>`, bar Partner Network, dan Copyright.
  14. **Floating WhatsApp & Scroll-Top**: Tombol floating WA dengan tooltip dan tombol scroll-top.
* **Structured Data (JSON-LD) Lengkap**:
  1. `@type: "LocalBusiness"` & `"Organization"` (NAP lengkap Surabaya, geo, logo, sameAs medsos).
  2. `@type: "Article"` (Utama - headline, description, author, publisher, image, datePublished, dateModified).
  3. `@type: "Article"` (Ringkasan Eksekutif - `headline: "Ringkasan: ..."`, abstract untuk AI overview).
  4. `@type: "BreadcrumbList"` (Beranda > Blog > Judul Artikel).
  5. `@type: "FAQPage"` (jika artikel memuat FAQ).

---

### 2. Update Indeks Blog (`blog.html`)

* Tambahkan atau perbarui kartu artikel pada grid postingan blog:
  - Gambar cover WEBP dari `assets/img/blog/`.
  - Badge kategori artikel.
  - Judul `<h2>` yang nge-link ke `blog/[slug-baru].html`.
  - Kutipan singkat (*excerpt*) dari meta description atau snippet Excel.
  - Avatar dan nama penulis yang nge-link ke `penulis.html#[slug-penulis]`.
  - Tanggal publikasi yang sesuai.
  - Tombol *Baca Selengkapnya*.

---

### 3. Update Halaman Tim Penulis (`penulis.html`)

* Tambahkan tautan judul artikel dalam boks `📑 Artikel & Panduan yang Disusun` di profil penulis:
  ```html
  <li class="d-flex align-items-start gap-2">
    <span class="text-success fw-bold">→</span>
    <a href="blog/[slug-baru].html" class="text-dark text-decoration-none fw-medium hover-green" style="font-size: 0.95rem;">
      [Judul Lengkap Artikel]
    </a>
  </li>
  ```

---

### 4. Update Sitemap XML (`sitemap.xml`)

Tambahkan entri URL artikel baru ke dalam `sitemap.xml`:
```xml
<url>
  <loc>https://corporategifts.id/blog/[slug-baru].html</loc>
  <lastmod>YYYY-MM-DD</lastmod>
  <changefreq>monthly</changefreq>
  <priority>0.8</priority>
</url>
```

---

### 5. Update Aturan Redirect Cloudflare Pages (`_redirects`)

Tambahkan aturan 301 Permanent Redirect dari URL Blogger lama ke URL baru di file `_redirects`:
```text
# [Judul Artikel]
/[path-lama-blogger].html /blog/[slug-baru].html 301
/[slug-lama] /blog/[slug-baru].html 301
/[slug-lama]/* /blog/[slug-baru].html 301
```

---

### 6. Update Indeks Pengetahuan LLM (`llms.txt`)

Tambahkan entri artikel di bagian `## Blog & Artikel` pada file `llms.txt`:
```markdown
- [Judul Artikel](https://corporategifts.id/blog/[slug-baru].html): [Ringkasan topik dan nama penulis].
```

---

### 7. Verifikasi Kualitas Otomatis (Quality Check)

Sebelum menyatakan selesai, lakukan validasi berikut:
1. **Heading Hierarchy**: Pastikan urutan heading runtut (H1 $\rightarrow$ H2 $\rightarrow$ H3 $\rightarrow$ H4).
2. **Path Gambar & Aset**: Pastikan seluruh gambar cover, avatar penulis, dan logo berstatus 200 (ada di disk).
3. **Karakter Em Dash**: Pastikan jumlah karakter `—` dan `&mdash;` adalah 0.
4. **Validasi Schema JSON-LD**: Pastikan seluruh script JSON-LD valid dan bebas error sintaks.
5. **Jumlah Internal Link**: Pastikan jumlah link di artikel sesuai dengan nilai pada kolom Excel `Jumlah Link`.

---

## Referensi Pemetaan Penulis (Author Mapping)

| Nama Penulis di Excel | Target Anchor di `penulis.html` | Jabatan Standar | Avatar Lokal |
| :--- | :--- | :--- | :--- |
| **Arinda Zakia** | `penulis.html#arinda-zakia` | Senior Corporate Gifting Specialist & Content Strategist | `assets/img/penulis/arinda-zakia.webp` |
| **Amelia** | `penulis.html#amelia` | Creative Product Designer & Bespoke Packaging Consultant | `assets/img/penulis/amelia.webp` |
| **Vendor Souvenir Kantor** | `penulis.html#vendor-souvenir-kantor` | Editorial Team & Merchandise Production Specialist | `assets/img/penulis/vendor-souvenir-kantor.png` |
