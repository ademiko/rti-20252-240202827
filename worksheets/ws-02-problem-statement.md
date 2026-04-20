# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Nama   : Ade Miko
NIM.   : 240202827

Domain & Konteks
  Domain   : Optimasi Teknologi Informasi dalam Penjadwalan.
  Konteks  : Penjadwalan Mata Kuliah Umum (MKU) di lingkungan universitas

System Context
  Input       : Data riil semester genap meliputi 120 dosen, 352 kelas, 14.080 mahasiswa, dan jadwal kerja dosen.
  Process     : Otomatisasi penjadwalan menggunakan perbandingan Algoritma Genetika dan Modified Improved Particle Swarm Optimization (MIPSO).
  Output      : Rekomendasi jadwal optimal dalam format sistem web dan dokumen Excel.
  Outcome     : Peningkatan efisiensi waktu pembuatan jadwal hingga 500% tanpa adanya jadwal yang bentrok.
  Constraints : ketiadaan bentrok pada jadwal mengajar dosen (C1) dan Batasan ketersediaan ruang kelas (C2) 
  Stakeholders: Admin MKU selaku pengelola, para dosen pengampu, dan LPPM sebagai pendukung riset.

Fenomena → Problem
  Fenomena yang diamati             : Kompleksitas tinggi dalam menyusun jadwal institusi pendidikan yang melibatkan banyak variabel.
  Gejala (symptom) yang terukur     : Proses manual memakan waktu hingga 3 hari dan sering menghasilkan jadwal yang bentrok (crash).
  Masalah yang didiagnosis          : Keterbatasan kemampuan manual dalam menangani ruang pencarian solusi (search space) yang sangat luas dan kompleks.
  Masalah riset (researchable)      : Analisis perbandingan kinerja antara Algoritma Genetika dan MIPSO untuk menentukan metode optimasi paling efisien.
  Variabel yang terukur             : Rata-rata waktu eksekusi (dalam detik) dan pencapaian nilai fitness maksimal (skala 0-1).

Problem Quality Check
  [ ] Clarity — Apakah satu orang membaca akan paham?
  [ ] Measurability — Apakah ada metrik kuantitatif?
  [ ] Relevance — Apakah penting untuk domain?
  [ ] Testability — Apakah bisa gagal?
  [ ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
Penjadwalan Mata Kuliah Umum (MKU) di UPN "Veteran" Jawa Timur saat ini masih dilakukan secara manual, sehingga membutuhkan waktu penyusunan hingga 3 hari dan rentan menghasilkan jadwal yang bentrok karena kompleksitas data 120 dosen serta 352 kelas. Kondisi ini menunjukkan adanya gap efisiensi yang menghambat persiapan proses belajar mengajar. Riset ini bertujuan untuk membandingkan kinerja Algoritma Genetika dan MIPSO guna mengidentifikasi metode otomatisasi yang paling unggul dalam hal kecepatan dan akurasi. Melalui pengukuran variabel waktu eksekusi dan nilai fitness, riset ini membuktikan bahwa MIPSO mampu menghasilkan jadwal optimal secara signifikan lebih cepat, yaitu rata-rata 190,281 detik, dibandingkan Algoritma Genetika yang membutuhkan 988,199 detik.
```
```
Rangkuman singkat dari jurnal

Pada, riset ini topik masalah berfokus ke masalah "klasik" di kampus yaitu: ribetnya bikin jadwal kuliah yang bebas bentrok. Di UPN "Veteran" Jawa Timur, admin MKU pusing/binggung karena harus mengurus 120 dosen dan 352 kelas secara manual yang makan waktu sampai 3 hari.pada, peneliti ini mencoba membandingkan dua "otak" komputer untuk mengotomatisasi jadwal tersebut menggunkan  Algoritma Genetika (GA) dan MIPSO (Modified Improved Particle Swarm Optimization). Penelitian ini membangun sistem berbasis web mengunggunakan Laravel untuk mengetes mana yang paling jago.Hasil :
- MIPSO Menang Telak: Dari sisi kecepatan, MIPSO cuma butuh waktu rata-rata 190 detik, sedangkan GA butuh 988 detik.
- Efisiensi Tinggi: Artinya, MIPSO 5 kali lipat (500%) lebih kencang daripada GA dalam menghasilkan jadwal yang sama-sama optimal atau tanpa bentrok (fitness = 1).

Jadi buat  penjadwal yang kompleks dengan banyak batasan (seperti jadwal dosen yang bentrok dengan unit kerja lain), algoritma MIPSO jauh lebih direkomendasikan daripada algoritma Genetika biasa karena kinerjanya yang jauh lebih efisien.
```
---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:**Optimasi Penjadwalan Mata Kuliah

| Tahap | Hasil |
|-------|-------|
| Reality | Penjadwalan mata kuliah adalah proses bisnis utama universitas yang sangat krusial namun terdapat banyak tantangan karena melibatkan banyak batasan (constraints).|
| Observed Issue (Symptom) | Di UPN "Veteran" Jawa Timur, pembuatan draf jadwal manual membutuhkan waktu kurang lebih 3 hari dan sering kali masih menyisakan jadwal yang bentrok (crash). |
| Diagnosed Problem (Root Cause) |Proses manual tidak lagi sanggup untuk menangani ruang pencarian solusi yang sangat luas dan banyak, terutama saat harus mengoordinasikan 120 dosen dan 352 kelas secara bersamaan. |
| Researchable Problem |Perlunya analisis perbandingan antara Algoritma Genetika dan MIPSO untuk memberikan rekomendasi algoritma mana yang paling efisien dalam hal efisiensi waktu dan akurasi untuk kasus penjadwalan ini. |
| Measurable Variable |Rata-rata waktu eksekusi sistem dalam satuan detik dan Nilai Fitness untuk mengukur ketiadaan bentrok pada jadwal (jadwal optimal jika nilai fitness = 1). |

**Apakah terjebak solution-first thinking?** [ ] Ya 
> Jika ya, kembali ke tahap mana? Saya cukup kesulitan dan tidak langsung menentukan satu algoritma sebagai solusi akhir. Sebaliknya, saya memulai dengan mengidentifikasi gejala nyata di lapangan (proses manual yang lambat dan bentrok) , lalu merancang riset untuk membandingkan dua metode berbeda (GA vs MIPSO) guna membuktikan secara ilmiah mana yang kinerjanya benar-benar lebih unggul.
---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Terdapat beberapa data riil pada penelitian ini yaitu, data semester genap 2021/2022 yang meliputi daftar 120 dosen pengampu, 352 kelas, 14.080 mahasiswa, serta jadwal mengajar dosen di unit kerja asalnya. |
| Process |Komputasi penjadwalan otomatis menggunakan dua metode, yaitu Algoritma Genetika dan Modified Improved Particle Swarm Optimization (MIPSO), yang diimplementasikan dengan framework Laravel dan basis data MariaDB.|
| Output |Rekomendasi jadwal perkuliahan (jadwal perkuliahan) yang telah diproses oleh sistem, yang dapat ditampilkan melalui antarmuka web ke dalam format dokumen Excel |
| Outcome |Terbentuknya jadwal kuliah yang optimal tanpa ada bentrok, dengan pencapaian efisiensi waktu eksekusi yang signifikan pada algoritma MIPSO dibandingkan metode manual maupun algoritma genetika. |
| Constraints |Batasan utama yang harus dipenuhi adalah ketiadaan bentrok pada jadwal dosen (C1) dan ketersediaan ruang kelas (C2), di mana nilai fitness akhir harus mencapai angka 1. |
| Stakeholders |Pihak yang terlibat mencakup Admin MKU sebagai pengelola penjadwalan, dosen pengampu sebagai penerima jadwal, serta LPPM UPN "Veteran" Jawa Timur sebagai pendukung riset |

**Komponen mana yang paling relevan dengan masalah riset?** Komponen Process
Bagian Process merupakan inti dari penelitian ini karena di sinilah letak perbandingan eksperimental antara Algoritma Genetika dan MIPSO dilakukan. Fokus riset/penelitian ini adalah untuk membuktikan algoritma mana yang memiliki kinerja paling efisien dalam mengolah input menjadi output jadwal yang valid.
---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 |Masalah yang diangkat sangat jelas dan mudah dipahami, yaitu ketidakefisienan proses manual dan perlunya perbandingan algoritma otomatis untuk penjadwalan.|
| Measurability | 5 |Riset ini memiliki metrik kuantitatif yang pasti, yaitu rata-rata waktu eksekusi dalam detik dan nilai fitness berdasarkan jumlah bentrok (C1 dan C2), membuat reviewer percaya dan mudah paham karena di dukung data yang nyata.|
| Relevance | 5 |Riset ini sangat relevan dengan kebutuhan institusi pendidikan untuk meningkatkan efisiensi operasional dan mutu pembelajaran|
| Testability | 5 |Masalah ini dapat diuji secara empiris melalui eksperimen sistem dan hasilnya bisa dibuktikan salah (falsifiable) jika data menunjukkan hasil sebaliknya.|
| Impact | 4 |Memberikan kontribusi nyata berupa rekomendasi algoritma terbaik bagi pengelola MKU, walaupun cakupannya masih spesifik hanya di satu institusi.|

**Skor total:** 24/ 25

**Problem statement versi final (1 paragraf):**
> Pembuatan jadwal Mata Kuliah Umum (MKU) secara manual di UPN "Veteran" Jawa Timur terhambat oleh kompleksitas data yang melibatkan 120 dosen dan 352 kelas, sehingga membutuhkan waktu yang cukup lama hingga 3 hari dan rentan menghasilkan jadwal yang bentrok. Masalah ini menunjukkan adanya kesenjangan (gap) efisiensi pada sistem yang berjalan saat ini. Riset ini dilakukan untuk mengevaluasi dan membandingkan kinerja Algoritma Genetika dengan MIPSO guna menentukan metode otomatisasi yang paling unggul. Berdasarkan hasil pengujian, algoritma MIPSO terbukti memberikan solusi jadwal optimal (fitness = 1) secara signifikan lebih cepat, yaitu 190,281 detik, dibandingkan Algoritma Genetika yang membutuhkan 988,199 detik.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
>Perbedaan fundamental antara masalah coding (seperti bug atau error) dengan masalah riset terletak pada tujuannya. Dalam coding, saya mendefinisikan masalah sebagai hambatan teknis yang harus segera diperbaiki agar sistem "berjalan" (orientasi solusi). Namun, dalam masalah riset, saya memandang hambatan tersebut sebagai gap pengetahuan yang perlu dibuktikan kebenarannya secara sistematis.

>Pendekatan riset menuntut saya untuk tidak hanya mencari solusi yang "penting jalan", tetapi harus bisa membuktikan mengapa solusi tersebut (misalnya algoritma MIPSO) lebih baik melalui variabel yang terukur, seperti nilai fitness yang dihitung dengan rumus:
Fitness = 1/1+(C1+C2)
