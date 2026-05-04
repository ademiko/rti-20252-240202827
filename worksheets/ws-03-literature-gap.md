# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database**: IEEE Xplore, ACM DL, Scopus, Google Scholar
2. **Boolean query** yang terdokumentasi eksplisit
3. **Snowballing**: backward (telusuri referensi) + forward (cari yang mengutip)
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Analisis Performa dan Efisiensi Modern Frontend Framework (React, Vue, Svelte, dan Next.js).
Database   : goggle scholar
Query      : Perbandingan performa ReactJS dan VueJS
Tahun      : 2023-2026
Hasil awal : 99 paper → Screening → 5 paper final

Literature Matrix (concept-centric):
```
| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|Sofi'ie |2023| Experimental|Simulasi data 20.000 baris|Vue lebih gesit merender dan jauh lebih hemat RAM dibanding React.|Hasil angka sangat dipengaruhi oleh spesifikasi perangkat keras pengujian.|
|Fakhrunnisa|2024|Scrum / Quant|Platform Talent Pool (PT XYZ)|Vue unggul di interaktivitas (INP 40ms) dan LCP tercepat (1,27 detik).|Vue unggul di interaktivitas (INP 40ms) dan LCP tercepat (1,27 detik).|
|Putra et.al|2025|Experimental|Render 1.000 item list|Svelte menang mutlak (110ms) dan ukuran file paling kecil (22KB)| Baru dites pada aplikasi web yang sangat sederhana.|
|Watung et.al| 2025|Qualitative	|Dokumentasi & Studi Komunitas| Vue paling ramah pemula, React paling kuat untuk proyek tim raksasa.|Belum melakukan pengujian teknis mandiri secara mendalam.|
|Taqiyassar|2026|Mann-Whitney U|3 Halaman Identik (Home, Ecom, News)|Next.js jauh lebih stabil dan kencang dibanding React Router (p<=> 0,05).| Pengujian masih terbatas pada skenario aplikasi testbed. |
```
Pola yang ditemukan:
  Metode dominan     : Eksperimental kuantitatif menggunakan alat benchmarking seperti Google Lighthouse dan Chrome DevTools.
  Dataset umum       : Menggunakan data riil perusahaan atau simulasi render daftar (list) dengan jumlah data besar.
  Limitasi berulang  : Hasil riset sering kali terbatas pada aplikasi sederhana atau perangkat dengan spesifikasi tinggi yang kurang mewakili pengguna umum.

GAP IDENTIFICATION

Gap 1: [Jenis: performance / method / data / context]
  Deskripsi    : Masalah overhead pada proses reconciliation Virtual DOM yang membuat performa menurun saat menangani data kompleks.
  Bukti        : React dan Vue menunjukkan waktu rendering lebih lambat (170ms & 140ms) dibanding Svelte yang tanpa Virtual DOM.
  Signifikansi : Penting untuk mengurangi latensi aplikasi pada perangkat dengan sumber daya terbatas agar tidak terjadi lag.

Gap 2: [Jenis: Context]
  Deskripsi    : Kurangnya pengujian performa framework modern pada skenario aplikasi kompleks dengan integrasi API intensif. 
  Bukti        : Mayoritas studi literatur masih menggunakan aplikasi sederhana (simple apps) sebagai objek uji coba utama.
  Signifikansi : Memastikan pemilihan teknologi tidak hanya berdasarkan popularitas, tapi benar-benar efisien untuk skala industri yang sesungguhnya

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
|ReactJS| Standar industri paling banyak dipakai untuk aplikasi enterprise.|Memiliki ekosistem paling matang dan jumlah unduhan tertinggi (12jt/minggu).|Swari et al. (2022) , Putra et al. (2025)|
VueJSL|awan tanding utama React dengan sistem reaktivitas yang lebih efisien.|Menjadi standar di banyak proyek karena kurva belajar yang ramah bagi pengembang.| Fakhrunnisa (2024) , Sofi'ie (2023).|
```

Review jurnal
| penulis (tahun) | Rumusan Masalah | Hasil & Pembahasan | kelebihan | kekurangan |
|-----------------|-----------------|--------------------|------------|-----------|
|Sofi'ie & Qoiriah (2023)|Mana yang lebih hemat RAM dan cepat saat render data ribuan baris, React atau Vue?|Vue lebih gesit dan hemat. Saat harus menampilkan sampai 20.000 baris data, Vue lebih cepat merender dan nggak makan banyak memori RAM dibanding React.|Mengetes sampai kondisi "ekstrim" (data sangat banyak) untuk melihat batas kemampuan framework.|Hasil angkanya sangat bergantung pada laptop yang dipakai saat ngetes.|
|Fakhrunnisa & Kurniawan (2024)|Gimana performa React, Vue, dan Blade kalau dipakai di satu proyek besar?|Semua punya tugas masing-masing. Blade paling cepat tampil di awal, Vue paling enak buat fitur yang banyak klik-klikannya, dan React paling stabil untuk aplikasi perusahaan yang rumit.|Risetnya pakai proyek asli di perusahaan (PT XYZ) jadi sangat nyata kasusnya.|Fitur yang dites berbeda-beda di tiap framework, jadi agak sulit membandingkan secara "apple-to-apple".|
|Putra et al. (2025)|Framework mana yang paling kencang di antara Svelte, React, dan Vue?|Svelte menang mutlak. Dia paling kencang (110ms) dan ukuran filenya paling kecil (22KB) karena kodenya langsung jadi JavaScript biasa tanpa sistem tambahan yang berat.|Menguji sampai ke cara sistem mengubah tampilan (DOM) secara sangat teliti.|Hanya dites pada aplikasi web yang sangat sederhana.  |
|Watung et al. (2025)|Dari sisi cara pakai dan kecepatan, mending pilih React atau Vue?|Vue buat pemula, React buat tim besar. Vue kodenya gampang dibaca karena mirip HTML biasa, tapi React punya bantuan (perpustakaan/komunitas) yang jauh lebih banyak untuk proyek raksasa|Membahas hal yang nggak cuma soal angka, tapi juga soal "gampang atau susahnya" dipelajari.|Kurang banyak tes teknis mandiri, lebih banyak merangkum dari riset-riset sebelumnya.|
|Taqiyassar et al. (2026)|Antara Next.js dan React Router, mana yang loading-nya lebih oke?|Next.js jauh lebih stabil. Secara statistik, Next.js jauh lebih cepat memuat gambar dan konten besar dibanding React Router, baik pakai memori sementara (cache) maupun tidak.|Metodenya sangat bagus, pakai hitungan statistik biar datanya nggak bohong.|Fokus pengujiannya cuma terbatas di tiga jenis halaman saja|

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan Google Scholar atau database lain.

**Topik riset:** Analisis Perbandingan Performa dan Efisiensi Modern Frontend Framework (React, Vue, Svelte, dan Next.js).
**Query pencarian:** Perbandingan performa ReactJS dan VueJS
**Database:** goggle scolar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Sofi'ie & Qoiriah (JINACS) | 2023 | Eksperimental (Benchmarking) | Aplikasi tabel (1.000 - 20.000 baris) | Vue lebih responsif dan hemat RAM dibanding React pada data besar | Hasil sangat bergantung pada spesifikasi perangkat keras pengujian |
| 2 | Fakhrunnisa & Kurniawan|2024 |Kuantitatif |Modul Talent Pool Platform terintegrasi |Vue unggul di interaktivitas (INP 40ms) dan LCP real-time (1,27s) |Modul memiliki fungsi berbeda, sehingga memicu variasi hasil |
| 3 |Putra et al. (Brilliance) |2025 |Controlled Experimental |Aplikasi web identik (render 1.000 item) |Svelte paling unggul di semua metrik (render 110ms, bundle 22KB) |Hasil hanya valid untuk konteks aplikasi web yang sederhana|
| 4 |Watung et al. (Kohesi)|2025 |Kualitatif |Studi literatur |Vue lebih ramah pemula; React lebih fleksibel untuk proyek besar|Belum melakukan pengujian teknis mandiri yang mendalam |
| 5 |Taqiyassar et al. (J-PTIIK) |2026 |Eksperimental & Statistik |Tiga halaman identik (Home, Ecommerce, News) |Next.js konsisten lebih stabil dan efisien dibanding React Router (p <= 0,05) |Pengujian masih terbatas pada skenario aplikasi testbed|

**Pola yang terlihat — Metode dominan:**Pendekatan eksperimental kuantitatif dengan melakukan benchmarking menggunakan alat ukur standar seperti Google Lighthouse dan Chrome DevTools.
**Limitasi yang berulang:** Sebagian besar penelitian masih menggunakan aplikasi uji coba sederhana (testbed atau simple apps) dan hasilnya sering kali sangat terikat pada spesifikasi perangkat keras tertentu yang digunakan saat pengujian.

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap |  Ya | Meskipun framework berbasis Virtual DOM (React dan Vue) umum digunakan, terdapat masalah overhead memori dan proses rendering yang lebih tinggi dibandingkan dengan pendekatan compile-time seperti Svelte. |
| Method Gap |  Ya  |Studi komparatif sistematis yang membandingkan performa teknis antara framework terbaru seperti Next.js 15 dan React Router v7 secara langsung masih sangat terbatas.|
| Data Gap |  Ya  |Data empiris yang membandingkan berbagai framework modern secara langsung di bawah kondisi eksperimental yang setara masih tergolong minim. |
| Context Gap |  Ya  |Mayoritas pengujian masih berfokus pada aplikasi web sederhana (simple applications) dan belum banyak menguji performa pada skenario aplikasi kompleks dengan integrasi API intensif. |

**Gap utama yang dipilih:** Data & Context Gap 
Keterbatasan pengujian pada aplikasi kompleks dan lingkungan dengan sumber daya terbatas.
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Hal ini sangat penting karena efisiensi teknis sebuah framework memiliki dampak langsung pada pengalaman pengguna, terutama bagi mereka yang menggunakan perangkat dengan spesifikasi rendah atau berada di lingkungan dengan jaringan internet terbatas. Tanpa data empiris yang komprehensif pada aplikasi skala besar, pengembang berisiko memilih teknologi yang terlihat cepat di tahap awal namun tidak efisien atau justru menyebabkan lag dan crash saat menangani data yang kompleks di dunia nyata.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | React (ReactJS)| Merupakan standar industri paling populer untuk membangun UI berbasis komponen. | Diadopsi secara global oleh komunitas pengembang besar dan menjadi tolok ukur utama dalam banyak studi. | Ya, merupakan standar industri yang matang. | Putra et al., 2025 |
| 2 |Vue (VueJS)|Sering dibandingkan langsung dengan React karena fleksibilitas dan efisiensinya pada aplikasi skala menengah.|Mewakili praktik umum (common practice) karena kemudahan integrasinya dan performa responsivitas yang tinggi. |Ya, merupakan salah satu framework modern terbaik saat ini.|Fakhrunnisa & Kurniawan, 2024 |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [x] Tidak
> Justifikasi:cMemasukkan React dan Vue sebagai baseline bukanlah bentuk straw man comparison karena keduanya adalah pemain besar yang kinerjanya sudah diakui di industri global saat ini. Justru karena mereka memiliki ekosistem yang matang, stabil, dan banyak digunakan di aplikasi skala besar, mereka menjadi lawan tanding yang sangat kompetitif untuk menguji apakah teknologi baru seperti Svelte atau Next.js benar-benar membawa perubahan yang signifikan secara teknis. Dengan membandingkan metode baru terhadap standar industri yang kuat, hasil penelitian ini menjadi lebih valid secara ilmiah karena peningkatan performa yang ditemukan bukan didapat dari membandingkan dengan metode yang sengaja dibuat lemah.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Perbedaan utama antara asal mengeklaim "belum ada yang meneliti ini" dengan research gap yang benar terletak pada proses audit literaturnya yang sistematis. Research gap yang valid muncul setelah kita membedah karya orang lain secara mendalam melalui Literature Mapping, di mana kita bisa menunjukkan secara konkret variabel, metrik, atau batasan apa yang belum tersentuh oleh peneliti terdahulu. Cara membuktikannya adalah dengan menyajikan bukti pencarian yang terdokumentasi, sehingga celah penelitian tersebut memiliki dasar yang kuat dan bisa diuji kembali oleh orang lain.
> 
