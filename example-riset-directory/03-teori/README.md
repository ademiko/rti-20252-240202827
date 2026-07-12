Arsitektur, Desain, dan Landasan Teori Sistem
1. Landasan Teori Sistem
Pengembangan sistem purwarupa dalam penelitian ini didasarkan pada tiga pilar teori utama yang saling berkaitan dalam interaksi manusia dan komputer (HCI):

Urgency Dark Pattern (Manipulasi Psikologis): Menurut literatur desain antarmuka, Dark Pattern adalah teknik desain manipulatif yang sengaja dibuat untuk mengecoh pengguna agar melakukan tindakan yang tidak mereka rencanakan. Secara spesifik, Urgency (tekanan waktu) dan Scarcity (kelangkaan) mengeksploitasi bias kognitif Fear of Missing Out (FOMO). Sistem dirancang untuk mensimulasikan ancaman waktu melalui fake countdown timer (waktu hitung mundur palsu) dan peringatan hangusnya diskon guna memicu beban kognitif pengguna.

Usability (Ketergunaan Sistem): Mengacu pada standar ISO 9241-11, usability adalah sejauh mana suatu sistem dapat digunakan oleh pengguna tertentu untuk mencapai tujuan dengan efektif, efisien, dan memuaskan. Dalam sistem ini, ketergunaan diukur secara kuantitatif menggunakan instrumen System Usability Scale (SUS) yang diciptakan oleh John Brooke.

User Trust (Kepercayaan Pengguna): Kepercayaan dalam ekosistem e-commerce adalah keyakinan konsumen terhadap integritas dan niat baik platform. Desain sistem dalam eksperimen ini mengisolasi variabel kepercayaan untuk melihat apakah manipulasi antarmuka secara langsung mengikis persepsi keamanan dan kejujuran platform di mata pengguna.

2. Arsitektur Sistem (Lingkungan Eksperimen)
Arsitektur dalam penelitian ini tidak berfokus pada backend server atau database, melainkan pada Arsitektur Instrumen Pengujian (Testing Infrastructure). Arsitektur ini dibagi menjadi tiga lapisan (layer) utama:

Presentation Layer (Lapisan Antarmuka):
Dibangun menggunakan platform Figma. Lapisan ini berfungsi untuk menampilkan High-Fidelity Mockup dari aplikasi e-commerce. Sistem ini dirender menggunakan teknologi WebGL agar dapat diakses secara dinamis melalui peramban web (web browser) standar tanpa perlu instalasi lokal.

Tracking & Execution Layer (Lapisan Pelacakan):
Diimplementasikan menggunakan Maze Platform. Purwarupa dari Figma diintegrasikan ke dalam cloud-based server Maze. Lapisan ini bertugas secara otomatis merekam telemetri pengguna, seperti durasi navigasi (time on task), persentase keberhasilan (success rate), dan jumlah klik yang salah (misclick rate).

Data Collection & Analytics Layer (Lapisan Analisis):
Menggunakan Google Forms untuk menangkap data perseptual (kuesioner SUS dan Trust Scale) segera setelah interaksi selesai. Data mentah berbentuk .csv kemudian ditarik ke dalam Google Colab (Python - Pandas & SciPy) sebagai mesin analitik untuk melakukan pembersihan data dan pengujian uji statistik Mann-Whitney U Test.

3. Desain Sistem (Skenario & Alur Purwarupa)
Desain sistem dibagi menjadi dua purwarupa terpisah untuk memfasilitasi pengujian Between-Subjects A/B Testing.

A. Skenario Pengguna (User Task)
Kedua kelompok (Kontrol dan Perlakuan) akan diberikan tugas (task) yang identik: "Menavigasi halaman aplikasi e-commerce, mencari pengaturan pesanan, dan melakukan pembatalan pesanan barang."

B. Desain Antarmuka Kelompok Kontrol (Standar)

Karakteristik: Bersih, netral, dan mengikuti Standard Operating Procedure (SOP) e-commerce umum.

Alur: Pengguna masuk ke profil -> Pilih pesanan -> Klik "Batalkan Pesanan" -> Muncul pop-up konfirmasi standar ("Apakah Anda yakin ingin membatalkan?") -> Pengguna klik "Ya" -> Selesai.

Tujuan Desain: Menjadi baseline pengukuran di mana pengguna dapat mengambil keputusan dengan tenang tanpa tekanan visual.

C. Desain Antarmuka Kelompok Perlakuan (Urgency Dark Pattern)

Karakteristik: Penuh tekanan visual, warna mencolok (merah/kuning), dan menggunakan teknik confirm-shaming.

Alur Modifikasi: Saat pengguna menekan tombol "Batalkan Pesanan", sistem akan memunculkan pop-up pencegatan yang dirancang secara manipulatif.

Elemen Desain Khusus:

Fake Timer: Munculnya teks hitung mundur animasi statis (misal: "Waktu Anda menit!").

Loss Aversion Text: Peringatan bahwa membatalkan pesanan akan menghanguskan seluruh voucher diskon.

Visual Asymmetry: Tombol untuk "Kembali" dibuat sangat besar dan terang, sedangkan tombol "Tetap Batalkan" dibuat sangat kecil, berwarna abu-abu pudar, dan seolah-olah tidak bisa diklik.
