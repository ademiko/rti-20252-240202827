# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST
 
Title   : Pengaruh Urgency Dark Pattern pada Antarmuka Aplikasi E-Commerce terhadap
          Tingkat Usability dan Kepercayaan Pengguna Menggunakan Metode A/B Testing
Target  : [x] Jurnal  [ ] Konferensi  [x] Laporan (Tugas Akhir Riset Teknik Informatika)
 
Section Check:
  [x] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [x] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [x] Related Work — concept-centric, gap positioning
  [x] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [x] Results — tabel + grafik + observasi (tanpa interpretasi)
  [x] Discussion — interpretasi, perbandingan, implikasi, limitation
  [x] Conclusion — jawaban RQ, kontribusi, future work
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Dark pattern jenis urgency banyak dipakai di e-commerce, namun dampak kuantitatifnya terhadap usability dan trust belum banyak diukur secara empiris. Studi A/B testing (n=70, 35/35) membandingkan antarmuka standar dengan antarmuka bermuatan fake countdown timer. Hasil: skor SUS turun dari 77.0 menjadi 22.5, dan Trust dari 4.11 menjadi 2.03 (Mann-Whitney U, p<0.001, r=0.86). | 200-250 |
| Introduction | Konteks: dark pattern urgency (fake timer, scarcity) makin lazim di platform belanja online dan berpotensi memanipulasi keputusan pengguna. Gap: penelitian terdahulu banyak bersifat kualitatif/observasional, belum banyak yang mengisolasi elemen urgency secara terkontrol dan mengukur besaran dampaknya. RQ: apakah antarmuka Urgency Dark Pattern menghasilkan skor usability dan trust yang signifikan lebih rendah dibanding antarmuka standar? | 500-700 |
| Related Work | Tinjauan literatur dark pattern (taksonomi Mathur et al. dan sejenisnya), studi usability SUS sebagai instrumen baku, dan studi trust pengguna e-commerce — diorganisir per konsep (dark pattern taxonomy → usability measurement → trust measurement), lalu diakhiri dengan penempatan gap penelitian ini di antara ketiganya. | 700-1000 |
| Method | Desain A/B testing between-subjects, 70 partisipan (35 kontrol, 35 perlakuan), purwarupa Figma dengan skenario tugas "batalkan langganan premium", instrumen SUS (10 item) dan Trust Scale (5 item), prosedur informed consent hingga debriefing, serta rencana analisis Mann-Whitney U Test (α=0.05). | 800-1200 |
| Results | Tabel statistik deskriptif (mean±std SUS dan Trust per kelompok), hasil uji Mann-Whitney U (U=1225, Z=7.19, p<0.001, r=0.86 untuk kedua DV), grafik bar chart perbandingan dan box plot distribusi skor, tanpa interpretasi — murni pelaporan angka dan temuan objektif. | 500-800 |
| Discussion | Interpretasi bahwa penurunan skor sangat besar (effect size large) dan konsisten dengan literatur kualitatif sebelumnya, namun juga diskusi jujur bahwa effect size sebesar ini kemungkinan lebih besar dari kondisi dunia nyata karena elemen dark pattern di purwarupa dibuat cukup mencolok (limitasi external validity), serta implikasi praktis bagi desainer UX dan regulator. | 600-900 |
| Conclusion | Menjawab RQ: Urgency Dark Pattern terbukti signifikan menurunkan usability dan trust pengguna. Kontribusi: bukti kuantitatif dengan effect size besar yang melengkapi studi kualitatif sebelumnya. Future work: menguji jenis dark pattern lain dan tingkat "kehalusan" manipulasi yang berbeda (ablation study). | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| RQ (perbandingan SUS & Trust) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Hipotesis H1 (Dark Pattern < Kontrol) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Metrik SUS (0–100) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Metrik Trust Scale (1–5) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel IV (Jenis Antarmuka) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Task Completion Rate | ✗ ← | ✓ | ✓ | ~ | ✗ ← |
| Effect size (r) | ✗ ← | ✗ ← | ✓ | ✓ | ✗ ← |
| Klaim/kontribusi kuantitatif | ✓ | ✗ ← | ✗ ← | ✓ | ✓ |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> *Task Completion Rate* muncul sebagai metrik sekunder di Method dan Results, tapi tidak diperkenalkan sejak Introduction (pembaca baru tahu ada metrik tambahan ini di tengah paper) dan tidak ditutup lagi di Conclusion. (2) *Effect size (r)* — angka pentingnya baru muncul di Results, padahal keputusan menggunakan effect size non-parametrik (bukan Cohen's d) seharusnya sudah disinggung di Method sebagai bagian dari rencana statistik. (3) Klaim kontribusi kuantitatif digaungkan besar di Introduction dan Conclusion ("bukti kuantitatif dengan effect size besar"), tapi kalimat serupa yang menegaskan *seberapa besar* kontribusi itu tidak benar-benar muncul eksplisit di Method atau Results — baru terasa di Discussion.

**Tindakan perbaikan:**
> Menambahkan satu-dua kalimat di akhir Introduction yang menyebutkan bahwa selain SUS dan Trust, tingkat keberhasilan tugas (task completion) juga akan dilaporkan sebagai indikator tambahan gangguan navigasi. Di bagian Method (rencana statistik), menegaskan sejak awal bahwa effect size akan dilaporkan sebagai r (bukan Cohen's d) karena uji yang dipakai non-parametrik. Terakhir, menambahkan satu kalimat penutup di Conclusion yang secara eksplisit merujuk kembali angka task completion (71.4% vs 85.7%) sebagai bagian dari ringkasan dampak dark pattern, supaya benang merahnya utuh dari awal sampai akhir.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> Hasil penelitian menunjukkan bahwa performa antarmuka dark pattern jauh lebih buruk dibanding antarmuka normal. Skornya turun banyak dan itu signifikan. Kepercayaan pengguna juga ikut turun secara signifikan sehingga bisa dibilang dark pattern ini benar-benar merugikan pengguna.

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | "Performa" dan "skornya turun banyak" ambigu — tidak jelas skor apa dan turun berapa | Sebutkan metrik dan angka eksplisit: "Skor SUS turun dari 77,0 menjadi 22,5" |
| Precision | "signifikan" tidak disertai nilai statistik (p, effect size); "benar-benar merugikan" adalah klaim evaluatif, bukan laporan objektif untuk bagian Results | Tambahkan p-value, U, dan effect size r; pindahkan klaim evaluatif "merugikan pengguna" ke bagian Discussion, bukan Results |
| Conciseness | Kalimat terakhir mengulang informasi (turun, signifikan) yang sudah disebut di kalimat sebelumnya tanpa menambah data baru | Gabungkan menjadi satu kalimat ringkas yang membawa kedua metrik sekaligus |


**Paragraf setelah perbaikan:**
> Kelompok Dark Pattern menghasilkan skor SUS yang secara signifikan lebih rendah dibanding kelompok Kontrol (22,5 ± 6,50 vs 77,0 ± 7,01; Mann-Whitney U=1225, p<0,001, r=0,86). Pola serupa ditemukan pada skor Trust Scale (2,03 ± 0,39 vs 4,11 ± 0,33; p<0,001, r=0,86), menunjukkan effect size yang besar pada kedua metrik.

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis "tentang" riset berarti menceritakan apa saja yang saya lakukan secara kronologis — seperti diary: "saya membuat purwarupa, lalu menyebar kuesioner, lalu menghitung skor". Menulis sebagai "argumen" berarti setiap kalimat harus menjawab pertanyaan yang muncul dari kalimat sebelumnya dan membangun menuju satu kesimpulan yang koheren (red thread di WS-08 dan WS-15) — bukan sekadar laporan aktivitas.
> 
> Menulis Method dan Results lebih dulu (bukan Introduction) sangat membantu saya karena angka-angka aktual (SUS 77 vs 22.5, r=0.86) baru benar-benar saya ketahui setelah data selesai dianalisis. Kalau saya menulis Introduction di awal sebelum tahu hasilnya, saya berisiko membingkai "janji" penelitian yang ternyata tidak seluruhnya sesuai dengan temuan aktual (misalnya menjanjikan akan membahas beberapa jenis dark pattern padahal akhirnya cuma fokus urgency). Dengan menulis Introduction terakhir, saya bisa membingkai gap dan RQ persis sesuai dengan apa yang benar-benar saya temukan dan buktikan.
