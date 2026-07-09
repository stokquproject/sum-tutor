![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 15 Mins](https://img.shields.io/badge/Durasi-15_Menit-blue?style=for-the-badge)
![OS: Windows](https://img.shields.io/badge/OS-Windows_10_|_11-0078D6?style=for-the-badge&logo=windows)

# ⚙️ Menyiapkan Markas Besar: Instalasi Git & Konfigurasi Pertama di Windows

Mesin waktu kita tidak akan bisa berjalan jika kita belum memasang mesinnya. Di bab ini, kita akan melakukan dua hal yang terlihat sederhana namun sangat fundamental:

1. Menginstal **Git for Windows** dengan pengaturan yang benar (bukan asal klik *Next*)
2. Memperkenalkan **identitas Anda** kepada Git — karena setiap "foto" (*commit*) yang Anda ambil harus tanda tangani atas nama Anda

Proses ini hanya butuh sekitar 15 menit, tapi efeknya akan menemani seluruh karier programming Anda.

## 📋 Daftar Isi
- [Mengunduh Git for Windows](#-mengunduh-git-for-windows)
- [Panduan Instalasi Pilihan Per Pilihan](#-panduan-instalasi-pilihan-per-pilihan)
- [Konfigurasi Identitas: Menandatangani Setiap Karya Anda](#-konfigurasi-identitas-menandatangani-setiap-karya-anda)
- [Mengenal Git Bash vs Command Prompt](#-mengenal-git-bash-vs-command-prompt)
- [Uji Coba: Memastikan Git Terpasang dengan Benar](#-uji-coba-memastikan-git-terpasang-dengan-benar)
- [Klinik Darurat: Solusi Error Umum](#-klinik-darurat-solusi-error-umum)

---

## 📥 Mengunduh Git for Windows

Kunjungi situs resmi dan unduh *installer* terbaru:

👉 **[git-scm.com/download/win](https://git-scm.com/download/win)**

Situs ini akan secara otomatis mendeteksi arsitektur Windows Anda (64-bit atau 32-bit) dan menawarkan versi yang sesuai. Unduh **"64-bit Git for Windows Setup"**.

> 💡 **PRO TIP:**
> File *installer* biasanya berukuran sekitar 60 MB. Jangan bingung jika ada opsi "Standalone Installer" dan "Portable". Pilih **Standalone Installer** — ini versi standar yang mengintegrasikan Git ke dalam sistem Anda secara proper.

---

## 🛠️ Panduan Instalasi Pilihan Per Pilihan

Di sinilah kebanyakan tutorial asal-asalan: mereka hanya bilang "klik Next terus". Kita tidak seperti itu. Ada beberapa pilihan krusial yang perlu Anda pahami:

### Layar 1: Select Components
Biarkan semua pilihan *default* tercentang. Pastikan **"Git Bash Here"** dan **"Git GUI Here"** tercentang — ini menambahkan opsi klik kanan yang sangat berguna nantinya.

### Layar 2: Choosing the Default Editor
Git perlu tahu editor mana yang harus dibuka saat Anda menulis pesan *commit* yang panjang. *Default*-nya adalah **Vim** — yang terkenal membingungkan pemula (ada lelucon populer: "Bagaimana cara keluar dari Vim? Restart komputer").

**Rekomendasi kami:** Pilih **Visual Studio Code** dari daftar dropdown jika Anda sudah menggunakannya. Jika belum, **Notepad++** adalah pilihan ramah pemula yang bagus.

### Layar 3: Adjusting your PATH environment ⭐ **(PILIHAN TERPENTING)**

Ini adalah pilihan yang paling berdampak. Anda akan melihat 3 opsi:

- ❌ **"Use Git from Git Bash only"** — Terlalu terbatas. Git hanya bisa dipakai dari Git Bash.
- ✅ **"Git from the command line and also from 3rd-party software"** — **PILIH INI.** Ini adalah opsi *recommended* yang memungkinkan Git diakses dari mana saja: CMD, PowerShell, VS Code Terminal, semuanya.
- ⚠️ **"Use Git and optional Unix tools..."** — Terlalu agresif. Menimpa beberapa perintah bawaan Windows.

### Layar 4: Choosing HTTPS transport backend
Biarkan *default*: **"Use the OpenSSL library"**. Tidak perlu diganti.

### Layar 5: Configuring line ending conversions ⭐ **(PENTING UNTUK KOLABORASI)**

Ini soal karakter tersembunyi di akhir setiap baris kode. Windows menggunakan `CRLF`, sedangkan Mac/Linux menggunakan `LF`. Jika tidak diatur dengan benar, Git akan mendeteksi perbedaan ini sebagai "perubahan" pada setiap baris, mengacaukan seluruh history.

Pilih: **"Checkout Windows-style, commit Unix-style line endings"** — Ini adalah pilihan *recommended* yang memastikan kompatibilitas sempurna saat berkolaborasi dengan teman yang pakai Mac atau Linux.

### Layar 6: Configuring the terminal emulator
Pilih: **"Use MinTTY (the default terminal of MSYS2)"** — Terminal yang lebih modern dan nyaman daripada CMD bawaan Windows.

### Sisanya
Semua layar berikutnya bisa dibiarkan *default*. Klik **Install** dan tunggu prosesnya selesai.

---

## 🪪 Konfigurasi Identitas: Menandatangani Setiap Karya Anda

Ini adalah langkah yang **WAJIB** dilakukan setelah instalasi dan sering dilewati oleh tutorial lain. Akibatnya? Setiap *commit* Anda akan tampil dengan nama "Unknown" di GitHub — memalukan.

Buka **Git Bash** (cari di Start Menu) dan masukkan dua perintah ini:

```bash
# Ganti dengan nama asli Anda — ini yang akan tampil di setiap commit Anda di GitHub
git config --global user.name "Nama Anda Di Sini"

# Gunakan email yang SAMA dengan akun GitHub Anda — ini sangat penting!
git config --global user.email "email.anda@contoh.com"
```

Flag `--global` berarti pengaturan ini berlaku untuk **semua proyek** di komputer Anda. Anda cukup melakukan ini sekali saja seumur hidup (di komputer ini).

**Verifikasi konfigurasi Anda:**

```bash
# Tampilkan semua konfigurasi Git yang aktif
git config --list
```

Anda akan melihat output yang menyertakan baris seperti ini:
```
user.name=Nama Anda Di Sini
user.email=email.anda@contoh.com
```

Bagus! Identitas Anda sudah resmi terdaftar. 🎉

> ⚠️ **PERINGATAN:**
> Pastikan email di `user.email` **sama persis** dengan email yang Anda daftarkan di GitHub. Jika berbeda, kontribusi Anda tidak akan terhubung ke profil GitHub Anda dan tidak akan terhitung di grafik kontribusi (*contribution graph*) Anda.

---

## 💻 Mengenal Git Bash vs Command Prompt

Setelah instalasi, Anda kini punya beberapa cara untuk mengetikkan perintah Git di Windows. Kenali perbedaannya:

| | **Git Bash** | **Command Prompt (CMD)** | **PowerShell** |
|---|---|---|---|
| **Bawaan dari** | Git for Windows | Windows | Windows |
| **Perintah Git** | ✅ Berfungsi penuh | ✅ Berfungsi penuh* | ✅ Berfungsi penuh* |
| **Perintah Unix** | ✅ `ls`, `cat`, `grep`, `mkdir` | ❌ Tidak dikenal | ⚠️ Sebagian |
| **Rekomendasi untuk** | Semua operasi Git harian | Tidak direkomendasikan | Boleh, jika sudah terbiasa |

\* *Selama Anda memilih opsi "Git from command line" saat instalasi tadi.*

**Rekomendasi**: Gunakan **Git Bash** atau langsung gunakan **terminal bawaan VS Code** (yang sudah otomatis terintegrasi dengan Git).

---

## ✅ Uji Coba: Memastikan Git Terpasang dengan Benar

Ritual wajib sebelum melanjutkan ke bab berikutnya. Buka **Git Bash** dan ketik:

```bash
# Cek versi Git yang terpasang
git --version
```

Jika output Anda terlihat seperti ini (versi mungkin berbeda, tidak masalah):

```
git version 2.47.1.windows.2
```

...maka selamat! Mesin waktu Anda sudah terpasang dan siap dijalankan.

---

## 🚑 Klinik Darurat: Solusi Error Umum

> [!WARNING]
> **Masalah: `git` is not recognized as an internal or external command**
>
> **Penyebab**: PATH environment variable tidak ter-update setelah instalasi. Windows tidak tahu di mana mencari program `git`.
>
> **Solusi**: **Restart komputer Anda** terlebih dahulu — ini menyelesaikan 90% kasus. Jika masih bermasalah, coba install ulang Git dan pastikan memilih opsi **"Git from the command line and also from 3rd-party software"** pada layar PATH.

> [!WARNING]
> **Masalah: Konfigurasi user.name dan user.email hilang setelah update Git**
>
> **Penyebab**: Beberapa versi update Git me-reset konfigurasi global.
>
> **Solusi**: Jalankan ulang dua perintah `git config --global` di atas. Konfigurasi tersimpan di file `C:\Users\NamaUser\.gitconfig` yang bisa Anda buka dan edit langsung jika perlu.

> [!NOTE]
> **Pertanyaan Umum: Apakah perlu buat akun GitHub dulu sebelum bisa pakai Git?**
>
> **Jawaban**: Tidak! Git bisa digunakan 100% secara *offline* tanpa akun GitHub. Anda baru membutuhkan akun GitHub saat ingin mulai menyimpan kode ke cloud atau berkolaborasi dengan orang lain (kita akan bahas di Part 5).

---

Instalasi selesai, identitas sudah terdaftar, dan Git Bash sudah menyambut Anda. Fondasi markas besar sudah berdiri kokoh.

Sekarang tibalah saatnya kita benar-benar *merasakan* kekuatan Git. Di bab selanjutnya, kita akan membuat repositori pertama kita dari nol dan mulai merekam sejarah kode kita, satu *commit* dalam satu waktu. 📸

---
*Sebelumnya: [Part 1 — Apa Itu Git & GitHub?](Part-01-Apa-Itu-Git-dan-GitHub.md)*
*Selanjutnya: [Part 3 — Perintah Dasar Git: Mulai Merekam Sejarah](Part-03-Perintah-Dasar-Git.md)*
