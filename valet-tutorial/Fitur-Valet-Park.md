![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 5 Mins](https://img.shields.io/badge/Durasi-5_Menit-blue?style=for-the-badge)
![Workflow Speed](https://img.shields.io/badge/Fokus-Kecepatan_Workflow-purple?style=for-the-badge)

# 🅿️ Jurus Parkir Otomatis: Keajaiban valet park

Selamat datang di Level 2, Sang Ninja! 🥷

Bayangkan kembali masa-masa kelam Anda. Di XAMPP, setiap kali Anda ingin membuat *domain* baru untuk proyek baru, Anda harus membuka `httpd-vhosts.conf`, menulis konfigurasi, lalu men- *restart* Apache. 
Di Docker, Anda harus menyalin *file* `docker-compose.yml`, memanipulasi *port*, dan menunggu berhari-hari (oke, mungkin berjam-jam) hingga *image* selesai di- *build*.

Bagaimana jika saya katakan bahwa dengan Valet, menciptakan *Custom Domain* (seperti `http://proyekku.test`) kini semudah **"Klik Kanan > Buat Folder Baru"**? 

Tanpa membuka *file* konfigurasi. Tanpa me- *restart server*. Tanpa menunggu sebentar pun.
Mari kita pelajari jurus paling ikonik dari Valet: **Membangun Lahan Parkir**.

## 📋 Daftar Isi
- [Konsep Lahan Parkir (Parking Lot)](#-konsep-lahan-parkir-parking-lot)
- [Tahap 1: Membangun Lahan Parkir Anda](#-tahap-1-membangun-lahan-parkir-anda)
- [Tahap 2: Membuktikan Sihir Sang Ninja](#-tahap-2-membuktikan-sihir-sang-ninja)
- [Manajemen Lahan Parkir](#-manajemen-lahan-parkir)

---

## 🏎️ Konsep Lahan Parkir (Parking Lot)

Daripada mendaftarkan folder proyek satu per satu ke dalam Nginx, Valet menggunakan pendekatan yang radikal.

Anda mendaftarkan **satu folder raksasa utama** (misalnya folder `Sites` atau `Projects` di Mac Anda) dan mendeklarasikannya sebagai "Lahan Parkir Valet".

Seketika, Valet akan memonitor lahan tersebut. **Setiap kali** ada folder baru yang dilemparkan atau dibuat di dalam Lahan Parkir itu, Valet akan otomatis menyihir nama folder tersebut menjadi nama *domain* berakhiran `.test`, dan langsung menayangkannya ke peramban tanpa Anda perlu melakukan *restart* apa pun!

---

## 🏗️ Tahap 1: Membangun Lahan Parkir Anda

Mari kita wujudkan keajaiban ini. Tradisi pengguna Mac yang paling umum adalah memiliki folder bernama `Sites` di dalam direktori profil (*Home*) mereka. Kita akan menggunakannya.

1. Buka **Terminal** Anda.
2. Buat folder `Sites` jika Anda belum memilikinya (di dalam *Home Directory* Anda):
   ```bash
   mkdir ~/Sites
   ```
3. Masuk ke dalam folder tersebut:
   ```bash
   cd ~/Sites
   ```
4. Rapalkan mantra jurus parkir pamungkas ini:
   ```bash
   valet park
   ```

Tampilan di terminal akan membalas dengan anggun:
`This directory has been added to Valet's paths.`

Selesai. Anda baru saja menyulap folder `Sites` tersebut menjadi pabrik *domain* otomatis!

---

## 🎩 Tahap 2: Membuktikan Sihir Sang Ninja

Mari kita buktikan bahwa tidak ada kebohongan di sini. Kita tidak akan merestart *server*, kita tidak akan menyentuh *Virtual Host*.

1. Masih di dalam direktori `~/Sites` di Terminal, buat folder proyek baru. Mari kita namakan `portal-berita`:
   ```bash
   mkdir portal-berita
   ```
2. Masuk ke folder tersebut dan buat satu *file* pancingan bernama `index.php`:
   ```bash
   cd portal-berita
   echo "<h1>Sihir Valet Bekerja Sempurna!</h1>" > index.php
   ```
3. Buka peramban (*Chrome / Safari*) Anda.
4. Tanpa melakukan *restart* apa pun, ketik alamat ini di peramban: **`http://portal-berita.test`**

**BOM! 🤯**
Tulisan *"Sihir Valet Bekerja Sempurna!"* langsung meroket muncul di layar Anda. 
Anda baru saja menghemat waktu 15 menit dari rutinitas pembuatan *Virtual Host* XAMPP. Kecepatan *workflow* seperti inilah yang membuat para Ninja sangat mematikan di industri *development* modern!

---

## 🧰 Manajemen Lahan Parkir

Seiring waktu, Anda mungkin lupa di mana saja Anda menaruh lahan parkir Valet Anda. 
Valet memiliki komando militer untuk memantaunya:

- **Melihat semua Lahan Parkir yang aktif:**
  Ketik perintah ini di mana saja:
  ```bash
  valet paths
  ```
  Terminal akan menampilkan daftar folder raksasa mana saja yang sedang diawasi oleh Valet.

- **Menghancurkan (Menghapus) Lahan Parkir:**
  Jika Anda sudah muak dan tidak ingin folder `Sites` tadi diawasi lagi oleh Valet, cukup masuk ke folder tersebut, dan ketik mantra pelupa:
  ```bash
  cd ~/Sites
  valet forget
  ```
  Lahan parkir pun musnah, dan *domain-domain* di dalamnya akan berhenti bekerja.

Di bab selanjutnya, kita akan mempelajari jurus yang lebih spesifik. Bagaimana jika proyek kita letaknya berserakan dan *tidak berada* di dalam area Lahan Parkir? Dan bagaimana kita bisa menyihirnya menjadi **`https://` (SSL hijau)** layaknya *server* sungguhan hanya dengan satu kata? Bersiaplah untuk jurus **valet link** dan **valet secure**! 🔒✨
