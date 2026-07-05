# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : ____________________
Jumlah data awal  : ____________________

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing |             |            |             |
| Duplikat|             |            |             |
| Error   |             |            |             |

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
|             |          |        |        |

Normalization:
  Metode    : ____________________
  Alasan    : ____________________
  Parameter : (dihitung dari: training set / seluruh data)

Leakage Check:
  [ ] Parameter normalisasi dari training set saja
  [ ] Tidak ada informasi test set dalam preprocessing
  [ ] Cross-validation dilakukan setelah split

Jumlah data akhir : ____________________
Script tersedia   : [ ] Ya → path: ____ | [ ] Belum
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
|Missing values | 0 dari 70 (0%) | Tidak ada tindakan diperlukan| Seluruh pertanyaan Google Forms ditandai Required, sehingga tidak ada respons kosong sejak sumbernya (lihat WS-10, WS-11).| 
|Duplikat| 0 dari 70 (0%) — dicek berdasarkan kombinasi ID Responden yang unik (RTI-001 s.d. RTI-070)| Tidak ada tindakan diperlukan, tapi tetap diverifikasi dengan cek COUNTIF pada kolom ID Responden di Excel | Google Forms tidak mengizinkan pengaturan "1 respons per akun" diaktifkan (form dibuat anonim), sehingga verifikasi manual duplikat ID tetap wajib dilakukan, bukan diasumsikan otomatis unik.|
|Error format | 0 dari 70 (0%) — seluruh kolom numerik (SUS1–10, T1–5, Usia) sudah bertipe angka, bukan teks | Tidak ada tindakan diperlukan | Google Forms untuk item Likert menggunakan tipe Linear scale, yang secara otomatis menghasilkan nilai numerik saat diekspor ke Sheets, sehingga risiko error tipe data (angka tersimpan sebagai teks) minim.|

**Jumlah data sebelum cleaning:** 70
**Jumlah data setelah cleaning:** 70
**Persentase data yang hilang/berubah:** 0%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| Total SUS |10 – 90 |Dua puncak terpisah jauh (Kontrol ~77, DP ~22.5) — bimodal karena memang dua kelompok berbeda, bukan satu populasi homogen | Tidak | Tidak perlu |Tidak perlu|
| Rata-rata Trus | 1.4 – 4.6 | Mendekati normal di masing-masing kelompok, tidak ada outlier | Tidak | Tidak perlu | Skala Likert 1–5 sudah dalam rentang tetap dan ordinal secara desain; uji Mann-Whitney U yang direncanakan (WS-07, WS-14) bekerja pada peringkat (rank), bukan jarak absolut, sehingga normalisasi tidak memberi manfaat tambahan. |

**Apakah normalisasi diperlukan?** [ ] Ya / [x] Tidak
**Justifikasi:**
> Kedua DV utama (SUS dan Trust) sudah berada dalam skala baku, terbatas (bounded), dan langsung diinterpretasikan menggunakan norma industri (misalnya skor SUS 77 = "Good", 22.5 = "Awful" ). Uji statistik yang direncanakan, Mann-Whitney U Test, adalah uji non-parametrik berbasis peringkat (rank), sehingga tidak mensyaratkan data dalam skala tertentu atau berdistribusi normal. Menormalisasi data di sini justru melanggar prinsip Minimal Distortion mengubah sesuatu yang tidak perlu diubah hanya akan mempersulit interpretasi tanpa manfaat statistik nyata.

**Leakage check:**
- [x] Parameter dihitung dari training set saja
- [x] Normalisasi diterapkan setelah train-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: dataset_penelitian_RTI_240202827.xlsx (sheet DATA MENTAH)
2. Data awal: 70 records, 25 kolom (No, ID, Kelompok, Kondisi, Usia, Jenis Kelamin,
   Frekuensi Belanja, Task Selesai, SUS1-10, Total SUS, T1-5, Rata2 Trust)
3. Cleaning:
   - Missing values: 0 kasus, metode: tidak diperlukan (seluruh field Required di Forms)
   - Duplikat: 0 kasus, tindakan: verifikasi manual ID unik, tidak ada yang dihapus
   - Error format: 0 kasus, tindakan: tidak diperlukan (tipe data numerik konsisten)
4. Transformation: Tidak ada transformasi — nilai mentah SUS1-10 dan T1-5 langsung dipakai
   untuk menghitung Total SUS (formula baku: [(pos-5)+(25-neg)]x2.5) dan Rata-rata Trust
   (mean T1-5), keduanya sudah disiapkan sebagai formula di spreadsheet sejak awal.
5. Normalisasi: Tidak diterapkan (lihat justifikasi Latihan 2), parameter dari — (n/a)
6. Data akhir: 70 records, 25 kolom (identik dengan data awal — tidak ada baris dibuang)
7. Leakage check: [x] Lulus / [ ] Ada masalah
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> tidak pernah, karena saya tahu nilai SUS dan Trust ini sudah standar internasional dan juga sudah pernah saya pakai pada semester sebelumnya(3)

