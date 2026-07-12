# Tahap 2 — Implementasi Purwarupa (Figma) & Kuesioner

**Status:** Selesai
**Acuan arsitektur:** [tahap-1-perancangan-eksperimen.md](tahap-1-perancangan-eksperimen.md)
**Lokasi kode:** [../05-kode/uipenelitian/](../05-kode/uipenelitian/)
**Tautan purwarupa (Figma):** https://www.figma.com/design/BERX4d1E8MyYA2Y6sLjpB6/helloPet?node-id=435-510 

---

## Tujuan

Mengimplementasikan dua purwarupa *High-Fidelity* aplikasi e-commerce (Figma) yang mendukung dua kondisi eksperimen melalui alur *routing* Maze:

- **Purwarupa A (Kontrol)** — antarmuka standar, bersih, tanpa elemen tekanan waktu.
- **Purwarupa B (Perlakuan)** — antarmuka identik dengan Purwarupa A, ditambah satu titik intervensi *Urgency Dark Pattern* pada alur pembatalan pesanan.

## Deliverable

- [x] Struktur file Figma per fungsi halaman (katalog produk, keranjang, checkout, pengaturan akun/pesanan) — komponen & *design system* (warna, tipografi, ikon *bottom bar*: beranda/pencarian/keranjang/profil) dikunci sama persis di kedua purwarupa
- [x] Purwarupa A — alur pembatalan pesanan: profil → pesanan → "Batalkan Pesanan" → pop-up konfirmasi netral ("Apakah Anda yakin ingin membatalkan?") → "Ya" → selesai
- [x] Purwarupa B — titik intervensi tunggal pada langkah konfirmasi: pop-up pencegatan berisi *fake countdown timer* statis (`02:59`), teks *loss aversion* (peringatan voucher gratis ongkir hangus), dan tombol asimetris (tombol "Kembali" besar/terang vs "Tetap Batalkan" kecil/abu-abu pudar)
- [x] Integrasi kedua purwarupa ke **Maze** sebagai platform *unmoderated usability testing* — satu skenario tugas identik ("temukan pengaturan pesanan, lalu batalkan pesanan") di-*assign* ke partisipan sesuai kelompok
- [x] Pengaturan *random assignment*: tautan uji terpisah per kondisi (Kontrol/Perlakuan) sehingga partisipan otomatis masuk ke satu purwarupa saja, tanpa tahu ada varian lain
- [x] Kuesioner **Google Forms** (SUS 10 item + Trust Scale) terpasang otomatis di akhir sesi Maze — wajib diisi sebelum sesi dianggap selesai
- [x] *Pre-filled field* "kelompok" pada Google Forms berbeda per tautan kondisi, agar label `KONTROL` / `DARK PATTERN` terisi otomatis (menghindari *human error* self-report partisipan)
- [x] Dokumentasi alur pengujian & tautan akses di [../05-kode/uipenelitian/README.md](../05-kode/uipenelitian/README.md)

## Hasil Verifikasi End-to-End

Diverifikasi manual melalui *dry-run* internal (beberapa sesi uji coba sebelum distribusi ke 70 responden):

- **Purwarupa A (Kontrol)**: partisipan uji coba dapat menyelesaikan skenario tanpa hambatan; Maze mencatat `task_success = 1` dan durasi navigasi wajar (tanpa jeda akibat elemen pengecoh).
- **Purwarupa B (Perlakuan)**: pop-up intervensi tampil konsisten di setiap sesi; *countdown* `02:59` bersifat statis (bukan berjalan mundur secara real-time) — cukup untuk memicu persepsi keterdesakan tanpa memerlukan logika timer dinamis di Figma. Beberapa sesi uji coba tercatat `misclick` pada tombol "Kembali" (sesuai desain visual asimetris yang disengaja).
- **Routing Maze → Google Forms**: partisipan yang menyelesaikan maupun yang meninggalkan tugas di tengah jalan tetap diarahkan ke kuesioner; kolom `kelompok` pada hasil ekspor sesuai dengan tautan yang diakses (tidak ada baris tercampur antar kelompok).
- **Struktur kolom hasil ekspor** dicek manual terhadap skema Tahap 1 (`participant_id`, `kelompok`, item `SUS_1..SUS_10`, `Trust_1..Trust_n`, dst.) — sudah sesuai dan siap ditarik ke Google Colab pada Tahap 3/4.

## Catatan Lingkungan

- Purwarupa Figma diakses via tautan publik mode *Present* (izin *view-only*); partisipan tidak memerlukan akun Figma untuk membuka atau berinteraksi dengan simulasi.
- Maze berjalan pada tingkat langganan (*tier*) dengan kuota sesi terbatas — distribusi ke 70 responden dijadwalkan bertahap agar tidak melebihi kuota bulanan.
- Google Forms tidak mendukung percabangan otomatis berbasis kelompok eksperimen dalam satu formulir tunggal; solusi yang dipakai adalah dua tautan formulir dengan *pre-filled field* `kelompok` berbeda, dipasangkan satu-satu dengan tautan Maze per kondisi — memastikan partisipan tidak perlu mengisi label kelompok secara manual.
- Elemen manipulatif pada Purwarupa B disengaja dibuat *statis* (bukan animasi dinamis) agar dapat direplikasi identik di setiap sesi pengujian, konsisten dengan prinsip *reproducibility* instrumen penelitian.

---

*Acuan: [../05-kode/README.md](../05-kode/README.md), [../03-teori/README.md](../03-teori/README.md), [tahap-1-perancangan-eksperimen.md](tahap-1-perancangan-eksperimen.md).*
