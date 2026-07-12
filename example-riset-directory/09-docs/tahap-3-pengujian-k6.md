# Tahap 3 — Eksekusi Eksperimen (A/B Testing)

**Status:** Selesai — total 70 sesi terkumpul (35 Kontrol, 35 Perlakuan), data tersedia di `04-data/data_mentah.csv`
**Bergantung pada:** [tahap-2-implementasi-purwarupa.md](tahap-2-implementasi-purwarupa.md)
**Lokasi data:** [../04-data/](../04-data/)

---

## Tujuan

Mendistribusikan kedua purwarupa (Kontrol vs Perlakuan) kepada partisipan sungguhan secara *Between-Subjects*, merekam telemetri navigasi via Maze, dan mengumpulkan respons kuesioner (SUS + Trust Scale) hingga tercapai target sampel N=70 (35 per kelompok), sebagai pengganti eksekusi skrip beban (k6) pada sistem backend.

## Deliverable

- [x] Kriteria perekrutan ditetapkan: pengguna aktif e-commerce, usia 18-25 tahun
- [x] Dua tautan uji terpisah (Kontrol/Perlakuan) didistribusikan secara bergelombang kepada calon partisipan, dengan alokasi diusahakan berimbang menuju 35/35
- [x] Briefing & *informed consent* disampaikan identik ke semua partisipan (tanpa mengungkap elemen manipulatif pada kelompok Perlakuan)
- [x] Monitoring jumlah respons masuk per kelompok secara berkala (via *response count* Google Forms) untuk menjaga keseimbangan sampel
- [x] Verifikasi kelengkapan data harian: entri ganda, jawaban kuesioner tidak lengkap, kombinasi kelompok-perangkat yang tidak sesuai
- [x] Ekspor & penggabungan data Maze (telemetri) dengan data Google Forms (SUS & Trust) menjadi satu dataset final
- [x] Pencatatan log pelaksanaan (gelombang distribusi, jumlah responden, kendala) di [../00-admin/jadwal-dan-log-penelitian.md](../00-admin/jadwal-dan-log-penelitian.md)

## Desain yang Diimplementasikan

### Struktur data (`04-data/`)

```
04-data/
├── data_mentah.csv        # gabungan telemetri Maze + kuesioner Google Forms — n=70, skema sesuai Tahap 1
├── log-distribusi.md       # catatan gelombang distribusi tautan & jumlah responden masuk per gelombang
└── _archive-dryrun/        # sesi uji coba internal (Tahap 2) — dipisah agar tidak tercampur dataset final
```

### Prosedur pelaksanaan (pengganti *runner* k6)

Untuk setiap partisipan:

1. Partisipan menerima **satu** dari dua tautan (Kontrol atau Perlakuan) sesuai jadwal alokasi gelombang — tidak pernah menerima keduanya (menjaga desain *Between-Subjects*).
2. Partisipan membuka sesi Maze, membaca briefing singkat & mengisi persetujuan partisipasi.
3. Partisipan menyelesaikan (atau meninggalkan di tengah jalan) skenario tugas tunggal: mencari pengaturan pesanan lalu membatalkan pesanan.
4. Maze secara otomatis mengarahkan partisipan ke Google Forms setelah sesi tugas berakhir (baik berhasil maupun gagal).
5. Respons kuesioner tersimpan otomatis ke *backend* Google Sheets, dengan kolom `kelompok` sudah terisi otomatis lewat *pre-filled field* — partisipan tidak pernah mengisi label kelompok secara manual.
6. Peneliti memeriksa entri baru secara berkala: memastikan tidak ada baris duplikat (partisipan yang sama mengisi dua kali) dan seluruh item SUS/Trust terisi penuh.

### Alokasi & keseimbangan sampel

Distribusi tautan dilakukan bergelombang, bukan sekaligus, agar jumlah responden di kedua kelompok dapat dipantau dan disesuaikan (mis. menambah gelombang khusus untuk kelompok yang tertinggal) sebelum kuota N=70 (35/35) ditutup. Pendekatan ini setara dengan *interleaved run* pada pengujian beban otomatis — memastikan setiap kombinasi (di sini: kelompok) mendapat jumlah sampel yang sama meski proses distribusi berhenti/lanjut di tengah jalan.

## Catatan Kendala & Penyesuaian

Selama pelaksanaan, ditemukan beberapa hal yang memerlukan penyesuaian prosedur (setara catatan *smoke test* pada pengujian otomatis):

- **Kompatibilitas perangkat**: sebagian partisipan mengakses tautan Maze/Figma dari perangkat mobile dengan lebar layar yang membuat elemen *countdown timer* pada Purwarupa B terpotong pada beberapa ukuran layar kecil. Partisipan yang mengalami tampilan tidak sesuai diarahkan ulang untuk mengakses dari perangkat lain, sesi lama ditandai tidak valid dan dikeluarkan dari dataset final.
- **Entri tidak lengkap**: beberapa respons Google Forms terhenti sebelum item Trust Scale terisi penuh (partisipan menutup tab sebelum submit). Entri semacam ini dicatat sebagai *drop-out*, tidak dihitung ke kuota 35/35, dan gelombang tambahan dijalankan untuk menutup kekurangan sampel.
- **Keseimbangan kelompok**: pada satu titik distribusi, kelompok Perlakuan sempat tertinggal responnya dibanding Kontrol (kemungkinan tautan tersebar tidak merata). Gelombang distribusi tambahan diarahkan khusus ke tautan Perlakuan hingga kedua kelompok kembali seimbang di angka 35.
- **Deteksi keberhasilan tugas**: Maze mencatat `task_success` berdasarkan pencapaian titik akhir alur (halaman "pesanan berhasil dibatalkan"); sesi yang berhenti di pop-up intervensi Purwarupa B (tanpa melanjutkan ke pembatalan) turut tercatat sebagai data valid berkategori `Gagal`, bukan dibuang — data ini penting karena merepresentasikan efek nyata dari tekanan visual terhadap penyelesaian tugas.

## Hasil Ringkas Pelaksanaan

- Total sampel akhir: **N = 70** partisipan (35 Kontrol, 35 Perlakuan), seluruhnya memenuhi kriteria usia 18-25 tahun dan berstatus pengguna aktif e-commerce.
- Seluruh 70 baris pada `data_mentah.csv` telah melalui pemeriksaan kelengkapan (tidak ada nilai kosong pada kolom item SUS/Trust) sebelum ditutup sebagai dataset final.
- Rincian *task success rate*, distribusi skor SUS, dan skor Trust Scale antar kelompok **belum diinterpretasikan** pada tahap ini — angka deskriptif dan uji signifikansi (Mann-Whitney U Test) disajikan pada [tahap-4-analisis-data.md](tahap-4-analisis-data.md), mengacu ke [../06-output/](../06-output/).
- Dataset final (`04-data/data_mentah.csv`) menjadi input tunggal dan tidak diubah lagi untuk seluruh perhitungan statistik pada Tahap 4.

## Catatan Lingkungan

- Distribusi tautan dan pemantauan respons dilakukan manual oleh peneliti (bukan skrip otomatis) — konsekuensi dari sifat eksperimen berbasis interaksi manusia, bukan beban trafik sistem.
- Sesi uji coba internal (*dry-run*, lihat Tahap 2) disimpan terpisah di `04-data/_archive-dryrun/` agar tidak pernah tercampur dengan data 70 partisipan sungguhan yang menjadi dasar analisis.

---

*Acuan: [tahap-2-implementasi-purwarupa.md](tahap-2-implementasi-purwarupa.md), [../00-admin/jadwal-dan-log-penelitian.md](../00-admin/jadwal-dan-log-penelitian.md), [../06-output/README.md](../06-output/README.md).*
