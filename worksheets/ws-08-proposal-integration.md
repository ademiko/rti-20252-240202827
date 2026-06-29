# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment). Setiap section menjawab pertanyaan yang diangkat section sebelumnya dan memunculkan pertanyaan baru.
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

**Operasionalisasi Red Thread** (benang merah):
```
Bab 2 (Problem) → | memperkenalkan masalah X + evidensi |
                          ↓ menimbulkan pertanyaan: "apa akar gap-nya?"
Bab 3 (Gap)     → | menjawab pertanyaan tadi + membuka "lalu apa yang perlu diteliti?" |
                          ↓
Bab 4 (RQ/H)    → | menjawab gap dengan pertanyaan spesifik + prediksi terukur |
                          ↓
Bab 5-7 (Method)→ | menjawab RQ melalui desain eksperimen yang tepat |
```
Jika ada lompatan (section B tidak menjawab pertanyaan section A), red thread putus.

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [ ] Problem → Gap: masalah terdokumentasi di literatur
  [ ] Gap → RQ: pertanyaan menjawab gap spesifik
  [ ] RQ → Hypothesis: hipotesis memprediksi jawaban
  [ ] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [ ] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [ ] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [ ] Istilah sama di semua bagian
  [ ] Variabel di RQ = variabel di hipotesis = metrik di desain
  [ ] Scope tidak berubah dari masalah ke eksperimen

Cognitive Trap Checklist:
  [ ] Tidak ada paragraf "promosi" di pendahuluan (hanya data & gap)
  [ ] Metodologi disesuaikan ke RQ, bukan copy-paste textbook
  [ ] Timeline sudah ditambah buffer 30-50% dari estimasi awal
  [ ] Proposal mengakui kemungkinan H0 tidak ditolak (honest uncertainty)
  [ ] Tidak ada klaim "pasti berhasil" atau "meningkatkan signifikan"

Rubrik Self-Assessment:
| Kriteria     | 1 (Lemah)                                        | 2 (Cukup)                                     | 3 (Baik)                                           | Skor |
|------------- |--------------------------------------------------|-----------------------------------------------|----------------------------------------------------|------|
| Koherensi    | >2 koneksi vertikal terputus                     | 1-2 koneksi lemah, argumen masih bisa diikuti | Semua 6 koneksi terhubung, red thread jelas        |      |
| Specificity  | Variabel/metrik masih abstrak, tidak ada angka   | Sebagian metrik terdefinisi numerik           | Semua metrik + threshold + unit pengukuran jelas   |      |
| Feasibility  | Timeline >6 bulan tanpa memperhitungkan sumber   | Timeline 3-6 bulan dengan asumsi tertentu     | Timeline 1-3 bulan realistis dengan rencana detail |      |
| Rigor        | Baseline tidak jelas atau straw man              | 1-2 baseline dengan justifikasi partial       | 2+ baseline SOTA + justifikasi pemilihan lengkap   |      |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 |Pengguna e-commerce menghadapi manipulasi tekanan waktu palsu (Urgency Dark Pattern) yang secara nyata mengganggu kenyamanan navigasi dan menghancurkan rasa aman serta kepercayaan konsumen|
| Gap | WS-03 | Riset sebelumnya hanya bersifat kualitatif, belum ada pengukuran kuantitatif empiris absolut yang membandingkan besaran penurunan metrik usability dan trust secara langsung jika elemen urgensi ini diisolasi. |
| RQ | WS-04 | Apakah desain antarmuka e-commerce yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?|
| Hipotesis | WS-04 | H₁: Terdapat penurunan skor usability (SUS) dan tingkat kepercayaan pengguna (Trust Scale) yang signifikan secara statistik pada antarmuka bermuatan Urgency Dark Pattern dibandingkan baseline.|
| Variabel & Metrik | WS-05 | IV = Jenis Antarmuka (Normal vs Dark Pattern); DV: Tingkat kenyamanan (Skor komposit SUS 0-100) dan Kepercayaan (Skor Trust Scale ordinal 1-5).|
| Sistem | WS-06 | Dua purwarupa Figma interaktif (satu standar, satu manipulatif dengan fake timer) yang terhubung dengan platform pengujian otomatis (Maze) untuk merekam respons.|
| Desain Eksperimen | WS-07 | A/B Testing (Between-Subjects) mandiri pada 40 partisipan independen untuk membandingkan kelompok kontrol dan perlakuan, dianalisis menggunakan Mann-Whitney U Test. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | ✅| Masalah rusaknya atau hilangnya kenyamanan dan kepercayaan divalidasi oleh literatur, namun belum ada angka empiris yang mengukur seberapa parah kerusakan tersebut secara kuantitatif. |
| Gap → RQ | ✅| RQ secara langsung menanyakan perbandingan signifikan skor usability dan trust untuk mengisi kekosongan data kuantitatif yang belum terjawab. |
| RQ → Hypothesis | ✅ | H₁ secara presisi memprediksi jawaban RQ dengan menyatakan adanya "penurunan signifikan" pada skor SUS dan Trust Scale akibat Urgency Dark Pattern|
| Hypothesis → Metric | ✅ | Penurunan yang diprediksi diukur dengan metrik absolut yang jelas: Skor SUS (0-100) dan Trust Scale (1-5).|
| Metric → System | ✅ | Instrumen kuesioner elektronik diintegrasikan di akhir alur Maze untuk memastikan metrik terekam langsung setelah partisipan selesai bernavigasi. |
| System → Experiment | ✅ | Purwarupa Figma memfasilitasi pengujian A/B Testing secara unmoderated, menjaga isolasi variabel dan mencegah bias kehadiran peneliti (Hawthorne Effect). |

**Koneksi mana yang paling lemah?** Metric → System
**Bagaimana cara memperkuatnya?**
> Karena pelacakan metrik seperti waktu penyelesaian (Time on Task) atau error rate secara manual di Figma cukup sulit, koneksi ini diperkuat dengan mengintegrasikan purwarupa ke dalam platform usability testing khusus (seperti Maze) agar data kuantitatif terekam secara otomatis dan akurat.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [x] Ya / [ ] Tidak

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 | Alur argumen vertikal sangat mulus; masalah manipulasi psikologis terhubung langsung ke pengujian A/B Testing yang spesifik mengisolasi variabel timer.|
| Specificity | 3 | Metrik sudah didefinisikan dalam bentuk numerik yang tervalidasi secara global (Skor SUS komposit dan Skala Likert untuk Trust). |
| Feasibility | 3 | Desain sistem dan instrumen sangat realistis dieksekusi secara daring menggunakan perangkat lunak tanpa biaya tinggi seperti Figma dan Google Forms. |
| Rigor | 3 |Eksperimen memiliki validitas tinggi karena menerapkan Random Assignment, standardisasi instruksi, dan kontrol ketat terhadap variabel perancu (confounding variables).|

**Skor total:** 12 / 12

**Apakah proposal siap untuk fase eksekusi?** [x] Ya / [ ] Belum

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** Menentukan Metrik (WS-05) dan RQ (WS-04) karena instrumen pengukurannya (System Usability Scale dan Trust Scale) sudah baku di industri dan siap digunakan. RQ juga mudah ditarik karena variabel independen dan dependennya sangat terpusat. 
**Bagian tersulit:** Memastikan External Validity pada Desain Eksperimen (WS-07) karena tantangan terbesarnya adalah membuat simulasi Figma terasa nyata. Rasa panik yang muncul akibat "waktu habis" di purwarupa tidak akan 100% sama dengan aplikasi asli yang melibatkan transaksi finansial sungguhan.
**Yang akan dilakukan berbeda:**
> Jika mengulang dari awal, saya akan memasukkan satu tahapan pilot testing singkat pada beberapa orang responden di luar target sampel sebelum menyusun proposal final. Hal ini penting untuk memverifikasi apakah timer manipulatif yang dibuat di Figma benar-benar mampu memicu efek terburu-buru, sehingga arsitektur purwarupa bisa disempurnakan lebih matang sejak awal eksperimen.
