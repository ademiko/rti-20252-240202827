# Tahap 1 — Perancangan Eksperimen & Variabel

**Status:** Selesai
**Judul Penelitian:** Pengaruh Urgency Dark Pattern pada Antarmuka Aplikasi E-Commerce terhadap Tingkat Usability dan Kepercayaan Pengguna Menggunakan Metode A/B Testing

---

## 1. Komponen Sistem (Instrumen Eksperimen)

Penelitian ini berada di ranah *Human-Computer Interaction* (HCI), sehingga "sistem" bukan backend server melainkan **instrumen pengujian** yang terdiri dari tiga lapisan:

1. **Presentation Layer (Figma)** — High-Fidelity Prototype aplikasi e-commerce, dirender via WebGL sehingga dapat diakses langsung dari browser tanpa instalasi. Dibangun dalam **dua varian purwarupa** yang identik kecuali pada satu elemen intervensi:
   - **Purwarupa A (Kontrol)** — antarmuka standar, bersih, mengikuti SOP e-commerce umum.
   - **Purwarupa B (Perlakuan)** — antarmuka yang disisipi *Urgency Dark Pattern* (fake countdown timer, *loss aversion text*, tombol asimetris) pada titik intervensi yang sama.
2. **Tracking & Execution Layer (Maze)** — purwarupa Figma diintegrasikan ke Maze sebagai platform *unmoderated usability testing*. Lapisan ini merekam telemetri partisipan secara otomatis: *time on task*, *task success rate*, dan *misclick rate*, tanpa kehadiran peneliti (menghindari *Hawthorne effect*).
3. **Data Collection & Analytics Layer (Google Forms + Google Colab)** — Google Forms menangkap data persepsi (kuesioner SUS dan Trust Scale) segera setelah sesi tugas selesai. Data mentah (`.csv`) kemudian ditarik ke Google Colab untuk dibersihkan dan diuji secara statistik menggunakan Python (Pandas & SciPy).

## 2. Alur Eksekusi Eksperimen (Between-Subjects A/B Testing)

```
Partisipan direkrut (N=70, pengguna aktif e-commerce usia 18-25 tahun)
  │
  ├─ Random assignment otomatis → 2 kelompok independen (tidak ada tumpang tindih)
  │     ├─ Kelompok Kontrol   (n=35) → Purwarupa A (standar)
  │     └─ Kelompok Perlakuan (n=35) → Purwarupa B (Urgency Dark Pattern)
  │
  ├─ Briefing & informed consent
  │     └─ Keberadaan elemen manipulatif TIDAK diungkap (agar perilaku tetap alami)
  │
  ├─ Sesi tugas tunggal (mandiri, unmoderated, direkam Maze)
  │     └─ Skenario: masuk akun → cari pengaturan pesanan → batalkan pesanan
  │           ├─ Kontrol   → pop-up konfirmasi standar ("Yakin ingin membatalkan?")
  │           └─ Perlakuan → pop-up pencegatan: fake countdown timer,
  │                          peringatan voucher hangus, tombol "Tetap Batalkan"
  │                          dibuat kecil & pudar vs tombol "Kembali" besar & terang
  │
  ├─ Maze mencatat: time on task, success/fail, misclick rate
  │
  └─ Kuesioner pasca-tugas (Google Forms, wajib diisi sebelum sesi ditutup)
        ├─ SUS — 10 item, skala Likert 1-5 → skor komposit 0-100
        └─ Trust Scale — skala 1-5
              └─ Tersimpan ke data_mentah.csv → input Tahap 4 (Mann-Whitney U Test)
```

**Catatan menjaga validitas (analog *fail-closed* pada sistem produksi):** seluruh partisipan menerima instruksi tertulis identik; tata letak tombol navigasi utama tidak diubah di kedua purwarupa; kuesioner bersifat wajib (*required field*) di Google Forms sehingga sesi tidak bisa ditutup tanpa data lengkap; sesi yang gagal menyelesaikan tugas tetap dicatat (ditandai "Gagal"), bukan dibuang, agar *task success rate* tetap merepresentasikan kondisi nyata.

## 3. Skema Variabel Penelitian

| Variabel | Peran | Definisi Operasional | Instrumen / Sumber | Tipe Data |
|---|---|---|---|---|
| Jenis Antarmuka | **IV** (Independent) | Standar (Kontrol) vs Urgency Dark Pattern (Perlakuan) | Purwarupa Figma A/B | Nominal |
| Usability | **DV** utama | Skor komposit System Usability Scale | Kuesioner SUS (Google Forms) | Ratio-like (0-100) |
| User Trust | **DV** utama | Rata-rata skor Trust Scale | Kuesioner Trust Scale (Google Forms) | Ordinal/Interval (1-5) |
| Task Success Rate | DV pendukung | Berhasil/gagal menyelesaikan pembatalan pesanan | Telemetri Maze | Nominal (biner) |
| Time on Task | DV pendukung | Durasi penyelesaian tugas | Telemetri Maze | Ratio (detik) |
| Misclick Rate | DV pendukung | Jumlah klik keliru selama navigasi | Telemetri Maze | Ratio (count) |
| Skenario tugas & struktur informasi | **CV** (Control) | Instruksi, alur, dan tata letak dasar dikunci identik | Desain purwarupa | — |
| Usia partisipan (18-25 tahun) | CV | Rentang usia dibatasi untuk homogenitas sampel | Kuesioner demografi | — |

## 4. Skema Struktur Data (Dataset Respons — `data_mentah.csv`)

| Kolom | Tipe | Keterangan |
|---|---|---|
| `participant_id` | STRING | ID unik anonim per partisipan |
| `kelompok` | STRING | `KONTROL` atau `DARK PATTERN` |
| `usia` | INTEGER | 18–25 |
| `jenis_kelamin` | STRING | Data demografi (validasi *external validity*) |
| `frekuensi_belanja_online` | STRING | Data demografi |
| `program_studi` | STRING | Data demografi |
| `task_success` | BOOLEAN (0/1) | Berhasil/gagal membatalkan pesanan |
| `time_on_task_detik` | INTEGER | Durasi dari Maze |
| `misclick_count` | INTEGER | Jumlah klik keliru dari Maze |
| `SUS_1` … `SUS_10` | INTEGER (1-5) | Item mentah kuesioner SUS |
| `Total_SUS` | FLOAT (0-100) | Skor komposit SUS terhitung |
| `Trust_1` … `Trust_n` | INTEGER (1-5) | Item mentah kuesioner Trust Scale |
| `Rata2_Trust` | FLOAT (1-5) | Rata-rata skor Trust Scale |
| `timestamp` | DATETIME | Waktu penyelesaian sesi |

Data ini bersifat mentah (raw), disimpan permanen di `04-data/data_mentah.csv`, dan menjadi *source of truth* untuk seluruh perhitungan statistik pada Tahap 4 — tidak ada agregasi/penghapusan baris sebelum tahap pembersihan data resmi.

## 5. Skema Platform & Integrasi (pengganti skema cache)

| Platform | Peran | Output | Catatan |
|---|---|---|---|
| **Figma** | Presentation layer — purwarupa High-Fidelity | 2 varian antarmuka interaktif (A/B) | Diakses via browser (WebGL), tanpa instalasi |
| **Maze** | Tracking & execution layer — unmoderated testing | Telemetri: success rate, time on task, misclick rate | Otomatis mengarahkan partisipan ke Google Forms setelah tugas selesai |
| **Google Forms** | Instrumen pengukuran persepsi | Respons SUS & Trust Scale (ekspor CSV) | Wajib diisi sebelum sesi ditutup |
| **Google Colab (Python: Pandas, SciPy)** | Data cleaning & pengujian hipotesis | `data_mentah.csv` → tabel statistik (Tahap 4) | Menjalankan Mann-Whitney U Test, α = 0.05 |

## 6. Keputusan Teknis (Final)

1. **Desain eksperimen**: *Between-Subjects* A/B Testing (bukan *within-subject*) — dipilih untuk menghindari efek pembelajaran (*learning/carry-over effect*) jika satu partisipan terpapar kedua kondisi.
2. **Ukuran & alokasi sampel**: minimal N=70 (35 Kontrol, 35 Perlakuan), pengguna aktif e-commerce usia 18-25 tahun, dialokasikan lewat *random assignment* otomatis untuk meminimalkan *selection bias*.
3. **Instrumen pengukuran**: System Usability Scale (John Brooke, 1986) untuk usability, dan Trust Scale untuk kepercayaan pengguna — keduanya dipilih karena validitas konstruk yang sudah teruji secara akademis.
4. **Stack teknis**: Figma (purwarupa High-Fidelity, WebGL), Maze (unmoderated usability testing), Google Forms (kuesioner digital terintegrasi), Google Colab dengan Python (Pandas, SciPy) untuk pipeline analisis — bukan implementasi backend/server, karena fokus eksperimen ada di lapisan antarmuka (frontend/HCI), bukan infrastruktur.
5. **Skenario tugas**: satu skenario tunggal (pembatalan pesanan/langganan) identik untuk kedua kelompok; satu-satunya perbedaan adalah keberadaan elemen Urgency Dark Pattern pada titik konfirmasi di Purwarupa B.
6. **Pertimbangan etis**: elemen manipulatif tidak diungkap saat *briefing* untuk menjaga validitas ekologis (*ecological validity*), namun eksperimen tidak melibatkan transaksi finansial nyata — murni simulasi — untuk meminimalkan risiko kerugian riil bagi partisipan.
7. **Teknik analisis**: Mann-Whitney U Test (α = 0.05) dipilih karena data tidak berdistribusi normal (uji asumsi awal mengonfirmasi hal ini); dilengkapi perhitungan *effect size* untuk mengukur besaran dampak, bukan sekadar signifikansi.
8. **Kontrol variabel (fairness)**: skenario tugas, struktur informasi, dan tata letak tombol navigasi utama dikunci identik pada kedua purwarupa, agar selisih skor SUS/Trust benar-benar berasal dari isolasi variabel Urgency Dark Pattern, bukan *confounding variable* lain.

---

*Acuan: [`01-proposal/proposal rti.pdf`](../01-proposal/proposal%20rti.pdf), [`03-teori/README.md`](../03-teori/README.md), [`05-kode/README.md`](../05-kode/README.md).*
