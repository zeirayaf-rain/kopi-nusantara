=====================================================================
 KOPI NUSANTARA - Website Promosi dan Pemesanan Produk Kopi Lokal
 Proyek Uji Kompetensi Junior Programmer
=====================================================================

DESKRIPSI
---------
Website coffeeshop "Kopi Nusantara" untuk menampilkan produk kopi kemasan
dan minuman siap saji, lengkap dengan pemesanan online dan panel admin
(CRUD) untuk mengelola produk, kategori, pelanggan, dan transaksi.

TEKNOLOGI
---------
- PHP 8+ (PDO), MySQL/MariaDB (phpMyAdmin)
- HTML5, CSS3, JavaScript (vanilla)
- Library front-end: Bootstrap 5, Bootstrap Icons, Animate.css (via CDN)

STRUKTUR FOLDER
---------------
kopi-nusantara/
|-- index.php            Halaman Beranda (hero, slider produk, statistik, video YouTube)
|-- produk.php           Halaman Produk (filter kategori)
|-- tentang.php          Halaman Tentang Kami
|-- kontak.php           Halaman Kontak (form dengan validasi)
|-- pesan.php            Form pemesanan + kalkulasi total + cek status pesanan
|-- database.sql         Skema dan data awal database
|-- README.txt           Dokumentasi ini
|-- config/
|   `-- koneksi.php      Konfigurasi dan koneksi database (PDO)
|-- includes/
|   |-- functions.php    Fungsi bantu (escape, rupiah, flash, CSRF, dll.)
|   |-- header.php       Navbar halaman publik
|   |-- kartu_pesanan.php Komponen kartu status pesanan
|   |-- footer.php       Footer halaman publik
|   `-- kartu_produk.php Komponen kartu produk
|-- admin/               Panel admin (wajib login)
|   |-- login.php, logout.php, _auth.php, _header.php, _footer.php
|   |-- index.php        Dashboard ringkasan
|   |-- produk.php       Daftar + hapus produk
|   |-- produk_form.php  Tambah / ubah produk (dengan unggah gambar)
|   |-- kategori.php     CRUD kategori
|   |-- pelanggan.php    Lihat / ubah / hapus pelanggan
|   `-- pesanan.php      Lihat transaksi, ubah status, hapus
`-- assets/
    |-- css/style.css    Seluruh gaya tampilan
    |-- js/main.js       Animasi, hitung total, validasi form
    `-- img/             Gambar produk (SVG) dan foto galeri; img/uploads untuk unggahan

CARA MENJALANKAN
----------------
1. Pasang XAMPP / Laragon (PHP 8+ dan MySQL), lalu aktifkan Apache dan MySQL.
2. Salin folder "kopi-nusantara" ke folder web server:
     XAMPP   -> C:\xampp\htdocs\kopi-nusantara
     Laragon -> C:\laragon\www\kopi-nusantara
3. Buka phpMyAdmin (http://localhost/phpmyadmin), pilih tab "Import",
   pilih file database.sql, lalu klik "Go/Kirim".
   (Database "kopi_nusantara" akan dibuat otomatis.)
4. Bila user/password MySQL Anda berbeda, ubah di config/koneksi.php.
5. Buka di browser:
     Website : http://localhost/kopi-nusantara/
     Admin   : http://localhost/kopi-nusantara/admin/login.php

AKUN ADMIN
----------
Username : admin
Password : admin123
(Segera ganti password pada tabel "admin" jika dipakai sungguhan.)

ALUR CRUD ADMIN (sesuai soal)
-----------------------------
1. Admin login.
2. Pilih menu Produk.
3. Klik "Tambah Produk", isi data "Kopi Toraja" -> Simpan   (Create)
4. Produk tampil di daftar produk                            (Read)
5. Klik "Ubah" untuk mengganti harga atau stok               (Update)
6. Klik "Hapus" bila produk sudah tidak dijual               (Delete)
Menu Kategori, Pelanggan, dan Transaksi juga memakai operasi serupa.

FITUR UTAMA
-----------
- Desain responsif (Bootstrap grid) dan navigasi mudah.
- Slider produk (carousel), animasi muncul saat scroll, animasi hitung
  angka, tombol kembali ke atas, video profil.
- Form pemesanan: validasi nama, telepon, alamat, produk, jumlah (JavaScript
  dan PHP); total harga dihitung otomatis; stok berkurang saat pesanan masuk.
- Keamanan dasar: prepared statement (anti SQL injection), htmlspecialchars
  (anti XSS), token CSRF, password_hash, validasi tipe file unggahan.

PEMESANAN TANPA AKUN DAN CEK STATUS
-----------------------------------
- Pemesan TIDAK perlu daftar atau login. Klik "Pesan" / "Pesan Sekarang / Cek Pesanan" (satu tombol di navbar)
  langsung masuk ke form pemesanan (pesan.php).
- Di halaman yang sama (bagian "Status Pesanan Anda", #status) pemesan melihat status tiap pesanan (Baru, Diproses,
  Dikirim, Selesai, atau Batal) beserta progresnya.
- Cara kerja: tiap pesanan punya kode_lacak acak di database dan peramban
  pemesan mengingatnya lewat cookie, sehingga pesanan tampil otomatis di
  perangkat yang sama (data pemesan juga terisi otomatis).
- Dari HP/perangkat lain: isi nomor pesanan + nomor telepon di kotak
  "Pesan dari HP atau perangkat lain?" (dibatasi 5 percobaan salah,
  lalu ditahan 5 menit).
- Notifikasi: saat admin mengubah status di admin/pesanan.php, kotak
  notifikasi singkat muncul di kiri bawah sampai status dilihat di
  halaman Pesan.
- Database lama (sudah diimport): jalankan migrasi_tanpa_akun.sql SEKALI.
  Database baru: cukup import database.sql.
- Catatan: bila cookie dihapus, pelanggan cukup memakai kotak cek di atas.

GALERI, ASAL KOPI, DAN ULASAN
-----------------------------
- Navbar: Beranda, Produk, Tentang Kami, Kontak, Pesan Sekarang / Cek Pesanan.
- Galeri ada di Tentang Kami (#galeri) dan cuplikannya di Beranda.
- Asal Kopi dan Ulasan Kopi ada di halaman Produk (#asal, #ulasan).
- Testimoni pelanggan bergerak otomatis di Beranda.
- Foto memakai file lokal di assets/img/galeri/ (kopi-1.jpg ... kopi-13.jpg).
  Daftarnya ada di daftarGaleri() dan daftarAsal() (includes/functions.php).
  Ganti foto dengan menimpa file bernama sama (disarankan lebar min. 1200 px).
  Kode foto tanpa ekstensi tetap didukung: angka = Pexels, lainnya = Unsplash.
- Data ulasan: daftarUlasan() dan daftarTestimoni() (contoh/demo).

MEDIA SOSIAL DAN PETA
---------------------
- Ikon Instagram, TikTok, Facebook, dan X muncul di footer, Beranda, dan
  halaman Kontak. Ganti URL akun di konstanta SOSMED pada
  includes/functions.php (cukup satu tempat).
- Peta di halaman Kontak adalah contoh (Bogor). Ganti alamat pada atribut
  src iframe di kontak.php dengan lokasi kedai Anda.

CATATAN
-------
- Library Bootstrap/Animate.css dimuat dari CDN sehingga perlu internet.
- Video profil di Beranda memakai YouTube Shorts (ID ECYhisX_GnY) lewat iframe
  di index.php. Ganti ID pada atribut src iframe bila ingin video lain.
- Agar unggah gambar berfungsi, folder assets/img/uploads harus dapat ditulis.
- Validasi kode: gunakan https://validator.w3.org (HTML) dan
  https://jigsaw.w3.org/css-validator (CSS) pada hasil render halaman.
