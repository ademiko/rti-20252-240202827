# 06-output

Hasil olahan data statistik & visualisasi komparatif — **Tahap 4** (lihat [../09-docs/tahap-4-analisis-data.md](../09-docs/tahap-4-analisis-data.md)).

Dihasilkan oleh skrip analitik Python (`05-kode/hypothesis_testing.py` via Google Colab) dari data mentah hasil kuesioner dan observasi partisipan `04-data/data_mentah.csv` (Total N=70 sampel; 35 Kontrol, 35 Perlakuan).

## tables/

| File | Isi |
|---|---|
| `descriptive_stats_sus_trust.csv` | Statistik deskriptif (Mean, Min, Max, Standar Deviasi) untuk metrik skor System Usability Scale (SUS) dan Trust Scale. Mengonfirmasi penurunan rata-rata yang sangat drastis pada aspek SUS (3.86 → 1.86) dan Trust (4.03 → 1.97) pada kelompok perlakuan akibat intervensi antarmuka. |
| `task_completion_metrics.csv` | Breakdown metrik *Task Success Rate* (Berhasil vs Gagal) dalam menyelesaikan skenario pembatalan pesanan komoditas antara kelompok Kontrol dan kelompok Perlakuan (*Urgency Dark Pattern*). |
| `demographic_summary.csv` | Ringkasan distribusi profil demografi partisipan (Usia, Jenis Kelamin, Frekuensi Belanja Online, dan Program Studi) untuk memvalidasi homogenitas sampel (*External Validity*). |
| `hypothesis_test_results.csv` | Hasil uji signifikansi komparatif menggunakan *Mann-Whitney U Test* yang memvalidasi diterimanya hipotesis alternatif (H1) secara mutlak (*p-value* = 0.00000 < 0.05) baik untuk variabel dependen Usability maupun User Trust. |

## figures/

| File | Isi |
|---|---|
| `fig_sus_boxplot.png` | *Boxplot chart* membandingkan distribusi kuartil dan membuktikan anjloknya skor Usability (SUS) secara ekstrem pada antarmuka *Urgency Dark Pattern* dibandingkan dengan antarmuka Standar. |
| `fig_trust_boxplot.png` | *Boxplot chart* membandingkan variansi dan nilai tengah (*median*) dari distribusi skor Kepercayaan Pengguna (Trust Scale) antara kelompok Kontrol dan Perlakuan. |
| `fig_task_completion_bar.png` | *Bar chart* persentase rasio keberhasilan tugas (*Task Selesai* vs *Task Gagal*) yang merepresentasikan beban kognitif nyata responden saat mencoba membatalkan pesanan. |
| `fig_effect_size_magnitude.png` | Visualisasi *Bar chart* sederhana yang menunjukkan besaran selisih (penurunan) skor aktual dan kekuatan efek (*Effect Size* $r$) akibat manipulasi visual *Dark Pattern*. |

## Acuan

[../09.../09-docs/tahap-4-analisis-data.md](../09-docs/tahap-4-analisis-data.md)
