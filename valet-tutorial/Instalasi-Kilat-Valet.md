![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 15 Mins](https://img.shields.io/badge/Durasi-15_Menit-blue?style=for-the-badge)
![System Setup](https://img.shields.io/badge/Fokus-Instalasi_Sistem-purple?style=for-the-badge)

# ⚡ Instalasi Kilat: Menempa Pedang Pertama

Proses instalasi Valet tidak sama dengan menginstal aplikasi biasa di Mac.
Di sini, Anda tidak akan menemukan tombol *Next, Next, Finish* atau *User Interface (UI)* yang cantik. 

Seorang Ninja bekerja di dalam bayangan, dan bayangan kita hari ini adalah **Terminal**. 
Kita akan menggunakan terminal untuk merakit mesin pembunuh lambatnya *development* ini dari nol. Proses ini hanya dilakukan **satu kali seumur hidup** di laptop Anda. Setelah pedang ini selesai ditempa, Anda bisa menebas ribuan proyek web ke depannya hanya dengan satu kali sabetan.

Mari kita nyalakan tungku api!

## 📋 Daftar Isi
- [Tahap 1: Mempersiapkan Tungku Api (Homebrew)](#-tahap-1-mempersiapkan-tungku-api-homebrew-php--composer)
- [Tahap 2: Memanggil Roh Sang Ninja](#-tahap-2-memanggil-roh-sang-ninja)
- [Tahap 3: Uji Coba Ketajaman Pedang](#-tahap-3-uji-coba-ketajaman-pedang)
- [Troubleshooting: Perang Perebutan Port 80](#-troubleshooting-perang-perebutan-port-80)

---

## 🌋 Tahap 1: Mempersiapkan Tungku Api (Homebrew, PHP, & Composer)

Sebelum Valet bisa masuk, kita harus memastikan pondasi sistem Mac Anda siap menerimanya.

1. Buka aplikasi **Terminal** (atau iTerm2) di Mac Anda.
2. Pastikan paket Homebrew Anda dalam keadaan segar. Ketik perintah ini dan tekan *Enter*:
   ```bash
   brew update
   ```
3. Valet membutuhkan mesin bahasa PHP untuk membaca kode Anda. Instal versi PHP terbaru:
   ```bash
   brew install php
   ```
4. Selanjutnya, kita membutuhkan manajer paket PHP dunia, yaitu **Composer**. Composer adalah kurir yang akan membawakan bungkus Valet ke laptop Anda:
   ```bash
   brew install composer
   ```

Tunggu hingga Homebrew selesai mengunduh dan merakit semuanya. Ini mungkin memakan waktu beberapa menit tergantung kecepatan internet Anda.

---

## 🥷 Tahap 2: Memanggil Roh Sang Ninja

Kini saatnya kita mengunduh senjata utamanya.

1. Di Terminal Anda, perintahkan Composer untuk mengunduh Valet dan menanamkannya ke seluruh penjuru sistem (*global*):
   ```bash
   composer global require laravel/valet
   ```

2. **Langkah Krusial (Jalan Setapak):** 
   Agar Mac mengenali kata perintah `valet`, sistem Mac harus tahu di mana Composer menyimpan pedangnya. Anda harus memasukkan direktori `~/.composer/vendor/bin` ke dalam *Environment Path* Mac Anda.
   *(Jika Anda menggunakan ZSH yang merupakan default Mac modern, edit file `~/.zshrc` dan tambahkan `export PATH="$PATH:$HOME/.composer/vendor/bin"` di paling bawah baris).*

3. Setelah *Path* disetel, ketik mantra pamungkas ini dan tekan *Enter*:
   ```bash
   valet install
   ```

Pada tahap ini, Anda akan diminta memasukkan kata sandi Mac Anda. Berikan izin!
Valet akan mulai bekerja dengan gila: Ia mengonfigurasi dan memasang daemon **Nginx** di latar belakang, serta mendaftarkan radar **Dnsmasq** untuk menyadap nama *domain* lokal.

---

## ⚔️ Tahap 3: Uji Coba Ketajaman Pedang

Bagaimana kita tahu bahwa Ninja tersebut sudah bersembunyi di dalam laptop Anda dan siap menerima perintah?

Buka terminal Anda, dan ketik perintah gila ini:
```bash
ping foobar.test
```

Jika Valet telah terinstal dengan sukses, radar Dnsmasq akan langsung bekerja seketika.
Tampilan terminal Anda akan terus-menerus memuntahkan tulisan yang mengarahkan kata acak `foobar.test` tersebut ke alamat laptop Anda sendiri (`127.0.0.1`):
```text
PING foobar.test (127.0.0.1): 56 data bytes
64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.045 ms
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.120 ms
```
*(Tekan `CTRL + C` di terminal untuk menghentikan ping tersebut).*

Jika alamat `127.0.0.1` muncul, selamat! Sihir Dnsmasq telah berhasil. Anda tidak perlu lagi menyentuh *file* `hosts` seumur hidup!

---

## 🚨 Troubleshooting: Perang Perebutan Port 80

Terkadang, perintah `valet install` akan gagal atau Nginx menolak untuk menyala.

Ini biasanya terjadi karena **Port 80 (Pintu Gerbang Utama HTTP)** di Mac Anda sedang diduduki oleh aplikasi lain yang sudah lebih dulu *nongkrong* di sana. Mac OS secara *default* memiliki Apache bawaan yang terkadang menyala sendiri, atau mungkin Anda masih menyalakan Docker/XAMPP/MAMP di saat yang bersamaan.

**Cara mengusir penghuni liar dari Port 80:**
1. Matikan dan *Quit* aplikasi Docker / MAMP / XAMPP yang masih terbuka.
2. Jika yang menduduki adalah Apache bawaan Mac, matikan secara paksa menggunakan perintah ini di Terminal:
   ```bash
   sudo apachectl stop
   ```
3. Setelah Port 80 kosong, ketik perintah ini untuk memulai ulang mesin jantung Valet:
   ```bash
   valet restart
   ```

Ninja Anda kini telah terbangun! 
Di bab selanjutnya (Level 2), kita akan melihat bagaimana sang Ninja ini melempar *Shuriken*: **Bagaimana memunculkan dan menjalankan proyek website Anda hanya dengan 2 kata di terminal.** Bersiaplah untuk terpukau! 💫
