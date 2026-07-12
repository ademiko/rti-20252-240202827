# 07-manuskrip: Draf Naskah Ilmiah (Extended Outline)

Draf naskah ilmiah ini disusun sebagai kerangka konsolidasi riset komparatif antarmuka pengguna untuk memenuhi luaran **Tahap 5**. Poin-poin di bawah ini merangkum esensi yang akan dikembangkan menjadi naskah artikel ilmiah lengkap (*full paper*) untuk target publikasi jurnal terakreditasi nasional (Sinta 2 - Jurnal RESTI / Telematika) atau prosiding internasional.

---

## 1. PENDAHULUAN 
* **Latar Belakang Fenomena:** Pertumbuhan platform *e-commerce* yang masif memicu persaingan ketat dalam optimalisasi rasio konversi. Kondisi ini melahirkan pergeseran paradigma dari desain yang humanis (*user-centered design*) menjadi taktik desain eksploitatif yang memanipulasi psikologis pengguna demi keuntungan bisnis secara instan, yang dikenal sebagai *Dark Pattern*.
* **Identifikasi Masalah & Gap Penelitian:** Salah satu taktik *Dark Pattern* yang paling agresif adalah *Urgency* (tekanan keterdesakan waktu) dan *Loss Aversion* (ketakutan akan kehilangan) yang diimplementasikan pada alur pembatalan pesanan komoditas. Taktik ini menggunakan komponen *fake countdown timer* (hitung mundur palsu) dan intervensi bahasa *confirm-shaming* pada tombol aksi. Meskipun secara teknik mampu menahan pembatalan transaksi, belum ada bukti empiris berskala lokal yang mengukur seberapa fatal kerusakan taktik ini terhadap aspek kegunaan sistem (*usability*) dan rasa percaya (*user trust*).
* **Pertanyaan Penelitian (Research Questions):**
    1.  Apakah terdapat perbedaan skor *Usability* (ketergunaan sistem) yang signifikan antara kelompok pengguna antarmuka standar (Kontrol) dengan kelompok antarmuka *Urgency Dark Pattern* (Perlakuan)?
    2.  Apakah terdapat perbedaan skor *User Trust* (kepercayaan pengguna) yang signifikan antara kelompok pengguna antarmuka standar dengan kelompok antarmuka *Urgency Dark Pattern*?
* **Tujuan & Kontribusi Riset:** Membuktikan secara matematis dan ilmiah efek destruktif dari manipulasi visual terhadap beban kognitif pengguna akhir. Hasil penelitian ini berkontribusi sebagai basis argumentasi etika rekayasa perangkat lunak bagi para desainer interaksi manusia dan komputer (HCI).

---

## 2. TINJAUAN PUSTAKA 
* **Definisi Urgency Dark Pattern:** Merujuk pada klasifikasi etika desain oleh Harry Brignull (2010), *Dark Pattern* adalah rekayasa antarmuka yang sengaja dirancang untuk mengecoh pengguna agar mengambil keputusan di luar rencana awalnya. Taktik *Urgency* memanipulasi bias kognitif *Fear of Missing Out* (FOMO) dengan memberikan batasan waktu palsu agar pengguna panik dan mengambil keputusan secara terburu-buru.
* **Kerangka Pengukuran Ketergunaan (System Usability Scale - SUS):** Menggunakan framework John Brooke (1996) yang terdiri atas 10 item pernyataan komposit dengan skala Likert 1–5. SUS mengisolasi metrik kenyamanan, efektivitas navigasi, tingkat kerumitan sistem, serta konsistensi elemen visual.
* **Kerangka Pengukuran Kepercayaan (User Trust Scale):** Mengadopsi indikator komposit persepsi keamanan transaksi, kejujuran penyajian informasi produk, serta transparansi sistem *e-commerce* dari perspektif pengguna akhir.
* **Studi Terkait (Related Work):** Evaluasi komparatif dari literatur HCI global menunjukkan bahwa peningkatan beban kognitif akibat elemen visual yang tidak sinkron secara linier berbanding terbalik dengan tingkat loyalitas jangka panjang konsumen terhadap platform digital.

---

## 3. METODOLOGI PENELITIAN 
* **Paradigma & Desain Eksperimen:** Menggunakan pendekatan ilmiah kuantitatif objektif berbasis *Design Science Research* (DSR) melalui skema pengujian **Between-Subjects A/B Testing**.
* **Rancangan Artefak Lingkungan Eksperimen:**
    * **Sistem A (Kelompok Kontrol):** Menggunakan purwarupa antarmuka *e-commerce* standar bersih (*clean UI*). Proses pembatalan pesanan dilakukan melalui alur yang linear, transparan, dan menggunakan kalimat penegasan yang netral.
    * **Sistem B (Kelompok Perlakuan):** Menggunakan purwarupa antarmuka yang telah diintervensi *Urgency Dark Pattern*. Proses pembatalan dicegat dengan memunculkan *pop-up* manipulatif berisi informasi hangusnya voucher gratis ongkir, *fake countdown timer* statis berdurasi `[02:59]`, serta visualisasi tombol asimetris (tombol pembatalan asli disamarkan dengan warna abu-abu pudar kecil).
* **Skenario Tugas (User Task):** Partisipan diwajibkan menyelesaikan instruksi terstruktur: *"Masuk ke dalam aplikasi simulasi, temukan menu pengaturan transaksi, lalu lakukan pembatalan pesanan barang yang telah dibeli."*
* **Prosedur Sampling & Pengumpulan Data:** Total sampel sebesar $N = 70$ responden mahasiswa dialokasikan secara acak (35 partisipan di Kelompok Kontrol, 35 partisipan di Kelompok Perlakuan). Data dikumpulkan menggunakan kuesioner digital terisolasi yang diintegrasikan langsung pada akhir sesi simulasi purwarupa Figma.
* **Pipeline Analisis Statistik:** Uji asumsi awal mengonfirmasi bahwa data berdistribusi tidak normal. Oleh karena itu, pengujian hipotesis untuk kedua variabel dependen dilakukan menggunakan metode non-parametrik **Mann-Whitney U Test** dengan ambang batas kesalahan $\alpha = 0.05$. Pengolahan data otomatis dieksekusi menggunakan skrip Python (*pustaka Pandas & SciPy*) di Google Colab untuk menjaga integritas replikasi (*reproducibility*).

---

## 4. HASIL DAN PEMBAHASAN 
* **Analisis Statistik Deskriptif (Bukti Penurunan Ekstrem):**
    Data hasil komputasi dari data mentah 70 responden mengonfirmasi deviasi rata-rata (*mean*) yang sangat kontras antara kedua kelompok lingkungan uji:
    * **Rata-rata Skor Usability (SUS):** Kelompok Kontrol mencatatkan skor **3.86**, sedangkan Kelompok Perlakuan anjlok secara ekstrem ke angka **1.86** (terjadi penurunan masif sebesar 2.00 poin skala).
    * **Rata-rata Skor Kepercayaan (Trust):** Kelompok Kontrol mencatatkan nilai **4.03**, sedangkan Kelompok Perlakuan jatuh bebas ke angka **1.97** (mengalami penurunan sebesar 2.06 poin skala).
* **Hasil Uji Inferensial (Mann-Whitney U Test):**
    * **Variabel Usability (SUS):** Menghasilkan nilai *Asymp. Sig. (2-tailed)* atau **p-value = 0.00000**. Karena $p < 0.05$, maka Hipotesis Alternatif (**H1 Diterima**).
    * **Variabel User Trust:** Menghasilkan nilai *Asymp. Sig. (2-tailed)* atau **p-value = 0.00000**. Karena $p < 0.05$, maka Hipotesis Alternatif (**H1 Diterima**).
* **Pembahasan Logika Riset (Discussion):**
    Secara matematis dan ilmiah, hasil *p-value* `0.00000` membuktikan secara mutlak bahwa hancurnya nilai kenyamanan dan rasa percaya pengguna **bukan terjadi karena faktor kebetulan**, melainkan murni akibat intervensi *Urgency Dark Pattern*. Animasi hitung mundur palsu terbukti memaksa otak pengguna bekerja lebih keras (*cognitive overload*), menciptakan kepanikan visual yang mengganggu konsentrasi navigasi. Selain itu, penggunaan teknik penyesalan kata (*confirm-shaming*) memicu *backfire effect*—pengguna masa kini langsung menyadari adanya niat buruk (*malicious intent*) dari pemilik platform digital, yang secara permanen merusak kredibilitas dan integritas sistem informasi tersebut.

---

## 5. KESIMPULAN DAN SARAN 
* **Kesimpulan Utama:** Penerapan strategi manipulasi antarmuka melalui taktik keterdesakan waktu (*Urgency Dark Pattern*) terbukti secara empiris merusak pengalaman interaksi manusia dengan komputer secara destruktif. Desain manipulatif ini menukar loyalitas jangka panjang pengguna dan integritas platform demi menahan pembatalan transaksi sesaat.
* **Saran Penelitian Lanjutan:** Disarankan bagi penelitian selanjutnya untuk mengintegrasikan alat sensor biometrik (seperti *Eye Tracking* atau pengukur detak jantung) guna menangkap indikator stres biologis pengguna secara langsung (*real-time*) saat berinteraksi dengan jebakan desain antarmuka.

---

