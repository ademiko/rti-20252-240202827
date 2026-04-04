# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (artefak dibuat sebagai instrumen pengujian hipotesis, bukan tujuan akhir).

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Ade Miko
Tanggal          : 4 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: 
   Apakah tingkat akurasi tersebut tetap konsisten jika diuji pada dataset yang berbeda atau lingkungan perangkat keras yang berubah
   - Data yang dibutuhkan untuk verifikasi:
   Rincian waktu eksekusi di setiap iterasi, 
   nilai fitness yang dihasilkan, 
   dan juga spesifikasi perangkat keras yang digunakan untuk memastikan perbandingan yang adil (apple-to-apple)
2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [ ] Design Science  [ ] Mixed
   - Alasan: 
    Penelitian ini menggunkan metode pengembangan waterfall untuk membangun sebuah artefak teknologi berupa sistem penjadwalan mata kuliah umum berbasis web. Fokus utamanya adalah memecahkan masalah praktis penjadwalan otomatis yang kompleks melalui pengembangan dan pengujian sistem secara langsung.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: 
   Kecepatan waktu pembentukan jadwal merupakan indikator tunggal bahwa suatu algoritma memiliki kinerja "lebih baik", tanpa mempertimbangkan aspek lain seperti fleksibilitas terhadap perubahan jadwal mendadak
   - Sumber bias potensial: 
   Sampling bias dapat terjadi karena data uji hanya terbatas pada penjadwalan semester Genap 2021/2022 untuk Mata Kuliah Umum (MKU) di satu institusi tertentu.
   - Langkah mitigasi: 
   Melakukan penambahan jumlah individu/kelompok dalam proses crossover dan mutation untuk memverifikasi apakah hasil optimal yang ditemukan memang benar-benar stabil pada berbagai skala populasi. 

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: 
   Hasil rata-rata waktu eksekusi algoritma (seperti 190,281 detik untuk MIPSO dan 988,199 detik untuk Genetika) serta data riil penjadwalan yang melibatkan 456 jadwal.
   - Batasan yang diakui sejak awal: 
   Penelitian ini hanya menguji kinerja menggunakan 5 hingga 20 individu/kelompok dan mengakui perlunya riset lebih lanjut untuk menemukan jumlah individu yang benar-benar optimal
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

**Paper yang dipilih:**
> Judul: Analisis Perbandingan Algoritma Genetika dan Modified Improved Particle Swarm Optimization dalam Penjadwalan Mata Kuliah
> Penulis (Tahun): Made Hanindia Prami Swari, Chrystia Aji Putra, I Putu Susila Handika, 2022 

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengumpulkan data riil penjadwalan semester Genap 2021/2022 di UPN "Veteran" Jawa Timur yang melibatkan 120 dosen dan 352 kelas.| Data hanya berfokus pada Mata Kuliah Umum (MKU). Karakteristik jadwal MKU mungkin lebih sederhana dibanding jadwal program studi teknis yang memiliki banyak batasan laboratorium. |
| Data → Processing | Memasukkan batasan (constraints) seperti ketersediaan ruang, jadwal dosen di unit kerja, dan jumlah mahasiswa ke dalam sistem berbasis Laravel| Tidak semua variabel kenyataan (seperti preferensi jam mengajar dosen secara subjektif) dimasukkan ke dalam model komputasi sistem.|
| Processing → Analysis | Menguji kinerja kedua algoritma dengan variasi jumlah individu/kelompok sebanyak 5, 10, 15, dan 20.| Pengujian hanya dilakukan pada rentang populasi yang kecil (maksimal 20). Performa algoritma mungkin berubah drastis jika populasi diperbesar|
| Analysis → Inference | Membandingkan rata-rata waktu eksekusi di mana MIPSO (190,281 detik) ditemukan 5 kali lebih cepat dibanding Genetika (988,199 detik).| kinerja lebih baik hanya didasarkan pada kecepatan waktu eksekusi saja , tanpa mengukur kualitas sebaran jadwal secara mendalam|
| Inference → Knowledge | Memberikan rekomendasi bahwa MIPSO adalah algoritma terbaik untuk diimplementasikan pada sistem penjadwalan otomatis.| Klaim "terbaik" ini bersifat lokal untuk kasus MKU di satu institusi dan belum tentu berlaku sama untuk institusi dengan skala data yang berbeda.|

**Distorsi paling besar di tahap:** Inference → Knowledge

**Dua distorsi spesifik yang teridentifikasi:**
1. Sampling Bias: Penelitian ini hanya menggunakan data spesifik Mata Kuliah Umum (MKU) di satu universitas, sehingga hasil efisiensinya mungkin tidak bisa digeneralisasi untuk semua jenis penjadwalan akademik.
2. Keterbatasan Eksperimental: Peneliti mengakui bahwa jumlah individu dalam proses crossover dan mutation masih terbatas dan perlu ditambah untuk mendapatkan hasil yang benar-benar optimal di riset selanjutnya.
---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Peneliti wajib melaporkan seluruh hasil pengujian, termasuk data yang ekstrim, karena dalam algoritma seperti Genetika, hasil acak adalah bagian dari karakteristik proses mutasi. Menghapus data hanya agar hasil terlihat lebih baik secara statistik adalah bentuk manipulasi data. |
| Transparansi | Peneliti harus menjelaskan secara terbuka mengapa terjadi perbedaan waktu yang signifikan antar pengujian (seperti pada Tabel 1 jurnal). Transparansi memungkinkan pembaca memahami bahwa algoritma tersebut memiliki risiko ketidakstabilan waktu eksekusi.|
| Peer review | Reviewer membutuhkan data yang lengkap dan jujur untuk memvalidasi klaim "kinerja lebih baik 5 kali lipat". Tanpa pelaporan data yang utuh, proses peer review tidak bisa mendeteksi kelemahan algoritma dalam skenario terburuk|

**Keputusan akhir dan justifikasi:**
> Peneliti harus tetap menyertakan seluruh data point (termasuk outlier) dalam laporan akhir. Justifikasinya adalah untuk menjaga integritas riset; dalam bidang IT, mengetahui bahwa sebuah algoritma bisa berjalan sangat lambat di kondisi tertentu (seperti proses mutasi acak pada Genetika) adalah pengetahuan yang sama pentingnya dengan mengetahui kecepatan rata-ratanya. Hal ini sesuai dengan prinsip falsifiability, di mana riset harus bisa diuji kebenarannya secara utuh.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** ________________________________________

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | *4* | *1* | *5* |
| Jenis data yang dikumpulkan | Data kuantitatif berupa rata-rata waktu eksekusi dalam detik.|Tidak mengumpulkan data kualitatif mengenai persepsi atau makna sosial | Evaluasi kinerja artefak (sistem) dalam menghasilkan jadwal tanpa bentrok (fitness = 1).|
| Limitasi paradigma | Kurang mempertimbangkan kenyamanan subjektif dosen dalam jadwal yang dihasilkan|Tidak dapat memberikan bukti empiris mengenai efisiensi algoritma secara komputasi. | Fokus lebih besar pada keberhasilan solusi teknis daripada pengembangan teori murni|

**Paradigma yang dipilih:** Design Science Research (DSR)
**Alasan:** Penelitian ini bertujuan utama untuk menciptakan sebuah artefak teknologi berupa sistem penjadwalan otomatis berbasis web menggunakan framework Laravel. Riset ini mengikuti pola DSR di mana sebuah masalah praktis di dunia nyata (penjadwalan manual yang rumit di UPN "Veteran" Jawa Timur) diselesaikan dengan membangun dan menguji efektivitas sebuah solusi teknis. Pengujian algoritma (Genetika vs MIPSO) dilakukan untuk memvalidasi kinerja dari artefak yang dibangun tersebut agar memberikan rekomendasi terbaik bagi pengelola.
---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, saya cenderung menerima klaim performa algoritma secara mentah-mentah hanya berdasarkan angka akurasi atau kecepatan yang disajikan. Namun, setelah memahami rantai distorsi, pertanyaan yang sekarang akan saya ajukan saat membaca paper adalah:
1. Bagaimana karakteristik data yang digunakan (apakah ada sampling bias)? 
2. Apakah metrik yang digunakan sudah mencakup seluruh realitas masalah atau hanya fokus pada satu sisi (seperti hanya waktu eksekusi saja)? 
3. Apakah hasil tersebut dapat direplikasi pada lingkungan yang berbeda?