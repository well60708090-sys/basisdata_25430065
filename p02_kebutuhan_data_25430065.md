# Dokumen Kebutuhan Data: Toko Daring Berkah 65

## 1. Latar belakang dan aktivitas organisasi
Toko Daring Berkah 65 adalah platform e-commerce berbasis web yang melayani pelanggan dalam mencari, memesan, dan membeli berbagai produk kebutuhan sehari-hari secara online...

## 2. Aktor dan proses bisnis (Tabel PB-xx)
PB-01 (Mendaftarkan Akun Pelanggan): Pelanggan baru mendaftarkan diri dengan mengisi data nama, email, nomor telepon, dan alamat pengiriman.

PB-02 (Mengelola Katalog Produk): Admin atau petugas gudang menambah, memperbarui informasi, atau mengubah stok produk yang dijual.

PB-03 (Melakukan Pemesanan / Checkout): Pelanggan memilih produk, memasukkannya ke keranjang, membuat pesanan (order), dan memilih metode pembayaran.

PB-04 (Memproses Pengiriman Pesanan): Petugas gudang memvalidasi pembayaran yang masuk, menyiapkan barang, dan mencatat nomor resi pengiriman melalui kurir.

PB-05 (Menyusun Laporan Penjualan Bulanan): Pemilik toko menerima rekapitulasi omzet, produk terlaris, serta status transaksi secara berkala setiap awal bulan.

## 3. Dokumen sumber yang dianalisis
**Dokumen Sumber:** Nota Pesanan / Invoice Digital E-Commerce.

**Pembedahan Elemen Data:**
***Identitas Transaksi:** Nomor Pesanan, Tanggal dan Jam Pemesanan.
***Relasi Pihak Terkait:** Data Pelanggan (Nama, Alamat) dan Petugas/Admin yang memproses.
***Rincian Produk:** Daftar produk, jumlah (qty), dan harga satuan produk saat transaksi.
***Nilai Turunan (Dihitung):** Subtotal, total biaya, ongkos kirim, dan total akhir.

## 4. Entitas kandidat dan elemen dataPelanggan: id_pelanggan, nama_pelanggan, email, telepon_pelanggan, alamat_pelanggan.Kategori Produk: id_kategori, nama_kategori.Produk: id_produk, kode_produk, nama_produk, id_kategori, harga_jual_produk, stok_produk, stok_min_produk.Pesanan (Order): id_pesanan, no_pesanan, tgl_pesanan, id_pelanggan, status_pesanan.Detail Pesanan: id_pesanan, id_produk, qty_detail_pesanan, harga_satuan_detail_pesanan.   Pembayaran: id_pembayaran, id_pesanan, tgl_pembayaran, metode_pembayaran, jumlah_bayar.Pengiriman: id_pengiriman, id_pesanan, kurir, no_resi, biaya_ongkir.

## 5. Aturan bisnis (Tabel AB-xx)AB-01: Setiap pesanan memiliki nomor pesanan yang unik dan memuat minimal satu baris produk.   AB-02: Pelanggan wajib memiliki akun terdaftar dan berstatus aktif untuk melakukan proses checkout pesanan.AB-03: Stok produk tidak boleh bernilai negatif; sistem akan menolak transaksi jika jumlah produk yang diminta melebihi stok yang tersedia.   AB-04: Harga produk yang tercatat pada detail pesanan disimpan secara mandiri per baris transaksi dan tidak berubah meskipun harga katalog produk tersebut naik di kemudian hari.   AB-05: Email pelanggan bersifat unik; satu alamat email hanya dapat digunakan untuk mendaftarkan satu akun pelanggan.   AB-06: Berdasarkan parameter $P = 3$, batas maksimal ragam item barang yang dapat dibeli dalam satu transaksi adalah $P + 2 = 5$ jenis barang berbeda.AB-07: Status pesanan harus melalui tahapan baku: Pending (menunggu bayar), Dibayar (diproses gudang), Dikirim (dalam pengiriman), hingga Selesai.

## 6. Kebutuhan informasi (Tabel KI-xx)KI-01: Laporan omzet dan jumlah total pesanan harian serta bulanan.   KI-02: Laporan 5 produk terlaris berdasarkan total kuantitas (qty) terjual per bulan.   KI-03: Daftar produk yang memiliki jumlah stok di bawah batas minimum (stok_min_produk).   KI-04: Daftar 10 pelanggan dengan total nilai nominal belanja terbesar per bulan.   KI-05: Rekapitulasi status pengiriman pesanan yang belum dikirim oleh bagian gudang.

## 7. Matriks CRUD

| Proses Bisnis | Pelanggan | Kategori | Produk | Pesanan | Detail Pesanan | Pembayaran | Pengiriman |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| PB-01 (Daftar Pelanggan) | C | - | - | - | - | - | - |
| PB-02 (Kelola Katalog) | - | C, U | C, U | - | - | - | - |
| PB-03 (Pesan/Checkout) | R | - | R, U | C | C | C | - |
| PB-04 (Proses Pengiriman) | - | - | - | U | - | - | C, U |
| PB-05 (Laporan Bulanan) | R | R | R | R | R | R | R |

## 8. Kamus data awal

| No | Elemen Data | Arti | Contoh Nilai | Aturan / Format | Penanggung Jawab |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `id_pelanggan` | Identitas unik pelanggan | 1 | Bilangan bulat > 0, Unik, Auto Increment | Admin Toko |
| 2 | `nama_pelanggan` | Nama lengkap pelanggan | Budi Santoso | Teks, Wajib isi (NOT NULL) | Pelanggan |
| 3 | `email` | Alamat email pelanggan | budi@example.com | Teks, Unik, Format email valid | Pemilik Toko |
| 4 | `telepon_pelanggan` | Nomor telepon/HP pelanggan | 081234567890 | Teks, 10–13 digit angka, Data pribadi | Admin Toko |
| 5 | `alamat_pelanggan` | Alamat lengkap pengiriman | Jl. Merdeka No. 10, Metro | Teks, Data pribadi | Admin Toko |
| 6 | `id_kategori` | Identitas unik kategori produk | 1 | Bilangan bulat > 0, Unik | Admin Toko |
| 7 | `nama_kategori` | Nama kelompok produk | Pakaian Pria | Teks, Wajib isi | Admin Toko |
| 8 | `id_produk` | Identitas unik produk | 101 | Bilangan bulat > 0, Unik | Petugas Gudang |
| 9 | `kode_produk` | Kode barang di katalog | PRD-ELK-001 | Teks, Unik, Format tetap | Petugas Gudang |
| 10 | `nama_produk` | Nama barang yang dijual | Kemeja Polos Hitam L | Teks, Wajib isi | Petugas Gudang |
| 11 | `harga_jual_produk` | Harga jual produk saat ini | 75000.00 | Bilangan desimal >= 0 (Rupiah) | Admin Toko |
| 12 | `stok_produk` | Jumlah stok barang tersedia | 50 | Bilangan bulat >= 0 (AB-03) | Petugas Gudang |
| 13 | `stok_min_produk` | Batas minimum stok barang | 5 | Bilangan bulat >= 0, Default 5 | Petugas Gudang |
| 14 | `id_pesanan` | Identitas unik transaksi pesanan | 5001 | Bilangan bulat > 0, Unik | Admin Toko |
| 15 | `no_pesanan` | Nomor nota transaksi | ORD-2610-0065 | Teks, Unik per nota (AB-01) | Admin Toko |
| 16 | `tgl_pesanan` | Waktu transaksi dilakukan | 2026-10-20 14:30:00 | Format DATETIME | Admin Toko |
| 17 | `status_pesanan` | Tahapan proses pesanan | Dibayar | ENUM ('Pending','Dibayar','Dikirim','Selesai') | Admin Toko |
| 18 | `qty_detail_pesanan` | Jumlah produk dibeli per baris | 2 | Bilangan bulat > 0, Maksimal P+2 (AB-06) | Admin Toko |
| 19 | `harga_satuan_detail_pesanan` | Harga produk saat dibeli | 75000.00 | Bilangan desimal >= 0, Tidak berubah (AB-04) | Admin Toko |
| 20 | `metode_pembayaran` | Cara pembayaran yang dipilih | Transfer Bank | ENUM ('Transfer Bank','E-Wallet','COD') | Pemilik Toko |
| 21 | `no_resi` | Nomor resi pelacakan kurir | JNT-98237412 | Teks, Boleh Kosong (NULL) sebelum dikirim | Petugas Gudang |
| 22 | `biaya_ongkir` | Tarif ongkos kirim pesanan | 15000.00 | Bilangan desimal >= 0 | Petugas Gudang |

## 9. Kebutuhan non-fungsional dataVolume Transaksi: Berdasarkan parameter $P = 3$, perkiraan volume transaksi harian adalah $40 + 5 \times 3 = 55$ transaksi per hari.   Retensi Data: Seluruh data transaksi historis disimpan sekurang-kurangnya selama 5 tahun.   Privasi Data: Data pribadi pelanggan (seperti email, nomor telepon, dan alamat lengkap) dikategorikan sebagai data privat sesuai dengan Undang-Undang Pelindungan Data Pribadi (UU PDP) dan hanya dapat diakses oleh pihak yang berwenang. 

## 10. Isu kualitas data yang diantisipasi
Potensi kesalahan penulisan alamat email atau nomor telepon yang tidak aktif dari pelanggan saat pendaftaran.

Risiko duplikasi akun pelanggan akibat pendaftaran berulang dengan nama yang mirip.

Kesalahan input nominal angka pada proses pencatatan pembayaran manual.