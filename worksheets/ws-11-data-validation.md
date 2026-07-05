# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [ ] Semua skenario tercakup
  [ ] Jumlah run sesuai rencana
  [ ] Tidak ada file output hilang
  Missing: ____ dari ____ data points

Format Consistency:
  [ ] Semua file format sama (CSV/JSON/...)
  [ ] Header konsisten
  [ ] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [ ] Nilai dalam range masuk akal
  [ ] Tidak ada waktu negatif
  [ ] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: ____________________

Cross-Validation:
  [ ] Run identik → hasil mendekati
  [ ] Trend konsisten dengan ekspektasi teori

Keputusan:
  [ ] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| KONTROL (Antarmuka Standar) | 35 | 35 | 0 | — |
| DARK PATTERN (Urgency) | 35 | 35 | 0 | — |


**Total expected:** 70 | **Total actual:** 70 | **Missing:** 0

**Keputusan untuk data missing:**
> Tidak ada data yang hilang pada dataset final (DATA MENTAH, baris RTI-001 s.d. RTI-070) seluruh field yang direncanakan (demografi, 10 item SUS, 5 item Trust, status Task Selesai) terisi penuh untuk 70 responden. Ini bisa dicapai karena seluruh pertanyaan kuesioner ditandai Required di Google Forms sejak awal (lihat panduan pembuatan form), sehingga responden tidak bisa submit dengan jawaban kosong. Sekiranya di lapangan ada responden yang keluar di tengah jalan, mereka otomatis tidak akan menghasilkan baris data sama sekali (bukan baris dengan kolom kosong)  sesuai protokol drop-out di WS-10.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Kelompok KONTROL (n=35):**

| Statistik | Nilai |
|-----|-------------|
|Q1 | 72.5| 
|Q3 | 82.5 | 
| IQR| 10.0 | 
|Batas bawah (Q1 − 1.5×IQR)| 57.5 | 
|Batas atas (Q3 + 1.5×IQR)| 97.5| 
|Rentang aktual| data60 – 90Out| 
|lier terdeteksi| Tidak ada — seluruh nilai (60–90) berada dalam batas [57.5, 97.5]|

**Kelompok DARK PATTERN (n=35):**
| Statistik | Nilai |
|-----|-------------|
|Q1 |17.5| 
|Q3 | 27.5| 
|IQR | 10.0 | 
| Batas bawah (Q1 − 1.5×IQR)| 2.5| 
|Batas atas (Q3 + 1.5×IQR)| 42.5| 
| Rentang aktual data | 10 – 37.5| 
|Outlier terdeteksi | tidak ada — seluruh nilai (10–37.5) berada dalam batas [2.5, 42.5]|

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| (tidak ditemukan) | - |- | Karena tidak ada nilai di luar pagar IQR pada kedua kelompok, tidak diperlukan investigasi lebih lanjut untuk skor SUS. |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul (70/70 responden, tidak ada field kosong)
**2. Format:** [x] Konsisten / [ ]  Ada inkonsistensi: ____ ,  seluruh data berada dalam satu file Excel (dataset_penelitian_RTI), sheet DATA MENTAH, dengan header dan tipe kolom yang seragam untuk seluruh 70 baris.
**3. Range check (anomali):** Tidak ditemukan outlier pada skor SUS maupun Trust berdasarkan metode IQR (lihat Latihan 2). Seluruh nilai item mentah SUS/Trust berada dalam rentang valid 1–5, dan skor komposit SUS dalam rentang valid 0–100.
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____, Tidak ditemukan outlier pada skor SUS maupun Trust berdasarkan metode IQR (lihat Latihan 2). Seluruh nilai item mentah SUS/Trust berada dalam rentang valid 1–5, dan skor komposit SUS dalam rentang valid 0–100.

**Kesimpulan:** [x] Data siap analisis / [ ] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> "Data yang benar" hanya berarti nilai tersebut memang persis seperti yang diklik/diketik responden di form — secara teknis akurat sebagai rekaman kejadian. Tapi itu belum tentu "data yang dipercaya", karena bisa saja responden mengklik asal (straight-lining), mengisi dalam waktu terlalu singkat untuk benar-benar membaca pernyataan, atau ada baris yang salah label kelompok akibat kesalahan penggabungan sheet Form A dan Form B. "Dipercaya" berarti data itu sudah melewati pemeriksaan bahwa ia benar-benar merepresentasikan pengalaman nyata partisipan sesuai desain eksperimen, bukan sekadar tercatat secara teknis.

> Proses validasi formal tetap wajib meskipun Google Forms mengumpulkan data secara otomatis, karena otomatisasi hanya menjamin data tersimpan dengan rapi — ia tidak menjamin data itu valid secara substansi. Formulir otomatis tidak bisa mendeteksi bahwa seseorang menjawab tanpa membaca, atau bahwa satu baris tertukar kelompok saat penggabungan manual ke Excel. Karena itu, langkah completeness check, IQR, dan logic check pada worksheet ini tetap saya lakukan sebagai lapisan kepercayaan tambahan sebelum data ini dipakai untuk uji Mann-Whitney U di WS-14.
