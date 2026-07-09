![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Database Security](https://img.shields.io/badge/Fokus-Keamanan_Data-purple?style=for-the-badge)

# 🛡️ Ksatria Penjaga Gerbang: Mengamankan phpMyAdmin & MySQL

Sadar atau tidak, sejak pertama kali Anda menginstal XAMPP, Anda telah melakukan sebuah dosa keamanan (*Security Flaw*) terbesar di dunia pemrograman.

Secara bawaan (*default*), konfigurasi MySQL di XAMPP menggunakan *username* **`root`** dan **TIDAK MEMILIKI KATA SANDI** (kosong).

Banyak *developer* pemula yang mengabaikan hal ini karena merasa *"Ah, ini kan cuma di laptop lokal saya, tidak mungkin ada yang meretas."* 

Padahal, jika Anda sedang berada di WiFi kafe publik dan pengaturan *Firewall* Windows Anda longgar, *hacker* iseng di meja sebelah bisa masuk ke `http://ip-anda/phpmyadmin` dan mencuri atau menghapus seluruh *database* proyek Anda. 
Selain itu, terbiasa membiarkan *password* kosong akan menciptakan "kebiasaan buruk" saat Anda nantinya bekerja di *server production* sesungguhnya.

Di bab ini, kita akan menempa zirah pelindung dan memasang gembok baja di pintu brankas harta karun Anda!

## 📋 Daftar Isi
- [Tahap 1: Memasang Gembok di Brankas MySQL](#-tahap-1-memasang-gembok-di-brankas-mysql)
- [Tragedi Kiamat "Access Denied"](#-tragedi-kiamat-access-denied)
- [Tahap 2: Menyelaraskan Kunci phpMyAdmin](#-tahap-2-menyelaraskan-kunci-phpmyadmin)
- [Level Pakar: Membangkitkan Layar Login](#-pro-tip-level-pakar-membangkitkan-layar-login)

---

## 🔐 Tahap 1: Memasang Gembok di Brankas MySQL

Mari kita kunci pintu utamanya terlebih dahulu:

1. Buka peramban (*browser*) Anda dan masuk ke: **`http://localhost/phpmyadmin`** (atau `localhost:8080` jika Anda sudah mengikuti tutorial Port sebelumnya).
2. Di baris menu paling atas, klik menu **User accounts** (Akun Pengguna).
3. Anda akan melihat sebuah daftar pengguna. Cari baris yang memiliki **User name: `root`** dan **Host name: `localhost`**.
4. Di baris tersebut, klik tautan teks **Edit privileges** (Edit hak akses).
5. Di halaman selanjutnya, pada deretan tombol abu-abu di atas, klik **Change password** (Ubah kata sandi).
6. Ketikkan kata sandi baja Anda (Misalnya: `rahasia123`). Ketik ulang di kolom konfirmasi.
7. Klik tombol **Go** di pojok kanan bawah.

Selesai! Anda baru saja mengganti kode brankas MySQL Anda. 
Tapi tunggu, perhatikan apa yang terjadi saat Anda mencoba me-*refresh* (memuat ulang) halaman phpMyAdmin tersebut.

---

## 🚨 Tragedi Kiamat "Access Denied"

**BOM! Layar merah penderitaan! 🤯**
Anda tiba-tiba ditendang keluar dan peramban Anda dipenuhi oleh pesan *error* merah mengerikan:
> *"Cannot connect: invalid settings. Access denied for user 'root'@'localhost'."*

Jangan panik! Ini sangat logis.
**phpMyAdmin** sebenarnya hanyalah sebuah "Aplikasi Web Biasa" berbasis PHP yang tugasnya membaca isi *database* MySQL. 

Sejak diinstal, aplikasi phpMyAdmin diprogram untuk selalu menggunakan kunci kosong saat mengetuk pintu MySQL. Karena Anda baru saja mengganti gembok MySQL di Tahap 1, aplikasi phpMyAdmin terbentur pintu dan ditolak masuk.

Tugas kita sekarang adalah memberikan anak kunci yang baru kepada phpMyAdmin.

---

## 🔑 Tahap 2: Menyelaraskan Kunci phpMyAdmin

Kita harus melakukan operasi kecil pada *file* konfigurasi inti milik phpMyAdmin:

1. Buka *File Explorer* Anda dan masuk ke kandang XAMPP: **`C:\xampp\phpMyAdmin`**.
2. Cari *file* bernama **`config.inc.php`**. Klik kanan dan *Open with Notepad* (atau Teks Editor favorit Anda).
3. Cari baris kode (sekitar baris 21) yang berbunyi seperti ini:
   ```php
   $cfg['Servers'][$i]['password'] = '';
   ```
4. Masukkan kata sandi baja Anda ke dalam tanda kutip kosong tersebut, sehingga menjadi:
   ```php
   $cfg['Servers'][$i]['password'] = 'rahasia123';
   ```
5. Simpan *file* tersebut (`CTRL + S`) dan tutup Notepad.
6. Kembali ke *browser*, dan *Refresh* halaman phpMyAdmin Anda.

Sihir kiamat merah tadi lenyap, dan Anda bisa kembali melihat brankas *database* Anda dengan tenang. 
Kini, XAMPP Anda kebal dari serangan intip WiFi publik!

---

## 🛡️ PRO TIP: Level Pakar (Membangkitkan Layar Login)

Bahkan setelah diberi *password*, phpMyAdmin masih terasa kurang aman karena ia otomatis *login* ke layar utama (*Bypass*) tanpa pernah meminta Anda mengetik *password* di peramban.

Jika Anda ingin keamanan sekelas *Server Production*, Anda bisa membangkitkan sebuah **Layar Login** rahasia.

1. Buka kembali *file* **`config.inc.php`** yang tadi.
2. Tepat di atas baris *password* tadi, cari kode ini:
   ```php
   $cfg['Servers'][$i]['auth_type'] = 'config';
   ```
3. Ubah kata `config` menjadi `cookie`:
   ```php
   $cfg['Servers'][$i]['auth_type'] = 'cookie';
   ```
4. *(Opsional)* Jika Anda menggunakan metode `cookie`, Anda bisa membiarkan baris `password` kosong (`''`).
5. Simpan *file* dan buka kembali phpMyAdmin di *browser*.

**Aha!** 
Anda kini diadang oleh sebuah halaman form *Login* bergaya elegan. Tidak ada satupun manusia yang bisa melihat isi *database* Anda sebelum mereka memasukkan *Username* (`root`) dan *Password* (`rahasia123`) Anda. 

Anda baru saja naik pangkat dari *Programmer* biasa menjadi seorang **Administrator Sistem (SysAdmin)** yang andal! Selamat! 🎖️🔐
