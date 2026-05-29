# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : 13th Gen Intel(R) Core(TM) i5-13450HX (2.40 GHz)
  RAM     : 12 GB DDR5
  GPU     : NVIDIA GeForce RTX 3050 6GB Laptop GPU (6 GB)
Intel(R) UHD Graphics (128 MB)
  Storage : 512 gb

Software:
  OS        : Windows 11 64-bit
  Runtime   : Google Chrome & Python
  Framework : Figma (Purwarupa), Maze (Testing Platform), Jupyter/Google Colab

Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| Figma|126.3.12|figma.com|(Cloud-based, N/A)|
|Maze Platform|Web Cloud|maze.co|(Cloud-based, N/A)|
| pandas (Python) | | PyPI / pip repository | sha256: 8a... (terlampir)|
|scipy (Python)| | PyPI / pip repository | sha256: 3f... (terlampir)  |

Konfigurasi:
  Config file     : config_eksperimen.json (Menyimpan variabel ambang batas & nama grup)
  Random seed     : 42 (Digunakan pada tahap pembersihan data Python/Pandas)
  Hyperparameters : Alpha threshold (Batas signifikansi) = 0.05

Reproducibility Check:
  [x] Dependency terdokumentasi (requirements.txt / lock file)
  [x] Seed ditetapkan di semua level (Python, NumPy, framework)
  [x] Config di version control
  [x] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | 13th Gen Intel(R) Core(TM) i5-13450HX (2.40 GHz) |
| RAM | 12 GB DDR5 |
| GPU | NVIDIA GeForce RTX 3050 6GB Laptop GPU (6 GB)
Intel(R) UHD Graphics (128 MB) |
| OS | Windows 11 |
| Runtime | Google Chrome |
| Framework | Figma (Desain Purwarupa) & Maze (Unmoderated Testing Platform) |
| Random Seed | 42 (Ditetapkan pada modul Python/SPSS saat melakukan random assignment pembagian kelompok responden agar dapat direproduksi) |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| Figma (Desktop) | 126.3.12 | Untuk mendesain antarmuka High-Fidelity dan komponen Fake Countdown Timer. |
| Maze Platform | Versi Web Cloud | Untuk meng- hosting purwarupa Figma, merekam durasi penyelesaian tugas, dan melacak misclick responden. |
| Google Forms | Google Forms | Untuk mendistribusikan kuesioner System Usability Scale (SUS) dan Trust Scale. |
| Python (SciPy) |(belum terinstal) | Library komputasi statistik untuk menjalankan uji Mann-Whitney U Test pada hasil kuesioner. |
| Python (Pandas) | (belum terinstal)| Library manipulasi data untuk membersihkan (cleaning) data mentah kuesioner (menghapus data outlier/anomali). |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 | Nilai p-value (Mann-Whitney) & Rata-rata Skor SUS | — |
| 2 | 42 | Nilai p-value (Mann-Whitney) & Rata-rata Skor SUS | [x] Ya / [ ] Tidak |
| 3 | 42 | Nilai p-value (Mann-Whitney) & Rata-rata Skor SUS | [x] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**
> File dataset (Excel/CSV) sumber mengalami perubahan di latar belakang (misalnya ada responden baru yang masuk ke Google Forms di tengah-tengah proses analisis).
> Parameter algoritma pembersihan data (data cleaning) untuk membuang nilai outlier tidak menggunakan urutan (seed) yang deterministik, sehingga baris data yang dibuang berbeda-beda setiap kali program dijalankan.

**Checklist kontrol yang sudah diterapkan:**
- [x] Random seed di-set di semua level
- [x] Tidak ada background process yang mengganggu
- [x] Cache dibersihkan antar-run
- [x] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Analisis Dampak Urgency Dark Pattern terhadap Usability dan User Trust pada Antarmuka E-Commerce

## 1. Environment
- CPU       : intel Core(TM) i5-13450HX 
- RAM       : 12 GB DDR5
- GPU       :  NVIDIA GeForce RTX 3050 6GB Laptop GPU (6 GB)
Intel(R) UHD Graphics (128 MB)
- OS        : Windows 11 64-bit
- Runtime   : Google Chrome Version 
- Alat      : Figma (126.3.12), Maze Platform, Google Colab
- Seed      : 42 (untuk analisis data)

## 2. Installation
Karena instrumen eksperimen menggunakan platform berbasis komputasi awan (Cloud/Web), tidak diperlukan instalasi perangkat lunak lokal yang rumit. Untuk analisis data, cukup jalankan perintah berikut pada environment Google Colab:
`pip install pandas==2.1.0 scipy==1.11.1`

## 3. Data
Data eksperimen merupakan data primer yang bersumber dari respons 40 partisipan melalui kuesioner daring (Google Forms) dan log navigasi dari platform Maze. 
- Format: File tabular `.csv` (Comma Separated Values).
- Ukuran: Estimasi < 100 KB (terdiri dari ~40 baris data partisipan beserta metrik waktu penyelesaian dan skor SUS/Trust).

## 4. Execution
1. Distribusikan tautan pengujian Maze kepada partisipan yang telah dikelompokkan (Kelompok Kontrol & Kelompok Perlakuan).
2. Setelah terkumpul 40 respons, ekspor data dari Maze dan Google Forms menjadi satu file bernama `dataset_eksperimen.csv`.
3. Buka tautan Google Colab yang memuat skrip `dark_pattern_analysis.ipynb`.
4. Unggah file `dataset_eksperimen.csv` ke dalam direktori kerja Colab.
5. Jalankan seluruh baris kode dengan menekan menu `Runtime -> Run all`.

## 5. Configuration
Konfigurasi parameter dikunci pada bagian awal skrip analisis data Python:
- `random_seed`: 42 (untuk menstabilkan pembersihan data outlier)
- `alpha_threshold`: 0.05 (batas signifikansi p-value)
- `group_a_label`: "Baseline (Normal)"
- `group_b_label`: "Dark Pattern (Fake Timer)"

## 6. Expected Output
Skrip akan mengeluarkan ringkasan statistik deskriptif berupa rata-rata skor SUS dan Trust Scale dari kedua kelompok. Selanjutnya, skrip akan menampilkan hasil uji Mann-Whitney U Test (berupa nilai statistik *U* dan *p-value*). Jika *p-value* < 0.05, layar akan mencetak string: "H1 Diterima: Terdapat penurunan skor yang signifikan akibat Dark Pattern."
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [ ] Repeatability / [ ] Reproducibility / [x] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Saat ini, rancangan riset baru berada pada tahap finalisasi proposal, sehingga instrumen pengujian sesungguhnya belum dibangun. Komponen krusial yang masih hilang meliputi: tautan purwarupa Figma interaktif, formulir kuesioner yang sudah disebarkan, serta draf script analisis data Python (berkas .ipynb) yang sesungguhnya. Untuk mencapai tingkat reproducibility, seluruh aset desain, file kuesioner, dan baris kode harus sudah rampung dibuat, diuji coba (pilot test), lalu diunggah secara publik ke dalam repositori GitHub agar peneliti lain dapat mereplikasi prosedur eksperimen ini dari awal hingga akhir.
