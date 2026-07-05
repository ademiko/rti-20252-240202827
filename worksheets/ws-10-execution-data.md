# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     |          |      |           |        |       |             |
| 2     |          |      |           |        |       |             |
| 3     |          |      |           |        |       |             |
| ...   |          |      |           |        |       |             |

Jumlah runs per skenario : ____
Total runs               : ____

DATA LOG (per run):
  Run ID    : ____________________
  Timestamp : ____________________
  Skenario  : ____________________
  Input     : ____________________
  Output    : ____________________
  Anomali   : ____________________
  Catatan   : ____________________
```

---

## Latihan 1 — Execution Plan

Karena eksperimen saya adalah studi berbasis partisipan manusia (bukan komputasi ML), satu "run" = satu sesi partisipan menyelesaikan skenario tugas pada purwarupa Figma lalu mengisi kuesioner. "Seed" saya adaptasi menjadi nomor urut penugasan acak (randomization order) yang menentukan partisipan ke-N masuk ke Form A (Kontrol) atau Form B (Dark Pattern), bukan seed komputasi.

| Run # | Skenario | Kode Penugasan | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | KONTROL | RTI-001 | Link Prototipe A (Standar), device bebas | Selesai |
| 2 | KONTROL | RTI-002 | Link Prototipe A (Standar), device bebas | Selesai |
| 3 |DARK PATTERN |RTI-036 | Link Prototipe B (Urgency Timer), device bebas|Selesai |
| 4 |DARK PATTERN |RTI-037 | Link Prototipe B (Urgency Timer), device bebas|Selesai |

**Total skenario:** 2 (Kontrol vs Dark Pattern)
**Run per skenario:** 35
**Total run keseluruhan:** 70
>Distribusi tautan Form A dan Form B tidak dilakukan berurutan (bukan 35 kontrol dulu baru 35 dark pattern) untuk menghindari temporal confound, misalnya jika seluruh kelompok kontrol diisi di pagi hari (saat orang lebih fokus) dan kelompok dark pattern diisi malam hari (saat lelah), perbedaan skor bisa disebabkan waktu pengisian, bukan perlakuan. Penugasan disebar secara acak berselang-seling ke daftar calon responden sebelum link dikirim, sehingga kedua kelompok terkumpul dalam rentang waktu yang tumpang-tindih.
---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID (ID Responden) |RTI-001 |
| Timestamp | Tanggal & jam submit Google Form (otomatis tercatat oleh Forms) |
| Skenario | KONTROL / DARK PATTERN |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Kelompok/Kondisi | "Antarmuka Standar" / "Urgency Dark Pattern" |
| Form yang digunakan | Form A / Form B |
| Platform pengujian | Figma (purwarupa) + Google Forms (kuesioner) |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| SUS1–SUS10 (per item) |integer | 1–5 |
| Total SUS (skor komposit) | float | 0–100 |
| T1–T5 (Trust, per item)| integer | 1–5 |
|Rata-rata Trust | float| 1.0–5.0 |
|Task Selesai | kategorikal | "Ya" / "Tidak"|
|Frekuensi Belanja Online | kategorikal | 5 kategori (Sangat jarang → Sangat sering) |

**Format output:** [x] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: [x] Excel (.xlsx, sheet DATA MENTAH)
>Kolom Total SUS dan Rata2 Trust dihitung otomatis lewat formula di spreadsheet (bukan dihitung manual per responden), supaya tidak ada human error saat kalkulasi skor komposit dari 10+5 item mentah.
---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) | Responden membuka link Figma tapi menutup tab sebelum menyelesaikan tugas / tidak submit form sama sekali. | Data tidak masuk DATA MENTAH sama sekali → dicatat di log terpisah sebagai drop-out, tidak dihitung dalam N=70, tapi jumlah drop-out tetap dilaporkan untuk transparansi completion rate. |
| Hasil ekstrem | Skor SUS = 100 atau 0 persis pada kelompok Dark Pattern, sangat jauh dari rata-rata kelompok. | Investigasi manual: cek pola jawaban 10 item SUS — apakah semua item bernilai sama (indikasi asal isi) atau memang jawaban logis yang konsisten? Jika logis, tetap dipakai dan dicatat sebagai variasi wajar, bukan dihapus begitu saja. |
| Waktu eksekusi anomali | Task diselesaikan/form disubmit dalam <20 detik — tidak masuk akal untuk membaca 10 pernyataan SUS + 5 pernyataan Trust dengan cermat. |  Ditandai sebagai speeder, lalu dicek silang dengan pola jawaban (straight-lining). Jika terbukti asal klik, data di-drop dan dicatat alasannya di log. |
| Inkonsistensi dengan run lain | Satu responden Kontrol memberi skor SUS 15 (jauh di bawah rentang Kontrol 60–90) padahal Task Selesai = "Ya" dan seluruh navigasi normal. | Tidak langsung dihapus — dicek apakah ada faktor lain (misal device error, purwarupa lambat dimuat) melalui catatan kualitatif atau follow-up singkat bila memungkinkan; jika tidak ada penjelasan, tetap dilaporkan sebagai outlier di WS-11 dengan investigasi IQR, bukan dibuang diam-diam. |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Pada tugas-tugas kuliah sebelumnya, saya beberapa kali hanya mengandalkan 1-2 responden uji coba untuk menyimpulkan bahwa sebuah desain antarmuka "sudah bagus". Risikonya besar: dengan sampel sekecil itu, saya tidak bisa membedakan apakah hasil baik itu murni karena desainnya memang bagus, atau sekadar kebetulan karena responden tersebut kebetulan familiar dengan pola UI serupa.
**Yang akan dilakukan berbeda:**
> Dalam penelitian dark pattern ini saya sengaja menetapkan N=70 (35 per kelompok) sejak awal proposal, bukan menambah responden setelah melihat hasil awal terlihat "kurang meyakinkan" (itu justru bentuk p-hacking). Dengan jumlah run sebesar ini, saya bisa melihat distribusi skor secara utuh (Kontrol: mean 77, std 7.01; Dark Pattern: mean 22.5, std 6.5) dan bukan hanya angka tunggal, sehingga perbedaan antar kelompok bisa diuji signifikansinya secara statistik, bukan sekadar "terlihat beda di mata saya".


Konten1783039023600_dataset_penelitian_RTI_240202827.xlsxxlsxrti-20252-240202827-main (2).zipzip
