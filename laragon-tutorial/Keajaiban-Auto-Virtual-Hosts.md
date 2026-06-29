![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 5 Mins](https://img.shields.io/badge/Durasi-5_Menit-blue?style=for-the-badge)
![Core Feature](https://img.shields.io/badge/Fitur-Auto_Virtual_Hosts-purple?style=for-the-badge)

# 🪄 Sihir Tanpa Mantra: Keajaiban Auto-Virtual Hosts (.test)

Mari kita bernostalgia sejenak ke masa lalu yang suram.

Dulu, saat Anda sedang mengerjakan proyek *website*, Anda mengaksesnya melalui *URL* yang sangat tidak elegan: `http://localhost/folder-proyek-saya/public`. Terlihat sangat amatir, bukan? 

Anda ingin *website* lokal Anda terlihat profesional, misalnya menjadi **`http://tokoku.test`**. Namun untuk melakukan itu di aplikasi lawas (seperti XAMPP), Anda harus melakukan ritual gaib yang menyiksa.

Di bab ini, Anda akan menyaksikan mengapa jutaan *developer* berpindah ke Laragon hanya karena **satu fitur magis ini**.

## 📋 Daftar Isi
- [Cara Tradisional yang Menyiksa](#-cara-tradisional-yang-menyiksa)
- [Sihir Laragon: Tanpa Mantra, Tanpa Konfigurasi](#-sihir-laragon-tanpa-mantra-tanpa-konfigurasi)
- [Praktik Langsung: Membuktikan Sihir](#-praktik-langsung-membuktikan-sihir)
- [Mengganti Akhiran Domain (.local atau .dev)](#-pro-tip-mengganti-akhiran-domain-local-atau-dev)

---

## ⛓️ Cara Tradisional yang Menyiksa

Untuk membuat domain lokal cantik di XAMPP, inilah neraka konfigurasi yang harus Anda lalui:
1. Membuka folder *Apache* yang terkubur dalam.
2. Mengedit *file* keramat bernama `httpd-vhosts.conf` dengan kode konfigurasi XML yang membingungkan.
3. Mencari *file* `hosts` milik OS Windows yang disembunyikan mati-matian di `C:\Windows\System32\drivers\etc\hosts`.
4. Membuka Notepad sebagai *Administrator* (jika lupa, Anda tidak bisa *save*).
5. Mendaftarkan IP `127.0.0.1 tokoku.test` secara manual.
6. Me-*restart* Apache. 

Setiap kali Anda membuat proyek baru, Anda **HARUS** mengulangi siksaan 6 langkah di atas. 

Lupakan semua itu. Buang ilmu lama Anda sekarang juga.

---

## 🦄 Sihir Laragon: Tanpa Mantra, Tanpa Konfigurasi

Laragon memiliki fitur cerdas bernama **Auto-Virtual Hosts**. 

Laragon bertindak layaknya penyihir yang selalu memantau folder utama Anda (`C:\laragon\www`). Sistem kerjanya luar biasa sederhana:
> *"Apapun nama folder yang Anda buat di dalam direktori `www`, Laragon akan otomatis membuatkan domain `.test` untuk Anda pada detik itu juga."*

Tidak ada Notepad yang perlu dibuka. Tidak ada hak akses *Administrator* yang perlu diminta. Tidak ada *Apache* yang harus di-*restart* secara manual. Semuanya terjadi di belakang layar dalam hitungan milidetik.

---

## 🎩 Praktik Langsung: Membuktikan Sihir

Pegang kata-kata saya. Mari kita buktikan sihir ini secara langsung.

1. Buka aplikasi Laragon Anda, dan pastikan Anda sudah menekan tombol **"Start All"**.
2. Klik tombol **Root** di aplikasi Laragon. (Ini akan langsung membuka folder `C:\laragon\www`).
3. Di dalam folder tersebut, buatlah sebuah folder kosong baru. Beri nama: `kedai-kopi`.
4. Masuk ke dalam folder `kedai-kopi` tersebut, buat sebuah *file* teks biasa bernama `index.php`.
5. Buka `index.php` tersebut dan ketik kode sederhana ini:
   ```php
   <?php
   echo "<h1>Selamat datang di Kedai Kopi Magis!</h1>";
   ```
6. Buka peramban (*browser*) favorit Anda, seperti Chrome atau Firefox.
7. Di baris *URL* paling atas, ketik alamat ini: **`http://kedai-kopi.test`** lalu tekan *Enter*.

**BOM!** 🤯
Halaman Anda langsung terbuka. Tidak ada `localhost`, tidak ada *path* folder yang panjang. Anda memiliki *domain* cantik milik Anda sendiri hanya dengan membuat folder!

Setiap kali Anda membuat folder baru bernama `proyek-rahasia`, maka detik itu juga Anda memiliki domain `http://proyek-rahasia.test`. Ini adalah efisiensi tingkat dewa.

---

## 💡 PRO TIP: Mengganti Akhiran Domain (.local atau .dev)

Apakah Anda tidak menyukai akhiran `.test`? Apakah Anda lebih suka domain Anda terlihat seperti `http://tokoku.local` atau `http://tokoku.app`?

Sangat mudah. Laragon tidak memaksa Anda:
1. Klik kanan di mana saja pada area putih aplikasi Laragon.
2. Masuk ke menu: **Preferences** (ikon gerigi⚙️).
3. Di jendela yang muncul, perhatikan kotak bertuliskan **"Hostname format"**.
4. Secara default, isinya adalah: `{name}.test`
5. Ubah menjadi `{name}.local` atau ekstensi apapun yang Anda inginkan (Namun hindari `.dev` karena *Google Chrome* akan memaksa .dev untuk menggunakan HTTPS yang bisa sedikit merepotkan).
6. Tutup jendela, dan selamat menikmati *domain custom* pribadi Anda!

Di bab selanjutnya, kita akan membongkar fasilitas luar biasa lainnya dari Laragon: **Ngrok terintegrasi**, yang memungkinkan Anda memamerkan web lokal Anda ke klien di ujung dunia hanya dengan satu klik! 🌍
