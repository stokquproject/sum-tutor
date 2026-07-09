![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 10 Mins](https://img.shields.io/badge/Durasi-10_Menit-blue?style=for-the-badge)
![OS: Linux](https://img.shields.io/badge/OS-Ubuntu_|_Debian_|_Fedora_|_Arch-FCC624?style=for-the-badge&logo=linux&logoColor=black)

# 📦 Instalasi Git di Linux: Elegan, Cepat, Satu Perintah

Ini adalah momen di mana pengguna Linux mendapat hak istimewa yang tidak dimiliki pengguna sistem operasi lain.

Tidak ada wizard instalasi. Tidak ada "Next → Next → Finish". Tidak ada memilih *checkbox* satu per satu.

Di Linux, Anda membuka terminal, mengetik satu perintah, dan Git sudah terpasang — dengan semua dependensinya, siap pakai, terintegrasi penuh dengan sistem Anda.

Beginilah seharusnya software diinstal.

## 📋 Daftar Isi
- [Apakah Git Sudah Terpasang?](#-apakah-git-sudah-terpasang)
- [Instalasi Berdasarkan Distro](#-instalasi-berdasarkan-distro)
- [Instalasi Versi Terbaru dari Source PPA](#-instalasi-versi-terbaru-dari-ppa-khusus-ubuntudebian)
- [Konfigurasi Identitas: Menandatangani Setiap Karya](#-konfigurasi-identitas-menandatangani-setiap-karya)
- [Konfigurasi Tambahan yang Sering Diabaikan](#-konfigurasi-tambahan-yang-sering-diabaikan)
- [Verifikasi Instalasi](#-verifikasi-instalasi)

---

## 🔍 Apakah Git Sudah Terpasang?

Sebelum menginstal, cek dulu. Banyak distribusi Linux modern sudah menyertakan Git secara *default*.

```bash
# Cek versi Git yang terpasang
git --version
```

Jika outputnya seperti ini, Git sudah ada:
```
git version 2.43.0
```

Jika outputnya `-bash: git: command not found`, lanjutkan ke section berikutnya.

> 💡 **PRO TIP:**
> Bahkan jika Git sudah terpasang, pastikan versinya tidak terlalu tua. Git versi di bawah 2.28 belum mendukung perintah `git switch` (cara modern berpindah branch) dan konfigurasi `defaultBranch`. Jika versi Anda di bawah 2.28, pertimbangkan untuk meng-upgrade.

---

## 📥 Instalasi Berdasarkan Distro

Pilih instruksi sesuai distribusi Linux Anda:

### 🟠 Ubuntu / Debian (dan turunannya: Linux Mint, Pop!_OS, Kali Linux)

```bash
# Update daftar package terlebih dahulu
sudo apt update

# Install Git
sudo apt install git -y
```

### 🔵 Fedora

```bash
# Fedora menggunakan dnf sebagai package manager
sudo dnf install git -y
```

### 🟢 CentOS / RHEL / AlmaLinux / Rocky Linux

```bash
# Aktifkan EPEL repository jika belum (untuk versi yang lebih baru)
sudo dnf install epel-release -y

# Install Git
sudo dnf install git -y

# Atau menggunakan yum (untuk versi CentOS yang lebih lama)
sudo yum install git -y
```

### 🟣 Arch Linux / Manjaro

```bash
# Arch menggunakan pacman — dan biasanya sudah punya Git versi terbaru
sudo pacman -S git
```

### 🔶 openSUSE

```bash
sudo zypper install git
```

---

## ⬆️ Instalasi Versi Terbaru dari PPA (Khusus Ubuntu/Debian)

Versi Git di repositori resmi Ubuntu/Debian kadang tertinggal beberapa versi dari rilis terbaru. Jika Anda ingin selalu menggunakan Git versi paling mutakhir, tambahkan PPA (*Personal Package Archive*) resmi dari tim Git:

```bash
# 1. Tambahkan PPA resmi Git
sudo add-apt-repository ppa:git-core/ppa -y

# 2. Update daftar package
sudo apt update

# 3. Install (atau upgrade) Git ke versi terbaru
sudo apt install git -y

# 4. Verifikasi versi
git --version
```

> 💡 **PRO TIP:**
> PPA `git-core/ppa` dikelola langsung oleh tim pengembang Git. Dengan menambahkan PPA ini, setiap kali ada rilis Git baru, Anda akan mendapatkannya secara otomatis melalui `sudo apt upgrade` biasa — tanpa perlu konfigurasi manual apapun.

---

## 🪪 Konfigurasi Identitas: Menandatangani Setiap Karya

Langkah ini **wajib** dilakukan setelah instalasi. Setiap *commit* yang Anda buat akan menyertakan informasi ini — nama dan email Anda akan terpampang di GitHub untuk setiap baris kode yang Anda kontribusikan.

```bash
# Set nama — ini yang akan tampil di setiap commit di GitHub
git config --global user.name "Nama Lengkap Anda"

# Set email — HARUS sama dengan email akun GitHub Anda
git config --global user.email "email.anda@contoh.com"
```

Flag `--global` menyimpan konfigurasi ini di `~/.gitconfig` — berlaku untuk semua repositori di sistem Anda. Cukup dilakukan sekali.

**Verifikasi:**

```bash
git config --list
```

```
user.name=Nama Lengkap Anda
user.email=email.anda@contoh.com
```

> ⚠️ **PERINGATAN:**
> Email di `user.email` harus **sama persis** dengan email yang terdaftar di akun GitHub Anda. Jika berbeda, kontribusi Anda tidak akan terhubung ke profil GitHub dan tidak terhitung di grafik kontribusi (*contribution graph*) Anda.

---

## ⚙️ Konfigurasi Tambahan yang Sering Diabaikan

Tiga konfigurasi berikut tidak wajib, tapi sangat direkomendasikan untuk pengalaman Git yang lebih menyenangkan:

### 1. Set Default Branch ke `main`

Sejak 2020, GitHub menggunakan `main` sebagai nama branch default (menggantikan `master` yang lama). Agar Git lokal Anda sinkron dengan GitHub:

```bash
git config --global init.defaultBranch main
```

Tanpa ini, `git init` akan membuat branch bernama `master`, yang bisa membingungkan saat dihubungkan ke GitHub.

### 2. Set Default Editor

Git perlu membuka editor teks untuk skenario tertentu (seperti menulis pesan commit panjang atau saat *merge conflict*). Set ke editor favorit Anda:

```bash
# Jika menggunakan VS Code
git config --global core.editor "code --wait"

# Jika menggunakan Nano (paling ramah pemula di terminal)
git config --global core.editor "nano"

# Jika menggunakan Vim (untuk yang sudah mahir)
git config --global core.editor "vim"
```

> 💡 **PRO TIP untuk pengguna Nano:**
> Nano jauh lebih ramah pemula daripada Vim. Saat Git membuka editor untuk input pesan commit, tulis pesan Anda lalu tekan `Ctrl+X` → `Y` → `Enter` untuk menyimpan dan keluar. Sederhana.

### 3. Set Line Ending (untuk Kolaborasi Lintas OS)

Jika Anda berkolaborasi dengan rekan yang menggunakan Windows:

```bash
# Di Linux/Mac: simpan dan checkout menggunakan LF (standar Unix)
git config --global core.autocrlf input
```

Ini memastikan Git tidak mengacaukan file Anda karena perbedaan karakter *line ending* antara Windows (`CRLF`) dan Linux (`LF`).

---

## ✅ Verifikasi Instalasi

Ritual wajib sebelum melanjutkan. Pastikan semua sudah berjalan sempurna:

```bash
# 1. Cek versi Git
git --version
# Output: git version 2.43.0 (atau lebih baru)

# 2. Lihat semua konfigurasi yang aktif
git config --list

# 3. Baca lokasi file konfigurasi global Anda
cat ~/.gitconfig
```

**Output `~/.gitconfig` yang ideal:**

```ini
[user]
	name = Nama Lengkap Anda
	email = email.anda@contoh.com
[init]
	defaultBranch = main
[core]
	editor = nano
	autocrlf = input
```

Semua sudah beres? Lanjut.

---

## 🚑 Klinik Darurat

> [!WARNING]
> **Error: `E: Package 'git' has no installation candidate`**
>
> **Penyebab**: Daftar package lokal terlalu lama dan tidak mengenali paket Git.
>
> **Solusi**: Jalankan `sudo apt update` terlebih dahulu, lalu coba install ulang.

> [!WARNING]
> **Error: `sudo: add-apt-repository: command not found`**
>
> **Penyebab**: Package `software-properties-common` belum terinstal.
>
> **Solusi**:
> ```bash
> sudo apt install software-properties-common -y
> # Lalu ulangi perintah add-apt-repository
> ```

> [!NOTE]
> **Pertanyaan: Apakah perlu `sudo` untuk semua perintah Git?**
>
> **Tidak.** `sudo` hanya diperlukan saat *menginstal* Git (karena menulis ke direktori sistem). Semua perintah Git sehari-hari (`git add`, `git commit`, `git push`, dsb.) dijalankan **tanpa** `sudo` — cukup sebagai user biasa di dalam folder proyek Anda.

---

Git terpasang. Identitas terdaftar. Konfigurasi optimal sudah teraplikasikan.

Di bab berikutnya, kita akan langsung terjun ke aksi — membuat repositori pertama dan merasakan sendiri kekuatan siklus `add → commit → log` yang akan menjadi ritual harian Anda sebagai developer. 📸

---
*Sebelumnya: [Part 1 — Apa Itu Git & GitHub?](Part-01-Apa-Itu-Git-dan-GitHub.md)*
*Selanjutnya: [Part 3 — Perintah Dasar Git: Mulai Merekam Sejarah](Part-03-Perintah-Dasar-Git.md)*
