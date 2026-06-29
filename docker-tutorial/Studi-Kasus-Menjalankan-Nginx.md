![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Hands-on: Terminal](https://img.shields.io/badge/Praktik-Terminal-critical?style=for-the-badge)

# ☕ Studi Kasus: Membangun Kedai Kopi Digital (Web Server Nginx)

Selamat datang kembali di galangan kapal, Kapten!

Banyak pemula menyerah belajar Docker karena langsung dihantam oleh pusaran teori yang rumit dan tanpa hasil yang terlihat. Di mahakarya ini, kita akan mendobrak tradisi tersebut. Kita akan memadukan konsep inti dan praktik langsung dengan satu misi visual yang epik: **Meluncurkan Kedai Kopi Digital (Web Server) Anda sendiri dalam waktu kurang dari 5 menit.**

Siapkan cangkir Anda, mari kita mulai!

## 📋 Daftar Isi
- [Filosofi Kedai Kopi (Image vs Container)](#-filosofi-kedai-kopi-image-vs-container)
- [Misi Praktik: Menahkodai Container Pertama](#-misi-praktik-menahkodai-container-pertama)
  - [1. docker run: Menyeduh Kopi](#1-docker-run-menyeduh-kopi)
  - [2. docker ps: Mengecek Radar Kapal](#2-docker-ps-mengecek-radar-kapal)
  - [3. docker exec: Masuk ke Dalam Kedai Kopi](#3-docker-exec-masuk-ke-dalam-kedai-kopi)
  - [4. docker stop: Menutup Kedai](#4-docker-stop-menutup-kedai)
  - [5. docker rm: Membongkar Bangunan Kedai](#5-docker-rm-membongkar-bangunan-kedai)
- [Kesimpulan Misi](#-kesimpulan-misi)

---

## 🏗️ Filosofi Kedai Kopi (Image vs Container)

Sebelum mengetik satu baris kode pun, mari kita luruskan kembali dua kosakata paling suci di dunia Docker: *Image* dan *Container*. Lupakan definisi buku teks yang membingungkan. 

Bayangkan Anda ingin membuka sebuah kedai kopi (*Web Server*).

- **Docker Image = Buku Resep & Cetak Biru**
  Buku resep berisi daftar bahan (kopi, gula, susu) dan instruksi presisi cara membuatnya. Buku resep itu sendiri *tidak bisa diminum*. Di Docker, Image adalah paket statis (tak berubah) yang berisi kode aplikasi, OS mini, dan semua pengaturan bawaan.

- **Docker Container = Secangkir Kopi Fisik**
  Ketika Anda menggunakan buku resep tersebut untuk benar-benar menyeduh kopi, Anda mendapatkan secangkir kopi yang siap dinikmati. Di Docker, Container adalah wujud nyata dan hidup dari Image yang sedang beroperasi.

> 💡 **THE WOW FACTOR:**
> Dari satu "Buku Resep" (Image) Nginx yang sama, Anda bisa menyeduh 1, 10, atau 10.000 "Cangkir Kopi" (Container) yang 100% identik di server mana pun di seluruh dunia secara bersamaan!

---

## 🚢 Misi Praktik: Menahkodai Container Pertama

Sekarang, mari kita ubah teori menjadi tindakan. Kita akan "meminjam" resep Web Server Nginx (*baca: engine-ex*) resmi dari Docker Hub dan langsung menyeduhnya.

Buka Terminal (Mac/Linux) atau Command Prompt / PowerShell (Windows) Anda. Pastikan layanan Docker Desktop sudah aktif.

### 1. `docker run`: Menyeduh Kopi

Perintah ini adalah mantra paling ajaib di Docker. Ia bertugas mencari Image, mengunduhnya jika belum ada di laptop Anda, dan langsung menjalankannya sebagai Container dalam hitungan detik.

Ketik perintah berikut secara utuh:

```bash
# -d : Menjalankan container di background (Detached), agar terminal Anda tidak macet.
# --name : Memberikan nama keren (kedai-kopi-digital) untuk container kita.
# -p 8080:80 : Meneruskan jalur. Traffic Port 8080 di laptop -> disalurkan ke Port 80 di container.
# nginx:alpine : Nama Image (Resep) yang kita gunakan. Alpine adalah versi super ringan.

docker run -d --name kedai-kopi-digital -p 8080:80 nginx:alpine
```

Tunggu beberapa detik. Docker akan mengunduh resepnya dan langsung membuka kedai kopi Anda.

**Buktikan sendiri:** Buka *browser* (Chrome/Safari) Anda dan ketik URL ini: `http://localhost:8080`.
Jika Anda melihat tulisan *"Welcome to nginx!"*, selamat! Anda baru saja meluncurkan Web Server Docker pertama Anda! 🎉

### 2. `docker ps`: Mengecek Radar Kapal

Bagaimana kita tahu pasti apa yang sedang berjalan di *background*? Gunakan perintah `ps` (Process Status).

```bash
# Menampilkan semua container yang SEDANG BERJALAN saat ini
docker ps
```

Anda akan melihat tabel rapi berisi `CONTAINER ID`, `IMAGE`, `STATUS`, dan `NAMES` (yang akan tertulis `kedai-kopi-digital`).

### 3. `docker exec`: Masuk ke Dalam Kedai Kopi

Ini adalah trik rahasia para *Senior DevOps*. Saat ini, Web Server Anda hanya menampilkan halaman default Nginx yang membosankan. Bagaimana jika kita ingin mengganti teksnya tanpa mematikan server? Kita harus "meretas masuk" ke dalam container yang sedang berjalan!

```bash
# -it : Interactive Terminal (agar kita bisa berinteraksi di dalam container)
# sh : Membuka program shell (semacam terminal bawaan Linux) di dalam container Alpine
docker exec -it kedai-kopi-digital sh
```

**Boom!** Tanda `$` di terminal Anda berubah. Secara virtual, Anda sekarang secara fisik berada di *dalam* container Nginx tersebut. 

Mari kita sulap halaman depannya secara *real-time* dengan perintah Linux sederhana ini:

```bash
# Mengganti isi file index.html bawaan Nginx dengan kalimat sambutan buatan kita sendiri
echo "<h1>Selamat Datang di Kedai Kopi Digital Kapten! ☕🚀</h1>" > /usr/share/nginx/html/index.html

# Keluar dari dalam container dan kembali ke sistem laptop utama kita
exit
```

Sekarang, kembali ke *browser* Anda dan tekan **Refresh (F5)** di halaman `http://localhost:8080`. 

Halamannya berubah seketika! ✨ Inilah kekuatan isolasi dan modifikasi *real-time* yang membuat Docker sangat dicintai oleh para *developer*.

### 4. `docker stop`: Menutup Kedai

Sudah larut malam, waktunya menutup kedai tanpa menghancurkan bangunannya.

```bash
# Menghentikan container yang sedang berjalan secara halus
docker stop kedai-kopi-digital
```

Coba *refresh* browser Anda. Halaman web pasti akan mati (Error/Site can't be reached). Jika Anda mengetik `docker ps`, container tersebut juga akan menghilang dari radar.

> 💡 **PRO TIP:**
> Container tersebut sebenarnya tidak hilang, hanya "tertidur". Untuk melihat semua container, termasuk yang sedang mati/stop, gunakan perintah `docker ps -a` (All).

### 5. `docker rm`: Membongkar Bangunan Kedai

Jika Anda ingin meratakan bangunan kedai ini dengan tanah dan menghapusnya selamanya dari *hardisk* Anda:

```bash
# Menghapus container secara permanen 
# Syarat: Container harus dalam keadaan STOP sebelum bisa dihapus secara normal
docker rm kedai-kopi-digital
```

> ⚠️ **PERINGATAN KRUSIAL:**
> Perintah `rm` (Remove) bersifat permanen. Segala perubahan yang Anda lakukan di dalam container (seperti saat kita mengubah teks HTML tadi) akan musnah tanpa sisa! Inilah sebabnya di *Level 2* nanti, kita wajib belajar tentang **Docker Volume** untuk menyelamatkan data permanen Anda.

---

## 🎯 Kesimpulan Misi

Luar biasa! Dalam satu sesi studi kasus yang singkat namun padat ini, Anda telah berhasil:

1. Memahami perbedaan mendasar dan nyata antara **Image** (Resep) dan **Container** (Kopi).
2. Menjalankan *Web Server Nginx* pertama Anda menggunakan `docker run`.
3. Memantau aktivitas radar container dengan `docker ps`.
4. Meretas masuk dan mengubah isi halaman HTML secara *live* menggunakan `docker exec`.
5. Membersihkan *environment* PC Anda dengan anggun menggunakan `docker stop` dan `docker rm`.

Anda baru saja mempraktikkan alur kerja harian para *Engineer* top dunia. Tarik napas sejenak, regangkan otot Anda, dan bersiaplah untuk membangun infrastruktur yang jauh lebih masif di level selanjutnya!
