# PAKET LANGKAH 6: VERIFIKASI & BKU

**Sumber kebenaran mutlak:** Dokumen 01 v1.53, Dokumen 02 v1.33, Dokumen 03 v1.58, Dokumen 04 v1.38, Dokumen 05 v1.64.  
**Cakupan paket ini:** Tahap A, yaitu frontend dengan data contoh. Pekerjaan backend Langkah 6 baru dimulai di Tahap B (lihat `SUSUNAN_PENGEMBANGAN_AMANDA_BERTAHAP.md`).

## Perintah kerja
Kerjakan hanya fitur yang tercantum di bagian 1, berurutan dari atas ke bawah, memakai aturan yang tertulis di bagian 2 dan 3. Jangan menambah, mengurangi, atau mengubah aturan bisnis. Bila ada hal yang tidak diatur dokumen, hentikan dan tanyakan, jangan merancang sendiri. Langkah selesai bila seluruh skenario di bagian 4 dapat didemonstrasikan pada antarmuka dengan data contoh.

## 1. Fitur Langkah 6 (urutan kerja)
| Urut | ID | Fitur | Peran | Prioritas | Pekerjaan | Dependensi |
|---|---|---|---|---|---|---|
| 96 | VER-01 | Pemeriksaan SPJ: setujui / kembalikan | Verifikator | P0 | Frontend | SPJ-05 |
| 97 | BKU-01 | Pencatatan BKU | Bendahara | P0 | Frontend | VER-01 |
| 98 | VER-02 | Larangan verifikasi mandiri | Verifikator, PPTK (Plh.) | P0 | Frontend | VER-01, PEN-05 |
| 99 | VER-03 | Token & nomor verifikasi | Sistem | P0 | Frontend | VER-01, TPL-04 |
| 100 | TPL-04 | Template Hasil Verifikasi SPJ & format nomor verifikasi per TA | Admin | P1 | Frontend | TPL-01, VER-03 |
| 101 | DSB-04 | Dasbor Verifikator (Pro Mode) | Verifikator | P1 | Frontend | VER-01 |
| 102 | BKU-02 | Cakupan BKU murni pengeluaran | Bendahara | P0 | Frontend | BKU-01 |
| 103 | BKU-04 | Pencabutan BKU berjenjang | Bendahara, Verifikator, PPTK | P0 | Frontend | BKU-01, VER-03, SPJ-03 |
| 104 | BKU-03 | Koreksi No./tanggal BKU tanpa pencabutan | Bendahara | P1 | Frontend | BKU-01, AUD-01 |
| 105 | BKU-05 | Daftar BKU dengan pencarian & filter | Bendahara, Verifikator | P1 | Frontend | BKU-01, UIX-07 |
| 106 | VER-04 | Cetak Hasil Verifikasi SPJ (PDF + QR) | PPTK, Verifikator | P1 | Frontend | VER-03, PEN-08 |
| 107 | VER-05 | Halaman keaslian SPJ via token | Publik | P1 | Frontend | VER-03 |

## 2. Aturan kunci per fitur (ringkasan)
### VER-01 — Pemeriksaan SPJ: setujui / kembalikan
- **Peran:** Verifikator
- **Aturan:** Setujui → Menunggu BKU; kembalikan → Draft dengan catatan revisi wajib; komitmen SPD tetap terkunci.
- **Rujukan:** D03 §5; D02 §5

### BKU-01 — Pencatatan BKU
- **Peran:** Bendahara
- **Aturan:** No. BKU manual (teks/angka) unik per TA; tanggal BKU bebas tanpa urutan kronologis; satu BKU per kuitansi; SPJ → Dibukukan; komitmen → realisasi.
- **Rujukan:** D02 §4 poin 6–7; D03 §3 poin 7; D04 §2.2

### VER-02 — Larangan verifikasi mandiri
- **Peran:** Verifikator, PPTK (Plh.)
- **Aturan:** Tidak ada personel yang boleh memverifikasi SPJ yang ia ajukan/kelola, definitif maupun Plh./Plt. PPTK; ditolak server.
- **Rujukan:** D01 §6 poin 9; D03 §5 poin 10

### VER-03 — Token & nomor verifikasi
- **Peran:** Sistem
- **Aturan:** Dibuat saat disetujui; token acak (tidak dicetak teks), nomor urut per TA tidak dipakai ulang; Tidak berlaku saat dikembalikan/BKU dicabut; verifikasi ulang → token & nomor baru.
- **Rujukan:** D02 §8 poin 3, 5; D04 §2.2

### TPL-04 — Template Hasil Verifikasi SPJ & format nomor verifikasi per TA
- **Peran:** Admin
- **Aturan:** Admin ubah tata letak, label, teks statis, logo, stempel (bukan data sistem); format nomor: awalan, pemisah, pola tahun, jumlah digit; nomor tercetak tidak berubah.
- **Rujukan:** D02 §2.3, §8 poin 2–3; D04 §2.2

### DSB-04 — Dasbor Verifikator (Pro Mode)
- **Peran:** Verifikator
- **Aturan:** Pagu Induk pada kartu TA (baca saja); antrean SPJ Terkunci; jumlah dikembalikan/disetujui.
- **Rujukan:** D03 §1, §5, §14; D01 §3.3
- **Keputusan pemilik yang sudah masuk dokumen:** N-10: Verifikator: antrean SPJ Terkunci, jumlah dikembalikan/disetujui, kartu Pagu Induk (baca saja).

### BKU-02 — Cakupan BKU murni pengeluaran
- **Peran:** Bendahara
- **Aturan:** Tanpa formulir/alur penerimaan kas, SP2D, saldo awal, atau saldo kas riil.
- **Rujukan:** D02 §4 poin 6; D01 §9 poin 2b

### BKU-04 — Pencabutan BKU berjenjang
- **Peran:** Bendahara, Verifikator, PPTK
- **Aturan:** Urutan: Bendahara cabut (audit, pop-up konfirmasi, tanpa alasan tertulis) → Verifikator kembalikan → Seksi lepas SPJ → Seksi batalkan kuitansi → SPD pulih; nomor BKU dicabut bebas dipakai ulang; token keaslian Tidak berlaku.
- **Rujukan:** D02 §6 poin 2; D03 §5 poin 4; D01 §15 poin 6

### BKU-03 — Koreksi No./tanggal BKU tanpa pencabutan
- **Peran:** Bendahara
- **Aturan:** Hanya bila nominal tidak berubah; cek keunikan; audit nilai lama & baru.
- **Rujukan:** D02 §6 poin 1; D03 §3 poin 7

### BKU-05 — Daftar BKU dengan pencarian & filter
- **Peran:** Bendahara, Verifikator
- **Aturan:** Filter seksi, periode, status; pencarian No. BKU/uraian dalam cakupan peran.
- **Rujukan:** D01 §15 poin 1, 3–5

### VER-04 — Cetak Hasil Verifikasi SPJ (PDF + QR)
- **Peran:** PPTK, Verifikator
- **Aturan:** PPTK seksinya, Verifikator semua seksi; hanya Menunggu BKU/Dibukukan; data sistem (termasuk pajak, Total Pajak, Jumlah dibayarkan); cetak ulang = nomor/QR sama selama token belum berganti; peran lain ditolak.
- **Rujukan:** D02 §8; D03 §4 poin 13, §5 poin 9

### VER-05 — Halaman keaslian SPJ via token
- **Peran:** Publik
- **Aturan:** Tanpa login; hanya status Berlaku/Tidak berlaku, nama TA, nama seksi, tanggal verifikasi; respons seragam untuk token tak dikenal/tak berlaku; tanpa daftar/pencarian token; tanpa nominal/identitas.
- **Rujukan:** D02 §8 poin 4; D03 §9 poin 10; D04 §2.3; D01 §10 poin 10

## 3. Kutipan bagian dokumen yang dirujuk (apa adanya)
Bagian berikut disalin tanpa perubahan dari dokumen sumber. Bila ringkasan di bagian 2 berbeda dengan kutipan ini, kutipan yang berlaku.

#### Dokumen 03 §5

## 5. Verifikator
1. Memeriksa SPJ yang diajukan Seksi.
2. Menyetujui untuk diteruskan ke proses pembukuan atau mengembalikan ke Seksi sebagai Draft dengan catatan revisi wajib.
3. Pengembalian membuka kunci SPJ menjadi Draft, tetapi tidak melepaskan kuitansi atau komitmen SPD.
4. Mengikuti urutan pencabutan berjenjang ketika BKU dicabut dan transaksi harus dikembalikan.
5. Melihat Pagu Induk pada kartu TA dan seluruh Jejak Audit TA, dalam mode baca saja.
6. Melihat drill-down anggaran seluruh seksi sampai rekening belanja, dalam mode baca saja.
7. Mengunduh laporan seluruh seksi dalam mode baca saja (Dokumen 01 §9).
8. Mengunduh lampiran PDF SPJ seluruh seksi (Dokumen 02 §9).
9. Mencetak Hasil Verifikasi SPJ dengan barcode dan nomor verifikasi untuk SPJ seluruh seksi setelah SPJ disetujui (Dokumen 02 §8).
10. Tidak memverifikasi SPJ yang ia ajukan atau kelola sendiri, baik sebagai pejabat definitif maupun Plh./Plt. PPTK (Dokumen 01 §6 poin 9).

- Menyusun dan mengunduh laporan kustom untuk seluruh seksi, dengan pilihan kolom sesuai Matriks Kolom yang Diizinkan per Peran (Dokumen 01 §9 poin 12). Kolom kuitansi, NIP/NIK, Nomor Rekening, dan kolom rekening belanja tersedia, dan NIP/NIK serta Nomor Rekening ditampilkan penuh tanpa penyamaran (Dokumen 01 §9 poin 12d dan Dokumen 05 skenario 158).

#### Dokumen 02 §5

## 5. Relasi SPJ dan verifikasi
- Satu kuitansi berpasangan dengan satu SPJ (1:1); kuitansi dapat dibuat terlebih dahulu.
- Seksi memilih jenis belanja di awal pembuatan SPJ, dan pilihan itu menentukan Form Dinamis yang tampil. Form disusun Admin per jenis belanja. Isian form manual; jangan mengasumsikan auto-kalkulasi yang belum disepakati.
- SPJ memuat rincian teknis belanja (Form Dinamis), pajak, serta unggahan bukti SPJ.
- Pajak diisi manual oleh Seksi sebagai bagian SPJ. Setelah isian SPJ disimpan, sistem menampilkan pop-up pajak. Seksi dapat menambah beberapa entri pajak; setiap entri memilih jenis pajak dari Master Jenis Pajak dan mengisi nominalnya secara manual. Sistem tidak menghitung pajak secara otomatis dari tarif atau master. Satu-satunya perhitungan otomatis terkait pajak adalah Total Pajak, yaitu jumlah seluruh entri pajak, dan Jumlah yang dibayarkan, yaitu nilai bruto dikurangi Total Pajak. Admin mengelola Master Jenis Pajak. Entri pajak tidak mengubah nominal bruto kuitansi. Sistem menolak penyimpanan entri pajak jika Total Pajak melebihi nilai bruto kuitansi terkait; Total Pajak yang sama dengan bruto tetap diterima, sehingga Jumlah yang dibayarkan bernilai nol. Pesan validasi menampilkan nilai bruto, Total Pajak, dan batas bahwa Total Pajak tidak boleh lebih dari nilai bruto kuitansi; entri yang ditolak tidak tersimpan. Penolakan ini hanya berlaku untuk pajak dan tidak berlaku untuk Form Dinamis. SPJ tanpa pajak diperbolehkan. Pajak tidak masuk Excel rekap isian SPJ; pajak dilaporkan pada rekap pajak per jenis pajak, hanya untuk SPJ yang sudah memiliki BKU (Dokumen 01 §9 poin 10).
- Isian Form Dinamis merupakan rincian administratif yang diisi oleh Seksi/PPTK untuk keperluan pertanggungjawaban. Pengisian ini bersifat pencatatan informasional murni dan tidak menambah maupun mengurangi anggaran. Sistem tidak melakukan validasi perhitungan matematis atau kecocokan antara total rincian pada Form Dinamis dengan nominal bruto kuitansi.
- Isian Form Dinamis disimpan sebagai jawaban SPJ sesuai versi form saat SPJ dibuat, dan dapat direkap per jenis belanja (Dokumen 01 §9). Unduhan Excel rekap tersebut berisi satu sheet per jenis belanja, dengan kolom berupa gabungan field dari versi form yang dipakai SPJ di sheet tersebut (Dokumen 01 §9 poin 6). Form dapat memiliki paling banyak satu blok berulang (Dokumen 01 §9 poin 9). Entri blok disimpan sebagai daftar pada SPJ, dan setiap entri menjadi satu baris di Excel.
- **Standar Format & Batas Berkas Unggahan (Terkunci):**
  - **Format Wajib:** Hanya menerima format `.pdf` (`application/pdf`). Berkas gambar mentah dan format dokumen lain ditolak.
  - **Hard Ceiling Berkas Asal:** Maksimum **30 MB** per berkas PDF sebelum optimasi. Berkas di atas batas ini ditolak sebelum kompresi.
  - **Client-First Threshold:** Berkas berukuran `<= 5 MB` diunggah tanpa kompresi. Berkas `> 5 MB` hingga 30 MB otomatis dikompresi lokal di peramban terlebih dahulu.
  - **Target Hasil:** Ukuran berkas final ditargetkan `<= 10 MB` (ideal `<= 5 MB`) dengan keterbacaan dokumen keuangan tetap terjaga.
  - **Server Fallback:** Jika kompresi peramban gagal, kehabisan memori, atau melewati toleransi proses 15 detik, sistem otomatis mengalihkan optimasi ke worker kompresi server. Kegagalan lokal tidak langsung menggagalkan unggahan.
  - **Integritas & Metadata:** Kompresi hanya mengubah representasi fisik berkas PDF, tidak mengubah Form Dinamis, data Excel, atau data transaksi terstruktur. Sistem mencatat nama dan ukuran berkas asli sebagai metadata, beserta ukuran akhir. Yang disimpan hanya berkas final hasil kompresi; berkas asli tidak disimpan. Berkas final dihapus bersama TA saat retensi 12 tahun.
  - **Keterbacaan:** Target kompresi sekitar 150 DPI dan kualitas JPEG gambar minimal 70% sebagai pedoman teknis; teks nominal, tanda tangan, dan stempel harus tetap terbaca jelas.
  - **Uji Pra-Rilis:** Pengujian menggunakan PDF berukuran kecil, menengah, dan mendekati batas 30 MB pada perangkat kelas rendah; berkas hasil harus lolos pemeriksaan visual dan dapat diunduh kembali.
- **Status SPJ:** SPJ berstatus **Terkunci** sejak dikirim ke Verifikator dan tidak dapat diedit selama Terkunci. Setelah disetujui Verifikator, SPJ berstatus Menunggu BKU hingga Bendahara mencatat BKU; sesudah itu SPJ berstatus Dibukukan. SPJ Menunggu BKU dan Dibukukan tetap Terkunci, dan kuitansi terkait tetap Terkunci.
- **Penandatangan SPJ saat Plh./Plt.:** Tanggal pengajuan SPJ ke Verifikator menentukan pejabat penanggung jawab pada dokumen SPJ dan Hasil Verifikasi SPJ. SPJ yang diajukan sebelum delegasi dimulai tetap atas nama pejabat definitif, meskipun diverifikasi saat delegasi Plh./Plt. berjalan, karena penguncian terjadi sejak pengiriman.
- Verifikator dapat mengembalikan SPJ kepada Seksi sebagai Draft dengan catatan revisi wajib. Pengembalian membuka kunci SPJ, tetapi tidak melepas komitmen kuitansi dari SPD. Kuitansi tetap Terkunci selama SPJ masih terkait.
- SPJ berstatus Draft, yaitu yang belum dikirim atau dikembalikan Verifikator, boleh dilepas atau dibatalkan oleh Seksi. Kuitansi terkait kembali Aktif tanpa jejak. SPJ yang sudah dikirim berstatus Terkunci dan hanya dapat dilepas setelah dikembalikan Verifikator menjadi Draft. Jika BKU sudah dicatat, tindakan mengikuti pencabutan berjenjang §6.2.


- **Pengisian Rincian Rekening Bank Penerima (Split View Workspace):**
  - Pada formulir rincian penerima SPJ, antarmuka ditampilkan dalam mode layar terbagi (*Split View*):
    - **Panel Sisi Kiri (Direktori Rekening Bank):** Menyediakan daftar rekening yang telah terdaftar dengan kotak pencarian terpadu (*omni-search*). Pencarian dapat dilakukan secara fleksibel melalui Nama Penerima, Alias/Instansi, atau Nomor Rekening. Menekan tombol *"Pilih / Gunakan"* langsung mengisi rincian ke form sisi kanan secara otomatis.
    - **Panel Sisi Kanan (Form Rincian SPJ):** Tempat PPTK melengkapi data penerima pembayaran. Jika data belum tersedia di direktori kiri, PPTK mengetik manual data baru tanpa validasi angka/format unik yang membatasi.
  - **Auto-Capture Rekening Baru:** Saat rincian atau draf SPJ disimpan, data rekening baru otomatis tersimpan ke Direktori Rekening Bank sistem untuk pemakaian berulang di masa mendatang.
  - **Snapshot Permanen pada SPJ:** Data rekening yang dipilih/diinput pada SPJ disalin sebagai snapshot permanen dokumen transaksi. Pembersihan data atau penggabungan duplikat oleh Admin di direktori tidak mengubah data SPJ yang sudah berstatus Terkunci, Menunggu BKU, atau Dibukukan.
  - **Dampak Pembatalan SPJ Draft:** Pembatalan SPJ Draft menghapus dokumen SPJ secara bersih, namun data rekening baru yang sempat ter-capture ke Direktori Rekening Bank tetap tersimpan di direktori.

#### Dokumen 02 §4

## 4. Alur kuitansi dan dampak saldo
1. Gatekeeper anggaran mengizinkan atau menahan pembuatan kuitansi dan SPJ baru sesuai status kesiapan alokasi seluruh seksi dan pengesahan ("Sahkan") Bendahara (Dokumen 01 §3.2). Gatekeeper tidak menahan pemrosesan SPJ yang sudah ada, verifikasi, maupun pencatatan BKU.
2. Seksi/PPTK membuat dan menyimpan kuitansi dengan nilai bruto. Kuitansi berstatus **Aktif**.
3. Kuitansi Aktif mengunci/mengurangi saldo SPD yang tersedia sebagai komitmen. Saldo yang sudah terikat tidak dapat dipakai membuat kuitansi lain.
4. Status kuitansi:
   - **Aktif:** belum dikaitkan SPJ, yaitu belum ada SPJ Draft. Boleh diedit dan dibatalkan pada status TA Aktif Penuh; pada Masa Transisi hanya boleh dibatalkan (§7). Pembatalan kuitansi melepas komitmen SPD.
   - **Terkunci:** sudah dikaitkan SPJ, yaitu sejak SPJ Draft dibuat dan selama SPJ masih terkait. Tidak dapat diedit atau dibatalkan. Untuk mengubahnya, SPJ harus dilepas atau dibatalkan dari kuitansi terlebih dahulu. Pelepasan SPJ Draft mengembalikan kuitansi menjadi Aktif.
   - Tidak ada status Dibatalkan. Kuitansi yang dibatalkan langsung dihapus dan tidak meninggalkan jejak (§6.3).
5. Kuitansi dapat dicetak.
6. **Sifat dan Input BKU:**
   - **Input Manual & Keunikan:** No. BKU diinput secara manual oleh Bendahara (bukan auto-number sistem) untuk menyesuaikan penomoran buku kas fisik/manual instansi. No. BKU wajib unik per TA; sistem menolak No. BKU yang sedang aktif dipakai di TA yang sama.
   - **Cakupan Murni Pengeluaran Belanja:** BKU AMANDA murni merupakan buku pembukuan realisasi pengeluaran belanja per kuitansi/SPJ. Sistem tidak mencatat transaksi penerimaan kas, SP2D (UP/GU/TU/LS), maupun saldo kas tunai/bank.
   - **Fleksibilitas Penanggalan (Bebas Batasan Kronologis):** Sistem membebaskan penanggalan transaksi tanpa validasi urutan kronologis antara Tanggal Kuitansi, tanggal pengajuan SPJ, dan Tanggal BKU, guna mengakomodasi pencatatan faktual lapangan maupun input susulan (backdate).
   - **Ketentuan Nomor Dicabut & Satu BKU per Kuitansi:** Jika suatu BKU dicabut melalui alur pencabutan berjenjang (§6.2), nomor BKU tersebut berstatus bebas kembali dan sah digunakan untuk transaksi kuitansi/SPJ lain di TA yang sama. Satu kuitansi hanya boleh memiliki satu BKU; sistem menolak input BKU kedua.
7. Saat BKU dicatat, komitmen kuitansi berubah menjadi realisasi. Sisa SPD Bebas tidak berubah karena nilainya hanya berpindah dari komitmen ke realisasi.

#### Dokumen 03 §3

## 3. Bendahara Pengeluaran
1. Membagi Pagu Induk ke subkegiatan sesuai DPA hingga total sama dengan Pagu Induk. Pagu seksi dihitung otomatis.
2. Mengatur jendela waktu input alokasi (WITA) dan memantau countdown serta status penyelesaian seluruh seksi.
3. Menangani pembukaan kembali jendela input bila diperlukan. Selama ada seksi belum seimbang, gatekeeper menahan pembuatan kuitansi dan SPJ baru untuk semua seksi. Pemrosesan SPJ yang sudah ada dan pencatatan BKU tetap berjalan.
4. Mengelola efisiensi dengan menurunkan SPD, maksimal sebesar sisa SPD bebas.
5. Melakukan pergeseran anggaran; Seksi tidak memiliki kewenangan pergeseran. Sumber dibatasi sisa SPD bebas dan setiap perubahan berjejak. Tujuan pergeseran harus pasangan subkegiatan dan rekening yang sudah dialokasikan.
6. Pada APBD-P, mengalokasikan pagu perubahan ke subkegiatan dan mengkoordinasikan penyelesaian alokasi rekening oleh PPTK.
7. Mencatat No. BKU dan tanggal BKU saat pembukuan, satu BKU per kuitansi. No. BKU diinput secara manual oleh Bendahara (bukan auto-number) dan wajib unik per TA. BKU AMANDA murni mencatat realisasi pengeluaran kas belanja per kuitansi/SPJ tanpa mencatat transaksi penerimaan kas (SP2D, UP, GU, TU) maupun saldo kas riil. Sistem membebaskan tanggal BKU tanpa batasan urutan kronologis terhadap tanggal kuitansi atau tanggal SPJ. Mengoreksi No. BKU atau tanggal BKU tanpa pencabutan jika nominal tidak berubah, dengan jejak di Jejak Audit. Mencabut BKU dan mengikuti urutan pencabutan berjenjang (Dokumen 02 §6).
8. Menekan tombol "Sahkan" setelah seluruh seksi berstatus Seimbang. SPD terbit sebesar pagu yang disahkan.
9. Tidak boleh merangkap PPTK/Seksi pada TA yang sama.
10. Melihat tampilan anggaran berjenjang seksi → subkegiatan → rekening belanja, dengan nilai pagu, realisasi, komitmen, sisa SPD bebas, serapan, dan status pada setiap tingkat.
11. Jejak Audit: hanya melihat entri aksinya sendiri.

- Menyusun dan mengunduh laporan kustom untuk seluruh seksi, dengan pilihan kolom sesuai Matriks Kolom yang Diizinkan per Peran (Dokumen 01 §9 poin 12).

#### Dokumen 04 §2.2

### 2.2 Snapshot/operasional TA
| Entitas | Data utama | Prinsip |
|---|---|---|
| Tahun Anggaran | Tahun, pagu induk, status siklus, mode APBD-P, tanggal arsip terakhir | Workspace terisolasi; penghapusan setelah memiliki transaksi hanya melalui retensi 12 tahun sejak tanggal arsip terakhir; paling banyak satu berstatus Aktif Penuh pada satu waktu |
| Seksi TA | Referensi versi SOTK, nama snapshot, periode/status | Perubahan master global tidak mengubah snapshot TA |
| Pemetaan Subkegiatan TA | TA, seksi TA, subkegiatan | Satu subkegiatan hanya untuk satu seksi per TA; satu seksi dapat banyak subkegiatan |
| Penugasan TA | Peran, personel, seksi opsional, TMT, akhir, provisional | Menyimpan riwayat; PA/KPA, Bendahara, Verifikator instansi, PPTK per seksi; satu personel sah memegang peran PPTK di lebih dari satu seksi pada TA yang sama |
| Penugasan Delegasi (Plh./Plt.) | TA, personel pengganti, peran yang digantikan (Bendahara, PPTK, atau PA/KPA), seksi jika PPTK, tanggal mulai, tanggal berakhir, status (Delegasi Aktif, Berakhir, atau Dicabut), alasan pencabutan dini, ID pejabat definitif | Entitas terpisah dari Penugasan TA definitif dan tidak mengakhiri atau memindahkannya; rentang tanggal inklusif; berakhir otomatis 23:59 WITA pada tanggal berakhir; pencabutan dini wajib beralasan; selama Delegasi Aktif hak transaksi definitif nonaktif; penunjukan ditolak bila personel memegang peran yang bertentangan (Dokumen 01 §6 poin 8) |
| Penugasan Pengawas TA | TA, akun Pengawas, tanggal mulai, tanggal akhir | Tanpa seksi; cakupan seluruh seksi pada TA yang ditugaskan; berakhir pada tanggal akhir akses |
| Register SK | Penugasan, nomor/tanggal SK, berkas, status provisional | SK lama tetap dapat dibuka setelah penugasan berakhir |
| Versi Alokasi Anggaran | TA, fase (murni/perubahan/pergeseran), tanggal efektif, aktor | Append-only/berhistori secara konseptual; perubahan tidak menimpa jejak lama |
| Alokasi Subkegiatan | TA, subkegiatan, pagu | Dikelola Bendahara sesuai DPA |
| Alokasi Rekening | TA, subkegiatan, rekening, pagu | Dikelola PPTK/Seksi; total sama dengan pagu subkegiatan; perubahan pagu per fase dicatat di Versi Alokasi Anggaran; pasangan subkegiatan + rekening membedakan baris alokasi, unik per TA, subkegiatan, dan rekening; kunci internal berupa ID, kode gabungan (misal 5.1.02.02.6.2.01.01) hanya untuk tampilan dan pencarian |
| Ledger SPD | TA, rekening/alokasi, nilai SPD, perubahan, referensi (pergeseran memakai nomor otomatis `Pergeseran/{nomor urut 3 digit}/{tahun TA}`, Dokumen 01 §5.1 poin 5) | SPD otomatis 100% pagu yang disahkan; efisiensi/pergeseran berjejak |
| Kuitansi | TA, seksi, subkegiatan, rekening, penerima, bruto, uraian, tanggal kuitansi, status (Aktif atau Terkunci) | Satu kuitansi Aktif atau Terkunci mengikat komitmen SPD; kuitansi Terkunci sejak SPJ Draft dibuat dan tidak dapat diubah selama SPJ masih terkait; pada Masa Transisi seluruh data kuitansi Aktif tidak dapat diedit dan hanya pembatalan yang diizinkan; tidak ada status Dibatalkan, kuitansi yang dibatalkan langsung dihapus |
| Form Dinamis | Jenis belanja, versi, field (tipe, urutan, wajib/opsional, system tag), blok berulang (maksimal satu per form, berisi field) | Dibuat Admin per jenis belanja; setiap perubahan membentuk versi baru; SPJ menyimpan versi yang berlaku saat dibuat. Untuk perjalanan dinas mendukung tag `[SYS_PERSONNEL_ID]`, `[SYS_PERSONNEL_NAME]`, `[SYS_START_DATE]`, `[SYS_END_DATE]`; tag ID/nama berpasangan dalam konteks field/baris yang sama |
| SPJ | Kuitansi, jenis belanja (pilihan awal Seksi, menentukan form), versi form, jawaban (field tunggal dan entri blok berulang), daftar pajak (jenis pajak dari master dan nominal manual, banyak entri), lampiran PDF beserta nama asli, ukuran asal, ukuran final, dan status optimasi, status (Draft, Terkunci, Menunggu BKU, Dibukukan) | Relasi 1:1 dengan kuitansi; form snapshot saat dibuat; Total Pajak tidak boleh melebihi bruto kuitansi terkait (penyimpanan entri pajak ditolak); isian rincian bersifat informasional murni tanpa validasi matematis terhadap nominal bruto kuitansi; SPJ Terkunci sejak dikirim ke Verifikator; kuitansi terkait ikut Terkunci sejak SPJ Draft dibuat |
| Token Verifikasi SPJ | SPJ, token acak untuk barcode, nomor verifikasi (teks cetak, dibuat otomatis, urut dan tidak dipakai ulang per TA, tidak sama dengan token), waktu verifikasi, status (Berlaku atau Tidak berlaku) | Dibuat saat Verifikator menyetujui SPJ, bersama token dan nomor verifikasi; menjadi Tidak berlaku saat SPJ dikembalikan menjadi Draft (pencabutan BKU saja tidak mengubah status); token dan nomor verifikasi baru dibuat saat verifikasi ulang; halaman keaslian publik tidak menampilkan nominal atau identitas |
| Format Nomor Verifikasi | Per TA: awalan, pemisah, pola tahun, jumlah digit urut | Diatur Admin; perubahan format tidak mengubah nomor yang sudah tercetak |
| Direktori Transaksional SPJ | Kunci identitas NIP/NIK yang dimasukkan, nama pasangan, referensi sumber/pembaruan seperlunya | Terpisah dari Master Personel; mencakup pegawai organik, honorer, narasumber, dan pihak luar tanpa kategori wajib; dipakai untuk lookup dan auto-fill; tetap dipertahankan saat SPJ dibatalkan/dihapus; Admin dapat mengoreksi dan merge duplikat dengan menjaga referensi SPJ historis |
| Rentang Penugasan SPJ | TA, SPJ, identitas NIP/NIK, tanggal mulai efektif, tanggal selesai efektif | Diperoleh dari field bertag pada Form Dinamis/snapshot jawaban; bukan komitmen terpisah. Validasi overlap hanya pada pengajuan ke Verifikator, dalam TA yang sama, terhadap status SPJ Terkunci/Menunggu BKU/Dibukukan |
| BKU | Kuitansi/SPJ terkait, nomor BKU (input manual), tanggal BKU, status | Menandai realisasi pengeluaran kas belanja (tidak mencatat penerimaan kas/SP2D); satu BKU per kuitansi; nomor diinput manual oleh Bendahara & unik per TA; penanggalan bebas tanpa batasan kronologis; koreksi No. BKU/tanggal tanpa pembatalan jika nominal tidak berubah; nomor BKU yang dicabut bebas digunakan kembali; pencabutan BKU |
| Audit Event | Waktu, aktor (ID akun, snapshot nama, NIP/NIK, peran saat aksi), entitas, aksi, nilai sebelum/sesudah, alasan | Merekam perubahan signifikan, pencabutan dan koreksi BKU, serta perubahan status akun. Peristiwa yang juga dicatat: pengesahan ("Sahkan"), perubahan alokasi setelah pengesahan atau APBD-P, verifikasi SPJ disetujui atau dikembalikan, dan pencatatan BKU. Login dan logout tidak dicatat. Pembatalan kuitansi atau SPJ Draft tidak dicatat; entri yang terkait kuitansi atau SPJ tersebut ikut terhapus otomatis oleh sistem dan tidak dapat dihapus manual. Penghapusan TA setelah retensi tidak dicatat, dan seluruh entri audit TA tersebut ikut terhapus. Aktor selalu personel nyata; Admin dapat membaca seluruh entri termasuk nominal. Pada aksi Delegasi Plh./Plt., entri memuat `definitive_officer_id` (ID pejabat definitif), `delegate_officer_id` (ID pejabat penerima delegasi), dan keterangan status Delegasi Aktif. Penetapan, tanggal berlaku, pencabutan dini, dan pengakhiran otomatis wajib tercatat; pengakhiran otomatis diberi penanda otomatis. |

#### Dokumen 01 §6

## 6. PEMISAHAN TUGAS & BATAS PERAN ADMIN
1. **Bendahara Tidak Merangkap PPTK:** Satu personel tidak boleh menjadi Bendahara Pengeluaran sekaligus PPTK/Seksi pada TA yang sama, termasuk saat ditunjuk sebagai Plh./Plt. Sistem menolak penugasan yang melanggar aturan ini.
2. **Lingkup Admin:** Admin mengelola data master dan status TA, termasuk membuka kembali TA Arsip dan menghapus TA sesuai retensi (poin 6 §1.3), serta menetapkan dan mencabut Delegasi Plh./Plt. (poin 7 dan 10). Admin tidak melihat alokasi, SPD, kuitansi, SPJ, verifikasi, BKU, atau angka realisasi/sisa SPD di dashboard.
3. **Pengecualian Admin yang Disetujui:** (a) Pagu Induk tampil pada kartu TA; (b) Jejak Audit menampilkan seluruh entri, termasuk entri keuangan dan nilai sebelum/sesudah, dalam mode baca saja; (c) countdown dan banner merah tampil pada dashboard Admin.
4. **Pengawas/Auditor:** Mengakses laporan dan Jejak Audit pada TA yang ditugaskan dalam mode baca saja (lihat §8). Tidak mengubah pagu, penugasan, kuitansi, SPJ, atau BKU, dan tidak memiliki akses master, akun, atau proses transaksi.
5. **Akses PPTK dan Verifikator:** PPTK tidak melihat Pagu Induk dan hanya melihat Jejak Audit milik seksinya. Bendahara Pengeluaran hanya melihat entri Jejak Audit aksinya sendiri. Verifikator melihat Pagu Induk pada kartu TA dan seluruh Jejak Audit TA, dalam mode baca saja.
6. **Jejak Audit Ringkas:** Jejak Audit mencatat aksi administratif (akun, master, status TA, penugasan, dan aksi Pengawas) serta koreksi dan pencabutan BKU. Jejak Audit juga mencatat pengesahan ("Sahkan"), perubahan alokasi setelah pengesahan atau APBD-P, verifikasi SPJ disetujui atau dikembalikan, dan pencatatan BKU. Login dan logout tidak dicatat. Pembatalan kuitansi atau SPJ Draft tidak meninggalkan jejak. Entri audit yang terkait kuitansi atau SPJ tersebut, termasuk koreksi dan pencabutan BKU, ikut terhapus otomatis oleh sistem bersama data kuitansi atau SPJ. Tidak ada tombol hapus manual untuk entri audit.
7. **Delegasi Wewenang Sementara (Plh./Plt.):** Admin dapat menambahkan penugasan sekunder berstatus Delegasi Aktif (Plh./Plt.) bagi Bendahara Pengeluaran, PPTK/Seksi, atau PA/KPA yang berhalangan sementara. Setiap delegasi wajib memiliki tanggal mulai dan tanggal berakhir yang tegas. Selama rentang tersebut sistem mengizinkan duplikasi peran sementara pada seksi yang sama dan secara otomatis menonaktifkan hak transaksi pejabat definitif. Penugasan definitif tetap tercatat dan tidak dihapus. Delegasi tidak memakai mekanisme mutasi. Nama pejabat Plh./Plt. tampil dengan keterangan atribut jabatan di bawahnya, misalnya "Plh. PPTK Seksi X".
8. **Validasi Perangkapan Delegasi:** Sistem menolak penunjukan Plh./Plt. jika personel yang ditunjuk sedang memegang peran yang bertentangan pada TA tersebut, sesuai poin 1. Aturan ini ditegakkan di server.
9. **Larangan Verifikasi Mandiri:** Tidak ada personel yang boleh memverifikasi SPJ yang ia ajukan atau kelola sendiri, baik saat berstatus pejabat definitif maupun sebagai Plh./Plt. PPTK. Sistem menolak aksi verifikasi mandiri ini di server.
10. **Pengakhiran Delegasi:** Delegasi Aktif berakhir otomatis oleh sistem pada pukul 23:59 WITA pada tanggal berakhir (end_date). Admin dapat mencabut delegasi lebih awal apabila pejabat definitif kembali lebih cepat dari jadwal. Pencabutan dini wajib disertai alasan tertulis dan tercatat di Jejak Audit.
11. **Snapshot Penandatangan Dokumen:** Nama dan NIP pejabat yang tampil pada kuitansi, lembar Hasil Verifikasi SPJ, dan dokumen cetak lainnya diambil dari penugasan aktif yang berlaku pada waktu dokumen dibuat. Untuk kuitansi, waktu tersebut adalah saat kuitansi disimpan di sistem, bukan Tanggal Kuitansi yang dapat diisi mundur. Untuk SPJ dan Hasil Verifikasi SPJ, waktu tersebut adalah saat SPJ diajukan ke Verifikator dan berstatus Terkunci. Cetak ulang selalu merujuk snapshot asli dan tidak berubah setelah delegasi berakhir. Dokumen yang dibuat sebelum tanggal mulai delegasi tetap atas nama pejabat definitif.

---

#### Dokumen 02 §8

## 8. Cetak hasil verifikasi SPJ dan verifikasi keaslian (barcode)
1. Setelah SPJ disetujui Verifikator (berstatus Menunggu BKU atau Dibukukan), PPTK pada seksi SPJ tersebut, dan Verifikator untuk seluruh seksi, dapat mencetak "Hasil Verifikasi SPJ" dalam format PDF.
2. Cetakan memakai template terpisah yang diatur Admin melalui Visual Live Editor seperti template kuitansi (§2.3). Data berikut diisi dari sistem, bukan dari editor: TA, seksi, identitas SPJ, nomor verifikasi, tanggal verifikasi, nama dan NIP Verifikator, sub kegiatan, kode rekening belanja, uraian, nilai bruto, nama penerima, bank dan nomor rekening penerima, serta setiap entri pajak beserta nominal yang diisi manual. Jumlah yang dibayarkan dan Total Pajak dihitung sistem sesuai §5 dan dicetak. Admin dapat mengubah tata letak, label, teks statis, logo, dan gambar stempel, tetapi tidak dapat mengubah data sistem dari editor.
3. Setiap cetakan memuat dua pengenal yang terpisah. (a) Barcode (QR) berisi tautan verifikasi keaslian dengan token acak yang dibuat sistem saat SPJ disetujui. Token tidak dicetak sebagai teks, bukan nomor urut, dan tidak memuat nomor kuitansi. (b) Nomor verifikasi tercetak sebagai teks di samping barcode. Sistem membuat nomor secara otomatis bersamaan dengan token, dengan urutan yang terus bertambah dalam TA dan tidak pernah dipakai ulang. Nomor tidak sama dengan token, serta tidak memuat nomor kuitansi, nominal, atau nama. Admin mengatur format nomor per TA (awalan, pemisah, pola tahun, dan jumlah digit urut). Nomor yang sudah tercetak tidak berubah ketika format diganti. Nomor verifikasi tidak dipakai sebagai pengganti token pada tautan.
4. Halaman verifikasi keaslian dapat dibuka tanpa login. Halaman hanya menampilkan status keaslian (Berlaku atau Tidak berlaku), nama TA, nama seksi, dan tanggal verifikasi. Halaman tidak menampilkan nominal, nama penerima, NIP/NIK, nomor rekening, lampiran, rincian kuitansi/SPJ, atau jejak audit. Ketentuan ini berlaku pada respons server, bukan hanya pada tampilan.
5. Status keaslian mengikuti status SPJ. Jika Verifikator mengembalikan SPJ menjadi Draft, halaman menampilkan Tidak berlaku untuk cetakan sebelumnya. Pencabutan BKU saja tidak mengubah status keaslian: selama SPJ belum dikembalikan menjadi Draft, belum dilepas dari kuitansi, dan kuitansinya belum dibatalkan, SPJ tetap sah (Berlaku) karena masih dapat diteruskan ke pencatatan BKU, misalnya untuk memperbaiki No. BKU yang salah. Setelah SPJ kembali disetujui, token dan nomor verifikasi baru dibuat, dan token serta nomor lama tidak berlaku.
6. Pencetakan ulang diperbolehkan selama SPJ berstatus Menunggu BKU atau Dibukukan. Cetakan untuk SPJ berstatus Draft atau Terkunci ditolak. Selama token belum berganti, cetakan ulang memuat nomor verifikasi dan barcode yang sama.
7. Nama dan NIP pejabat pada Hasil Verifikasi SPJ diambil dari snapshot penugasan sesuai Dokumen 01 §6 poin 11. Cetak ulang selalu memakai snapshot tersebut dan tidak berubah setelah delegasi Plh./Plt. berakhir.

#### Dokumen 02 §2.3

### 2.3 Editor template
Admin mengelola tata letak dan teks melalui Visual Live Editor tanpa coding, dengan preview cetak. Opsi unggah template `.doc`/`.docx` merupakan alternatif. Editor mengatur template, bukan menggantikan data transaksi; data seperti TA, uraian, nominal, subkegiatan, pejabat dan tanggal diisi dari transaksi/Workspace TA sesuai sumbernya. Editor juga mengatur template Hasil Verifikasi SPJ (§8).

#### Dokumen 03 §1

## 1. Prinsip lintas role
- Master data bersifat global; setiap TA memiliki snapshot operasionalnya sendiri.
- **Autentikasi Cerdas & Desain Antarmuka Halaman Login:**
  - **Arsitektur Visual (Treasury & Market Terminal):**
    - Halaman login memakai tema Treasury & Market Terminal: nuansa terminal keuangan yang tenang dan mudah dibaca, bukan layar hitam pekat dengan teks hijau terang.
    - Latar memakai slate/charcoal gelap (`#0B1120`) dengan permukaan panel `#111827` dan garis tepi 1 px `#1F2937`. Halaman login tidak memakai efek kaca (*glassmorphism*), blur, gradasi cahaya, animasi, atau ticker.
    - Garis kisi mikro boleh dipakai sebagai ornamen statis tipis pada panel kiri, dengan kontras teks tetap memenuhi aturan aksesibilitas pada bagian Tema Visual.
  - **Tata Letak Responsif (Split-Hero):**
    - **Panel Kiri (Identitas & Wibawa Instansi):**
      - Header identitas resmi: *"Pemerintah Kabupaten Balangan • Kecamatan Batumandi"*.
      - Logo instansi daerah bersanding dengan jenama **AMANDA** (*Aplikasi Manajemen Data Anggaran*), tampil datar tanpa efek cahaya.
      - Pesan nilai/etos kerja aparatur muda: *"Tertib Administrasi, Akuntabel, dan Transparan dalam Setiap Rupiah."*
      - Halaman bebas dari ticker/banner animasi yang mengganggu fokus.
    - **Panel Kanan (Kartu Login Datar):**
      - Kartu datar dengan garis tepi 1 px dan tanpa blur atau bayangan tebal.
      - *Field Identitas Terpadu (Single-Field Identifier):* Satu kolom berlabel `NIP / NIK / Email Auditor` dengan teks monospace untuk NIP/NIK. Input angka dikenali sebagai personel internal; tanda `@` dikenali sebagai Pengawas/Auditor dan ditandai dengan ikon serta label teks "Akun Pengawas/Auditor", tidak hanya warna.
      - *Field Kata Sandi:* Dilengkapi **tombol intip sandi** (*toggle show/hide password*) responsif (password minimal 6 karakter).
      - *Tombol Aksi Utama:* Tombol *"Masuk ke Sistem"* berwarna amber (`#F59E0B`) dengan teks gelap (`#0B1120`). Saat diproses, tombol menampilkan teks "Memeriksa akun..." dan tidak dapat ditekan dua kali.
      - *Pesan Galat:* Galat login ditampilkan sebagai teks dengan ikon di atas tombol, tanpa menyebut apakah NIP atau kata sandi yang salah.
      - *Catatan Bantuan Admin:* Kotak informasi mikro berlabel tegas *"Lupa password atau akun terkendala? Hubungi Administrator Sistem."* (karena reset password bersifat terpusat oleh Admin).
      - *Tautan Cepat Portal Publik:* Tombol sekunder teal outline (`#2DD4BF`) berlabel jelas *"Lihat Ringkasan Publik"* untuk akses instan ke Portal Keterbukaan Informasi anonim tanpa login.
  - **Responsif Layar Sempit:** Pada layar sempit, panel kiri menjadi header ringkas di atas kartu login. Seluruh elemen tersusun satu kolom dengan field dan tombol selebar layar.
- **Tata Letak Dasbor (Sidebar & Topbar):**
  - Semua peran kecuali Pengawas/Auditor memakai sidebar untuk menu dan topbar tipis untuk konteks (TA aktif, peran aktif sebagai label, mini progress bar, dan logout).
  - Pengawas/Auditor memakai navigasi atas tanpa sidebar dan tanpa mini progress bar.
  - Admin hanya melihat Pagu Induk pada topbar.
  - Larangan dropdown ganti TA atau peran di topbar tetap berlaku.
- **Tema Visual Treasury (Login, Pro Mode, dan Mode Standar):**
  - **Token Bersama:** Seluruh antarmuka memakai satu set token warna, huruf, dan jarak. Nilai awal: latar `#0B1120`; permukaan `#111827`; garis tepi `#1F2937`; teks utama `#E5E7EB`; teks sekunder `#9CA3AF`; aksen utama amber `#F59E0B`; aksen sekunder teal `#2DD4BF`; status baik/naik hijau `#34D399`; kritis merah `#F87171`; peringatan kuning `#FBBF24`; lonjakan oranye `#FB923C`.
  - **Huruf:** Sans-serif (Inter) untuk teks umum dan judul. Monospace (JetBrains Mono) untuk NIP/NIK, kode TA, nomor BKU, nomor bukti, dan kode rekening. Angka nominal memakai angka tabular (lebar digit sama) agar kolom angka sejajar.
  - **Pro Mode (Dashboard Utama dan Monitoring/Analitik):**
    - Diterapkan pada dasbor utama dan modul monitoring atau analitik bagi pengelola keuangan tingkat lanjut, yaitu dasbor PA/KPA (§6 dan §11), dasbor Bendahara, dan dasbor Verifikator.
    - Kepadatan tinggi: ticker ringkasan horizontal di bagian atas (sesuai §6 dan §11), tabel rapat dengan tinggi baris sekitar 32 px, angka rata kanan, dan titik warna untuk zona analitik.
    - Pro Mode tidak mengubah cakupan data. Setiap dasbor hanya menampilkan angka yang diizinkan untuk role tersebut.
  - **Mode Standar (Input Transaksi dan Laporan Harian):**
    - Diterapkan pada halaman input kuitansi, SPJ, Form Dinamis, dan halaman BKU serta laporan harian.
    - Kepadatan lega: jarak antarelemen 16–24 px, ukuran teks dasar 16 px, tinggi baris tabel sekitar 48 px, dan hanya kolom yang diperlukan untuk keputusan.
    - Setiap layar memiliki satu aksi utama yang jelas. Pop-up dan halaman sendiri mengikuti Dokumen 01 §15.
    - Tidak ada tombol ganti mode. Mode standar otomatis dipakai pada layar kecil (di bawah 768 px), sedangkan Pro Mode mengikuti lebar layar yang lebih besar.
  - **Status dan Keterbacaan:** Setiap status (zona hijau, kuning, merah, dan oranye; status Dibukukan atau Terkunci; dan sejenisnya) wajib memakai teks atau ikon, tidak hanya warna. Kontras teks normal minimal 4,5:1 dan teks besar serta ikon minimal 3:1 (WCAG AA). Fokus keyboard memakai cincin amber 2 px yang terlihat. Transisi dibatasi, dan dimatikan jika pengguna memilih pengurangan gerak di perangkatnya.
  - **Batas Data:** Tema tidak mengubah cakupan data. Dasbor Admin tidak menampilkan realisasi atau sisa SPD (§2.1 poin 6 dan Dokumen 01 §6). Portal publik tidak menampilkan nominal rupiah (§9 poin 6). Portal publik mengikuti tema ini sesuai §9 poin 7–9.
- **Alur Masuk Berjenjang & Auto-Skip Pasca-Login:**
  1. **Admin:** Langsung masuk ke Dasbor Administrasi Global (Master & TA) tanpa melalui layar pemilih TA atau jabatan.
  2. **Pengawas/Auditor:** Langsung masuk ke Dasbor Pengawas (Laporan & Audit Trail Baca-Saja) TA yang ditugaskan. Jika surat tugas menugaskan lebih dari satu TA, Auditor memilih TA penugasan terlebih dahulu lalu langsung masuk ke dasbor TA tersebut.
  3. **Personel Internal (Bendahara, PPTK, Verifikator, PA/KPA):**
     - Jika personel hanya memiliki tepat 1 penugasan di 1 TA: sistem otomatis langsung masuk (*auto-skip*) ke dasbor TA dan jabatan tersebut.
     - Jika personel memiliki penugasan di lebih dari 1 TA: sistem menampilkan layar daftar TA penugasan terlebih dahulu, dilanjutkan layar daftar jabatan aktif pada TA yang dipilih (bila memegang lebih dari 1 jabatan di TA tersebut), baru kemudian masuk ke dasbor operasional.
     - Jika personel hanya memiliki penugasan di 1 TA tetapi memegang lebih dari 1 jabatan di TA tersebut: sistem langsung menampilkan layar daftar jabatan aktif lalu masuk ke dasbor operasional.
- **Isolasi Konteks Sesi & Larangan Alih Konteks Tanpa Logout:** Sesi operasional terisolasi ketat pada tepat satu TA (`active_ta_id`) dan satu Peran (`active_role`) yang aktif. Sistem dilarang menyediakan mekanisme alih TA (*switch TA*) atau alih peran (*switch role*) secara langsung di dalam aplikasi (misalnya melalui dropdown navbar). Untuk berpindah Tahun Anggaran atau berganti jabatan/peran, pengguna **wajib melakukan Logout** (menghancurkan sesi aktif) dan melakukan login ulang.
- **Pembatasan Percobaan Login & Batas Tidak Aktif:** Setelah 10 kali gagal login berturut-turut, akun terkunci dan pemulihannya dilakukan melalui reset password oleh Admin. Batas ini tidak berlaku untuk akun Admin, yang tidak dikunci karena percobaan gagal. Bila Admin lupa password, reset dilakukan melalui backend, bukan melalui aplikasi. Sesi berakhir otomatis (auto logout) setelah 1 jam tanpa aktivitas. Tidak ada batas maksimum lama login dan tidak ada peringatan sebelum logout.
- Penugasan, transaksi, dan perubahan anggaran terikat pada TA dan masa berlaku masing-masing.
- **Delegasi Plh./Plt.:** Delegasi sementara mengikuti Dokumen 01 §6 poin 7–11. Penugasan Delegasi Aktif ikut dihitung dalam alur masuk berjenjang, dan selama delegasi aktif hak transaksi pejabat definitif nonaktif.
- Perubahan tidak menghapus sejarah. Dokumen lama tetap dapat ditelusuri dan diakses sesuai hak.
- Mini progress bar di topbar mengikuti Dokumen 01 §3.3; laporan PDF dan Excel mengikuti Dokumen 01 §9 dan hanya memuat data Dibukukan. Rincian Kartu Kendali Kegiatan per subkegiatan dan rekening belanja (Dokumen 01 §9 poin 2g) mengikuti cakupan laporan a. Unduhan Excel rekap isian SPJ berisi satu sheet per jenis belanja (Dokumen 01 §9 poin 6–7). Pajak tidak termasuk rekap isian SPJ; rekap pajak per jenis pajak (Dokumen 01 §9 poin 10, hanya SPJ yang sudah memiliki BKU) dapat dilihat Bendahara, PPTK untuk seksinya, Verifikator, PA/KPA, dan Pengawas.
- Input nominal memakai format Rupiah dengan pemisah ribuan titik; kode dan nomor rekening adalah teks.
- Pencarian dan filter hanya pada daftar yang ditetapkan, dan hanya dalam cakupan data peran pengguna. Aksi singkat dan konfirmasi memakai pop-up; isian panjang memakai halaman sendiri (Dokumen 01 §15).
- Rekening belanja adalah kamus global yang dapat dipakai di subkegiatan mana pun; pasangan subkegiatan dan rekening membedakan baris alokasi (Dokumen 04 §2.2).
- Setiap aksi tercatat atas nama personel yang login, bukan akun generik (lihat Dokumen 04 §6).
- Batas peran Admin dan pemisahan tugas mengikuti Dokumen 01 §6: Bendahara tidak boleh merangkap PPTK pada TA yang sama, dan hanya satu TA yang boleh berstatus Aktif Penuh pada satu waktu.

#### Dokumen 01 §3.3

### 3.3 Topbar dan Mini Progress Bar
Istilah navbar pada seluruh dokumen berarti topbar. Navigasi menu memakai sidebar untuk semua peran kecuali Pengawas/Auditor. Topbar menampilkan label TA aktif dan peran aktif (tanpa dropdown ganti TA atau peran), mini progress bar realisasi terhadap pagu, dan tombol logout. Mini progress bar disertai angka sesuai cakupan peran:

| Peran | Isi mini progress bar topbar |
|---|---|
| Bendahara, PA/KPA, Verifikator | Pagu, realisasi, sisa SPD bebas, dan serapan seluruh instansi |
| PPTK | Pagu, realisasi, dan sisa SPD bebas seksinya saja |
| Admin | Pagu Induk saja |
| Pengawas/Auditor | Tidak ada mini progress bar dan tidak ada sidebar |

---

#### Dokumen 01 §9

## 9. KATALOG LAPORAN
1. **Format:** Setiap laporan tersedia dalam PDF untuk cetak dan arsip, serta Excel untuk diolah lebih lanjut, sesuai hak peran.
2. **Daftar laporan:**
   a. Rekap realisasi per seksi: pagu, realisasi BKU, Realisasi (%) (Realisasi BKU ÷ Pagu), dan status per seksi.
   b. Buku Kas (BKU): nomor BKU (input manual Bendahara, unik per TA), tanggal BKU, nominal, dan kuitansi terkait (kolom ini tidak ditampilkan untuk PA/KPA). BKU AMANDA murni mencatat pembukuan realisasi pengeluaran belanja per kuitansi/SPJ dan tidak mencatat transaksi penerimaan kas, SP2D, atau saldo Uang Persediaan (UP/GU/TU). Sistem membebaskan penanggalan tanpa batasan kronologis antar-tanggal kuitansi, SPJ, dan BKU.
   c. Daftar kuitansi dan SPJ: nomor, tanggal, seksi, status kuitansi (Aktif atau Terkunci), dan status SPJ. Hanya kuitansi dan SPJ yang sudah Dibukukan (BKU tercatat). Laporan ini tidak ditampilkan kepada PA/KPA.
   d. Laporan realisasi per seksi dan subkegiatan: kolom Realisasi (%) (Realisasi BKU ÷ Pagu) per seksi dan per subkegiatan.
   e. Rekap isian SPJ per jenis belanja: per SPJ, isian Form Dinamis dalam format Excel. Isian mengikuti versi form saat SPJ dibuat (Dokumen 04 §2.2). Susunan kolomnya diatur pada poin 6. Pajak tidak termasuk dalam laporan ini. Laporan ini berlaku untuk semua peran yang berhak.
   f. Rekap pajak per jenis pajak: entri pajak pada SPJ yang sudah memiliki BKU, dikelompokkan per jenis pajak. Diatur pada poin 10.
   g. Rincian Kartu Kendali Kegiatan (realisasi per subkegiatan dan rekening belanja): laporan baru yang terpisah dari laporan (d). Tampil dalam PDF dan Excel dengan susunan berikut:
      1) Kepala: logo dan nama instansi, judul "Rincian Kartu Kendali Kegiatan", dan keterangan "per [tanggal akhir periode laporan]".
      2) Blok identitas: kode dan nama subkegiatan, kode dan nama rekening belanja, serta pagu akhir pasangan subkegiatan dan rekening pada TA tersebut (Dokumen 04 §2.2). Unit organisasi, program, kegiatan, dan aktivitas tidak ditampilkan.
      3) Satu blok per pasangan subkegiatan dan rekening belanja yang sudah memiliki realisasi BKU. Pasangan atau rekening tanpa realisasi tidak membentuk blok.
      4) Kolom tabel: No; Tanggal (tanggal BKU); No. Bukti (nomor BKU); Uraian (uraian kuitansi yang dibukukan); Realisasi (nominal bruto BKU); Sisa Anggaran (pagu akhir dikurangi akumulasi realisasi BKU sampai baris tersebut, tanpa komitmen). Kolom LS, UP/GU/TU, dan kolom Form Dinamis tidak ada.
      5) Urutan baris menurut tanggal BKU naik, lalu nomor BKU. Setiap blok diakhiri baris TOTAL yang memuat total realisasi dan sisa anggaran akhir.
      6) Blok disusun ke bawah, satu blok setelah blok lain, tidak berdampingan. Dalam PDF, blok boleh berlanjut ke halaman berikutnya dengan header kolom diulang. Dalam Excel, setiap blok memakai baris judul sendiri dan dipisahkan satu baris kosong dalam satu sheet.
      7) Filter tersedia untuk seksi, subkegiatan, dan periode tanggal BKU. Filter hanya membatasi baris yang tampil dan diunduh; sisa anggaran selalu dihitung dari awal TA, tidak dimulai ulang dari tanggal awal periode filter.
      8) Cakupan per peran mengikuti laporan (a) pada poin 3. Hanya data SPJ Dibukukan yang masuk laporan.
   h. Unduhan lampiran PDF SPJ diatur pada Dokumen 02 §9 dan bukan bagian dari katalog ini.
3. **Cakupan per peran:** Bendahara dan Verifikator melihat seluruh seksi. PPTK hanya melihat seksinya. Pengawas/Auditor melihat seluruh seksi pada TA yang ditugaskan dalam mode baca saja. Admin tidak mendapat laporan apa pun. Akses PA/KPA: laporan (a), (b), (d), (e), (f), dan (g) untuk seluruh seksi, hanya data SPJ Dibukukan. Laporan (c) tidak ditampilkan kepada PA/KPA. Laporan (b) dan (f) tampil tanpa kolom kuitansi untuk PA/KPA. Laporan (f) mengikuti cakupan laporan (e). Laporan (g) mengikuti cakupan laporan (a). Seluruh laporan berbasis realisasi: hanya SPJ berstatus Dibukukan (BKU tercatat) yang masuk laporan. Komitmen kuitansi yang belum dibukukan dan SPJ berstatus Menunggu BKU tidak dilaporkan.
4. **Pengisian form:** Seksi memilih jenis belanja di awal pembuatan SPJ, dan pilihan itu menentukan Form Dinamis yang tampil. Daftar jenis belanja berasal dari Form Dinamis yang dikelola Admin, bukan daftar tetap di aplikasi. Jenis belanja bukan field di dalam form dan tidak diisi ulang. Seluruh field Form Dinamis diisi manual oleh Seksi. Nilai tidak diwarisi dari rekening belanja dan tidak dihitung otomatis. Laporan (e) menampilkan jawaban tersebut seperti tanggapan Google Form di spreadsheet: satu baris per SPJ, satu kolom per field; jika form memiliki blok berulang, satu baris per entri blok (poin 9). Pengelompokan per jenis belanja mengikuti jenis belanja yang dipilih di awal SPJ. Tampilan dan unduhan diatur pada poin 7 dan 8.
5. **Jejak:** Setiap unduhan atau cetakan laporan oleh Pengawas/Auditor tercatat di Jejak Audit (§8 poin 8).
6. **Susunan kolom laporan e (Excel):** Setiap jenis belanja menjadi satu sheet di file Excel. Kolom sheet adalah gabungan field dari semua versi form yang dipakai SPJ di sheet tersebut, diurutkan mengikuti versi terbaru; field yang tidak ada pada versi form SPJ tertentu tampil kosong. Jenis belanja tidak menjadi kolom, karena sudah menjadi nama sheet. Contoh untuk jenis belanja perjalanan dinas luar daerah: Nama, NIP, Uraian, Seksi, Nama Rekening Penerima, Nomor Rekening, Nama Bank, Upload SPJ, Nomor Surat Perintah Tugas, Tanggal Surat Perintah Tugas, Golongan Pangkat, Daerah Tujuan, Tanggal Berangkat, Tanggal Kembali, Lama Hari, Uang Harian Per Hari, Total Uang Harian, Uang Transport, Total Biaya Lainnya, Nama Hotel, Tanggal Check In, Tanggal Check Out, Jumlah Malam, Rate/Malam, Total Biaya Penginapan, Dari, Tujuan, lalu kelompok field Penerbangan 1 (Tanggal Penerbangan, Nama Maskapai, Kode Penerbangan, Nomor Tiket, Kode Booking, Asal Keberangkatan, Tujuan Keberangkatan, Harga Tiket), kelompok field Penerbangan 2 dengan kolom yang sama, Total Biaya Tiket, dan Total Yang Dibayarkan.
   - Field yang namanya berulang diberi penanda urut (Penerbangan 1 dan Penerbangan 2) agar kolom dapat dibedakan.
   - Laporan (e) tidak menambahkan kolom BKU, kode subkegiatan, kode rekening, atau kuitansi setelah kolom form.
   - Visibilitas kolom NIP dan Nomor Rekening: Tidak ada penyamaran (masking). Kolom NIP dan Nomor Rekening ditampilkan penuh dan terbuka di seluruh unduhan laporan Excel bagi semua peran yang berhak mengunduh (Bendahara, PPTK untuk seksinya, Verifikator, PA/KPA, dan Pengawas/Auditor). Ketentuan ini tidak berlaku untuk Laporan Kustom; kolom NIP/NIK dan Nomor Rekening pada Laporan Kustom tetap mengikuti Matriks Kolom poin 12 d.
7. **Tampilan dan unduhan:** Laporan (e) tampil di dalam AMANDA sebagai tabel yang dapat difilter, misalnya per jenis belanja, seksi, TA, dan periode. Unduhan Excel hanya memuat baris dan kolom sesuai filter yang sedang aktif. Kolom Excel mengikuti field Form Dinamis dari jenis belanja yang difilter. Setiap jenis belanja memiliki form dan susunan kolomnya sendiri, sehingga perjalanan dinas luar daerah dan belanja habis pakai tidak berbagi kolom. Jika filter mencakup lebih dari satu jenis belanja, Excel berisi satu sheet per jenis belanja yang terpilih, dengan nama sheet sesuai jenis belanja. Sheet tidak digabung karena field tiap jenis belanja berbeda.
8. **Wajib atau opsional:** Admin menandai setiap field Form Dinamis sebagai wajib atau opsional, seperti pengaturan wajib pada Google Form. Field wajib harus terisi sebelum SPJ dapat diajukan. Field opsional yang dikosongkan tersimpan kosong dan tampil kosong di laporan maupun Excel; pengisian dengan tanda strip atau teks pengganti tidak diperlukan.

9. **Blok berulang pada Form Dinamis:**
   a. Admin dapat menambahkan paling banyak **satu blok berulang** per form. Admin memberi nama blok, misalnya "Pelaku", lalu memasukkan field ke dalam blok tersebut. Field di luar blok diisi sekali per SPJ.
   b. Form tanpa blok berulang menghasilkan satu baris per SPJ.
   c. Pada SPJ, Seksi/PPTK mengisi entri pertama blok berulang, lalu menekan "+ Tambah" untuk menambah entri berikutnya. Form dengan blok berulang minimal memiliki satu entri.
   d. Field wajib di dalam blok wajib diisi pada setiap entri. Field opsional yang kosong tetap kosong.
   e. Di laporan dan Excel, setiap entri blok menjadi satu baris. Nilai field di luar blok diulang pada setiap baris SPJ tersebut.
   f. Field biasa yang namanya berulang, seperti Penerbangan 1 dan Penerbangan 2 pada contoh perjalanan dinas di poin 6, bukan blok berulang. Keduanya adalah field tunggal yang dipasang Admin di dalam form.
   g. Struktur blok mengikuti versi form saat SPJ dibuat (Dokumen 04 §2.2).

10. **Rekap pajak per jenis pajak (laporan f):**
   a. Laporan hanya memuat entri pajak pada SPJ yang sudah memiliki BKU (terealisasi), satu baris per entri pajak. SPJ yang belum dibukukan tidak muncul di laporan.
   b. Kolom: Jenis Pajak, Nominal Pajak, Seksi, Jenis Belanja, Kode Subkegiatan, Kode Rekening Belanja, No. BKU, dan Tanggal Kuitansi (kolom Tanggal Kuitansi tidak ditampilkan untuk PA/KPA).
   c. Tampilan di AMANDA dikelompokkan per jenis pajak. Unduhan Excel berisi satu sheet per jenis pajak, sama seperti aturan sheet per jenis belanja (poin 7).
   d. Laporan dapat difilter menurut jenis pajak, seksi, TA, dan periode. Unduhan Excel hanya memuat baris sesuai filter aktif.
   e. Excel tidak memuat subtotal atau total otomatis.
   f. Pajak tidak masuk laporan rekap isian SPJ (laporan e). Nominal pajak tidak mengubah nominal bruto kuitansi.

11. **Mode Pratinjau Interaktif Form Dinamis (Admin):**
   a. Pratinjau dibuka sebagai tab "Pratinjau Langsung" di dalam halaman Visual Live Editor, berdampingan dengan tab "Konfigurasi Editor". Admin dapat beralih seketika antara kedua tab tanpa kehilangan draf. Pratinjau tidak dibuka sebagai pop-up (§15 poin 7 dan Dokumen 05 poin 148).
   b. Pratinjau menguji draf form yang belum disimpan. Tampilannya mengikuti tampilan pengisian PPTK, termasuk field wajib, blok berulang dengan tombol "+ Tambah", dan tag sistem.
   c. Auto-fill NIP/NIK pada tag `[SYS_PERSONNEL_ID]` dan `[SYS_PERSONNEL_NAME]` membaca Direktori Transaksional SPJ secara read-only. Pembacaan ini tidak mengubah direktori dan tidak menambah entri Jejak Audit. Jika NIP/NIK tidak ditemukan, nama diisi manual sesuai §11 poin 2.
   d. Cek bentrok jadwal di pratinjau disimulasikan sepenuhnya dengan data contoh (mock data) yang terisolasi. Pratinjau tidak menjalankan validasi bentrok terhadap SPJ asli dan tidak menampilkan status atau tanggal SPJ operasional kepada Admin.
   e. Seluruh isian dalam pratinjau, termasuk ketikan, entri blok berulang, dan hasil simulasi, hanya berada di memori sisi klien sebagai draf editor. Tidak ada data pratinjau yang disimpan ke server, sehingga tidak diperlukan pembersihan berkala. Pratinjau tidak menghasilkan kuitansi, SPJ, BKU, maupun entri Jejak Audit.
   f. Uji batas maksimal satu blok berulang tetap dilakukan di logika Form Builder (Dokumen 05 poin 58), bukan di pratinjau. Pratinjau berfokus pada kenyamanan pengisian dan responsivitas field bagi PPTK.
   g. Pratinjau hanya dapat diakses Admin. Peran lain tidak memiliki akses ke Visual Live Editor maupun tab pratinjau ini.
   h. Tampilan pratinjau mengikuti Tema Visual Treasury & Market Terminal (§1 Dokumen 03): latar slate/charcoal #0B1120, permukaan #111827, garis tepi #1F2937, tidak memakai layar hitam pekat, dan memenuhi kontras WCAG AA.

12. **Penyusunan Laporan Kustom (On-the-Fly Report Builder):**
   a. Menu "Penyusunan Laporan Kustom" tersedia di panel laporan untuk Bendahara, PPTK, PA/KPA, dan Verifikator. Admin dan Pengawas/Auditor tidak memiliki akses. Pengawas/Auditor tetap memakai Katalog Laporan baku secara baca saja (poin 2 dan 3).
   b. Parameter laporan: Tahun Anggaran mengikuti Workspace TA aktif; cakupan seksi mengikuti peran (PPTK hanya seksinya; Bendahara, PA/KPA, dan Verifikator seluruh seksi); rentang tanggal BKU.
   c. Data bersumber hanya dari SPJ Dibukukan dengan BKU tercatat. Kuitansi Aktif, kuitansi Terkunci, SPJ Draft, dan SPJ Menunggu BKU tidak ikut. Kolom Status SPJ tidak tersedia, karena statusnya selalu Dibukukan.
   d. Pilihan kolom diatur melalui Matriks Kolom yang Diizinkan per Peran berikut. Kolom yang tidak diizinkan tidak ditampilkan pada antarmuka peran tersebut.

| Kolom | Bendahara | PPTK (seksi sendiri) | Verifikator | PA/KPA |
|---|---|---|---|---|
| Tanggal BKU, No. BKU | Ya | Ya | Ya | Ya |
| Kode dan Nama Subkegiatan | Ya | Ya | Ya | Ya |
| Kode dan Nama Rekening Belanja | Ya | Ya | Ya | Tidak |
| Uraian Kuitansi | Ya | Ya | Ya | Tidak |
| Nama Penerima | Ya | Ya | Ya | Tidak |
| Nilai Bruto | Ya | Ya | Ya | Ya |
| Total Pajak | Ya | Ya | Ya | Ya |
| Jumlah Dibayarkan | Ya | Ya | Ya | Ya |
| NIP/NIK dan Nomor Rekening | Ya | Ya | Ya | Tidak |

   e. Server memvalidasi daftar kolom pada setiap pratinjau dan unduhan. Jika daftar memuat kolom yang tidak diizinkan untuk peran tersebut, server menolak seluruh permintaan, termasuk permintaan melalui pemanggilan langsung.
   f. Pratinjau menampilkan paling banyak 10 baris pertama dengan kolom yang dipilih. Unduhan tersedia dalam format Excel (.xlsx) atau PDF (.pdf), dengan baris dan kolom sesuai filter aktif.
   g. Kolom NIP/NIK dan Nomor Rekening ditampilkan penuh tanpa penyamaran (masking) bagi peran yang berhak, sesuai poin 6.
   h. Unduhan laporan kustom oleh Bendahara, PPTK, PA/KPA, atau Verifikator tidak menghasilkan entri Jejak Audit, sesuai aturan poin 5.
   i. Halaman penyusunan laporan kustom berupa halaman sendiri, bukan pop-up (§15 poin 7).


---

#### Dokumen 02 §6

## 6. BKU, koreksi, dan pencabutan berjenjang
BKU menandai penyelesaian pembukuan oleh Bendahara dan mengubah komitmen menjadi realisasi kas.

1. **Koreksi tanpa pencabutan:** Bendahara dapat mengoreksi No. BKU atau tanggal BKU tanpa mencabut BKU, selama nominal tidak berubah. Sistem mengecek keunikan No. BKU. Setiap koreksi tercatat di Jejak Audit dengan nilai lama dan nilai baru.
2. **Pencabutan berjenjang:** Untuk mencabut BKU yang salah, urutan yang terkunci adalah:
   1. Bendahara mencabut BKU; pencabutan tercatat di Jejak Audit.
   2. Verifikator mengembalikan SPJ menjadi Draft dengan catatan.
   3. Seksi melepas SPJ dari kuitansi.
   4. Seksi membatalkan kuitansi.
   5. Sistem memulihkan komitmen/saldo SPD terkait.
3. **Pembatalan tanpa jejak mutlak:** Pembatalan kuitansi atau SPJ Draft benar-benar dihapus tuntas dari sistem tanpa meninggalkan jejak. Seluruh entri Jejak Audit yang terkait kuitansi atau SPJ tersebut, termasuk riwayat pencatatan, koreksi, dan pencabutan BKU, ikut terhapus bersih secara otomatis oleh sistem bersama data kuitansi atau SPJ. Tidak ada rekaman pembatalan yang tersisa di audit trail.

#### Dokumen 01 §15

## 15. PENCARIAN, FILTER, DAN POP-UP (ATURAN UMUM ANTARMUKA)

1. **Daftar yang memakai pencarian dan filter:** Kuitansi, SPJ, BKU, Jejak Audit, Subkegiatan, Rekening Belanja, Personel, Akun, Akun Pengawas/Auditor, Direktori Rekening Bank, dan Direktori Transaksional SPJ. Daftar ini tumbuh seiring data TA dan master.
2. **Daftar tanpa pencarian:** Master SOTK dan Jenis Pajak. Datanya kecil dan jarang berubah sehingga cukup ditampilkan penuh.
3. **Pencarian:** satu kotak yang menyaring hasil langsung saat diketik. Pencarian mencocokkan kode, nama, nomor BKU, dan uraian sesuai daftar. Pencarian hanya bersifat membaca dan tidak mengubah data.
4. **Filter per daftar:** hanya field yang dipakai untuk memilah. Kuitansi dan SPJ: status, seksi, periode, dan jenis belanja. BKU: seksi, periode, dan status. Subkegiatan dan Rekening Belanja: status. Personel dan Akun: status akun dan peran. Filter dapat dikombinasikan dan dihapus sekaligus dengan satu tombol reset.
5. **Batas cakupan data:** pencarian dan filter hanya bekerja dalam cakupan data peran pengguna, sesuai Dokumen 05. Hasil di luar cakupan tidak pernah ditampilkan, termasuk melalui pencarian langsung.
6. **Pop-up untuk aksi singkat:** aksi yang muat tanpa scroll dalam sekitar empat field, dan semua konfirmasi yang tidak dapat dibatalkan, dibuka dalam pop-up. Contoh: tambah atau ubah unit kerja, tambah entri pajak, nonaktifkan akun dengan alasan, reset password, dan pencabutan BKU dengan konfirmasi.
7. **Halaman sendiri untuk isian panjang:** buat kuitansi, buat atau lengkapi SPJ, Form Dinamis, Visual Live Editor, dasbor, dan seluruh laporan. Aturan praktisnya: jika form muat di layar tanpa scroll, gunakan pop-up; jika tidak, gunakan halaman.
8. **Jejak audit tidak berubah:** aksi yang dilakukan melalui pop-up tetap dicatat sesuai aturan jejak audit yang berlaku untuk aksi tersebut, tanpa jalur tercatat yang berbeda.

#### Dokumen 03 §4

## 4. PPTK / Seksi
1. Melihat seksi dan subkegiatan yang ditetapkan untuknya pada TA.
2. Setelah alokasi Bendahara tersedia, membagi pagu subkegiatan ke rekening belanja hingga total rekening sama persis dengan pagu subkegiatan. Satu rekening belanja dapat dialokasikan di lebih dari satu subkegiatan milik seksinya; setiap pasangan dialokasikan terpisah dan pasangan yang sama tidak boleh ganda.
3. Menyelesaikan alokasi sesuai tenggat. Jika satu seksi belum seimbang, pembuatan kuitansi ditahan untuk semua seksi.
4. Setelah gatekeeper terbuka, membuat kuitansi dengan memilih subkegiatan dan rekening, mengisi nominal bruto, uraian, penerima dan tanggal kuitansi.
5. Kuitansi mengikat saldo SPD sebagai komitmen. SPJ merupakan alur terpisah setelah kuitansi, sesuai aturan SPJ yang disepakati. Kuitansi Aktif dapat diedit atau dibatalkan sampai SPJ Draft dibuat pada status TA Aktif Penuh; pada Masa Transisi kuitansi Aktif hanya dapat dibatalkan, tidak diedit. Sejak SPJ Draft dibuat, kuitansi Terkunci. SPJ Draft dapat dilepas atau dibatalkan, dan kuitansinya kembali Aktif.
6. Seksi tidak boleh melakukan pergeseran anggaran.
7. Tidak melihat Pagu Induk instansi. Jejak Audit yang terlihat hanya entri milik seksinya sendiri.
8. Melihat drill-down anggaran hanya untuk seksinya: seksi → subkegiatan → rekening belanja.
9. Mengunduh laporan seksinya dalam PDF atau Excel (Dokumen 01 §9).
10. Mengisi Form Dinamis SPJ sesuai jenis belanja yang dipilih di awal SPJ. Jika form memiliki blok berulang, PPTK menambah entri sesuai jumlah item atau orang yang dicakup SPJ (Dokumen 01 §9 poin 9).

11. Mengisi pajak pada SPJ setelah isian SPJ disimpan: memilih jenis pajak dari Master Jenis Pajak, mengisi nominal secara manual, dan dapat menambah beberapa entri. Sistem tidak menghitung pajak secara otomatis dari tarif atau master. Satu-satunya perhitungan otomatis terkait pajak adalah Total Pajak, yaitu jumlah seluruh entri pajak, dan Jumlah yang dibayarkan, yaitu nilai bruto dikurangi Total Pajak. Sistem menolak penyimpanan jika Total Pajak melebihi nilai bruto kuitansi dan menampilkan pesan validasi yang menjelaskan batas tersebut (Dokumen 02 §5).
12. Mengunduh lampiran PDF SPJ seksinya (Dokumen 02 §9).
13. Mencetak Hasil Verifikasi SPJ dengan barcode untuk SPJ seksinya setelah SPJ disetujui Verifikator (Dokumen 02 §8).
14. Selama menjadi Plh./Plt. PPTK, menjalankan kewenangan PPTK untuk seksinya. Tidak memverifikasi SPJ yang ia ajukan atau kelola sendiri (Dokumen 01 §6 poin 9).

- Menyusun dan mengunduh laporan kustom untuk seksinya sendiri, dengan pilihan kolom sesuai Matriks Kolom yang Diizinkan per Peran (Dokumen 01 §9 poin 12).

#### Dokumen 03 §9

## 9. Pengunjung Publik (Anonim)
1. Pengunjung membuka halaman keterbukaan informasi tanpa login dan secara default melihat TA Aktif; TA terdahulu/arsip yang tersedia dapat dipilih.
2. Pengunjung membaca persentase realisasi berdasarkan BKU yang telah dibukukan, grafik distribusi status SPJ dalam bentuk cacah dan proporsi, serta peringkat seksi berdasarkan persentase realisasi.
3. Halaman dapat menampilkan donut/pie status SPJ, gauge atau busur realisasi, bar progres horizontal dan ticker ringkasan. Ticker, label, tooltip, dan tampilan fullscreen hanya menampilkan informasi yang telah diizinkan untuk publik.
4. Pengunjung dapat mengaktifkan fullscreen melalui kontrol halaman; tata letak menyesuaikan layar besar. Pintasan seperti F dapat didukung. F11 merupakan kendali browser/perangkat dan tidak dijamin oleh aplikasi.
5. Data agregat diperbarui di latar belakang setiap 15–30 menit. Pengunjung tetap anonim dan tidak memperoleh akses ke menu internal.
6. Tidak tersedia akses publik ke nominal rupiah, data sumber transaksi, kuitansi, lampiran, identitas penerima/personel, NIP/NIK, nomor rekening, akun, maupun jejak audit. Server hanya menyediakan agregat aman sebagaimana Dokumen 01 §10 dan Dokumen 04 §2.3, kecuali halaman keaslian SPJ pada poin 10 yang hanya memuat status, nama TA, nama seksi, dan tanggal verifikasi satu SPJ.
7. Tampilan portal publik memakai tema Treasury & Market Terminal (§1, Tema Visual Treasury) dengan token warna dan huruf yang sama dengan login dan Pro Mode: latar `#0B1120`, permukaan `#111827`, garis tepi `#1F2937`, huruf sans-serif untuk teks umum, dan angka monospace bertabel angka sejajar untuk persentase dan cacah. Amber dipakai untuk bar realisasi utama; teal untuk aksen sekunder dan tautan.
8. Di layar besar dan mode fullscreen, portal memakai kepadatan Pro Mode: ticker ringkasan di bagian atas, lalu donut status SPJ, gauge realisasi, dan bar peringkat seksi sesuai poin 2 dan 3. Huruf dibuat lebih besar agar terbaca dari jarak jauh. Di layar kecil, portal beralih ke mode standar satu kolom dengan kartu bertumpuk.
9. Setiap zona atau status pada portal publik wajib memakai ikon dan teks, tidak hanya warna, dan memenuhi kontras WCAG AA sebagaimana aturan Keterbacaan pada §1. Portal tidak menampilkan nominal rupiah, nomor, nama personel, atau lampiran sesuai poin 6, dan hanya menampilkan persentase, cacah, proporsi, serta peringkat seksi.
10. **Halaman terpisah:** Halaman keaslian SPJ (Dokumen 02 §8) adalah halaman publik terpisah dari portal ini. Halaman itu hanya memeriksa keaslian satu SPJ melalui token pada barcode, dengan batas tampilan mengikuti Dokumen 02 §8 poin 4. Portal ini tidak menampilkan data keaslian SPJ, dan halaman keaslian tidak menampilkan persentase, cacah, atau grafik.

#### Dokumen 04 §2.3

### 2.3 Proyeksi agregat publik (tanpa akses data sumber)
| Proyeksi konseptual | Data yang boleh disajikan | Aturan |
|---|---|---|
| Statistik Keterbukaan Publik per TA | ID/tahun TA, total cacah SPJ, cacah per kategori status, persentase per kategori, persentase realisasi BKU terhadap pagu, waktu pembaruan | Hasil agregasi dihitung di server. Tidak ada nominal pagu/realisasi/sisa atau baris transaksi dalam payload publik. TA Aktif menjadi default; TA historis hanya untuk workspace yang tersedia. |
| Peringkat Realisasi per Seksi | ID seksi TA, nama snapshot seksi, persentase realisasi BKU terhadap pagu seksi, urutan peringkat | Hanya nama seksi dan persentase yang keluar ke pengunjung. Seksi dengan denominator nol/tidak tersedia tidak diberi persentase buatan dan ditandai belum tersedia. |
| Status Keaslian SPJ (halaman keaslian, Dokumen 02 §8) | Status Berlaku atau Tidak berlaku, nama TA, nama seksi, dan tanggal verifikasi; hanya untuk satu token yang diperiksa | Pengecualian terbatas dari portal agregat. Tidak ada persentase, cacah, nominal, identitas, lampiran, atau jejak audit. Token tidak dikenal atau tidak berlaku menghasilkan respons seragam. Tidak ada daftar atau pencarian token. |

- Rumus persentase realisasi publik: total BKU dibukukan ÷ pagu yang berlaku pada TA/cakupan yang sama × 100%. Komitmen kuitansi belum dibukukan tidak dihitung sebagai realisasi. Kalkulasi dilakukan di server; nominal mentah tidak dipulangkan ke klien.
- Kategori cacah SPJ: Selesai/Dibukukan BKU, Dalam Verifikasi, Perlu Perbaikan, dan Draf/Persiapan PPTK. Kategori saling eksklusif dan satu SPJ hanya masuk satu kategori. Karena status Draft dapat berasal dari persiapan atau pengembalian, pembeda workflow perlu direpresentasikan eksplisit sebagai status/penanda agar agregat akurat.
- Grafik pie/donut, gauge/busur, progres horizontal, ticker, dan fullscreen hanya memakai agregat yang diizinkan. Tooltip maupun metadata chart tidak boleh menyertakan nominal atau detail sumber. Pembaruan agregat dilakukan setiap 15–30 menit.
- Skema fisik, nama tabel, materialized view, endpoint, dan strategi cache merupakan keputusan teknis implementasi; proyeksi di atas adalah batas kontrak data, bukan SQL final.
- Akses anonim hanya boleh membaca proyeksi ini, ditambah baris status keaslian SPJ di atas yang hanya dapat dibuka melalui token pada barcode. Endpoint publik tidak boleh menyediakan akses ke tabel transaksi, file lampiran, identitas, atau audit.

#### Dokumen 01 §10

## 10. PORTAL KETERBUKAAN INFORMASI PUBLIK (TANPA LOGIN)

1. **Akses dan cakupan:** AMANDA menyediakan halaman publik baca-saja yang dapat dibuka tanpa login. Pengunjung dapat memilih TA yang tersedia; TA Aktif menjadi pilihan awal, sedangkan TA terdahulu/arsip dapat dipilih sebagai histori.
2. **Batas data yang ditampilkan:** Portal keterbukaan hanya menampilkan persentase dan cacah berkas SPJ. Halaman keaslian SPJ (poin 10) dikecualikan dan hanya menampilkan status keaslian satu SPJ. Tidak menampilkan nominal rupiah dalam bentuk apa pun, termasuk pagu, realisasi rupiah, sisa, nilai kuitansi, atau nilai per seksi. Halaman juga tidak menampilkan data sumber transaksi, data penerima, rincian kuitansi/SPJ, lampiran, NIP/NIK, nomor rekening, akun, jejak audit, atau informasi pribadi lainnya.
3. **Realisasi agregat:** Persentase realisasi instansi dihitung di sisi server sebagai total nilai BKU (realisasi pengeluaran belanja yang sudah dibukukan) dibagi total pagu TA, dikali 100%. Persentase seksi dihitung dengan rumus yang sama pada cakupan seksi. Komitmen kuitansi yang belum dibukukan bukan realisasi untuk indikator publik ini. Jika denominator tidak tersedia atau nol, tampilkan indikator sebagai “Belum tersedia” dan bukan nilai tak terhingga/hasil yang menyesatkan. Angka rupiah mentah tidak dikirim ke browser.
4. **Progres SPJ:** Tampilkan total cacah SPJ beserta cacah dan proporsi untuk kategori: Selesai/Dibukukan BKU; Dalam Verifikasi; Perlu Perbaikan; dan Draf/Persiapan PPTK. Satu SPJ hanya dihitung pada satu kategori pada satu waktu. Status/kategori yang dipakai harus mengikuti workflow Dokumen 02 dan Dokumen 03; sistem perlu membedakan draf persiapan dari draf yang dikembalikan untuk perbaikan melalui status atau penanda alur, bukan menebak dari isi dokumen.
5. **Peringkat seksi:** Tampilkan seluruh seksi TA yang memenuhi cakupan data, diurutkan dari persentase realisasi tertinggi ke terendah. Tampilkan nama seksi dan persentase saja, tanpa pagu/realisasi nominal. Seksi tanpa denominator yang dapat dihitung ditampilkan sebagai “Belum tersedia” dan tidak diberi persentase buatan.
6. **Visualisasi dan layar penuh:** Halaman dapat menyajikan grafik donat/pie untuk distribusi status SPJ, gauge atau indikator busur untuk realisasi keseluruhan, bar progres horizontal untuk realisasi instansi/seksi, serta ticker ringkasan yang hanya memuat TA, persentase, cacah SPJ, dan nama seksi. Visualisasi bersifat informatif dan seluruh angka di dalam tooltip/label harus mengikuti batas data publik pada poin 2. Tersedia kontrol fullscreen dan tata letak responsif untuk layar besar/kiosk. Pintasan papan ketik boleh disediakan; F11 tetap mengikuti kendali browser/perangkat dan tidak dijamin dapat dikendalikan aplikasi.
7. **Pembaruan data:** Data agregat diperbarui berkala secara halus setiap 15–30 menit tanpa memuat ulang seluruh halaman. Waktu pembaruan terakhir dapat ditampilkan.
8. **Pemisahan akses dan keamanan:** Pengunjung publik pada portal keterbukaan adalah akses anonim baca-saja khusus agregat; halaman keaslian SPJ (poin 10) hanya membaca status satu SPJ melalui token. Server hanya mengembalikan field agregat yang diperlukan (persentase, cacah, label TA/seksi, kategori status, dan waktu pembaruan); tidak mengirimkan baris sumber/nominal mentah atau data pribadi. Batasan ini wajib ditegakkan pada layanan/server, bukan hanya dengan menyembunyikan elemen antarmuka. Pengujian kebocoran meliputi response jaringan dan akses langsung ke endpoint.
9. **Tampilan dan keterbacaan:** Portal publik mengikuti Tema Visual Treasury pada Dokumen 03 §1 dan §9 poin 7–9. Tampilan memakai kepadatan Pro Mode di layar besar dan mode standar di layar kecil. Setiap status atau zona wajib memakai ikon dan teks, tidak hanya warna, serta memenuhi kontras WCAG AA. Aturan ini tidak mengubah batas data pada poin 2 dan 8.


---
10. **Halaman terpisah:** Halaman keaslian SPJ (Dokumen 02 §8) adalah halaman publik terpisah dari portal ini. Halaman itu hanya memeriksa keaslian satu SPJ melalui token pada barcode, dengan batas tampilan mengikuti Dokumen 02 §8 poin 4 (status, nama TA, nama seksi, dan tanggal verifikasi). Portal ini tidak menampilkan data keaslian SPJ, dan halaman keaslian tidak menampilkan persentase, cacah, atau grafik.

## 4. Skenario uji Dokumen 05 untuk langkah ini (apa adanya)
Format Bagian-Nomor.

- **B-10d** (DSB-04): PPTK tidak dapat melihat Pagu Induk pada kartu TA. Verifikator dapat melihatnya dalam mode baca saja.
- **B-10k** (VER-02): Personel yang mengajukan atau mengelola SPJ sendiri, baik sebagai pejabat definitif maupun Plh./Plt. PPTK, tidak dapat memverifikasi SPJ tersebut; server menolak aksi ini meskipun dipanggil langsung.
- **D-19** (BKU-01): Kuitansi aktif mengurangi SPD bebas sebagai komitmen; BKU mengurangi/menandai realisasi kas.
- **F-28a** (BKU-01): Sistem menolak No. BKU yang sudah dipakai di TA yang sama.
- **F-28b** (BKU-01): Sistem menolak input BKU kedua untuk kuitansi yang sudah memiliki BKU.
- **F-28c** (BKU-01): No. BKU menerima input teks/angka manual dari Bendahara, dan sistem tidak memvalidasi urutan kronologis tanggal (misal Tanggal BKU mendahului atau menyusul Tanggal Kuitansi/SPJ tetap berhasil disimpan).
- **F-28d** (BKU-02): Modul BKU hanya mencatat realisasi belanja kuitansi dan tidak memuat formulir/alur penerimaan SP2D, saldo awal, atau pencatatan saldo kas riil.
- **F-30b** (VER-01): SPJ yang sudah dikirim ke Verifikator berstatus Terkunci. Pengembalian oleh Verifikator membuka kunci SPJ menjadi Draft, tetapi kuitansi terkait tetap Terkunci.
- **F-31** (VER-01): Pengembalian SPJ oleh Verifikator memerlukan catatan dan membuat status Draft, tetapi komitmen SPD tetap terkunci.
- **F-33** (BKU-04): Pencabutan BKU hanya berjalan melalui urutan pencabutan berjenjang; nomor BKU yang telah dicabut berstatus bebas kembali dan dapat dicatat pada transaksi kuitansi/SPJ lain di TA yang sama; SPD pulih setelah kuitansi dibatalkan sesuai alur.
- **F-33b** (BKU-03): Koreksi No. BKU atau tanggal BKU tanpa pencabutan hanya dapat dilakukan jika nominal tidak berubah, dan tercatat di Jejak Audit dengan nilai lama dan nilai baru.
- **F-33c** (BKU-04): Pencabutan BKU tercatat di Jejak Audit tanpa alasan tertulis.
- **Q-130** (VER-04): Cetak Hasil Verifikasi hanya tersedia untuk SPJ berstatus Menunggu BKU atau Dibukukan; SPJ Draft dan Terkunci ditolak.
- **Q-131** (VER-03, VER-04): PDF Hasil Verifikasi memuat barcode dan nomor verifikasi yang tercetak sebagai teks. Token tidak tercetak sebagai teks, dan nomor verifikasi tidak sama dengan token. Template dapat diubah melalui Visual Live Editor tanpa mengubah data sistem.
- **Q-131a** (VER-03): Saat SPJ disetujui kembali setelah dikembalikan, nomor verifikasi dan token baru dibuat; nomor dan token lama menampilkan Tidak berlaku. Pencetakan ulang selama token belum berganti memuat nomor verifikasi dan barcode yang sama.
- **Q-131b** (VER-04): Verifikator dapat mencetak Hasil Verifikasi untuk SPJ seluruh seksi; PPTK hanya untuk seksinya. Pencetakan oleh Admin, Bendahara, PA/KPA, Pengawas/Auditor, atau Publik ditolak di server, termasuk melalui URL langsung.
- **Q-131c** (TPL-04, VER-04): Admin dapat mengubah tata letak, label, teks statis, logo, dan gambar stempel Hasil Verifikasi SPJ melalui Visual Live Editor dengan preview cetak. Cetakan hanya memuat data sesuai Dokumen 02 §8 poin 2; data sistem tidak dapat diubah dari editor, dan Jumlah yang dibayarkan dan Total Pajak tercetak sebagai hasil perhitungan sistem sesuai 131e.
- **Q-131d** (TPL-04, VER-03): Nomor verifikasi dibuat otomatis saat SPJ disetujui, berurutan dalam TA, dan tidak dipakai ulang. Admin mengatur format nomor per TA; nomor yang sudah tercetak tidak berubah ketika format diganti. Peran selain Admin tidak dapat mengubah format, termasuk melalui URL langsung.
- **Q-131e** (VER-04): Total Pajak dihitung sistem sebagai jumlah seluruh entri pajak SPJ, dan Jumlah yang dibayarkan sebagai nilai bruto dikurangi Total Pajak. Tidak ada perhitungan otomatis lain pada lembar verifikasi.
- **Q-132** (VER-05): Halaman keaslian tanpa login hanya menampilkan status, nama TA, nama seksi, dan tanggal verifikasi. Respons server tidak memuat nominal, nama penerima, NIP/NIK, rekening, lampiran, atau jejak audit.
- **Q-133** (VER-03, VER-04, VER-05, BKU-04): Setelah SPJ dikembalikan menjadi Draft, cetakan lama menampilkan Tidak berlaku pada halaman keaslian. Pencabutan BKU saja tidak mengubah status: selama SPJ belum dikembalikan dan kuitansi belum dibatalkan, cetakan lama tetap menampilkan Berlaku dan SPJ dapat diteruskan ke input BKU ulang.
- **Q-134** (VER-05): Token keaslian yang tidak dikenal atau sudah tidak berlaku menghasilkan respons seragam tanpa membocorkan data.
- **R-142** (BKU-05): Daftar Kuitansi, SPJ, BKU, Jejak Audit, Subkegiatan, Rekening Belanja, Personel, Akun, Akun Pengawas/Auditor, Direktori Rekening Bank, dan Direktori Transaksional SPJ menampilkan kotak pencarian dan filter (Dokumen 01 §15 poin 1).
- **R-144** (BKU-05): Pencarian mencocokkan kode, nama, nomor BKU, atau uraian sesuai daftar. Hasil berubah saat pengguna mengetik dan pencarian tidak mengubah data.
- **R-145** (BKU-05): Filter Kuitansi dan SPJ menyediakan status, seksi, periode, dan jenis belanja; filter BKU menyediakan seksi, periode, dan status. Kombinasi filter menghasilkan irisan, dan tombol reset mengembalikan daftar penuh dalam cakupan.
- **R-149** (BKU-04): Setiap konfirmasi aksi yang tidak dapat dibatalkan, termasuk pencabutan BKU, memakai pop-up konfirmasi. Menutup pop-up tanpa konfirmasi tidak mengubah data.

Selesai bila SEMUA skenario yang tercantum di bagian 4 lulus.