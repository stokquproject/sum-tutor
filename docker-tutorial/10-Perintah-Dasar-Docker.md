![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Hands-on: Terminal](https://img.shields.io/badge/Praktik-Terminal-critical?style=for-the-badge)

# 🕹️ 10 Perintah Kemudi: Mengendalikan Container Layaknya Kapten Kapal

Sekarang Anda sudah mengerti perbedaan antara resep dan kue. Instalasi pun sudah selesai. Ini saatnya memakai topi kapten Anda, berdiri di depan kemudi (*Terminal/Command Prompt*), dan mulai melayarkan kapal-kapal kontainer Anda!

Meski Docker punya puluhan perintah, 80% dari pekerjaan sehari-hari Anda hanya akan berkutat pada 10 perintah magis ini. Mari kita pelajari tidak hanya sekadar *bagaimana* mengetiknya, tapi juga rahasia kecil (*Pro Tips*) yang membedakan pemula dari seorang profesional.

## 📋 Daftar Isi
- [1. docker run (Menciptakan & Menyalakan)](#1-docker-run-menciptakan--menyalakan)
- [2. docker ps (Mengecek Radar)](#2-docker-ps-mengecek-radar)
- [3. docker stop (Melabuhkan Kapal)](#3-docker-stop-melabuhkan-kapal)
- [4. docker start (Berlayar Kembali)](#4-docker-start-berlayar-kembali)
- [5. docker rm (Menghancurkan Kapal Tua)](#5-docker-rm-menghancurkan-kapal-tua)
- [6. docker images (Melihat Koleksi Cetak Biru)](#6-docker-images-melihat-koleksi-cetak-biru)
- [7. docker rmi (Membakar Cetak Biru)](#7-docker-rmi-membakar-cetak-biru)
- [8. docker logs (Membaca Jurnal Kapal)](#8-docker-logs-membaca-jurnal-kapal)
- [9. docker exec (Menyusup ke Dalam Kapal)](#9-docker-exec-menyusup-ke-dalam-kapal)
- [⭐ Ekstra: Mengenal Docker Hub (Supermarket Cetak Biru)](#-ekstra-mengenal-docker-hub-supermarket-cetak-biru)
- [10. docker pull (Mengambil Cetak Biru Baru)](#10-docker-pull-mengambil-cetak-biru-baru)

---

## 1. `docker run` (Menciptakan & Menyalakan)
Ini adalah perintah yang paling sering Anda gunakan. Tugasnya adalah mengambil Image (cetak biru), membuat Container (bangunan fisik), dan langsung menyalakannya dalam satu tarikan napas.

```bash
# Contoh: Menjalankan web server Nginx
# -d : (Detach) Biarkan berjalan diam-diam di background (tidak memblokir terminal)
# --name : Memberi nama kapal yang cantik, alih-alih nama acak yang membingungkan
# -p 8080:80 : Menyambungkan port komputer kita (8080) ke dalam container (80)
docker run -d --name web-pertamaku -p 8080:80 nginx:latest
```

## 2. `docker ps` (Mengecek Radar)
Bagaimana kita tahu kapal apa saja yang sedang berlayar? Gunakan perintah radar ini.

```bash
# Menampilkan container yang SEDANG BERJALAN saat ini
docker ps

# PRO TIP: Tambahkan flag -a (all) untuk melihat SEMUA container, 
# termasuk yang sudah mati/berhenti. Ini sangat berguna untuk mencari container yang crash!
docker ps -a
```

## 3. `docker stop` (Melabuhkan Kapal)
Jika Anda ingin mematikan mesin kapal secara halus (memberi waktu bagi aplikasi untuk menyimpan data sebelum mati).

```bash
# Anda bisa menggunakan nama container atau Container ID (cukup 3-4 digit pertama)
docker stop web-pertamaku
```

## 4. `docker start` (Berlayar Kembali)
Container yang sudah di-`stop` tidak hancur, ia hanya tertidur. Bangunkan kembali dengan perintah ini.

```bash
# Menyalakan kembali container yang sedang tertidur
docker start web-pertamaku
```

## 5. `docker rm` (Menghancurkan Kapal Tua)
Jika Container sudah tidak terpakai, hancurkan agar tidak memenuhi ruang *hardisk* Anda layaknya rongsokan kapal.

```bash
# Menghapus container (Pastikan container sudah di-stop terlebih dahulu!)
docker rm web-pertamaku

# PRO TIP: Ingin menghapus paksa container yang masih menyala? Gunakan -f (force)
# Bagaikan menembakkan torpedo langsung ke kapal yang sedang berlayar!
docker rm -f web-pertamaku
```

## 6. `docker images` (Melihat Koleksi Cetak Biru)
Melihat daftar "Resep" atau "Cetak Biru" yang sudah Anda unduh ke komputer lokal.

```bash
# Menampilkan daftar Docker Image, versi (TAG), dan ukurannya
docker images
```

## 7. `docker rmi` (Membakar Cetak Biru)
Menghapus Image yang sudah tidak digunakan. Image seringkali berukuran besar (ratusan MB), jadi rajin-rajinlah membersihkannya.

```bash
# RMI = Remove Image. Menghapus image Nginx versi terbaru
docker rmi nginx:latest
```

> ⚠️ **PERINGATAN:**
> Anda tidak bisa menghapus sebuah Image jika masih ada Container (baik yang hidup maupun mati) yang menggunakan Image tersebut. Hancurkan dulu Container-nya dengan `docker rm`, baru hapus Image-nya.

## 8. `docker logs` (Membaca Jurnal Kapal)
Saat aplikasi di dalam Container mengalami *error*, bagaimana cara melihat pesan *error*-nya jika ia berjalan diam-diam di *background*?

```bash
# Membaca log dari awal sampai akhir
docker logs web-pertamaku

# PRO TIP: Tambahkan -f (follow) agar log terus ter-update secara live di layar Anda.
# Sangat krusial untuk proses debugging! (Tekan Ctrl+C untuk keluar)
docker logs -f web-pertamaku
```

## 9. `docker exec` (Menyusup ke Dalam Kapal)
Ini adalah trik favorit para *hacker* (dan *System Administrator*). Bagaimana jika Anda ingin masuk ke sistem operasi di DALAM Container yang sedang menyala dan menjalankan perintah di sana?

```bash
# -i : (Interactive) Tetap buka saluran input
# -t : (TTY) Alokasikan pseudo-TTY agar terlihat seperti terminal asli
# sh / bash : Program shell yang ingin dijalankan di dalam container
docker exec -it web-pertamaku bash
```
Bagus! Setelah mengetikkan itu, Anda secara harfiah sudah berada di *dalam* sistem Container tersebut. (Ketik `exit` untuk kembali ke komputer Anda).

---

## ⭐ Ekstra: Mengenal Docker Hub (Supermarket Cetak Biru)
Sebelum kita masuk ke perintah terakhir, Anda harus tahu dari mana asal-muasal semua "Cetak Biru" (Image) ini. Jawabannya adalah **Docker Hub** (hub.docker.com).

Docker Hub adalah raksasa supermarket global tempat jutaan Image resmi (dari vendor seperti Ubuntu, MySQL, Nginx) maupun Image komunitas disimpan. Saat Anda butuh software apa pun, langkah pertama selalu sama: cari di Docker Hub!

```bash
# Anda bahkan bisa mencari ketersediaan image langsung dari terminal!
# Perintah ini akan menampilkan daftar image yang berkaitan dengan 'wordpress'
docker search wordpress
```

## 10. `docker pull` (Mengambil Cetak Biru Baru)
Bagaimana jika Anda hanya ingin mengunduh Image dari Docker Hub untuk disimpan, tapi tidak ingin langsung menjalankannya menjadi Container?

```bash
# Mengunduh image database PostgreSQL versi 15
docker pull postgres:15
```

---

> 💡 **PRO TIP PAMUNGKAS:** 
> Merasa *hardisk* penuh karena terlalu banyak Container rongsokan dan Image yang tidak terpakai? Jalankan perintah sapu jagat ini:
> ```bash
> docker system prune -a
> ```
> Perintah ini akan membersihkan SEMUA Container yang mati, jaringan yang tak terpakai, dan Image yang menggantung. Sebuah tombol *refresh* yang sangat melegakan!

Luar biasa, Kapten! Anda baru saja menguasai 10 kemudi utama. Dengan perintah-perintah ini, Anda sudah bisa mengoperasikan 90% dari kebutuhan *containerization* harian. 

Di level selanjutnya, kita akan belajar menghubungkan kapal-kapal ini menjadi sebuah armada yang canggih! 🚢
