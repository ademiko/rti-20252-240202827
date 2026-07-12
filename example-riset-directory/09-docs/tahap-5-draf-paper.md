# Tahap 5 — Penulisan Draf Paper Jurnal

**Status:** Draf konten inti selesai — kerangka naskah lengkap (5 bagian + kesimpulan) tersusun di [../07-manuskrip/README.md](../07-manuskrip/README.md), matriks tinjauan pustaka (15 entri terannotasi) tersedia di [../02-literatur/](../02-literatur/). Sisa pekerjaan: pemecahan ke file per bagian, penyusunan bibliografi terformat, dan pemindahan ke template jurnal tujuan (lihat "Yang Masih Perlu Dilengkapi").
**Bergantung pada:** [tahap-4-analisis-data.md](tahap-4-analisis-data.md) — *Selesai*

---

## Tujuan

Menyusun draf naskah ilmiah dengan gaya bahasa akademis formal, objektif, dan pasif, sesuai target publikasi **Sinta 4 (Jurnal JAMI — Jurnal Ahli Muda Indonesia)**, berdasarkan hasil eksperimen A/B Testing *Urgency Dark Pattern* pada Tahap 1–4.

## Rencana Deliverable (Struktur Naskah)

| Bagian | File Rencana | Status |
|---|---|---|
| Pendahuluan (latar belakang, gap, RQ, kontribusi) | `07-manuskrip/02-pendahuluan.md` | Konten inti selesai di [README.md §1](../07-manuskrip/README.md) — belum dipecah ke file terpisah |
| Tinjauan Pustaka (definisi Urgency Dark Pattern, SUS, Trust Scale, *related work*) | `07-manuskrip/03-tinjauan-pustaka.md` | Konten inti selesai di [README.md §2](../07-manuskrip/README.md); didukung matriks 15 entri di [../02-literatur/review fiksss.csv](../02-literatur/review%20fiksss.csv) |
| Metodologi (desain eksperimen, purwarupa A/B, variabel, prosedur) | `07-manuskrip/04-metodologi.md` | Konten inti selesai di [README.md §3](../07-manuskrip/README.md), mengacu [tahap-1](tahap-1-perancangan-eksperimen.md)–[tahap-3](tahap-3-eksekusi-eksperimen.md) |
| Hasil & Pembahasan (statistik deskriptif, uji Mann-Whitney U, *effect size*) | `07-manuskrip/05-hasil-pembahasan.md` | Konten inti selesai di [README.md §4](../07-manuskrip/README.md), mengacu [tahap-4-analisis-data.md](tahap-4-analisis-data.md) dan [../06-output/](../06-output/) |
| Kesimpulan & Saran Penelitian Lanjutan | `07-manuskrip/06-kesimpulan.md` | Konten inti selesai di [README.md §5](../07-manuskrip/README.md) |
| Abstrak (ID & EN) | `07-manuskrip/01-abstrak.md` | **Belum dibuat** — perlu diringkas dari §1 & §4 |
| Daftar Pustaka (terformat sesuai gaya JAMI) | `07-manuskrip/07-daftar-pustaka.md` | **Belum diformat** — 16 referensi tersedia di Daftar Pustaka proposal ([../01-proposal/proposal%20rti.pdf](../01-proposal/proposal%20rti.pdf)), belum disusun ulang ke format sitasi baku (APA/IEEE) & belum ada berkas BibTeX terpisah |
| Naskah konsolidasi (template jurnal) | `07-manuskrip/naskah-jurnal.md` / `.docx` | **Belum disusun** — masih berupa outline diperluas di `README.md`, belum digabung jadi satu naskah utuh |

## Yang Masih Perlu Dilengkapi Sebelum Submit

1. **Pemecahan outline menjadi naskah utuh** — konten `07-manuskrip/README.md` saat ini berbentuk *extended outline* per bagian; perlu ditulis ulang menjadi paragraf naskah akademik penuh (bukan poin-poin) sesuai template jurnal JAMI.
2. **Penyusunan Abstrak** (Indonesia & Inggris, ±200 kata) — belum ada berkas terpisah, perlu diringkas dari Pendahuluan & Hasil.
3. **Formalisasi Daftar Pustaka** — 16 referensi (14 di antaranya adalah studi *dark patterns*/UX yang sudah dianotasi mendalam di matriks literatur) perlu disusun ke format sitasi baku (APA 7 untuk Sinta 4) dan idealnya diekspor ke berkas BibTeX agar mudah dikelola di Mendeley/Zotero.
4. **Keputusan bahasa final naskah** — draf saat ini seluruhnya Bahasa Indonesia (sesuai target Sinta 4); perlu dipastikan konsisten dari judul hingga daftar pustaka.
5. **Pemindahan ke template jurnal JAMI** — dilakukan oleh peneliti (di luar cakupan asisten AI), menggunakan konten `07-manuskrip/README.md` sebagai sumber utama.
6. **Penempatan figure & tabel final** sesuai gaya jurnal (caption, penomoran, resolusi) — sumber: [../06-output/figures/](../06-output/figures/) (4 PNG: boxplot SUS, boxplot Trust, bar chart task completion, effect size) dan [../06-output/tables/](../06-output/tables/) (4 CSV: statistik deskriptif, task completion, demografi, hasil uji hipotesis).
7. **Lengkapi metadata penulis & afiliasi** pada naskah final.

## Catatan

Konten Hasil & Pembahasan mengacu langsung pada output Tahap 4 ([../06-output/](../06-output/)) — statistik deskriptif SUS/Trust, hasil Mann-Whitney U Test, dan breakdown *task completion*. Ringkasan naratif tambahan (versi lebih panjang, gaya laporan institusional) tersedia di [../08-laporan/laporan-penelitian.md](../08-laporan/laporan-penelitian.md). Matriks tinjauan pustaka lengkap dengan anotasi (rumusan masalah, metode, kelebihan/kekurangan tiap studi) tersedia di [../02-literatur/](../02-literatur/) dan menjadi dasar penulisan §2 Tinjauan Pustaka.

---

*Acuan: [tahap-4-analisis-data.md](tahap-4-analisis-data.md), [../07-manuskrip/README.md](../07-manuskrip/README.md), [../02-literatur/](../02-literatur/), [../01-proposal/proposal%20rti.pdf](../01-proposal/proposal%20rti.pdf).*
