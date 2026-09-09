# SOP & Panduan Lengkap Migrasi Artikel Blog
**Project**: CorporateGifts.ID  
**Target Hosting**: Cloudflare Pages  
**Template Acuan**: `blog/souvenir-dosen-penguji-skripsi-hemat.html` / `blog/proses-custom-apparel-perusahaan.html`

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

* **Lokasi File**: Selalu di dalam folder `blog/` (contoh: `blog/panduan-menyusun-seminar-kit.html`). **DILARANG** membuat folder tanggal fisik seperti `2025/09/`.
* **Cetak Biru Desain**: 100% identik dengan `blog/souvenir-dosen-penguji-skripsi-hemat.html`:
  1. **Breadcrumbs Bar**: Bar putih ramping (`breadcrumbs-bar py-3 bg-white`) dengan border bawah halus.
  2. **Article Header**: Badge kategori (`badge rounded-pill fw-semibold`), judul `<h1>`, meta-bar avatar penulis bulat, nama penulis (link ke `../penulis.html#[slug-penulis]`), tanggal publikasi, dan estimasi waktu baca.
  3. **Featured Image**: Gambar cover WEBP lokal dari `assets/img/blog/` dengan caption teks miring di bawahnya.
  4. **Table of Contents (Daftar Isi)**: Komponen TOC interaktif dengan tombol toggle Buka/Tutup.
  5. **Article Body**:
     - **Teks 100% Asli**: Menggunakan redaksi kata demi kata dari HTML Blogger tanpa parafrase, tanpa tambahan boks summary buatan, dan tanpa tabel buatan di luar naskah asli.
     - **Bebas Em Dash**: Ganti semua simbol em dash (`—` dan `&mdash;`) menjadi tanda hubung standar (`-`) atau koma.
     - **Internal Linking**: Pasang tautan internal natural sesuai angka di kolom Excel `Jumlah Link` menuju halaman `../produk/*.html`, `../layanan/*.html`, atau `../index.html`.
  6. **Kotak "Baca Juga" (In-Article Callout)**: Pasang boks rekomendasi artikel internal di tengah naskah (`article-baca-juga`) dengan badge hijau dan tautan ke artikel terkait lainnya.
  7. **Blog CTA Banner**: Banner RFQ standar artikel (`blog-cta-banner`) dengan tombol formulir penawaran dan WhatsApp.
  8. **FAQ Section (Bootstrap Accordion)**: Jika ada FAQ di naskah asli, letakkan tepat di atas author box menggunakan accordion Bootstrap flush (`article-faq-compact my-4`) berstandar `blog/panduan-menyusun-seminar-kit.html`.
  9. **Author Box**: Kotak profil penulis (`article-author-box`) dengan avatar bulat, jabatan, ringkasan keahlian, dan tombol menuju `../penulis.html#[slug-penulis]`.
  10. **Share Bar**: Tombol share ke WhatsApp, LinkedIn, Facebook, dan Salin Link.
  11. **Sidebar Kanan**: 3 widget standar (Kategori Produk Kami, Bantuan Pengadaan Cepat via WA, dan Unduh E-Katalog PDF).
  12. **Section Artikel Terkait (3 Rekomendasi)**: Pasang section `<!-- ══ SECTION: ARTIKEL TERKAIT ══ -->` tepat di bagian bawah sebelum `</main>` yang menampilkan grid 3 kartu artikel rekomendasi lainnya.
  13. **Footer**: Footer standar tanpa komponen CTA tambahan di luar artikel.
* **Structured Data (JSON-LD)**:
  - `@type: "Article"` (headline, description, author Person/Organization, image, datePublished, dateModified).
  - `@type: "BreadcrumbList"` (Beranda > Blog > Judul Artikel).
  - `@type: "FAQPage"` (jika artikel memuat FAQ).
* **CSS & Design Consistency**: Wajib menyertakan blok `<style>` standar artikel di dalam `<head>` (mengatur `.blog-cta-banner`, `.blog-cta-actions`, `.article-baca-juga`, `.table-of-contents`, `.article-author-box`, `.article-faq-compact`, dll.) agar ukuran kartu CTA, padding, border radius (16px), gradien hijau, dan tata letak responsif seragam 100% dengan artikel acuan.

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

* **List Artikel Penulis**: Tambahkan tautan judul artikel dalam boks `📑 Artikel & Panduan yang Disusun` langsung di dalam kartu profil penulis yang bersangkutan (`#arinda-zakia`, `#vendor-souvenir-kantor`, dll.):
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
1. **Heading Hierarchy**: Pastikan urutan heading runtut (H1 $\rightarrow$ H2 $\rightarrow$ H3 $\rightarrow$ H4) tanpa ada level yang terlewat.
2. **Path Gambar & Aset**: Pastikan seluruh gambar cover, avatar penulis, dan logo berstatus 200 (ada di disk).
3. **Karakter Em Dash**: Pastikan jumlah karakter `—` dan `&mdash;` adalah 0.
4. **Validasi Schema JSON-LD**: Pastikan seluruh script JSON-LD valid dan bebas error sintaks.
5. **Jumlah Internal Link**: Pastikan jumlah link di artikel sesuai dengan nilai pada kolom Excel `Jumlah Link`.

---

## Referensi Pemetaan Penulis (Author Mapping)

| Nama Penulis di Excel | Target Anchor di `penulis.html` | Avatar Lokal |
| :--- | :--- | :--- |
| **Arinda Zakia** | `penulis.html#arinda-zakia` | `assets/img/penulis/arinda-zakia.webp` |
| **Vendor Souvenir Kantor** | `penulis.html#vendor-souvenir-kantor` | `assets/img/penulis/vendor-souvenir-kantor.png` |
| **Amelia** | `penulis.html#amelia` | `assets/img/penulis/amelia.webp` |
