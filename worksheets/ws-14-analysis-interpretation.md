# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario     | Mean SUS | Std SUS | Mean Trust | Std Trust | n  |
   |--------------|----------|---------|------------|-----------|----|
   | Kontrol      | 77.0     | 7.01    | 4.11       | 0.33      | 35 |
   | Dark Pattern | 22.5     | 6.50    | 2.03       | 0.39      | 35 |

2. Uji Hipotesis:
   Uji yang digunakan   : Mann-Whitney U Test (one-tailed, arah: Kontrol > Dark Pattern)
   Justifikasi          : Dua kelompok independen (between-subjects), DV Trust Scale bersifat
                           ordinal, dan uji ini sudah ditetapkan sebagai primary test di
                           proposal (WS-07) sebelum data dikumpulkan — sesuai prinsip
                           pre-registration (WS-05).
   Hasil SUS   : U = 1225.0, p < 0.001 (p ≈ 2.95×10⁻¹³), Z = 7.19, effect size r = 0.86
   Hasil Trust : U = 1225.0, p < 0.001 (p ≈ 2.60×10⁻¹³), Z = 7.19, effect size r = 0.86

3. Keputusan:
   [x] H0 ditolak → H1 diterima (untuk kedua DV: SUS dan Trust)
   [ ] H0 tidak ditolak
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 2 (Kontrol vs Dark Pattern) |
| Apakah data berpasangan (paired)? | Tidak — between-subjects, tiap responden hanya mengalami satu kondisi (bukan orang yang sama dites dua kali) |
| Apakah distribusi normal? (uji normalitas) | Tidak diasumsikan normal secara default — Trust Scale adalah data ordinal (skala Likert 1–5), dan meskipun Total SUS bisa diperlakukan sebagai interval, dengan n=35 per kelompok uji non-parametrik lebih aman tanpa perlu bergantung pada asumsi normalitas Shapiro-Wilk yang belum tentu terpenuhi |
| **Uji yang dipilih:** | Mann-Whitney U Test |
| **Justifikasi:** | Dua grup independen, salah satu DV berskala ordinal (Trust), dan uji ini sudah dikunci sebagai rencana analisis sejak proposal (WS-07) — bukan dipilih setelah melihat hasil, sehingga terhindar dari p-hacking |

**Effect size yang akan dilaporkan:** [ ] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
**| Model | Kontrol | Dark Pattern  |  U | Z | p | r |**
|-------|----------------------|---|----|-----|----|----|
| Total SUS | 77.0 ± 7.01 | 22.5 ± 6.50 | 1225.0 | 7.19 | <0.001 | 0.86 |
| Rata-rata Trust | 4.11 ± 0.33 | 2.03 ± 0.39 | 1225.0 | 7.19 | <0.001 | 0.86 |

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | p < 0.001 untuk kedua DV, jauh di bawah α = 0.05 → signifikan secara statistik dengan sangat kuat |
| Effect size | r = 0.86 untuk SUS maupun Trust → **jauh melebihi ambang "large effect" (r ≥ 0.5)**, menunjukkan pemisahan antar kedua kelompok sangat tegas, bukan hanya signifikan tipis |
| Practical significance | Selisih mean SUS (77.0 vs 22.5 = beda 54.5 poin dari skala 0–100) dan Trust (4.11 vs 2.03) bukan sekadar signifikan secara statistik, tapi juga bermakna praktis: skor 77 dikategorikan "Good" secara industri sementara 22.5 dikategorikan "Awful" — perbedaan dua kategori kualitas usability yang jauh berbeda, bukan pergeseran kecil |
| Hubungan ke RQ | Hasil ini secara langsung menjawab RQ: desain antarmuka dengan Urgency Dark Pattern **memang** menghasilkan skor usability dan kepercayaan yang secara signifikan lebih rendah dibanding antarmuka standar — H1 didukung penuh oleh data |
| Perbandingan literatur | Sejalan dengan temuan-temuan sebelumnya (WS-03) yang bersifat kualitatif mengenai dampak negatif dark pattern terhadap trust pengguna; penelitian ini menambah bukti kuantitatif dengan effect size besar yang belum banyak dilaporkan secara eksplisit di gap literatur sebelumnya |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

> Karena hasil eksperimen saya justru **mendukung** H1 dengan sangat kuat (bukan hasil gagal/tidak signifikan), latihan ini saya kerjakan dalam dua bagian: (a) mengikuti skenario contoh di worksheet sebagai latihan murni memahami metode failure analysis, dan (b) refleksi jujur tentang potensi kelemahan hasil saya sendiri meskipun signifikan.

**(a) Skenario contoh dari worksheet:** Metode baru F1 = 83.2%, baseline = 84.7%, p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Bukan gagal total — p=0.12 berarti perbedaan yang teramati (83.2% vs 84.7%) belum cukup kuat untuk disimpulkan sebagai efek nyata dan bisa saja hanya variasi acak; ini adalah temuan valid bahwa metode baru **tidak terbukti lebih baik**, bukan bukti bahwa metode baru pasti buruk. |
| Kemungkinan penyebab? | Ukuran sampel kurang besar untuk mendeteksi perbedaan sekecil 1.5 poin F1 (*underpowered*), atau memang secara substansi kedua metode setara performanya pada dataset yang diuji. |
| Boundary condition? | Metode baru mungkin hanya unggul pada kondisi tertentu (misal dataset besar/noisy) yang tidak tercakup dalam eksperimen ini. |
| Insight yang bisa diambil? | Kompleksitas tambahan metode baru belum tentu sepadan dengan manfaatnya pada kondisi yang diuji — perlu pengujian pada kondisi lain sebelum diklaim lebih unggul. |
| Apakah layak dilaporkan? Mengapa? | Ya — hasil non-signifikan tetap kontribusi ilmiah yang jujur, mencegah klaim berlebihan dan membantu peneliti lain menghindari jalan buntu yang sama. |
 
**(b) Kelemahan potensial pada hasil saya sendiri (meski H1 didukung kuat):**
 
| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah effect size sebesar r=0.86 mungkin "terlalu sempurna"? | Ya, ini patut dicermati — pemisahan yang nyaris tanpa tumpang tindih (SUS Kontrol 60–90 vs Dark Pattern 10–37.5) lebih ekstrem dari efek dark pattern pada studi lapangan nyata. Kemungkinan penyebab: purwarupa Figma dark pattern dibuat *terlalu* mencolok/dipaksakan sehingga responden dengan mudah menyadarinya sebagai manipulasi (bukan dark pattern yang "halus" seperti di aplikasi nyata), sehingga efek yang terukur di simulasi lebih besar dari efek asli di dunia nyata. |
| Boundary condition? | Efek sebesar ini mungkin hanya berlaku pada dark pattern jenis *urgency/fake timer* yang eksplisit; jenis dark pattern lain yang lebih halus (misalnya *confirmshaming*, *hidden cost*) berpotensi menghasilkan effect size yang jauh lebih kecil dan perlu diuji terpisah. |
| Insight yang bisa diambil? | Studi lanjutan sebaiknya membandingkan beberapa tingkat "kehalusan" dark pattern (ablation study, seperti direncanakan di WS-06 Latihan 3) untuk mengetahui apakah efek sebesar ini konsisten atau khusus untuk desain yang sangat mencolok. |
 
**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| External | Simulasi Figma tanpa risiko finansial nyata, dan elemen urgency dibuat cukup mencolok | Effect size yang terukur (r=0.86) berpotensi lebih besar dari efek dark pattern di aplikasi e-commerce sungguhan (over-estimate) |
| Construct | Kesadaran responden terhadap "sedang diteliti" (mereka tahu ini simulasi akademik) | Bisa membuat responden lebih kritis/sadar terhadap manipulasi dibanding pengguna awam di kondisi nyata, memengaruhi skor Trust |
---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Sebelum mengerjakan worksheet ini, saya cenderung berpikir hasil penelitian hanya "berhasil" kalau H1 diterima dengan p<0.05 — dan kebetulan hasil saya memang seperti itu. Tapi mengerjakan Latihan 3 membuat saya sadar bahwa kekuatan sebuah riset bukan cuma soal signifikan atau tidak, melainkan seberapa jujur dan dalam saya menginterpretasikan *mengapa* angka itu muncul — termasuk mempertanyakan apakah effect size sebesar r=0.86 pada penelitian saya sendiri justru terlalu besar untuk dipercaya mentah-mentah sebagai representasi dunia nyata, bukan cuma dirayakan sebagai "hasil bagus". Ke depannya saya akan selalu menuliskan bagian limitation dan boundary condition bahkan ketika hasil signifikan, bukan hanya saat hasil gagal — supaya laporan riset saya tetap jujur dan tidak melebih-lebihkan klaim.

