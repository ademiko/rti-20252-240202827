# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi


VARIABLE & METRIC DEFINITION

Research Question: Apakah desain antarmuka yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
| Jenis Antarmuka | IV | Desain manipulatif | Kategori (Normal vs Dark Pattern) | Nominal | — | Ditetapkan oleh peneliti melalui pembagian kelompok A/B Testing. | Menjadi pembeda utama (perlakuan) untuk menguji dampak dari antarmuka. |
| Usability | DV | Kenyamanan interaksi | Skor komposit SUS | Interval | Poin (0-100) | Pengisian kuesioner SUS (10 pertanyaan) setelah simulasi selesai. | SUS adalah instrumen standar industri yang valid untuk mengukur kegunaan sistem. |
| Kepercayaan | DV | Rasa aman pengguna | Skor rata-rata Trust Scale | Ordinal | Poin (1-5) | Pengisian skala Likert (Sangat Tidak Setuju - Sangat Setuju). | Merupakan metrik tervalidasi dari literatur terdahulu untuk menangkap sentimen dan persepsi manipulasi. |
| Skenario Tugas | CV | Beban kognitif | Keberhasilan task | Nominal | — | Observasi apakah responden menyelesaikan tugas yang sama. | Memastikan kedua kelompok mendapat tingkat kesulitan tugas yang setara agar perbandingan adil. |

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [X] Setiap langkah terdokumentasi
  [X] Tidak ada "lompatan logis"
  [X] Metrik mengukur apa yang dimaksud (construct validity)

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Apakah desain antarmuka yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
|Jenis Antarmuka| IV |Praktik desain manipulatif|Kategori: Normal vs Dark Pattern |Nominal | — |
|System Usability| DV |Kemudahan dan kenyamanan interaksi|Skor komposit SUS (System Usability Scale)|Interval|Poin (0-100)|
|Trust Level| CV |Kepercayaan pengguna terhadap aplikasi|Rata-rata skor Trust Scale (Skala Likert)|Ordinal|Poin (1-5)|

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Jika ya, di mana?tidak ada
>Rantai operasionalisasi ini sudah logis karena konsep abstrak "kenyamanan" langsung diukur secara kuantitatif menggunakan instrumen baku di industri (SUS), dan konsep "kepercayaan" diukur menggunakan kuesioner skala Likert yang sudah divalidasi oleh literatur jurnal terdahulu.

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 | Kuesioner SUS dan instrumen Trust Scale (Skala Kepercayaan) secara langsung dan akurat mewakili variabel tingkat kenyamanan serta rasa aman pengguna yang dirumuskan pada Research Question. |
| Sensitive | 4 | Rentang skala poin 0-100 pada SUS memiliki tingkat sensitifitas yang sangat baik untuk menangkap perbedaan yang kecil dalam pengalaman pengguna. Skala Likert 1-5 untuk kepercayaan juga cukup peka menangkap sentimen. |
| Feasible | 5 | Pengumpulan data realistis dan hemat biaya karena dapat diotomatisasi sepenuhnya menggunakan form daring (seperti Google Forms) yang langsung diisi responden setelah mereka mencoba purwarupa di Figma. |

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? 
>Metrik Task Completion Time dan Error Rate dibutuhkan sebagai pelengkap data yang bersifat objektif. Berbeda dengan kuesioner SUS dan uji kepercayaan yang hanya mencerminkan pendapat pengguna, kedua metrik ini menghasilkan angka konkret, berapa lama pengguna menyelesaikan tugas dan seberapa sering mereka salah klik. Dari situ, kita bisa melihat secara langsung apakah dark pattern benar-benar membuat pengguna bingung dan terkecoh saat bernavigasi.

**Contoh kasus ceiling effect untuk metrik ini:**
> Skenario tugas dalam purwarupa dirancang terlalu mudah; misalnya, pengguna hanya perlu mengklik satu tombol besar di tengah layar. Akibatnya, semua responden dari kedua kelompok, baik antarmuka Normal maupun Dark Pattern, berhasil menyelesaikan tugas dalam satu detik dan memberikan skor SUS sempurna. Eksperimen pun gagal menghasilkan data yang bermakna karena semua nilai menumpuk di batas tertinggi (ceiling effect), sehingga perbedaan performa antara kedua antarmuka tidak bisa terdeteksi sama sekali.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | *Apakah semua data point terkumpul?* | Ditargetkan ya. Namun, pada praktiknya ada potensi data tidak utuh jika responden berhenti di tengah pengujian Figma atau skip pertanyaan. | Mengatur semua kolom di form kuesioner menjadi Required (wajib diisi). Jika data log waktu dari Figma terputus, data responden tersebut langsung dihapus (drop). |
| Consistency | *Apakah ada kontradiksi internal?* | Ada kemungkinan muncul kontradiksi, misalnya responden malas membaca lalu menekan angka 5 untuk semua pertanyaan SUS agar cepat selesai. | Melakukan filtering data mentah. Kuesioner SUS menggunakan pola pertanyaan positif dan negatif berselang-seling. Jika ada yang menjawab lurus/asal, datanya langsung dibuang. |
| Validity | *Apakah benar-benar mengukur yang dimaksud?* | Ya, selama responden benar-benar paham maksud dari setiap pertanyaan kuesioner tanpa ada salah tafsir (misscom). | Menggunakan kuesioner SUS dan Trust Scale berbahasa Indonesia yang sudah baku dan tervalidasi dari literatur sebelumnya, bukan menerjemahkan sendiri. |
| Representativeness | *Apakah sampel mewakili populasi target?* | Belum tentu, apalagi jika tautan hanya disebar di grup kampus berisi anak IT yang sudah paham dengan Dark Patterns. | Melakukan random sampling dengan menyebar tautan ke mahasiswa non-IT atau pengguna awam agar profilnya sesuai dengan populasi pengguna aplikasi e-commerce asli. |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> P-hacking, atau memilih metrik setelah melihat data, merupakan pelanggaran serius terhadap integritas akademik. Ini terjadi ketika peneliti hanya melaporkan metrik yang kebetulan mendukung hipotesisnya, sementara data yang bertentangan sengaja disembunyikan. Kesimpulan yang dihasilkan pun menjadi menyesatkan terlihat signifikan di permukaan, padahal tidak lebih dari kebetulan statistik.
>Praktik ini berbeda mendasar dari eksplorasi data yang sah, dan pembedanya adalah transparansi. Dalam penelitian yang etis, metrik utama (primary metric) sudah ditetapkan dan dikunci sebelum pengujian dimulai, lalu hasilnya dilaporkan secara jujur, baik ketika hipotesis terbukti maupun ketika gagal menolak Hipotesis Nol (H₀). Jika selama analisis peneliti menemukan pola baru yang menarik di luar rencana awal, temuan itu tetap sah untuk dilaporkan — asalkan secara jujur diberi label sebagai "temuan sekunder/eksploratori", bukan diklaim sebagai tujuan utama yang sudah dirancang sejak awal penelitian.
