# Standard Operating Procedure & Immutable Rules: Blog Migration

## 1. Golden Rule
**Setiap artikel blog yang dimigrasikan WAJIB 100% identik strukturnya dengan baseline referensi (`blog/cara-mengukur-efektivitas-program-recognition.html`).**
Dilarang memodifikasi class name, menghapus wrapper, mengganti format font, atau mengubah komponen HTML.

---

## 2. Standard HTML Blueprint Components

### A. `<head>` & Fonts
- Wajib memuat Google Fonts **Poppins (500, 600, 700)** dan **Inter (400, 500, 600, 700)**.
- Preload stylesheet:
  ```html
  <link rel="preload" as="style" href="https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700&family=Inter:wght@400;500;600;700&display=swap">
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" media="print" onload="this.media='all'">
  ```
- Vendor CSS:
  ```html
  <link rel="preload" href="../assets/vendor/bootstrap/css/bootstrap.min.css" as="style">
  <link rel="preload" href="../assets/css/main.min.css" as="style">
  <link href="../assets/vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet">
  <link href="../assets/css/main.min.css" rel="stylesheet">
  <link href="../assets/vendor/bootstrap-icons/bootstrap-icons.css" rel="stylesheet" media="print" onload="this.media='all'">
  <link href="../assets/vendor/aos/aos.css" rel="stylesheet" media="print" onload="this.media='all'">
  ```

### B. JSON-LD Schemas (5 Blok Wajib & Komprehensif)
1. **`LocalBusiness & Organization`**:
   - Lengkap dengan `@id: "https://corporategifts.id/#localbusiness"`, `alternateName`, `logo`, `image`, `description`, `telephone: "+62895639068080"`, `email: "info@corporategifts.id"`, `priceRange: "Rp15.000 - Rp750.000"`, `paymentAccepted: "Cash, Bank Transfer, Invoice B2B"`, `currenciesAccepted: "IDR"`, `address`, `geo`, `openingHoursSpecification`, `areaServed`, dan `sameAs`.
2. **`Article (Utama)`**:
   - `@id` berakhiran `#article`, `headline`, `image` array absolut, `datePublished`, `dateModified`, `author` (Person dengan URL profil penulis), `publisher` (Organization link `#localbusiness`), dan `inLanguage: "id-ID"`.
3. **`Article (Ringkasan Eksekutif)`**:
   - `@id` berakhiran `#summary`, headline diawali `Ringkasan: ...`, rangkuman deskripsi artikel untuk rich snippet Google & AI Overview.
4. **`BreadcrumbList`**:
   - 3 tingkat: Beranda (`https://corporategifts.id/`) -> Blog (`https://corporategifts.id/blog.html`) -> Judul Artikel (`https://corporategifts.id/blog/<slug>.html`).
5. **`FAQPage`**:
   - Array `Question` dan `Answer` yang sinkron 1:1 dengan konten Accordion FAQ pada body artikel.

### C. Body & Breadcrumbs
- Tag Body: `<body class="blog-detail-page">`
- Breadcrumbs Bar:
  ```html
  <div class="breadcrumbs-bar py-3 bg-white" style="border-bottom: 1px solid #f1f5f9;">
    <div class="container">
      <nav aria-label="breadcrumb" class="m-0 p-0" style="background: transparent;">
        <ol class="breadcrumb m-0 p-0" style="background: transparent; font-size: 0.88rem;">
          <li class="breadcrumb-item"><a href="/" style="color: var(--accent-color, #15803d); text-decoration: none; font-weight: 500;">Beranda</a></li>
          <li class="breadcrumb-item"><a href="../blog.html" style="color: var(--accent-color, #15803d); text-decoration: none; font-weight: 500;">Blog</a></li>
          <li class="breadcrumb-item active" aria-current="page" style="color: #64748b; font-weight: 500;">{Judul Pendek}</li>
        </ol>
      </nav>
    </div>
  </div>
  ```

### D. Main Article Layout
```html
<section class="py-5">
  <div class="container" data-aos="fade-up">
    <div class="row g-5">
      <div class="col-lg-8">
        <article class="article-detail-wrap">
          
          <!-- Article Header -->
          <div class="article-header">
            <span class="badge px-3 py-2 rounded-pill fw-semibold" style="background: rgba(22, 163, 74, 0.1); color: var(--accent-color, #16a34a); font-size: 0.82rem;">
              <i class="bi bi-award-fill me-1"></i> {Kategori/Badge}
            </span>
            <h1>{Judul Artikel Lengkap}</h1>
            <div class="article-meta-bar">
              <div class="d-flex align-items-center">
                <a href="../penulis.html#{author-anchor}" class="d-inline-flex me-2">
                  <img src="../assets/img/penulis/{author-img}.webp" alt="{Author} | CorporateGifts.ID" class="rounded-circle" width="44" height="44" loading="lazy" style="object-fit:cover;">
                </a>
                <div>
                  <a href="../penulis.html#{author-anchor}" class="text-dark d-block fw-bold text-decoration-none" style="font-size: 0.88rem;">{Author Name}</a>
                  <span class="text-muted" style="font-size: 0.76rem;">{Author Title}</span>
                </div>
              </div>
              <div class="text-muted ms-auto">
                <i class="bi bi-calendar3 me-1"></i> {Tanggal ID} &nbsp;|&nbsp; 
                <i class="bi bi-clock me-1"></i> {Waktu Baca} Menit Baca
              </div>
            </div>
          </div>

          <!-- Featured Image -->
          <div class="article-featured-img">
            <img src="../assets/img/blog/{featured-image}.webp" alt="{Judul} | CorporateGifts.ID" class="img-fluid" loading="lazy" width="1200" height="675">
            <p class="text-muted text-center small mt-2 fst-italic">{Caption}</p>
          </div>

          <!-- Table of Contents -->
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
                <!-- Links -->
              </ol>
            </div>
          </div>

          <!-- Article Body -->
          <div class="article-body">
            <!-- Konten dengan H2 bersesuaian dengan TOC, Callout Baca Juga, dan FAQ Flush Accordion -->
          </div>

          <!-- Bottom RFQ CTA Banner -->
          <div class="card border-0 mt-5 shadow-sm text-center text-md-start blog-cta-banner">
            <!-- CTA Content -->
          </div>

          <!-- Author Box -->
          <div class="article-author-box mt-4">
            <!-- Author Profile -->
          </div>

          <!-- Share Bar -->
          <div class="article-share-bar">
            <!-- WhatsApp, LinkedIn, Facebook, Copy Link -->
          </div>

        </article>
      </div>

      <!-- Right Column: Sidebar -->
      <div class="col-lg-4">
        <!-- 3 Widgets: Categories, Quick WA, PDF Catalog -->
      </div>
    </div>
  </div>
</section>
```

---

## 3. Mandatory 5-Step Synchronization Checklist
Setiap kali artikel baru dibuat:
1. `blog/<slug>.html` dibuat sesuai blueprint di atas.
2. `blog.html` disisipkan card artikel di grid dengan badge, thumbnail, excerpt, dan metadata (kapasitas 30 artikel per halaman).
3. `sitemap.xml` ditambahkan URL artikel lengkap dengan `<lastmod>` dan `<priority>0.8</priority>`.
4. `_redirects` ditambahkan rule 301 redirect dari URL Blogger lama.
5. `llms.txt` ditambahkan rangkuman 1 baris di bawah seksi `Blog & Artikel`.
