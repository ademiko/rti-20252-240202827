# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah desain antarmuka yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?
Metrik Utama      : Skor SUS (0–100) dan Skor Trust Scale (1–5)

Tabel Hasil:
| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
|          |                      |                      |   |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 |             |             |        |
| 2 |             |             |        |

Bias Check:
  [ ] Y-axis mulai dari 0 (atau dijustifikasi)
  [ ] Error bar/CI ditampilkan
  [ ] Semua data disertakan (tidak cherry-picked)
  [ ] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario |Total SUS (mean ± std) | Rata-rata Trust  (mean ± std) | n |
|----------|----------------------|----------------------|---|
| Kontrol (Antarmuka Standar) |77.0 ± 7.01 | 4.11 ± 0.33 |35 |
| Dark Pattern (Urgency Timer) | 22.5 ± 6.50 | 2.03 ± 0.39 | 35 |

**Checklist tabel:**
- [x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x] Mean ± std (bukan single number)
- [x] Diurutkan berdasarkan metrik utama
- [x] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | *Contoh: Bar chart + error bar* | Perbandingan rata-rata skor SUS & Trust antar kedua kelompok, dengan variabilitas (std) ditampilkan sebagai error bar | Mean ± std SUS dan Trust, per kelompok |
| 2 | *Box plot* | Menunjukkan sebaran penuh skor SUS tiap kelompok (median, kuartil, rentang) — memperlihatkan bahwa kedua distribusi sama sekali tidak tumpang tindih| Seluruh 35 nilai Total SUS per kelompok |
| 3 | *Scatter plot* |Membandingkan tingkat keberhasilan task (Task Selesai: Ya/Tidak) antar kelompok | Jumlah "Ya"/"Tidak" per kelompok (34 vs 1 di Kontrol; 32 vs 3 di Dark Pattern) |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | Ya — perbedaan sebenarnya hanya 0.4 poin persentase, tapi karena sumbu-Y dipotong mulai dari 90%, batang A terlihat jauh lebih tinggi (hampir 3× lipat secara visual) dibanding batang B, padahal bedanya kecil. |
| Apakah error bar ditampilkan? | Tidak disebutkan — kemungkinan besar tidak ada, sehingga pembaca tidak tahu apakah perbedaan 0.4% itu bahkan berada dalam rentang variabilitas normal (bisa jadi tidak signifikan sama sekali).|
| Apakah semua kondisi ditampilkan? | Tidak — hanya 2 metode disebut |
| Apa solusinya? | Set Y-axis mulai dari 0% (atau jika dipotong, beri tanda jeda sumbu yang jelas dan disertai penjelasan eksplisit), tambahkan error bar/CI, dan laporkan hasil uji signifikansi (p-value, effect size) alih-alih hanya menampilkan selisih visual. |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [x] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: ____

>Untuk grafik SUS/Trust pada Latihan 2 #1, sumbu-Y bar chart SUS akan saya mulai dari 0 (bukan dipotong), karena rentang skor SUS teoretis memang 0–100 dan perbedaan antar kelompok saya (77 vs 22.5) sudah sangat besar secara alami, memotong sumbu justru tidak diperlukan dan berisiko dituduh melebih-lebihkan efek yang sebenarnya memang besar. Error bar (±std) akan selalu disertakan di setiap batang, dan seluruh 70 data point ditampilkan tanpa ada yang disembunyikan (termasuk melaporkan bahwa task completion di kelompok Dark Pattern tetap 71.4%, bukan seolah semua orang gagal total, supaya gambaran tidak dibuat lebih dramatis dari kondisi sebenarnya).
---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik menjawab kebutuhan yang berbeda. Tabel memberi angka presisi yang bisa dikutip ulang secara pasti (misalnya saat penguji bertanya "berapa persis mean SUS kelompok kontrol?", saya bisa langsung menjawab 77.0 ± 7.01 dari tabel), sementara grafik membuat pola perbedaan itu langsung terasa secara intuitif dalam hitungan detik, sesuatu yang sulit ditangkap hanya dari deretan angka di tabel, apalagi saat presentasi lisan di mana audiens hanya mendengar sekali (lihat WS-16). Kalau saya hanya menyajikan tabel, presentasi jadi berat dan sulit diikuti; kalau saya hanya menyajikan grafik, presisi angka untuk keperluan analisis statistik jadi hilang.

Saya sendiri pernah membuat grafik proyek kuliah sebelumnya dengan sumbu-Y yang saya potong "supaya perbedaannya kelihatan lebih jelas" tanpa menyadari bahwa itu justru melebih-lebihkan hasil secara visual dan berpotensi menyesatkan pembaca yang hanya melihat sekilas.
