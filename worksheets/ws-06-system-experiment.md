# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Apakah desain antarmuka yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Jenis Antarmuka| IV   |Purwarupa interaktif (Figma)|Memanipulasi komponen UI: mengaktifkan/menonaktifkan elemen Urgency (fake timer).|
|Usability & Kepercayaan| DV   |Instrumen Kuesioner (Google Forms / Maze)|Mengukur respons melalui kuesioner SUS dan Trust Scale setelah simulasi.|
|Skenario Tugas| CV   |Alur Navigasi (User Flow)|Mengunci alur penyelesaian tugas agar persis sama untuk kedua kelompok.|

4 Prinsip Desain:
  [ x ] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [ x ] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [ x ] Measurement Integration — Pengukuran DV built-in
  [ x ] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : Interaksi klik dan waktu respons dari pengguna.
  Parameter      : Versi antarmuka (Normal vs Dark Pattern).
  Output format  : Skor komposit (0-100 untuk SUS) dan skala ordinal (1-5 untuk kepercayaan) dalam format CSV/Excel.
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Apakah desain antarmuka yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Trik Dark Pattern | IV | Komponen visual di Frame Figma | Mengganti tampilan frame (tambah/hapus banner timer diskon palsu). |
| Skor SUS | DV | Modul pengumpulan data (Google Forms) | Menghitung otomatis skor dari 10 pertanyaan baku SUS. |
| Skenario Tugas | CV | User Flow Checkout | Memastikan tombol navigasi utama tidak diubah ukurannya atau posisinya. |

**Apakah semua variabel bisa di-map?** [x] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan?Tidak ada komponen yang perlu ditambahkan karena variabel teknis dan psikologis sudah terwakili oleh purwarupa dan instrumen kuesioner

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | ✅ Memenuhi | Variabel independen terpetakan langsung ke varian desain di Figma, dan variabel dependen ke form kuesioner. |
| Modularity | ✅ Memenuhi | Elemen Dark Pattern dibuat sebagai component independen di Figma, sehingga bisa dihidupkan/dimatikan tanpa merusak layout dasar aplikasi. |
| Controllability | ✅ Memenuhi | Skenario tugas, instruksi awal, dan durasi pengerjaan dibakukan dalam bentuk script eksperimen yang dikontrol ketat oleh peneliti. |
| Measurability | Sebagian | Hasil survei otomatis terekap di spreadsheet, namun pelacakan durasi (Task Completion Time) murni di Figma cukup sulit secara bawaan. |

**Prinsip mana yang paling sulit dipenuhi?** Measurability (khususnya untuk akurasi waktu penyelesaian tugas di Figma).
**Strategi untuk mengatasinya:**
> Mengintegrasikan purwarupa Figma dengan platform unmoderated testing (seperti Maze atau Useberry). Platform ini akan bertindak sebagai "sistem perekam" yang otomatis mencatat durasi, jumlah salah klik (misclick), dan heatmap tanpa perlu coding dari nol

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama,(dalam konteks Urgency Dark Pattern), rencanakan ablation study untuk melihat elemen mana yang paling manipulatif.

| Kondisi | Komponen A (Fake Timer) | Komponen B (Low Stock Warning) | Komponen C (Social Proof/Activity) | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | ✅ aktif | ✅ aktif | ✅ aktif| Penurunan skor SUS dan Kepercayaan paling parah (Baseline) |
| – A | ❌ dinonaktifkan | ✅ aktif | ✅ aktif | Melihat apakah tanpa tekanan waktu, pengguna menjadi lebih logis. |
| – B | ✅ aktif | ❌ dinonaktifkan| ✅ aktif | Mengukur dampak ancaman kelangkaan barang (scarcity). |
| – C | ✅ aktif | ✅ aktif | ❌ dinonaktifkan | Mengukur efek fear of missing out (FOMO) komunal. |

**Komponen mana yang diprediksi paling berkontribusi?** Komponen A (Fake Countdown Timer).
**Mengapa?**
> Karena elemen ini memberikan tekanan kognitif dan visual secara langsung berupa waktu yang terus berkurang. Hal ini memicu kepanikan dan memaksa pengguna untuk mengambil keputusan impulsif (terburu-buru) tanpa sempat membaca informasi lain secara rasional, sehingga sangat merusak kenyamanan navigasi

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibangun penuh layaknya produk rilis (monolitik) sebelum dieksperimen, peneliti tidak akan bisa mengetahui elemen spesifik mana yang sebenarnya memengaruhi perilaku pengguna. Variabel pengganggu (noise) akan sangat banyak—apakah pengguna bingung karena ada Dark Pattern, atau sekadar karena warna tombolnya kurang mencolok, atau karena aplikasinya lag?
> Arsitektur yang modular (seperti memisahkan elemen manipulatif ke komponen tersendiri) sangat penting dalam riset karena memungkinkan penerapan prinsip Isolasi Variabel. Peneliti bisa membongkar-pasang satu komponen secara terukur sambil memastikan bahwa kondisi sistem lainnya tetap konstan dan adil untuk dibandingkan.
 
