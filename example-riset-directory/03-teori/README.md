# Tahap 1 — Arsitektur, Desain, dan Landasan Teori Sistem

**Judul Penelitian:** Analisis Dampak Urgency Dark Pattern terhadap Usability dan User Trust pada Antarmuka E-Commerce
**Peneliti:** Ade Miko (NIM 240202827)
**Status:** Selesai (Perancangan)

---

## 1. Landasan Teori

Sistem yang dirancang pada tahap ini bukan produk akhir, melainkan **artifact eksperimental** (Design Science Research — Hevner et al., 2004) yang dibangun untuk menguji satu proposisi ilmiah secara terkontrol. Empat teori berikut menjadi fondasi setiap keputusan desain sistem.

### 1.1 Dark Pattern & Urgency Persuasion

**Dark Pattern** didefinisikan oleh Brignull (2010) sebagai elemen antarmuka yang sengaja dirancang untuk menjebak pengguna melakukan tindakan yang sebenarnya tidak mereka inginkan. Gray et al. (2018) mengklasifikasikan dark pattern ke dalam beberapa kategori strategi, salah satunya **Urgency** — menciptakan tekanan waktu palsu (misalnya *countdown timer* diskon) agar pengguna mengambil keputusan secara impulsif tanpa evaluasi rasional. Mathur et al. (2019), dalam studi empiris skala besar terhadap situs e-commerce, mengonfirmasi bahwa pola urgency-scarcity adalah salah satu jenis dark pattern paling banyak ditemukan di dunia nyata.

Landasan psikologis dari pola ini merujuk pada prinsip **Scarcity** dan **Urgency** dalam teori persuasi Cialdini (2009): manusia cenderung menilai sesuatu lebih berharga dan bertindak lebih cepat ketika mempersepsikan ketersediaannya terbatas dalam waktu. Prinsip inilah yang secara sengaja dimanipulasi menjadi komponen **Independent Variable (IV)** dalam sistem — bukan fitur produk, melainkan stimulus eksperimen yang bisa dinyalakan/dimatikan.

### 1.2 Usability & System Usability Scale (SUS)

**Usability** didefinisikan ISO 9241-11 sebagai sejauh mana suatu produk dapat digunakan oleh pengguna tertentu untuk mencapai tujuan tertentu secara efektif, efisien, dan memuaskan. **System Usability Scale (Brooke, 1996)** dipilih sebagai instrumen pengukuran karena merupakan skala baku, tervalidasi lintas domain, ringkas (10 item), dan menghasilkan skor komposit interval (0–100) yang memungkinkan perbandingan statistik antar kelompok. SUS menjadi dasar teoritis bagi komponen **Dependent Variable (DV) pertama** dalam sistem.

### 1.3 Trust Theory pada E-Commerce

**Kepercayaan (trust)** pengguna terhadap platform digital, menurut model McKnight, Choudhury, & Kacmar (2002), terbentuk dari persepsi terhadap *competence*, *benevolence*, dan *integrity* sistem. Manipulasi antarmuka yang terasa memaksa (seperti tekanan waktu palsu) berpotensi merusak persepsi *integrity* tersebut. Teori ini melandasi penggunaan **Trust Scale** (skala Likert 1–5) sebagai instrumen pengukuran **DV kedua**.

### 1.4 Desain Eksperimen Between-Subjects & Uji Statistik Non-Parametrik

Karena setiap partisipan hanya boleh terpapar satu kondisi (Normal atau Dark Pattern) — untuk menghindari *carry-over effect* dan bias pembelajaran — desain yang dipilih adalah **Between-Subjects Design** dengan **Random Assignment** untuk mengontrol *selection bias* (ancaman validitas internal). Karena data skor Trust bersifat ordinal dan ukuran sampel relatif kecil (target ≥40 responden, 20 per kelompok), maka uji hipotesis menggunakan **Mann-Whitney U Test** — uji non-parametrik yang tidak mensyaratkan asumsi distribusi normal, sesuai kaidah pemilihan uji statistik berdasarkan tipe data (skala NOIR).

**Ringkasan pemetaan teori → komponen sistem:**

| Landasan Teori | Konsep yang Dijelaskan | Komponen Sistem yang Merepresentasikannya |
|---|---|---|
| Dark Pattern Taxonomy (Gray et al., 2018) & Persuasion (Cialdini, 2009) | Mekanisme manipulasi urgency | Komponen visual *fake countdown timer* di purwarupa Treatment |
| Usability / SUS (ISO 9241-11; Brooke, 1996) | Kenyamanan interaksi | Instrumen kuesioner SUS di akhir alur pengujian |
| Trust Theory (McKnight et al., 2002) | Persepsi integritas sistem | Instrumen kuesioner Trust Scale |
| Between-Subjects Design & Mann-Whitney U | Kausalitas & validitas statistik | Mekanisme random assignment + modul analisis statistik |

---

## 2. Komponen Sistem

Sistem eksperimen terdiri dari empat komponen utama yang saling terhubung sebagai satu instrumen pengukuran, bukan sekadar rangkaian tools terpisah:

1. **Purwarupa Interaktif (Figma, High-Fidelity)** — dua varian antarmuka aplikasi belanja (skenario: pembatalan langganan premium):
   - **Grup Kontrol** — antarmuka standar, tanpa elemen tekanan waktu.
   - **Grup Perlakuan (Treatment)** — antarmuka identik, ditambah komponen *urgency dark pattern* (fake countdown timer diskon).
   - Kedua varian dijaga identik pada seluruh elemen non-IV (layout, palet warna, alur navigasi) agar manipulasi terisolasi hanya pada satu variabel.
2. **Platform Pengujian Tanpa Moderasi (Maze)** — meng-hosting kedua purwarupa, mendistribusikan tautan ke partisipan secara acak (random assignment), dan merekam data perilaku secara otomatis: *task completion time*, *misclick/error rate*, dan heatmap navigasi.
3. **Instrumen Kuesioner (Google Forms / built-in Maze)** — ditampilkan tepat setelah partisipan menyelesaikan skenario tugas; berisi 10 item SUS dan item Trust Scale (skala Likert 1–5), beserta pertanyaan latar belakang responden (untuk mendeteksi *selection bias*).
4. **Modul Analisis Data (Python — pandas, scipy, di Google Colab)** — membersihkan data mentah (cleaning, filtering respons anomali), menghitung skor komposit SUS dan rata-rata Trust, lalu menjalankan uji Mann-Whitney U untuk menentukan signifikansi statistik.

## 3. Arsitektur & Alur Sistem

```
Partisipan mendaftar/klik tautan
        │
        ▼
Random Assignment (Maze) ──► menentukan kelompok
        │
   ┌────┴─────┐
   ▼          ▼
Kelompok A   Kelompok B
(Kontrol)    (Treatment)
Purwarupa    Purwarupa
Normal       + Fake Timer
   │          │
   └────┬─────┘
        ▼
Partisipan menyelesaikan skenario tugas
(direkam otomatis: waktu, misclick, heatmap)
        │
        ▼
Kuesioner SUS + Trust Scale (wajib diisi, di dalam alur Maze)
        │
        ▼
Data terkumpul → diekspor sebagai dataset_eksperimen.csv
        │
        ▼
Modul Analisis (Python: cleaning → deskriptif → Mann-Whitney U)
        │
        ▼
Keputusan statistik: H0 ditolak / gagal ditolak (α = 0.05)
```

**Catatan desain penting:**
- **Fail-safe pengumpulan data**: seluruh field kuesioner diset *required*; jika partisipan keluar (drop) sebelum menyelesaikan alur Maze secara penuh, datanya otomatis tidak lengkap dan akan di-*exclude* saat cleaning, bukan diikutsertakan sebagian.
- **Isolasi variabel**: perubahan hanya terjadi pada satu komponen visual (timer), sehingga hasil pengukuran dapat ditelusuri secara langsung ke IV tanpa perancu dari elemen lain (prinsip *Traceability* & *Modularity*, WS-06).
- **Randomisasi** dilakukan oleh Maze pada level pembagian tautan, bukan manual, untuk mengurangi risiko *experimenter bias*.

## 4. Skema Data (Dataset Eksperimen)

Karena sistem ini adalah instrumen survei/perilaku (bukan aplikasi berbasis basis data transaksional), "skema database" pada konteks ini diwujudkan sebagai **struktur dataset tabular** yang menjadi output tunggal dari seluruh alur di atas, dan menjadi input bagi Tahap 4 (Analisis Data).

| Kolom | Tipe / Skala | Sumber | Deskripsi |
|---|---|---|---|
| `respondent_id` | Nominal | Maze | ID unik anonim per partisipan |
| `group` | Nominal | Maze (random assignment) | `control` / `treatment` |
| `task_completion_time_sec` | Ratio | Maze (log otomatis) | Durasi penyelesaian skenario tugas |
| `misclick_count` | Ratio | Maze (log otomatis) | Jumlah klik salah/tidak relevan selama tugas |
| `task_success` | Nominal | Maze (log otomatis) | Berhasil / gagal menyelesaikan tugas |
| `sus_item_1..10` | Ordinal (1–5) | Kuesioner SUS | Jawaban mentah 10 item baku SUS |
| `sus_score` | Interval (0–100) | Turunan (dihitung) | Skor komposit SUS hasil transformasi baku |
| `trust_item_1..n` | Ordinal (1–5) | Kuesioner Trust Scale | Jawaban mentah skala kepercayaan |
| `trust_score` | Ordinal (rata-rata 1–5) | Turunan (dihitung) | Rata-rata skor Trust Scale per responden |
| `background_info` | Nominal | Kuesioner (self-report) | Latar belakang IT/non-IT, untuk cek selection bias |

Baris data yang gagal lolos **Data Quality Check** (WS-05) — misalnya pola jawaban lurus/asal atau data tidak lengkap — ditandai dan dikeluarkan (drop) sebelum masuk ke tahap analisis statistik, bukan dihapus diam-diam tanpa dokumentasi.

## 5. Keputusan Teknis (Final)

1. **Tipe eksperimen**: Comparison Study, desain **Between-Subjects** dengan dua kondisi (Control vs Treatment) — bukan Within-Subjects, untuk menghindari efek pembelajaran/carry-over antar kondisi.
2. **Platform purwarupa**: **Figma** (High-Fidelity) — dipilih karena memungkinkan simulasi antarmuka realistis tanpa perlu pengembangan aplikasi penuh, sekaligus mempertahankan kontrol penuh atas elemen visual yang dimanipulasi.
3. **Platform pengujian**: **Maze** — dipilih karena mendukung *unmoderated testing*, random assignment otomatis, dan perekaman metrik perilaku (waktu, misclick, heatmap) tanpa perlu instrumentasi coding tambahan, sekaligus meniadakan *Hawthorne effect* dari kehadiran peneliti.
4. **Instrumen pengukuran**: SUS (baku, berbahasa Indonesia tervalidasi) dan Trust Scale (skala Likert 1–5) — dipilih karena representative, sensitive, dan feasible (kriteria WS-05), serta memiliki dasar teori yang kuat (Bagian 1).
5. **Target sampel**: minimal 40 partisipan (20 per kelompok), sebagai ambang aman untuk daya statistik uji dua sampel independen.
6. **Uji statistik**: **Mann-Whitney U Test** (α = 0.05), dengan alternatif Independent T-Test bila asumsi normalitas data terpenuhi — keputusan final ditentukan setelah uji normalitas pada Tahap 4.
7. **Alat analisis**: Python (pandas untuk cleaning, scipy untuk uji statistik) dijalankan di Google Colab — dipilih karena tidak memerlukan instalasi lokal dan mendukung reproducibility melalui notebook yang dapat dibagikan.
8. **Random seed**: dikunci di angka `42` pada tahap pembersihan/pengacakan data untuk menjamin repeatability hasil analisis.

---
