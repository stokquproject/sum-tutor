![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 15 Mins](https://img.shields.io/badge/Durasi-15_Menit-blue?style=for-the-badge)
![Core Concept](https://img.shields.io/badge/Fokus-Manajemen_Versi-purple?style=for-the-badge)

# 🎭 Sang Bunglon: Berganti Versi PHP & Node.js dalam 3 Klik

Selamat datang di Level 2, Kapten! Kini saatnya kita mengasah persenjataan.

Bayangkan skenario horor ini: Anda sedang mengerjakan Proyek A peninggalan *programmer* lama yang menggunakan **PHP 7.4**. Tiba-tiba, atasan Anda meminta Anda membuat Proyek B (sebuah *startup* baru) yang mewajibkan **PHP 8.2**. 

Di lingkungan tradisional (seperti XAMPP), ini adalah sebuah mimpi buruk. Anda harus melakukan *uninstall*, mencari *installer* versi lama, mengedit *Environment Variables* Windows, hingga mempertaruhkan rusaknya OS Anda. 

Di dalam ekosistem Laragon, pergantian ini sehalus bunglon yang berganti warna. Tidak ada instalasi. Tidak ada *error*. Hanya butuh **3 klik**.

## 📋 Daftar Isi
- [Kutukan "Version Conflict"](#-kutukan-version-conflict)
- [Arsitektur Bunglon: Rahasia di Balik Layar](#-arsitektur-bunglon-rahasia-di-balik-layar)
- [Praktik: Menambahkan Versi PHP Baru](#-praktik-menambahkan-versi-php-baru)
- [Menjinakkan Ekosistem Node.js](#-menjinakkan-ekosistem-nodejs)

---

## ☠️ Kutukan "Version Conflict"

Konflik versi adalah pembunuh produktivitas nomor satu. Saat *website* lama Anda dipaksa berjalan di atas versi bahasa pemrograman yang baru, fungsi-fungsinya akan usang (*deprecated*) dan layar Anda akan dipenuhi teks *error* berwarna merah.

Aplikasi lawas mengatasi ini dengan menyuruh Anda menginstal *multiple software* yang saling tumpang tindih. Pada akhirnya, *registry* Windows Anda membengkak dan laptop Anda menjadi sangat lambat.

Laragon memecahkan masalah ini dengan sebuah terobosan brilian: **Isolasi Folder Binari**.

---

## 🦎 Arsitektur Bunglon: Rahasia di Balik Layar

Di Laragon, mesin PHP, MySQL, Apache, atau Node.js **bukanlah** sebuah program yang diinstal ke dalam sistem Windows. Mereka hanyalah sekumpulan *file* (*binary*) yang diletakkan di dalam folder `C:\laragon\bin`.

Jika Anda ingin menambahkan 10 versi PHP yang berbeda secara bersamaan, Anda hanya perlu meletakkan 10 folder PHP tersebut bersebelahan. Saat Anda menyuruh Laragon menggunakan PHP 8.2, Laragon hanya akan "menunjuk" ke folder PHP 8.2 dan mengabaikan yang lain. 

Tidak ada yang menimpa satu sama lain. Sebuah harmoni yang sempurna.

---

## 🛠️ Praktik: Menambahkan Versi PHP Baru

Mari kita asumsikan Laragon Anda saat ini menggunakan PHP 8.1, namun proyek Anda membutuhkan **PHP 7.4**. Mari kita bawa masuk sang bunglon:

1. Kunjungi arsip resmi PHP untuk Windows di: **[windows.php.net/downloads/releases/archives](https://windows.php.net/downloads/releases/archives/)**
2. Cari dan unduh versi yang Anda inginkan, misalnya `php-7.4.33-nts-Win32-vc15-x64.zip`.
   > **Pro Tip:** Selalu pilih versi **NTS (Non-Thread Safe)** untuk performa Nginx/Apache yang lebih baik di Laragon, dan pastikan arsitekturnya **x64** (64-bit).
3. Setelah selesai diunduh, ekstrak *file zip* tersebut.
4. Buka *File Explorer* Anda, dan masuklah ke dalam brankas mesin Laragon: **`C:\laragon\bin\php`**
5. Pindahkan folder PHP 7.4 hasil ekstrak tadi ke dalam folder ini. (Pastikan isi foldernya langsung berupa sekumpulan *file*, bukan folder di dalam folder).

**Momen Sihir (The 3 Clicks):**
1. Buka aplikasi Laragon Anda.
2. **Klik Kanan** di area kosong > Pilih menu **PHP** > Pilih **Version**.
3. Di sana, Anda akan melihat versi `php-7.4.33` baru saja muncul di daftar! Klik versi tersebut.

**BOM! 🤯**
Laragon akan secara otomatis me-*restart* *Apache/Nginx*, mengubah jalur mesin, dan memuat ulang sistem Anda. Dalam waktu kurang dari 2 detik, *server* Anda telah mundur ke masa lalu menggunakan PHP 7.4 dengan sempurna. Tanpa *uninstall*, tanpa *error*.

---

## 🟩 Menjinakkan Ekosistem Node.js

Filosofi ajaib ini tidak hanya berlaku untuk PHP. Laragon juga sangat memanjakan *developer* Javascript (React/Vue/Express).

Jika Anda butuh mengganti versi **Node.js**:
1. Kunjungi situs resmi: **[nodejs.org/dist](https://nodejs.org/dist/)**
2. Pilih versi yang Anda mau (misal: `v18.16.0`), lalu unduh *file* berakhiran **`win-x64.zip`** (JANGAN unduh yang `.msi`!).
3. Ekstrak *file zip* tersebut.
4. Pindahkan folder hasil ekstrak ke: **`C:\laragon\bin\nodejs`**
5. Buka Laragon > **Klik Kanan** > **Node.js** > **Version** > Pilih versi Anda.

> [!IMPORTANT]
> **Otomatisasi Environment Variable**
> Saat Anda mengganti versi PHP atau Node.js melalui "Klik Kanan" Laragon, Anda tidak hanya mengganti versi *web server*, tetapi Laragon juga secara gaib dan instan mengubah konfigurasi terminal Windows Anda. 
> 
> Silakan buka terminal (Menu Laragon > klik **Terminal**) dan ketik `php -v` atau `node -v`. Terminal akan selalu merespons dengan versi yang baru saja Anda pilih di menu. Sangat brilian!

Di bab selanjutnya, kita akan membongkar senjata rahasia Laragon untuk para penguasa data. Tinggalkan `phpMyAdmin` yang lambat, dan bersiaplah menyambut **HeidiSQL**: Sang Brankas Harta Karun. 🗄️💎
