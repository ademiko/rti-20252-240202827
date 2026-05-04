# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : ____________________

Research Question:
  Tipe         : [x] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah penggunaan framework Next.js menghasilkan nilai metrik Largest Contentful Paint (LCP) yang secara signifikan lebih rendah dibandingkan React Router v7 pada skenario halaman web E-commerce yang memuat aset gambar berukuran rata-rata 2MB per item?
  Variabel IV  : Jenis framework website yang digunakan (Next.js vs React Router v7)
  Variabel DV  : Performa kecepatan pemuatan konten utama (Largest Contentful Paint)
  Metrik       : Waktu pemuatan dalam satuan milidetik (ms)
  Dataset      : Aplikasi testbed berupa halaman E-commerce dengan beban aset gambar 2MB per item
  Baseline     : React Router v7

Quality Check RQ:
  [x] Variabel spesifik
  [x] Metrik jelas
  [x] Baseline ada
  [x] Konteks disebutkan
  [xx] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Bukti empiris terukur mengenai efisiensi strategi rendering antara Next.js dan React Router pada kondisi riil dengan beban aset gambar yang berat
  Jenis kontribusi        : [ ] Improvement  [x] Comparison  [ ] Novel approach
  Gap yang diisi          : Context Gap dan Method Gap terkait perbandingan performa framework modern pada skenario aplikasi skala besar

Hypothesis Pair:
  H₀ : Tidak ada perbedaan yang signifikan pada nilai metrik Largest Contentful Paint (LCP) antara penggunaan Next.js dan React Router pada skenario halaman web E-commerce dengan beban aset gambar 2MB per item
  H₁ : Penggunaan Next.js menghasilkan nilai metrik Largest Contentful Paint (LCP) yang secara signifikan lebih rendah (lebih cepat) dibandingkan React Router pada skenario halaman web E-commerce dengan beban aset gambar 2MB per item
  Threshold              : Nilai signifikansi (p-value) <= 0,05
  Justifikasi threshold  : Tingkat signifikansi 5% merupakan standar pengujian statistik inferensial (seperti uji Mann-Whitney U) dalam riset Informatika untuk menolak H₀ secara meyakinkan, sehingga perbedaan performa dipastikan valid dan bukan sekadar kebetulan
```

---
Melanjutkan dari literatur gap ws 3, di mana pengujian framework modern masih banyak yang terbatas pada aplikasi sederhana dan belum menguji kondisi riil dengan beban aset yang besar. Pada WS-04, akan menarik gap tersebut menjadi sebuah rumusan masalah (Research Question) dan hipotesis yang solid. Tujuannya adalah agar celah penelitian yang sudah ditemukan bisa dieksekusi menjadi eksperimen yang spesifik, terukur, dan dapat dibuktikan kebenarannya secara statistik. 
---
## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Minimnya pengujian empiris dan perbandingan performa teknis secara langsung antara framework terbaru (Next.js vs React Router) pada skenario aplikasi kompleks dengan beban aset yang besar (heavy assets).

**RQ versi pertama (tulis bebas):**
> Bagaimana perbandingan performa kecepatan antara Next.js dan React Router kalau dipakai untuk membuat halaman website dengan banyak gambar dan video berukuran besar?
**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | ya |Komparasi strategi rendering antara Next.js dan React Router. |
| Metrik terukur |tidak |Hanya menyebut "performa kecepatan" (belum ada metrik spesifik seperti FCP atau LCP) |
| Baseline | ya |React Router v7. |
| Dataset/konteks | sebagian | "Website dengan banyak gambar dan video" masih terlalu ambigu dan belum terukur. |

**Tipe RQ:** [x] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah penggunaan framework Next.js menghasilkan nilai metrik Largest Contentful Paint (LCP) yang secara signifikan lebih rendah (lebih cepat) dibandingkan React Router v7 pada skenario halaman web E-commerce yang memuat aset gambar berukuran rata-rata 2MB per item?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak ada perbedaan yang signifikan pada nilai metrik Largest Contentful Paint (LCP) antara penggunaan framework Next.js dan React Router pada skenario halaman web E-commerce dengan beban aset gambar 2MB per item. |
| H₁ | Penggunaan framework Next.js menghasilkan nilai metrik Largest Contentful Paint (LCP) yang secara signifikan lebih rendah (lebih cepat) dibandingkan React Router pada skenario halaman web E-commerce dengan beban aset gambar 2MB per item. |
| Metrik | Waktu Largest Contentful Paint (LCP) yang diukur dalam satuan milidetik (ms). |
| Threshold | Nilai signifikansi (p-value) <= 0,05. |
| Justifikasi threshold | Tingkat signifikansi 5% (a(alpha) = 0,05) merupakan standar pengujian statistik inferensial (seperti uji Mann-Whitney U) dalam riset Informatika. Batas ini digunakan untuk menolak hipotesis nol (H0) secara meyakinkan dan memastikan bahwa perbedaan performa yang terjadi bukan sekadar kebetulan. |

**Apakah hipotesis ini falsifiable?** [x] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? 
> Dengan mengumpulkan data waktu LCP dari kedua framework lalu menjalankan uji statistik non-parametrik Mann-Whitney U. Jika hasil perhitungan menunjukkan p-value > 0,05, maka H0 gagal ditolak. Hal ini secara otomatis akan membuktikan bahwa klaim H1 (bahwa Next.js lebih cepat) adalah salah atau tidak terbukti secara statistik pada skenario tersebut.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah penggunaan framework Next.js menghasilkan nilai metrik Largest Contentful Paint (LCP) yang secara signifikan lebih rendah dibandingkan React Router v7 pada skenario halaman E-commerce dengan aset gambar 2MB? |
| Variable (IV) | Jenis framework website yang diuji (Next.js vs. React Router v7) |
| Variable (DV) | Performa kecepatan pemuatan konten utama (Largest Contentful Paint). |
| Metric | Waktu pemuatan dalam satuan milidetik (ms) |
| Data source | Data hasil pengujian otomatis pada aplikasi testbed yang dikumpulkan melalui tools WebPageTest |
| Analysis method | Analisis statistik deskriptif (rata-rata/standar deviasi) dan uji inferensial Mann-Whitney U untuk menentukan tingkat signifikansi. |

**Apakah rantai lengkap?** [x] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? (Sudah lengkap, karena semua tahapan dari variabel hingga metode analisis sudah saling terhubung secara logis dan siap untuk dieksekusi dalam eksperimen).

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Analisis Perbandingan Performa Framework Website Next.js dan React Router.
**RQ yang diekstrak:** Apakah terdapat perbedaan signifikan pada metrik Largest Contentful Paint (LCP) antara Next.js dan React Router v7 pada skenario halaman E-commerce dengan aset gambar 2MB?.
**Komponen yang hilang:** Secara teknis, RQ ini sudah memenuhi semua komponen inti karena mencakup metode (perbandingan framework), metrik (LCP), baseline (React Router), dan konteks (halaman E-commerce dengan aset 2MB). Namun, jika dilihat dari sisi operasional, hal yang sering "tersembunyi" atau tidak disebutkan langsung di kalimat RQ adalah threshold signifikansi statistik (seperti penggunaan alpha = 0,05) dan alat uji spesifik yang digunakan (misalnya uji Mann-Whitney U). Tanpa penyebutan ambang batas ini, pembaca hanya tahu apa yang diukur, tapi tidak tahu standar apa yang digunakan untuk menyatakan bahwa perbedaan tersebut benar-benar signifikan secara ilmiah.
