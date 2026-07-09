![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Core Fundamentals](https://img.shields.io/badge/Fokus-Anatomi_Sistem-purple?style=for-the-badge)

# 📂 Membedah Jantung Hati: Anatomi htdocs dan Control Panel

Sebuah kesalahan paling umum dan lucu yang dilakukan oleh 99% *programmer* pemula adalah: Mereka menulis kode PHP di *Notepad*, menyimpan filenya di folder **Desktop** atau **My Documents**, lalu bingung mengapa halaman tersebut tidak bisa diakses saat mereka mengetik `http://localhost` di *browser*.

XAMPP memiliki aturan wilayah teritorial yang sangat ketat. Di bab ini, kita akan membedah logika di balik struktur folder XAMPP menggunakan analogi, dan membongkar fitur-fitur tersembunyi di dalam *Control Panel*-nya.

## 📋 Daftar Isi
- [Gedung Perkantoran Bernama XAMPP](#-gedung-perkantoran-bernama-xampp)
- [Misteri Ruang Pameran "htdocs"](#-misteri-ruang-pameran-htdocs)
- [Praktik: Membuka Kedai Kopi Pertama Anda](#-praktik-membuka-kedai-kopi-pertama-anda)
- [Harta Karun Tersembunyi di Control Panel](#-harta-karun-tersembunyi-di-control-panel)

---

## 🏢 Gedung Perkantoran Bernama XAMPP

Mari kita bayangkan folder `C:\xampp` di laptop Anda sebagai sebuah **Gedung Perkantoran Raksasa**. Di dalam gedung ini, terdapat banyak ruangan dan staf yang bekerja secara harmoni:

1. **Apache:** Resepsionis utama gedung. Dia berdiri di Pintu Gerbang (Port 80/8080) bertugas menerima tamu (peramban/browser web) yang datang berkunjung.
2. **PHP:** Pekerja pabrik di ruang bawah tanah. Dia bertugas merakit data mentah menjadi halaman web HTML yang utuh.
3. **MySQL (MariaDB):** Ruang arsip dan brankas raksasa di mana semua data perusahaan (akun *user*, artikel, *password*) disimpan rapat-rapat (Port 3306).

Jika Anda secara acak meletakkan *file* kode Anda di *Desktop*, sang Resepsionis (Apache) tidak akan pernah bisa menemukannya, karena *Desktop* berada di luar yurisdiksi gedung perkantoran ini!

---

## 🖼️ Misteri Ruang Pameran "htdocs"

Di dalam gedung `C:\xampp` tersebut, terdapat sebuah ruangan suci bernama **`htdocs`** (singkatan dari *HyperText Documents*). 

Dalam analogi kita, `htdocs` adalah **Ruang Pameran (Etalase) Publik**. 
Apapun, saya ulangi, *apapun* yang Anda letakkan di dalam folder `htdocs`, akan bisa dilihat dan diakses oleh Resepsionis (Apache) untuk ditunjukkan kepada peramban (*browser*).

Oleh karena itu, setiap kali Anda ingin membuat proyek *website* baru, Anda **WAJIB** membangunnya di dalam ruang pameran ini.

---

## ☕ Praktik: Membuka Kedai Kopi Pertama Anda

Mari kita buktikan hukum alam semesta XAMPP ini:

1. Buka *File Explorer* Anda, lalu masuk ke kandang suci: **`C:\xampp\htdocs`**.
2. Buat sebuah folder baru di sana, beri nama: **`kedai-kopi`**.
3. Masuk ke dalam folder `kedai-kopi` tersebut.
4. Buat sebuah *file* baru bernama **`index.php`**. *(Mengapa index? Karena Apache didesain untuk selalu mencari dokumen bernama 'index' sebagai menu utama saat ia masuk ke sebuah ruangan).*
5. Buka `index.php` tersebut dengan *Notepad* atau VS Code, lalu ketik kode berikut:

```php
<?php
  echo "<h1>Selamat Datang di Kedai Kopi Lokal!</h1>";
  echo "<p>Kopi ini diseduh langsung dari dalam folder htdocs.</p>";
?>
```
6. Simpan *file* tersebut.
7. Pastikan Apache di XAMPP Control Panel sedang menyala (*Start*).
8. Buka *browser* Anda, dan ketik: **`http://localhost:8080/kedai-kopi/`** *(Gunakan 8080 jika Anda telah mengikuti bab sebelumnya, atau cukup localhost jika Anda menggunakan Port default).*

**BOM! 🤯**
Teks HTML Anda akan dirender dengan sempurna di layar peramban. Sang Resepsionis (Apache) berhasil menemukan kedai kopi Anda di dalam ruang pameran.

---

## 🧰 Harta Karun Tersembunyi di Control Panel

Banyak *developer* hanya menggunakan *Control Panel* XAMPP untuk mengklik tombol *Start* dan *Stop* lalu membiarkannya tenggelam. 
Kenyataannya, panel ini dirancang sebagai Pusat Komando (*Command Center*) yang sangat kuat:

1. **Tombol "Explorer":** Berada di baris tombol sebelah kanan. Mengeklik ini akan langsung membawa Anda masuk ke dalam folder `C:\xampp` secara magis tanpa harus membuka *My Computer* secara manual.
2. **Tombol "Netstat":** Radar canggih milik XAMPP. Jika Apache menolak menyala, klik *Netstat*. Anda akan melihat daftar semua aplikasi (Skype, IIS, Zoom) lengkap beserta nomor Port yang sedang mereka bajak. Ini adalah senjata utama seorang detektif *server*.
3. **Tombol "Logs":** Di sebelah setiap tombol *Start*, ada tombol *Logs*. Jika PHP atau Apache tiba-tiba memberikan halaman putih (*White Screen of Death*), klik *Logs* > *Apache (error.log)*. Semua pesan penderitaan dan sumber *error* akan tercatat rapi di *file* teks tersebut.

Di bab selanjutnya (Level 2), kita akan melangkah maju meninggalkan *Notepad* dan mulai merakit arsitektur *Database* layaknya seorang profesional menggunakan phpMyAdmin. Bersiaplah untuk menambang data! 💎📊
