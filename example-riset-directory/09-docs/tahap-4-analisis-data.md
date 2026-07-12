# Tahap 4 — Ekstraksi Data & Visualisasi

**Status:** Selesai — pipeline analisis sudah dijalankan atas dataset final (N=70, 35 Kontrol/35 Perlakuan), tabel & figure tersedia di `06-output/`
**Bergantung pada:** [tahap-3-eksekusi-eksperimen.md](tahap-3-eksekusi-eksperimen.md)
**Lokasi kode:** [../05-kode/analysis](../05-kode/analysis) (dieksekusi via Google Colab)

---

## Tujuan

Mengolah data mentah hasil eksperimen (`04-data/data_mentah.csv`) — respons kuesioner SUS & Trust Scale serta telemetri *task success* dari Maze — menjadi statistik deskriptif, uji signifikansi (Mann-Whitney U Test), perhitungan *effect size*, dan visualisasi pembanding Kontrol vs Perlakuan untuk Tahap 5.

## Deliverable

- [x] Skrip pemuatan data (`load_dataset.py` / sel Colab) — baca `data_mentah.csv`, pisahkan `group_kontrol` vs `group_dark_pattern`
- [x] Statistik deskriptif (mean, min, max, standar deviasi) skor SUS dan Trust Scale per kelompok
- [x] Ringkasan demografi partisipan (usia, jenis kelamin, frekuensi belanja online, program studi) untuk validasi homogenitas sampel (*external validity*)
- [x] Breakdown *task completion* (Berhasil vs Gagal) per kelompok dari telemetri Maze
- [x] Uji signifikansi non-parametrik **Mann-Whitney U Test** (α = 0,05) untuk variabel Usability (SUS) dan Trust
- [x] Perhitungan *effect size* untuk mengukur besaran dampak, bukan sekadar signifikansi
- [x] Visualisasi *boxplot* & *bar chart* perbandingan Kontrol vs Perlakuan
- [x] Ringkasan tabel & figure hasil untuk Tahap 5 (`06-output/tables/`, `06-output/figures/`)

## Desain yang Diimplementasikan

### Struktur kode (`05-kode/analysis/`, dijalankan via Google Colab)

```
05-kode/analysis/
├── requirements.txt       # pandas, numpy, scipy, matplotlib
├── load_dataset.py         # baca data_mentah.csv, split group_kontrol vs group_dark_pattern
├── descriptive_stats.py    # mean/min/max/std SUS & Trust per kelompok + ringkasan demografi
├── task_completion.py       # breakdown Task Selesai vs Gagal per kelompok
├── hypothesis_testing.py    # Mann-Whitney U Test (SUS & Trust) + effect size
├── charts.py                 # 4 figure PNG -> 06-output/figures/
└── run_all.ipynb              # notebook Colab yang menjalankan seluruh sel di atas berurutan
```

Dataset yang dimuat memiliki kolom: `No`, `ID Responden`, `Kelompok`, `Kondisi`, `Prodi`, `Frekuensi Belanja Online`, `Task Selesai`, item-item `SYSTEM USABILITY SCALE (SUS)`, dan item-item `TRUST SCALE` (masing-masing 1 kolom per pernyataan kuesioner).

### Cuplikan skrip pengujian hipotesis (dieksekusi via Google Colab)

```python
import pandas as pd
from scipy import stats

# Memuat data hasil pengujian purwarupa Figma & Google Forms
df = pd.read_csv('data_mentah.csv')
group_kontrol = df[df['Kelompok'] == 'KONTROL']
group_dark_pattern = df[df['Kelompok'] == 'DARK PATTERN']

# Uji Variabel Usability (SUS)
stat_sus, p_sus = stats.mannwhitneyu(group_kontrol['Total SUS'].dropna(),
                                     group_dark_pattern['Total SUS'].dropna(),
                                     alternative='two-sided')

# Uji Variabel Kepercayaan (Trust)
stat_trust, p_trust = stats.mannwhitneyu(group_kontrol['TRUST SCALE'].dropna(),
                                          group_dark_pattern['TRUST SCALE'].dropna(),
                                          alternative='two-sided')

print(f"P-Value (SUS)   = {p_sus:.5f}")
print(f"P-Value (Trust) = {p_trust:.5f}")
```

### Modul

| Modul | Fungsi utama | Output |
|---|---|---|
| `load_dataset.py` | Baca & bersihkan `data_mentah.csv`, drop NaN, split per kelompok | DataFrame tidy (dipakai modul lain) |
| `descriptive_stats.py` | Statistik deskriptif SUS/Trust + ringkasan demografi | `descriptive_stats_sus_trust.csv`, `demographic_summary.csv` |
| `task_completion.py` | Breakdown Task Selesai vs Gagal per kelompok | `task_completion_metrics.csv` |
| `hypothesis_testing.py` | Mann-Whitney U Test + effect size (r / Cohen's d) | `hypothesis_test_results.csv` |
| `charts.py` | `fig_sus_boxplot`, `fig_trust_boxplot`, `fig_task_completion_bar`, `fig_effect_size_magnitude` | 4x PNG di `06-output/figures/` |

## Hasil

### Statistik Deskriptif (`descriptive_stats_sus_trust.csv`, N=70; 35 Kontrol, 35 Perlakuan)

| Metrik | Kontrol (mean) | Dark Pattern (mean) | Selisih |
|---|---|---|---|
| Skor SUS (0-100 skala komposit, ditampilkan dalam basis kuesioner) | **3,86** | **1,86** | **-2,00** |
| Skor Trust Scale (1-5) | **4,03** | **1,97** | **-2,06** |

Kedua metrik menunjukkan penurunan rata-rata yang sangat kontras pada kelompok Perlakuan dibanding Kontrol — konsisten dengan hipotesis awal (H1) bahwa elemen *Urgency Dark Pattern* menurunkan usability dan kepercayaan pengguna.

### Hasil Uji Hipotesis (`hypothesis_test_results.csv`, lihat juga `fig_effect_size_magnitude.png`)

```
=== HASIL UJI HIPOTESIS (MANN-WHITNEY U TEST) ===
P-Value (SUS)   = 0.00000
Kesimpulan SUS  : H1 Diterima (Ada perbedaan SIGNIFIKAN akibat Dark Pattern)

P-Value (Trust) = 0.00000
Kesimpulan Trust: H1 Diterima (Ada perbedaan SIGNIFIKAN akibat Dark Pattern)
```

Karena kedua *p-value* < 0,05, Hipotesis Alternatif (H1) diterima untuk **kedua** variabel dependen: baik Usability maupun Trust terbukti berbeda secara signifikan antara kelompok Kontrol dan kelompok Perlakuan. *Effect size* dihitung mendampingi hasil ini untuk menunjukkan bahwa besaran perbedaan bukan hanya signifikan secara statistik, tetapi juga besar secara praktis (bukan sekadar signifikansi ambang batas).

### Task Completion (`task_completion_metrics.csv`, `fig_task_completion_bar.png`)

Breakdown *Task Selesai* vs *Gagal* per kelompok menunjukkan tingkat keberhasilan penyelesaian tugas (pembatalan pesanan) pada kelompok Perlakuan lebih rendah dibanding Kontrol — merepresentasikan beban kognitif nyata yang dialami responden saat mencoba membatalkan pesanan di tengah tekanan visual *fake countdown timer* dan tombol asimetris.

### Ringkasan Demografi (`demographic_summary.csv`)

Distribusi usia, jenis kelamin, frekuensi belanja online, dan program studi partisipan dirangkum untuk memvalidasi homogenitas sampel antar kedua kelompok (*external validity*) — memastikan perbedaan skor SUS/Trust yang ditemukan bukan disebabkan oleh perbedaan komposisi demografi antar kelompok.

### Boxplot SUS & Trust (`fig_sus_boxplot.png`, `fig_trust_boxplot.png`)

*Boxplot* membandingkan distribusi kuartil kedua metrik, menunjukkan secara visual anjloknya skor Usability dan menyempit/menurunnya median skor Trust pada kelompok Perlakuan dibanding Kontrol — melengkapi angka rata-rata di atas dengan gambaran sebaran data, bukan sekadar titik tunggal.

### Catatan untuk Tahap 5

- Penurunan skor SUS (3,86 → 1,86) dan Trust (4,03 → 1,97) tergolong sangat besar untuk skala pengukuran ini — relevan untuk penekanan pada bagian "Pembahasan" bahwa dampaknya bukan sekadar signifikan secara statistik, melainkan juga besar secara praktis.
- *Task completion rate* yang lebih rendah pada kelompok Perlakuan memperkuat argumen bahwa dark pattern tidak hanya menurunkan persepsi (SUS/Trust) tetapi juga performa aktual (kemampuan menyelesaikan tugas) — poin penting untuk bagian "Kontribusi" paper.
- Karena eksperimen berlangsung di lingkungan simulasi Figma (tanpa risiko finansial nyata), keterbatasan ini perlu ditegaskan kembali di bagian "Keterbatasan"/"Saran Penelitian Lanjutan" pada Tahap 5.
- Seluruh angka di atas dihitung dari N=70 (35/35); lihat `descriptive_stats_sus_trust.csv` untuk standar deviasi (dipakai sebagai *error bar* pada figure).

---

*Acuan: [tahap-3-eksekusi-eksperimen.md](tahap-3-eksekusi-eksperimen.md), [../06-output/README.md](../06-output/README.md), [../05-kode/README.md](../05-kode/README.md).*
