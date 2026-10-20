## Dokumen Kebutuhan Data: Koperasi Mahasiswa Sejahtera (Kopma)

## 1. Latar belakang dan aktivitas organisasi
Koperasi Mahasiswa Sejahtera (Kopma) adalah unit usaha di lingkungan kampus yang menjual berbagai kebutuhan mahasiswa seperti alat tulis, makanan ringan, dan minuman. Selama ini pencatatan transaksi dilakukan secara konvensional menggunakan buku tulis dan spreadsheet, sehingga sering terjadi kendala seperti harga lama yang hilang, stok barang yang menjadi minus, serta kesulitan dalam memantau keaktifan anggota. Sistem basis data baru dirancang untuk mendigitalisasi proses pencatatan penjualan, pengelolaan stok gudang, dan layanan keanggotaan agar lebih akurat dan terpercaya.

## 2. Aktor dan proses bisnis (Tabel PB-xx)
Berdasarkan hasil wawancara dan narasi studi kasus Kopma, teridentifikasi 5 proses bisnis utama:   PB-01 (Mendaftarkan Anggota): Kasir mendaftarkan mahasiswa menjadi anggota dengan mencatat NIM, nama, program studi, dan nomor HP untuk memperoleh nomor anggota A-XXXX.   PB-02 (Mencatat Penjualan): Kasir mencatat transaksi penjualan barang kepada pembeli (anggota atau umum) dan mencetak nota.   PB-03 (Memesan Barang ke Pemasok): Petugas gudang membuat pesanan pembelian ketika stok suatu barang berada di bawah batas minimum.   PB-04 (Menerima Barang dari Pemasok): Petugas gudang menerima kedatangan barang beserta faktur, yang kemudian menambah jumlah stok barang di koperasi.   PB-05 (Menyusun Laporan Bulanan): Ketua koperasi menerima laporan omzet, barang terlaris, barang menipis, dan keaktifan anggota setiap awal bulan.

## 3. Dokumen sumber yang dianalisis
Dokumen Sumber: Nota Penjualan Koperasi Mahasiswa Sejahtera.   Pembedahan Elemen Data:Identitas Transaksi: Nomor Nota dan Tanggal-Jam.   Relasi Pihak Terkait: Kasir yang bertugas dan Data Anggota (jika ada).   Rincian Produk: Daftar barang, jumlah (qty), harga satuan, dan subtotal per baris.   Nilai Turunan (Dihitung): Jumlah total belanja, diskon anggota 5%, total akhir, uang tunai, dan kembalian.  

## 4. Entitas kandidat dan elemen data
Anggota: no_anggota, nim_anggota, nama_anggota, prodi_anggota, no_hp_anggota, status_anggota, tgl_daftar_anggota.   Barang: kode_barang, nama_barang, kategori_barang, harga_jual_barang, stok_barang, stok_min_barang.   Penjualan: no_nota_penjualan, tgl_penjualan, kode_petugas, no_anggota, bayar_penjualan.   Detail Penjualan: no_nota_penjualan, kode_barang, qty_detail_penjualan, harga_satuan_detail_penjualan.   Petugas: kode_petugas, nama_petugas, peran_petugas (kasir/gudang/ketua).   Pemasok: kode_pemasok, nama_pemasok, telepon_pemasok, alamat_pemasok.   Pembelian & Detail Pembelian: no_faktur_pembelian, tgl_pembelian, kode_pemasok, kode_barang, qty_detail_pembelian, harga_beli_detail_pembelian, status_pembelian. 

## 5. Aturan bisnis (Tabel AB-xx)
AB-01: Setiap nota penjualan memiliki nomor unik dan memuat minimal satu baris barang.   AB-02: Penjualan dapat dilakukan tanpa data anggota (pembeli umum); jika menggunakan keanggotaan, status anggota harus aktif untuk mendapatkan diskon 5%.   AB-03: Stok barang di sistem tidak boleh bernilai negatif; transaksi penjualan akan ditolak jika qty melebihi stok yang tersedia.   AB-04: Harga jual produk pada saat transaksi dicatat per baris detail nota dan bersifat tetap meskipun harga dasar barang di katalog mengalami kenaikan di kemudian hari.   AB-05: Nomor identitas mahasiswa (NIM) bersifat unik, dan pencarian anggota dapat dilakukan melalui nomor anggota atau NIM.   AB-06: Pemesanan pembelian ke pemasok baru akan dilakukan apabila stok barang fisik di gudang berada di bawah batas minimum. 

## 6. Kebutuhan informasi (Tabel KI-xx)
KI-01: Laporan omzet dan jumlah nota transaksi per hari serta per bulan.   KI-02: Laporan 5 jenis barang terlaris per bulan berdasarkan total kuantitas (qty) terjual.   KI-03: Laporan daftar barang yang memiliki stok di bawah batas minimum (stok_min_barang).   KI-04: Laporan 10 anggota paling aktif dengan total nominal belanja terbesar per bulan. 

## 7. Matriks CRUD

| Proses Bisnis | Anggota | Barang | Penjualan | Detail Penjualan | Pemasok | Pembelian |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **PB-01 (Mendaftarkan Anggota)** | C | - | - | - | - | - |
| **PB-02 (Mencatat Penjualan)** | R | R, U | C | C | - | - |
| **PB-03 (Pesan ke Pemasok)** | - | R | - | - | R | C |
| **PB-04 (Terima Barang)** | - | U | - | - | U | U |
| **PB-05 (Laporan Bulanan)** | R | R | R | R | - | R |

## 8. Kamus data awal

| No | Elemen Data | Arti | Contoh Nilai | Aturan / Format | Penanggung Jawab |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | `no_anggota` | Nomor keanggotaan koperasi | A-0457 | Unik, format A-4 digit | Ketua |
| 2 | `nim_anggota` | Nomor induk mahasiswa | 2301010123 | Unik, 10 digit | Ketua |
| 3 | `nama_anggota` | Nama lengkap anggota | Siti Aminah | Teks, Wajib isi | Ketua |
| 4 | `prodi_anggota` | Program studi anggota | Sistem Informasi | Teks, Wajib isi | Ketua |
| 5 | `no_hp_anggota` | Nomor HP/WhatsApp anggota | 081234567890 | Data pribadi, akses terbatas | Ketua |
| 6 | `status_anggota` | Status keaktifan anggota | Aktif | ENUM ('Aktif','Non-Aktif') | Ketua |
| 7 | `kode_barang` | Kode unik jenis barang | BRG-ATK-01 | Unik, Format tetap | Petugas Gudang |
| 8 | `nama_barang` | Nama barang dagangan | Buku Tulis Sinar Dunia | Teks, Wajib isi | Petugas Gudang |
| 9 | `kategori_barang` | Kelompok jenis barang | Alat Tulis | Teks, Wajib isi | Petugas Gudang |
| 10 | `harga_jual_barang` | Harga jual barang ke pembeli | 4000.00 | Bilangan desimal >= 0 (Rupiah) | Petugas Gudang |
| 11 | `stok_barang` | Jumlah ketersediaan barang | 35 | Bilangan bulat >= 0 (AB-03) | Petugas Gudang |
| 12 | `stok_min_barang` | Batas minimum stok barang | 5 | Bilangan bulat >= 0, Default 5 | Petugas Gudang |
| 13 | `no_nota_penjualan` | Nomor unik lembar nota kasir | PJ-2610-0142 | Unik per nota | Kasir |
| 14 | `tgl_penjualan` | Waktu transaksi penjualan | 2026-10-20 09:15:00 | Format DATETIME | Kasir |
| 15 | `kode_petugas` | Identitas petugas yang melayani | PTG-02 | Unik, Relasi ke tabel petugas | Ketua |
| 16 | `bayar_penjualan` | Jumlah uang tunai dari pembeli | 50000.00 | Bilangan desimal >= total belanja | Kasir |
| 17 | `qty_detail_penjualan` | Jumlah barang dibeli per baris | 3 | Bilangan bulat > 0 | Kasir |
| 18 | `harga_satuan_detail_penjualan`| Harga barang saat transaksi | 4000.00 | Bilangan desimal >= 0 (AB-04) | Kasir |
| 19 | `kode_pemasok` | Identitas unik pemasok barang | SUP-01 | Unik, Relasi ke tabel pemasok | Petugas Gudang |
| 20 | `nama_pemasok` | Nama perusahaan pemasok | PT Berkah Stationery | Teks, Wajib isi | Petugas Gudang |
| 21 | `no_faktur_pembelian` | Nomor faktur dari pemasok | FK-2026-8891 | Unik per faktur pembelian | Petugas Gudang |
| 22 | `tgl_pembelian` | Tanggal barang masuk dari pemasok | 2026-10-18 | Format DATE | Petugas Gudang |

## 9. Kebutuhan non-fungsional data
Volume Transaksi: Perkiraan volume transaksi harian di koperasi mencapai $pm 150$ nota per hari.   Retensi Data: Arsip data transaksi penjualan wajib disimpan minimal selama 5 tahun.   Privasi Data: Kolom data pribadi anggota (seperti nomor telepon/HP) dikategorikan sebagai informasi sensitif dan hanya memiliki hak akses terbatas bagi ketua koperasi guna mematuhi Undang-Undang Pelindungan Data Pribadi (UU PDP). 

## 10. Isu kualitas data yang diantisipasi
Potensi kesalahan ejaan nama anggota atau duplikasi data NIM akibat pendaftaran ganda secara manual.

Ketidakkonsistenan penulisan nama pemasok atau kategori barang pada catatan dokumen lama.