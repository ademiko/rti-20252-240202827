# Laporan Penelitian

**Judul:** Pengaruh Urgency Dark Pattern pada Antarmuka Aplikasi E-Commerce terhadap Tingkat Usability dan Kepercayaan Pengguna

**Peneliti:** Ade Miko (240202827)
**Target Publikasi:** Sinta 4 (Jurnal JAMI / Jurnal ahli muda indonesia)
**Status Penelitian:** Tahap 1–5 selesai

---

## 1. Ringkasan Eksekutif

Penelitian ini merancang, mengimplementasikan, dan mengevaluasi secara empiris dampak dari praktik Urgency Dark Pattern terhadap pengalaman pengguna pada aplikasi e-commerce. Evaluasi difokuskan pada penggunaan elemen manipulatif seperti hitung mundur palsu (fake countdown timer) dan confirm-shaming. Pengujian dilakukan melalui eksperimen terkontrol menggunakan metode Between-Subjects A/B Testing. Purwarupa diuji dalam dua kondisi: Kelompok Kontrol dengan antarmuka standar yang netral, dan Kelompok Perlakuan dengan antarmuka manipulatif. Eksperimen melibatkan 70 responden yang dibagi secara acak (35 per kelompok), dengan pengukuran metrik System Usability Scale (SUS) dan Trust Scale.

**Temuan utama:**

- Paparan antarmuka manipulatif menurunkan skor Usability (SUS) secara drastis, anjlok dari rata-rata 77,0 (kategori Good) menjadi 22,5 (kategori Awful).
- Integritas platform mengalami penurunan tajam di mata pengguna, ditandai dengan turunnya skor Trust Scale dari 4,11 menjadi 2,03.
- Hasil uji statistik non-parametrik (Mann-Whitney U Test) membuktikan bahwa perbedaan skor tersebut sangat signifikan secara statistik (p < 0,001) dengan ukuran efek (effect size) yang sangat besar (r = 0,86). Hal ini membuktikan secara empiris bahwa taktik manipulasi visual secara mutlak membebani kognitif pengguna.
- Ditemukan batasan riset (trade-off): Mengingat pengujian dilakukan melalui purwarupa simulasi (Figma), ancaman kerugian finansial tidak sepenuhnya nyata bagi responden. Kondisi ini berpotensi membuat effect size yang terukur sedikit lebih besar dibandingkan interaksi organik pada aplikasi sungguhan.

Seluruh desain purwarupa, data eksperimen, skrip analisis Python, tabel, dan grafik hasil visualisasi telah diintegrasikan dan tersedia di repositori penelitian.

---

## 2. Latar Belakang dan Rumusan Masalah

### 2.1 Latar Belakang

Persaingan yang semakin ketat dalam industri e-commerce memicu pergeseran pendekatan desain dari yang berpusat pada pengguna (user-centered design) menjadi desain yang cenderung eksploitatif (Dark Pattern). Pengembang platform kerap memanipulasi aspek psikologis pengguna dengan memanfaatkan taktik keterdesakan waktu (Urgency) dan kelangkaan (Scarcity). Praktik ini umumnya diimplementasikan melalui komponen batas waktu diskon palsu yang mengeksploitasi bias kognitif Fear of Missing Out (FOMO). Meskipun taktik ini diklaim mampu mencegah pembatalan transaksi secara instan, penerapannya berisiko tinggi merusak pilar utama dalam interaksi manusia dan komputer (HCI).

### 2.2 Rumusan Masalah

1. Apakah desain antarmuka e-commerce yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability yang secara signifikan lebih rendah dibandingkan antarmuka standar?
2. Apakah tingkat kepercayaan pengguna (User Trust) mengalami penurunan yang signifikan akibat intervensi antarmuka manipulatif tersebut?
3. Seberapa besar efek (besaran dampak) dari tekanan visual palsu terhadap beban kognitif pengguna saat mengeksekusi skenario pembatalan pesanan?

### 2.3 Tujuan Penelitian

Penelitian ini bertujuan untuk mengukur dan membuktikan secara kuantitatif besaran penurunan metrik Usability dan Trust akibat intervensi Dark Pattern. Hasil penelitian ini diharapkan dapat mengisi celah literatur yang selama ini lebih banyak didominasi oleh pendekatan kualitatif, sekaligus memberikan landasan empiris untuk perumusan etika desain UI/UX ke depannya.

---

## 3. Metodologi dan Pelaksanaan

Penelitian ini dilaksanakan dalam 5 tahapan yang terstruktur. Berikut adalah rangkuman implementasi dari keseluruhan proses eksperimen.

### 3.1 Tahap 1 — Perancangan Eksperimen & Variabel
**Status: Selesai.** Pendekatan yang digunakan adalah Between-Subjects A/B Testing. Variabel Independen (IV) ditetapkan sebagai Jenis Antarmuka (Standar vs Dark Pattern). Variabel Dependen (DV) dioperasionalisasikan menjadi metrik System Usability Scale (rentang skor 0-100) dan Trust Scale (skala Likert 1-5). Skenario tugas pengguna (membatalkan langganan) dikunci sebagai Variabel Kontrol (CV) untuk memastikan keadilan pengujian (fairness) bagi kedua kelompok.

### 3.2 Tahap 2 — Implementasi Purwarupa

**Status: Selesai.** Instrumen eksperimen dibangun menggunakan arsitektur modular di Figma sebagai antarmuka interaktif, yang diintegrasikan dengan Maze Platform dan Google Forms untuk otomasi perekaman data. Kelompok kontrol dihadapkan pada alur pembatalan yang linear dan netral. Sebaliknya, kelompok perlakuan dicegat oleh pop-up confirm-shaming dan elemen fake timer yang berdetak mundur.

### 3.3 Tahap 3 — Eksekusi & Pengumpulan Data

**Status: Selesai.** Distribusi tautan pengujian dilakukan melalui teknik Random Assignment guna memitigasi bias seleksi (Selection Bias). Pengumpulan data berhasil menjaring 70 partisipan independen (35 perlakuan, 35 kontrol) tanpa adanya insiden data dropout. Keseluruhan data tercatat dalam lembar kerja utama eksperimen.

### 3.4 Tahap 4 — Validasi, Ekstraksi & Analisis Data

**Status: Selesai.** Dataset mentah telah melewati proses Completeness Check dengan tingkat kelengkapan 100% dan deteksi anomali menggunakan metode Interquartile Range (IQR). Tidak ditemukan outlier yang berada di luar ambang batas kewajaran. Transformasi atau normalisasi data tidak dilakukan mengingat pengujian bersifat non-parametrik. Skrip komputasi dieksekusi menggunakan bahasa Python (pustaka Pandas dan SciPy) via Google Colab untuk menjalankan Mann-Whitney U Test.

### 3.5 Tahap 5 — Draf Naskah Jurnal

**Status: Sedang berjalan.** Naskah ilmiah telah disusun sepenuhnya menggunakan struktur IMRAD (Abstrak, Pendahuluan, Tinjauan Pustaka, Metode, Hasil, Diskusi, Kesimpulan). Matriks konsistensi alur argumen telah diverifikasi secara menyeluruh dan siap untuk proses publikasi.

---

## 4. Hasil Penelitian

## 4. Hasil Penelitian

### 4.1 Statistik Deskriptif

| Variabel Dependen | KONTROL (Mean ± Std) | DARK PATTERN (Mean ± Std) | Selisih (Delta) |
| --- | --- | --- | --- |
| Total SUS (Skor 0-100) | 77,0 ± 7,01 | 22,5 ± 6,50 | **- 54,5 poin** |
| Rata-rata Trust (Skor 1-5) | 4,11 ± 0,33 | 2,03 ± 0,39 | **- 2,08 poin** |

### 4.2 Uji Hipotesis (Mann-Whitney U Test)

| Metrik | U-Statistic | Z-Score | p-value | Effect Size (r) | Keputusan |
| --- | --- | --- | --- | --- | --- |
| Usability (SUS) | 1225,0 | 7,19 | **0,00000** | 0,86 | H1 Diterima |
| User Trust | 1225,0 | 7,19 | **0,00000** | 0,86 | H1 Diterima |

### 4.3 Visualisasi Data

| File | Deskripsi Visualisasi |
| --- | --- |
| `fig_sus_boxplot.png` | *Boxplot chart* distribusi skor SUS, menunjukkan pemisahan ekstrem tanpa adanya tumpang tindih data antara kelompok Kontrol dan *Dark Pattern*. |
| `fig_trust_boxplot.png` | *Boxplot chart* yang mengilustrasikan anjloknya variansi dan median skor Kepercayaan Pengguna (*Trust Scale*). |
| `fig_task_completion_bar.png` | *Bar chart* persentase rasio keberhasilan navigasi responden (*Task Selesai*). |

### 4.4 Interpretasi Hasil

1. Manipulasi visual secara radikal menurunkan tingkat kenyamanan pengguna. Skor SUS anjlok drastis dari rentang yang dapat diterima menjadi kategori kegagalan antarmuka (*Awful*).
2. Taktik *confirm-shaming* dan batas waktu palsu memicu *backfire effect*. Pengguna modern secara proaktif menyadari adanya niat buruk (*malicious intent*) dari platform, yang berujung pada runtuhnya kepercayaan secara absolut (p-value < 0,001).
3. Nilai *Effect Size* yang tercatat (r = 0,86) masuk dalam kategori sangat besar (*Large*), menegaskan bahwa desain antarmuka manipulatif merupakan faktor kausalitas utama yang memicu beban kognitif pada responden.

---

## 5. Evaluasi Keterbatasan (Failure Analysis)

- **Ancaman External Validity:** Eksperimen ini dioperasikan pada lingkungan simulasi berbasis purwarupa Figma. Walaupun desain dibuat menyerupai aplikasi sungguhan (*High-Fidelity*), responden menyadari bahwa tidak ada transaksi finansial nyata yang terlibat. Kondisi psikologis ini berpotensi menjadikan *effect size* yang terukur sedikit lebih besar (*overestimate*) dibandingkan dampak aktual pada aplikasi *e-commerce* komersial.
- **Deteksi Durasi Interaksi:** Pengukuran durasi navigasi (*Task Completion Time*) secara *native* di dalam Figma memiliki keterbatasan akurasi. Sebagai langkah kompensasi, pengukuran objektif didukung oleh integrasi platform pihak ketiga (Maze) dan triangulasi data kuesioner.

---

## 6. Kesimpulan dan Saran

**Kesimpulan:**

Implementasi strategi manipulasi antarmuka melalui taktik *Urgency Dark Pattern* secara empiris terbukti merusak pengalaman interaksi pengguna. Hipotesis Alternatif (H1) didukung sepenuhnya oleh data statistik. Penggunaan desain manipulatif ini menuntut *trade-off* yang merugikan: platform mungkin dapat menahan laju pembatalan pesanan untuk sesaat, namun harus menanggung kerugian jangka panjang berupa hancurnya integritas sistem, kenyamanan navigasi, dan loyalitas konsumen.

**Saran:**

Penelitian lanjutan disarankan untuk melakukan *Ablation Study* guna mengukur efektivitas dari berbagai tingkat kehalusan *Dark Pattern*. Selain itu, pemanfaatan perangkat pelacakan biometrik seperti *Eye Tracking* direkomendasikan untuk memvalidasi indikator kepanikan kognitif secara *real-time*.

---

## 7. Lampiran — Peta Artefak Penelitian

| Direktori | Isi | Status |
| --- | --- | --- |
| `01-proposal/` | Proposal penelitian dan Desain Eksperimen. | Selesai |
| `02-literatur/` | Matriks kajian literatur *Dark Pattern* dan *Usability*. | Selesai |
| `04-data/` | Data primer 70 responden dalam format spreadsheet. | Selesai |
| `05-kode/analysis/` | Skrip komputasi analisis data (Python/Jupyter). | Selesai |
| `06-output/` | Tabel statistik deskriptif dan grafik hasil visualisasi. | Selesai |
| `07-manuskrip/` | Naskah publikasi jurnal siap kirim. | Selesai |
| `08-laporan/` | Laporan akhir penelitian (dokumen ini). | Selesai |

**Cara reproduksi penuh:**


```bash
# Tahap 2: jalankan gateway (lihat 05-kode/gateway/README.md)
cd 05-kode/gateway && docker compose up -d

# Tahap 3: jalankan matrix 400 run / 40 replikasi (lihat 05-kode/k6/README.md)
cd 05-kode/k6 && ./run-matrix.sh

# Tahap 4: jalankan pipeline analisis
cd 05-kode/analysis && python run_all.py
```
