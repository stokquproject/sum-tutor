![Difficulty: Advanced](https://img.shields.io/badge/Tingkat-Mahir-red?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![Workflow Speed](https://img.shields.io/badge/Fokus-Kecepatan_Workflow-purple?style=for-the-badge)

# 🎭 Ilmu Ganti Wujud: Mengendalikan Versi PHP Tanpa Air Mata

Jauh sebelum Valet mencapai bentuk sempurnanya, mengubah versi PHP di Mac adalah sebuah **mimpi buruk** yang bisa memakan waktu berjam-jam.

Jika Anda memiliki dua proyek (satu aplikasi lawas (*legacy*) yang butuh PHP 7.4 dan satu aplikasi modern Laravel 11 yang mewajibkan PHP 8.3), Anda harus bertarung dengan *Terminal*. 
Anda harus memutus sambungan *Homebrew* (`brew unlink php@7.4`), menyambungkan versi baru (`brew link php@8.3`), mengedit *Environment PATH*, dan me-*restart* Nginx secara manual setiap kali berpindah proyek. 

Banyak *developer* menangis dan berakhir memformat ulang Mac mereka karena sistem PHP-nya tumpang tindih dan korup.

Namun hari ini, sang Ninja telah mempelajari **Ilmu Ganti Wujud**. Anda bisa berganti kulit PHP hanya dalam satu tarikan napas.

## 📋 Daftar Isi
- [Jurus Ganti Wujud Global (valet use)](#-jurus-ganti-wujud-global-valet-use)
- [Jurus Kloning Bayangan (Per-Site PHP)](#-jurus-kloning-bayangan-per-site-php-isolate)
- [Praktik: Memanipulasi Dimensi Waktu](#-praktik-memanipulasi-dimensi-waktu)
- [Memonitor Wujud Kloning](#-memonitor-wujud-kloning)

---

## 🌎 Jurus Ganti Wujud Global (valet use)

Jika Anda ingin mengubah versi PHP secara **menyeluruh (Global)** untuk seluruh isi Mac Anda, Valet merangkum seluruh siksaan *Homebrew* tadi menjadi dua kata sederhana.

Buka Terminal Anda dan ketik perintah ini:
```bash
valet use php@8.2
```

Seketika, keajaiban terjadi di latar belakang:
1. Valet akan mengecek apakah Mac Anda sudah memiliki `php@8.2`. Jika belum, Valet akan mengunduhnya via *Homebrew* secara otomatis!
2. Valet akan memutuskan tautan versi PHP lama dengan aman.
3. Valet akan menyambungkan versi `php@8.2` ke Nginx dan me-*restart* *server* dalam diam.

**BOM!** Seluruh *website* di laptop Anda kini ditenagai oleh mesin PHP 8.2 yang baru. Selesai. Tanpa mengedit satu pun teks konfigurasi.

---

## 👥 Jurus Kloning Bayangan (Per-Site PHP / isolate)

*(Ini adalah The Wow Factor dari pembaruan Valet terbaru!)*

Fitur global di atas sangat hebat, namun belum menyelesaikan masalah utama kita: Bagaimana jika saya ingin `portal-lama.test` tetap menggunakan **PHP 7.4**, sementara `aplikasi-baru.test` menggunakan **PHP 8.3** berjalan **secara bersamaan** di satu Mac?

XAMPP dan MAMP konvensional akan menyerah di titik ini (atau mengharuskan penggabungan port yang sangat rumit).
Docker adalah satu-satunya alat yang terkenal mampu melakukan ini, namun dengan memakan RAM ber-GigaByte.

Valet? Valet meluncurkan mantra pamungkas bernama **Isolate** (Kloning Bayangan). Valet akan menciptakan pekerja PHP khusus hanya untuk folder tersebut.

---

## ⏳ Praktik: Memanipulasi Dimensi Waktu

Mari kita buat sebuah aplikasi lawas berjalan beriringan dengan sistem modern Anda.

1. Buka Terminal Anda, dan masuklah ke dalam folder proyek lawas Anda (Misalnya di dalam Lahan Parkir Anda):
   ```bash
   cd ~/Sites/portal-lama
   ```
2. Saat ini, folder tersebut menggunakan versi PHP Global Anda (misal PHP 8.3). Aplikasi lawas Anda pasti akan *Error* dan hancur.
3. Untuk menyembuhkannya, rapalkan mantra bayangan ini:
   ```bash
   valet isolate php@7.4
   ```
4. Valet akan mengunduh versi lawas tersebut dan mengikatnya **hanya** untuk folder `portal-lama` ini.

**Ajaib! 🤯**
Sekarang, cobalah buka peramban Anda:
- Saat Anda membuka `http://portal-lama.test`, mesin yang melayani adalah pekerja **PHP 7.4**.
- Di *Tab* sebelahnya, saat Anda membuka `http://aplikasi-baru.test`, mesin yang melayani adalah pekerja **PHP 8.3**.

Kedua aplikasi dari era berbeda tersebut hidup berdampingan secara damai di satu Mac, memakan RAM sangat kecil, tanpa adanya konflik *Port*. Ini adalah tingkatan sihir *Development* tertinggi!

---

## 👁️ Memonitor Wujud Kloning

Jika Anda memiliki banyak proyek bayangan dan mulai lupa *website* mana yang menggunakan versi PHP berapa, Anda bisa memanggil mata Elang Valet.

Ketik di sembarang direktori terminal:
```bash
valet isolated
```
Valet akan mencetak daftar rapi berisi nama proyek-proyek Anda beserta versi PHP aneh yang sedang merasukinya.

Dan jika Anda ingin mengembalikan sebuah proyek ke versi PHP masa kini (Global), cukup masuk ke foldernya dan ruqyah folder tersebut dengan:
```bash
valet unisolate
```
*(Proyek akan kembali mematuhi versi global).*

Di bab pemungkas selanjutnya, kita akan mengisi kekosongan terbesar Valet. Valet memang cepat, tapi dia tidak memiliki *Database* bawaan. Bagaimana cara meracik *Database* mewah, kilat, dan ringan di Mac? Bersiaplah menyambut sang pendamping sejati: **DBngin**! 🗄️⚡
