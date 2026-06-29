![Difficulty: Advanced](https://img.shields.io/badge/Tingkat-Mahir-red?style=for-the-badge)
![Time: 5 Mins](https://img.shields.io/badge/Durasi-5_Menit-blue?style=for-the-badge)
![Killer Feature](https://img.shields.io/badge/Fitur-Quick_App-critical?style=for-the-badge)

# ⚡ Mantra Kilat: Meluncurkan WordPress & Laravel dalam 60 Detik

Selamat datang di puncak Level 3, Sang Penyihir!

Mari kita ingat kembali bagaimana rutinitas kita di masa lalu saat ingin memulai sebuah proyek **WordPress** yang baru. Anda harus melakukan "ritual" yang panjang dan membosankan:

1. Pergi ke *wordpress.org* dan mengunduh *file* `.zip`.
2. Mengekstrak *file* tersebut ke folder `htdocs`.
3. Mengubah nama folder.
4. Membuka phpMyAdmin yang lambat.
5. Membuat sebuah *database* baru secara manual.
6. Membuka *browser* ke `localhost/folder_baru`.
7. Mengisi *form database name*, *username*, *password*, dll.

Sebuah proses 7 langkah yang bisa memakan waktu hingga 15 menit. 
Di bab ini, Laragon akan memangkas ke-7 langkah tersebut menjadi **satu klik kanan** dan mengeksekusinya dalam waktu kurang dari 60 detik.

## 📋 Daftar Isi
- [Mengenal Tongkat Ajaib: Quick App](#-mengenal-tongkat-ajaib-quick-app)
- [Praktik: Menyihir WordPress Pertama Anda](#-praktik-menyihir-wordpress-pertama-anda)
- [Bukan Hanya WordPress: Ekosistem Laravel](#-bukan-hanya-wordpress-ekosistem-laravel)

---

## 🪄 Mengenal Tongkat Ajaib: Quick App

Laragon memiliki sebuah senjata rahasia bernama **Quick App** (Aplikasi Cepat). Ini adalah *script* otomatisasi tingkat dewa.

Fitur ini didesain khusus untuk para *developer* yang menghargai waktu. Daripada melakukan proses pengunduhan dan instalasi *database* secara manual, *Quick App* memerintahkan Laragon untuk bertindak layaknya seorang asisten pribadi (*DevOps*). 

Asisten ini akan mengunduh inti aplikasi, membedahnya, dan merakitnya untuk Anda dalam hitungan detik.

---

## 🚀 Praktik: Menyihir WordPress Pertama Anda

Pastikan laptop Anda terhubung ke internet. Mari kita panggil asisten gaib ini:

1. Buka aplikasi Laragon Anda (pastikan Apache dan MySQL sedang berjalan).
2. **Klik Kanan** di area putih yang kosong.
3. Arahkan *mouse* ke menu **Quick app**, lalu pilih **WordPress**.
4. Sebuah jendela kecil akan muncul (Terminal). Ia akan meminta satu pertanyaan sederhana: **"Project Name:"** (Nama proyek).
5. Ketik nama proyek Anda, misalnya: `toko-buku` lalu tekan **Enter**.

**BOOM! 🤯 Lepaskan tangan Anda dari keyboard dan saksikan sihirnya.**

Dalam hitungan detik, Laragon akan:
- Secara diam-diam mengunduh *file* WordPress inti (versi terbaru) langsung dari *server* pusat.
- Mengekstraknya ke folder `C:\laragon\www\toko-buku`.
- Terhubung ke MySQL Anda dan otomatis membuatkan *database* kosong bernama `toko-buku`.
- Meracik *file* konfigurasi `wp-config.php` dan menyambungkannya dengan *database* tersebut tanpa campur tangan Anda.
- Membuatkan *domain* cantik `http://toko-buku.test`.

Begitu proses di Terminal selesai, Laragon akan langsung membukakan *browser* Anda menuju `http://toko-buku.test`. Yang perlu Anda lakukan hanyalah mengisi Judul Website dan Password Admin.

Selesai. Sebuah mahakarya efisiensi waktu yang mutlak.

---

## 💎 Bukan Hanya WordPress: Ekosistem Laravel

Keajaiban *Quick App* ini tidak terbatas pada WordPress. Jika Anda adalah seorang *developer* PHP modern, Anda pasti sering membuat proyek **Laravel**.

Proses instalasi Laravel melalui terminal (`composer create-project...`) sering kali menakutkan bagi pemula. Di Laragon, sihirnya sama persis:

1. **Klik Kanan** di Laragon.
2. Masuk ke **Quick app**, pilih **Laravel**.
3. Ketik nama proyek (misal: `aplikasi-kasir`).
4. Tekan **Enter**.

Seketika, Laragon akan memerintahkan *Composer* (*Package Manager* bawaan Laragon) untuk merakit proyek Laravel terbaru, membangkitkan `APP_KEY`, dan membuatkan *database* bernama `aplikasi_kasir` secara otomatis. 

Saat proses selesai, kunjungi **`http://aplikasi-kasir.test`** dan halaman *Welcome* Laravel yang ikonik sudah menyapa Anda.

---

## 🏆 Epilog Level 3

*(Catatan: Materi tentang berbagi Web Lokal menggunakan Ngrok [telah kita selesaikan secara epik di bab sebelumnya!])*

Dengan dikuasainya sihir **Quick App** (bersamaan dengan integrasi **Ngrok** yang memukau klien Anda di belahan dunia lain), Anda kini telah resmi mencapai derajat **The Sorcerer** di dunia Laragon.

Anda tidak lagi membuang waktu 15 menit untuk konfigurasi dasar. Anda mendelegasikan tugas-tugas kotor tersebut kepada mesin, agar otak Anda bisa berfokus penuh pada hal yang benar-benar penting: **Membangun kode dan merangkai karya seni yang hebat.** 🎩✨
