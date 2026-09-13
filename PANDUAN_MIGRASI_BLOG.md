# SOP & Panduan Lengkap Migrasi Artikel Blog
**Project**: CorporateGifts.ID  
**Target Hosting**: Cloudflare Pages  
**Template Acuan**: `blog/souvenir-kantor-pajak.html` (Artikel #56) & `blog/tren-seminar-kit-korporat-terbaru-2026.html` (Artikel #57)

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

### 3. Header Navigasi Standar Lengkap
```html
  <!-- ══ HEADER ════════════════════════════════════════════════════════════════ -->
  <header id="header" class="header d-flex align-items-center sticky-top">
    <div class="container position-relative d-flex align-items-center justify-content-between">

      <a href="/" class="logo d-flex align-items-center me-auto me-xl-0">
        <img src="../assets/img/logo-header.png" alt="CorporateGifts.ID - Vendor Corporate Gift &amp; Souvenir Perusahaan"
          style="max-height:40px;width:auto;" width="214" height="40" loading="lazy">
      </a>

      <nav id="navmenu" class="navmenu mx-xl-auto">
        <ul>
          <li><a href="/">Beranda</a></li>
          <li><a href="../tentang-kami.html">Tentang Kami</a></li>
          <li><a href="../layanan.html">Layanan</a></li>
          <li><a href="../katalog.html">Katalog</a></li>
          <li><a href="../portofolio.html">Portofolio</a></li>
          <li class="dropdown">
            <a href="../produk.html"><span>Produk</span> <i class="bi bi-chevron-down toggle-dropdown"></i></a>
            <ul>
              <li><a href="../produk/souvenir-kantor.html">Souvenir Kantor</a></li>
              <li><a href="../produk/souvenir-custom.html">Souvenir Custom</a></li>
              <li><a href="../produk/merchandise.html">Merchandise Perusahaan</a></li>
              <li><a href="../produk/seminar-kit.html">Seminar Kit</a></li>
              <li><a href="../produk/hampers.html">Hampers &amp; Parcel</a></li>
              <li><a href="../produk/souvenir-promosi.html">Paket Souvenir Promosi</a></li>
            </ul>
          </li>
          <li><a href="../blog.html" class="active">Blog</a></li>
          <li><a href="../galeri.html">Galeri</a></li>
        </ul>
        <i class="mobile-nav-toggle d-xl-none bi bi-list"></i>
      </nav>

      <a class="btn-getstarted"
        href="https://wa.me/62895639068080?text=Halo%2C%20saya%20ingin%20konsultasi%20souvenir%20kantor%20perusahaan" target="_blank"
        rel="noopener">
        <i class="bi bi-whatsapp me-1"></i> Hubungi Kami
      </a>

    </div>
  </header>
```

### 4. Breadcrumbs Bar Standar
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

### 5. Article Header & Meta Bar Standar
```html
<div class="article-header">
  <span class="badge px-3 py-2 rounded-pill fw-semibold" style="background: rgba(22, 163, 74, 0.1); color: var(--accent-color, #16a34a); font-size: 0.82rem;">
    <i class="bi bi-tag-fill me-1"></i> [Kategori Artikel]
  </span>
  <h1>[Judul Lengkap H1 Artikel]</h1>
  
  <div class="article-meta-bar">
    <div class="d-flex align-items-center">
      <a href="../penulis.html#[slug-penulis]" class="d-inline-flex me-2">
        <img src="../assets/img/penulis/[slug-penulis].webp" alt="[Penulis] | CorporateGifts.ID" class="rounded-circle" width="44" height="44" loading="lazy" style="object-fit:cover;">
      </a>
      <div>
        <a href="../penulis.html#[slug-penulis]" class="text-dark d-block fw-bold text-decoration-none" style="font-size: 0.88rem;">[Nama Penulis]</a>
        <span class="text-muted" style="font-size: 0.76rem;">[Jabatan / Spesialisasi Penulis]</span>
      </div>
    </div>
    <div class="text-muted ms-auto">
      <i class="bi bi-calendar3 me-1"></i> [Tanggal Update dari Excel] &nbsp;|&nbsp; 
      <i class="bi bi-clock me-1"></i> [N] Menit Baca
    </div>
  </div>
</div>
```
*(Catatan: Tanggal yang digunakan selalu mengambil nilai dari kolom **Tanggal Update** / kolom sebelah kanan di Excel).*

### 6. Table of Contents (TOC) Standar
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

### 7. Kotak Poin Kunci & Callout Baca Juga
```html
<!-- Box Poin Kunci / Ringkasan Eksekutif -->
<div class="article-key-points">
  <h3 class="h6 fw-bold text-dark mb-2"><i class="bi bi-lightbulb-fill text-success me-2"></i> Poin Kunci [Topik]:</h3>
  <ul class="mb-0 small text-muted ps-3" style="line-height: 1.7;">
    <li><strong>[Label 1]:</strong> [Deskripsi 1]</li>
    <li><strong>[Label 2]:</strong> [Deskripsi 2]</li>
  </ul>
</div>

<!-- Strip Callout Baca Juga -->
<div class="article-baca-juga">
  <span class="badge bg-success text-white px-2 py-1 rounded-pill small fw-bold">Baca Juga</span>
  <a href="[slug-artikel-terkait].html" class="hover-green">[Judul Artikel Terkait] <i class="bi bi-arrow-right ms-1"></i></a>
</div>
```

### 8. Tabel Responsif Standar
```html
<div class="tbl-wrap">
  <table class="tbl-corporategifts">
    <thead>
      <tr>
        <th>Kolom 1</th>
        <th>Kolom 2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td data-label="Kolom 1">Data 1</td>
        <td data-label="Kolom 2">Data 2</td>
      </tr>
    </tbody>
  </table>
</div>
```

### 9. Komponen FAQ Standar (Bootstrap Accordion)
```html
<div class="article-faq-compact my-4" id="faq-section">
  <h3 class="h5 fw-bold text-dark mb-3"><i class="bi bi-question-circle-fill text-success me-2"></i> Pertanyaan Seputar [Topik] (FAQ)</h3>
  <div class="accordion accordion-flush" id="blogFaqAccordion">

    <div class="accordion-item border-bottom">
      <h4 class="accordion-header" id="faqHead1">
        <button class="accordion-button collapsed py-2 px-3 fw-semibold text-dark bg-white" type="button"
          data-bs-toggle="collapse" data-bs-target="#faqCollapse1" aria-expanded="false"
          aria-controls="faqCollapse1" style="font-size: 0.88rem;">
          1. [Pertanyaan 1]
        </button>
      </h4>
      <div id="faqCollapse1" class="accordion-collapse collapse" aria-labelledby="faqHead1"
        data-bs-parent="#blogFaqAccordion">
        <div class="accordion-body py-2 px-3 text-muted" style="line-height: 1.6; font-size: 0.84rem;">
          [Jawaban 1]
        </div>
      </div>
    </div>

    <!-- FAQ Item selanjutnya (border-bottom pada semua item kecuali item terakhir) -->

  </div>
</div>
```

### 10. Bottom RFQ CTA Banner & Author Box
```html
<!-- Bottom RFQ CTA Banner -->
<div class="card border-0 mt-5 shadow-sm text-center text-md-start blog-cta-banner">
  <div class="d-flex flex-column flex-md-row align-items-center justify-content-between gap-3">
    <div>
      <h3 class="h5 fw-bold text-dark mb-1">[Judul CTA Pengadaan]</h3>
      <p class="small text-muted mb-0">Dapatkan katalog resmi 2026, sampel mockup digital gratis, dan penawaran harga B2B terbaik yang lengkap dengan faktur pajak.</p>
    </div>
    <div class="blog-cta-actions flex-shrink-0">
      <a href="../minta-penawaran.html" class="btn btn-success rounded-pill px-4 py-2 fw-semibold" style="background: var(--accent-color, #16a34a); border-color: var(--accent-color, #16a34a);">
        <i class="bi bi-pencil-square me-1"></i> Minta Penawaran
      </a>
      <a href="https://wa.me/62895639068080?text=Halo%20CorporateGifts.ID,%20saya%20ingin%20konsultasi" target="_blank" rel="noopener" class="btn btn-outline-success rounded-pill px-3 py-2 fw-semibold">
        <i class="bi bi-whatsapp me-1"></i> WhatsApp CS
      </a>
    </div>
  </div>
</div>

<!-- Author Box -->
<div class="article-author-box mt-4">
  <a href="../penulis.html#[slug-penulis]" class="flex-shrink-0 me-3">
    <img src="../assets/img/penulis/[slug-penulis].webp" alt="[Nama Penulis] | CorporateGifts.ID" width="90" height="90" loading="lazy" class="rounded-circle shadow-sm" style="object-fit:cover;">
  </a>
  <div>
    <h3 class="h6 fw-bold text-dark mb-1">
      Ditulis oleh: <a href="../penulis.html#[slug-penulis]" class="text-dark text-decoration-none hover-green">[Nama Penulis]</a>
    </h3>
    <span class="badge bg-success-subtle text-success px-2 py-1 rounded-pill small fw-semibold mb-2 d-inline-block">[Spesialisasi]</span>
    <p class="small text-muted mb-2">
      [Bio Penulis]
    </p>
    <a href="../penulis.html#[slug-penulis]" class="text-success small fw-semibold text-decoration-none">
      Lihat Profil Lengkap &amp; Panduan Lainnya <i class="bi bi-arrow-right ms-1"></i>
    </a>
  </div>
</div>

<!-- Share Bar -->
<div class="article-share-bar">
  <div class="fw-semibold small text-dark">Bagikan Artikel Ini:</div>
  <div class="article-share-buttons">
    <a href="https://api.whatsapp.com/send?text=[Judul]%20https://corporategifts.id/blog/[slug].html" target="_blank" rel="noopener" class="btn-share btn-wa" aria-label="Share via WhatsApp"><i class="bi bi-whatsapp"></i></a>
    <a href="https://www.linkedin.com/sharing/share-offsite/?url=https://corporategifts.id/blog/[slug].html" target="_blank" rel="noopener" class="btn-share btn-li" aria-label="Share on LinkedIn"><i class="bi bi-linkedin"></i></a>
    <a href="https://www.facebook.com/sharer/sharer.php?u=https://corporategifts.id/blog/[slug].html" target="_blank" rel="noopener" class="btn-share btn-fb" aria-label="Share on Facebook"><i class="bi bi-facebook"></i></a>
    <button onclick="navigator.clipboard.writeText(window.location.href); alert('Tautan artikel berhasil disalin!');" class="btn-share btn-copy border-0" aria-label="Copy Link"><i class="bi bi-link-45deg"></i></button>
  </div>
</div>
```

### 11. Sidebar Kanan (3 Widget Standar Wajib)
```html
<div class="col-lg-4">
  <div class="sidebar position-sticky" style="top: 100px;">

    <!-- Widget 1: Kategori Produk Terkait -->
    <div class="card border-0 rounded-4 p-4 shadow-sm bg-white mb-4">
      <h3 class="h6 fw-bold text-dark mb-3"><i class="bi bi-grid-fill text-success me-2"></i> Kategori Produk Kami</h3>
      <ul class="list-unstyled mb-0" style="font-size: 0.92rem;">
        <li class="py-2 border-bottom"><a href="../produk/souvenir-kantor.html" class="text-decoration-none text-dark d-flex justify-content-between"><span>Souvenir Kantor</span> <i class="bi bi-chevron-right text-muted"></i></a></li>
        <li class="py-2 border-bottom"><a href="../produk/souvenir-custom.html" class="text-decoration-none text-dark d-flex justify-content-between"><span>Souvenir Custom VIP</span> <i class="bi bi-chevron-right text-muted"></i></a></li>
        <li class="py-2 border-bottom"><a href="../produk/merchandise.html" class="text-decoration-none text-dark d-flex justify-content-between"><span>Merchandise Perusahaan</span> <i class="bi bi-chevron-right text-muted"></i></a></li>
        <li class="py-2 border-bottom"><a href="../produk/seminar-kit.html" class="text-decoration-none text-dark d-flex justify-content-between"><span>Paket Seminar Kit</span> <i class="bi bi-chevron-right text-muted"></i></a></li>
        <li class="py-2 border-bottom"><a href="../produk/hampers.html" class="text-decoration-none text-dark d-flex justify-content-between"><span>Hampers &amp; Parcel</span> <i class="bi bi-chevron-right text-muted"></i></a></li>
        <li class="pt-2"><a href="../produk/souvenir-promosi.html" class="text-decoration-none text-dark d-flex justify-content-between"><span>Souvenir Promosi</span> <i class="bi bi-chevron-right text-muted"></i></a></li>
      </ul>
    </div>

    <!-- Widget 2: Bantuan Konsultasi Kilat -->
    <div class="card border-0 rounded-4 p-4 text-center shadow-sm" style="background: color-mix(in srgb, var(--accent-color, #16a34a) 8%, transparent);">
      <div class="mx-auto mb-3 text-success fs-1">
        <i class="bi bi-headset"></i>
      </div>
      <h3 class="h6 fw-bold text-dark mb-2">Bantuan Konsultasi Kilat</h3>
      <p class="small text-muted mb-3">Diskusikan kebutuhan souvenir kantor, seminar kit, dan penawaran resmi bersama kami.</p>
      <div class="fw-bold text-success fs-6 mb-3">+62 895-6390-68080</div>
      <a href="https://wa.me/62895639068080?text=Halo%20CorporateGifts.ID,%20saya%20ingin%20konsultasi" target="_blank" rel="noopener" class="btn btn-success rounded-pill w-100 py-2 fw-semibold" style="background: var(--accent-color, #16a34a); border-color: var(--accent-color, #16a34a);">
        <i class="bi bi-whatsapp me-1"></i> Chat WhatsApp Sekarang
      </a>
    </div>

    <!-- Widget 3: Unduh Katalog PDF -->
    <div class="card border-0 rounded-4 p-4 shadow-sm bg-white mt-4 text-center">
      <i class="bi bi-file-earmark-pdf text-danger fs-1 mb-2"></i>
      <h3 class="h6 fw-bold text-dark mb-2">E-Katalog Resmi 2026</h3>
      <p class="small text-muted mb-3">Unduh dokumen katalog resmi lengkap dengan aneka pilihan merchandise instansi, seminar kit, dan gift set siap custom logo.</p>
      <a href="../assets/docs/katalog-corporategifts-id.pdf" download="Katalog-CorporateGifts-ID-2026.pdf" target="_blank" rel="noopener" class="btn btn-outline-dark rounded-pill w-100 py-2 small fw-semibold">
        <i class="bi bi-download me-1"></i> Unduh Katalog (PDF)
      </a>
    </div>

  </div>
</div>
```

### 12. Section Rekomendasi Artikel Terkait (3 Kartu)
```html
<section class="py-5 bg-light border-top">
  <div class="container" data-aos="fade-up">
    <div class="d-flex flex-wrap justify-content-between align-items-center mb-4 gap-2">
      <div>
        <span class="text-uppercase fw-bold small text-success" style="letter-spacing:1px;">Rekomendasi Wawasan</span>
        <h2 class="h3 fw-bold text-dark mb-0 mt-1">Artikel Terkait Lainnya</h2>
      </div>
      <a href="../blog.html" class="btn btn-sm btn-outline-success rounded-pill px-3 py-2 fw-semibold">
        Lihat Semua Artikel <i class="bi bi-arrow-right ms-1"></i>
      </a>
    </div>
    <div class="row g-4">
      <!-- Card 1, 2, 3 dengan badge position-relative, cover img, excerpt, dan author footer -->
    </div>
  </div>
</section>
```

---

## Alur Kerja Setiap Migrasi Artikel (Checklist 5 Langkah Wajib)

```
[1. Buat blog/<slug>.html] 
       ↓
[2. Update blog.html (urut tanggal update kronologis)] 
       ↓
[3. Update sitemap.xml] 
       ↓
[4. Update _redirects] 
       ↓
[5. Update llms.txt] 
```

---

## Referensi Pemetaan Penulis (Author Mapping)

| Nama Penulis di Excel | Target Anchor di `penulis.html` | Jabatan Standar | Avatar Lokal |
| :--- | :--- | :--- | :--- |
| **Arinda Zakia** | `penulis.html#arinda-zakia` | Senior Corporate Gifting Specialist & Content Strategist | `../assets/img/penulis/arinda-zakia.webp` |
| **Amelia** | `penulis.html#amelia` | Creative Product Designer & Bespoke Packaging Consultant | `../assets/img/penulis/amelia.webp` |
| **Vendor Souvenir Kantor** | `penulis.html#vendor-souvenir-kantor` | Editorial Team & Merchandise Production Specialist | `../assets/img/penulis/vendor-souvenir-kantor.png` |
