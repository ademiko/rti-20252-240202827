# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Apakah desain antarmuka yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?
Hypothesis        : Terdapat penurunan skor usability dan tingkat kepercayaan yang signifikan secara statistik pada antarmuka dengan Urgency Dark Pattern dibandingkan antarmuka standar.
Tipe Eksperimen   : [ x ] Comparison  [ ] Ablation  [ ] Parameter
---
```
Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |Purwarupa aplikasi belanja baseline tanpa tekanan waktu.|UI Normal (Standar)|Skenario tugas (Batal langganan), layout dasar, dan platform pengujian (Figma) identik.|
| Treatment |Purwarupa aplikasi belanja dengan timer diskon hitung mundur palsu.|UI Urgency Dark Pattern|Skenario tugas, layout dasar, dan platform pengujian identik.|
```
---
Fairness Checklist:
  [x] Dataset identik untuk semua kondisi
  [x] Preprocessing setara
  [x] Tuning effort setara
  [x] Environment identik
  [x] Metrik evaluasi sama

```
Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    | Ada ketimpangan skill IT (Selection Bias) antara Kelompok A dan Kelompok B. | Melakukan pembagian kelompok secara acak (Random Assignment). |
| External    | Rasa panik di purwarupa Figma tidak senyata di aplikasi e-commerce sungguhan. | Membuat desain antarmuka High-Fidelity yang sangat detail dan realistis. |
| Construct   | Responden salah tafsir pertanyaan kuesioner atau mengisi secara asal-asalan. | Memakai kuesioner baku berbahasa Indonesia dan menyaring (drop) data yang anomali. |
| Conclusion  | Jumlah responden terlalu sedikit sehingga hasil uji statistik tidak valid. | Menetapkan target minimal 40 responden (20 per kelompok eksperimen). |
```
Statistical Plan:
  Uji statistik   : Mann-Whitney U Test (atau Independent T-Test jika data berdistribusi normal).
  Justifikasi      : Desain Between-Subjects menghasilkan dua kelompok sampel independen. Uji ini cocok untuk membandingkan perbedaan rata-rata skor SUS dan Trust antar dua kelompok
  Alpha            : 0.05 (Tingkat kepercayaan 95%)
  Effect size min  : Cohen’s d > 0.5 (Medium effect)
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah desain antarmuka yang menggunakan trik Urgency Dark Pattern menghasilkan skor usability dan tingkat kepercayaan pengguna yang secara signifikan lebih rendah dibandingkan antarmuka standar?
**Tipe eksperimen:** [x] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Kelompok A mencoba purwarupa bersih. | Antarmuka Normal |Task mencari halaman pengaturan, device bebas, batas waktu pengerjaan tidak dibatasi. |
| Treatment | Kelompok B mencoba purwarupa manipulatif | Antarmuka Dark Pattern | Task mencari halaman pengaturan, device bebas, batas waktu pengerjaan tidak dibatasi (hanya secara visual diintimidasi timer palsu). |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅Fair | Kedua kelompok diminta menyelesaikan satu skenario spesifik yang persis sama ("Membatalkan langganan premium"). |
| Preprocessing setara |✅Fair | Teks pengantar, instruksi awal, dan jaminan kerahasiaan (informed consent) yang dibaca responden sebelum tes dibuat sama persis. |
| Tuning effort setara | ✅Fair | Kualitas font, palet warna, dan kemulusan transisi frame di Figma dibuat sama tingginya. Dark pattern ditambahkan tanpa merusak resolusi desain. |
| Environment identik | ✅Fair | Keduanya disebar secara online tanpa moderasi, sehingga bebas dari tekanan tatap muka dengan peneliti. |
| Metrik evaluasi sama | ✅Fair | Sama-sama dinilai menggunakan skor akhir dari 10 soal SUS dan 5 soal Trust Scale. |

**Ada yang tidak fair?** [ ] Ya / [x] Tidak
> Jika ya, bagaimana cara memperbaikinya? Semua variabel kontrol sudah diisolasi dengan baik sehingga perbandingan Apple-to-Apple terjamin

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Selection Bias: Kelompok A isinya anak IT (paham UI), Kelompok B orang awam (mudah bingung). | *Menerapkan Random Assignment (pengacakan) saat membagi link purwarupa, dan menaruh pertanyaan "Fakultas/Latar Belakang Pekerjaan" di awal kuesioner. |
| External | Eksperimen dilakukan di Figma, sehingga tidak ada ancaman kehilangan uang sungguhan seperti di aplikasi e-commerce asli. Responden mungkin tidak merasa benar-benar panik. | Membuat purwarupa High-Fidelity yang sangat realistis (lengkap dengan logo bank/e-wallet tiruan) agar suasana simulasi terasa lebih nyata (immersive). |
| Construct | Responden salah memahami pertanyaan kuesioner atau mengisinya asal-asalan. | Menggunakan template SUS berbahasa Indonesia yang sudah tervalidasi dan memasang filter jika ada responden yang menjawab lurus angka 5 semua. |
| Conclusion | Jumlah sampel terlalu kecil sehingga hasil uji statistik tidak memiliki daya (underpowered). | Menetapkan target minimal 40 responden terverifikasi (20 per kelompok) sebagai baseline aman untuk uji perbedaan dua sampel independen |

**Ancaman mana yang paling sulit dimitigasi?** External Validity
**Mengapa?**
> Karena bagaimanapun canggihnya purwarupa Figma dibuat, secara sadar responden tahu bahwa ini hanya sekadar "tugas penelitian mahasiswa". Tekanan psikologis akibat timer hitung mundur palsu di Figma tidak akan sekuat ketika responden berhadapan dengan timer di aplikasi belanja sungguhan yang mengancam saldo rekening mereka.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah perbandingannya fair? (Apakah metode baru tersebut diberikan parameter tuning dan data preprocessing yang jauh lebih optimal dibandingkan metode baseline yang sengaja dibiarkan "apa adanya"?)
2. Apakah baseline yang dikalahkan memang yang terbaik saat ini (State-of-the-Art)? (Jangan-jangan hanya membandingkan dengan metode kuno yang memang sudah pasti kalah, bukan membandingkan dengan standar industri terkini).
3. Apakah perbedaannya signifikan secara statistik, dan apakah dampaknya terasa secara praktis (effect size)? (Kadang metode baru menang 0,1 detik lebih cepat, tapi secara statistik itu hanya variansi kebetulan dan secara praktik tidak membawa dampak berarti bagi pengguna).
