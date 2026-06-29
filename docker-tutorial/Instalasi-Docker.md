![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 15 Mins](https://img.shields.io/badge/Durasi-15_Menit-blue?style=for-the-badge)
![OS: Windows | Mac | Linux](https://img.shields.io/badge/OS-Windows_|_Mac_|_Linux-lightgrey?style=for-the-badge)

# 🐳 Prolog: Menyiapkan Pelabuhan Anda

Selamat datang di dunia _containerization_! Sebelum kapal-kapal kontainer digital Anda bisa berlayar, kita perlu membangun pelabuhannya terlebih dahulu. Dalam bab ini, kita tidak akan sekadar menekan "Next" dan "Install". Kita akan memastikan fondasi sistem Anda benar-benar siap dan optimal.

Mari siapkan lingkungan kerja Anda dengan langkah-langkah yang presisi dan bebas dari rasa pusing.

## 📋 Daftar Isi
- [Pengecekan Spesifikasi Minimum](#-pengecekan-spesifikasi-minimum)
- [Instalasi di Windows (Docker Desktop)](#-instalasi-di-windows-docker-desktop)
- [Instalasi di macOS (Docker Desktop)](#-instalasi-di-macos-docker-desktop)
- [Instalasi di Linux (Docker Engine)](#-instalasi-di-linux-docker-engine)
- [Uji Coba: Verifikasi Pelabuhan Anda](#-uji-coba-verifikasi-pelabuhan-anda)

---

## 🔍 Pengecekan Spesifikasi Minimum

Sama seperti pelabuhan sungguhan yang membutuhkan kedalaman air tertentu agar kapal besar bisa bersandar, Docker juga memiliki syarat minimum untuk sistem operasi Anda. Memaksa instalasi tanpa memenuhi syarat ini hanya akan membawa Anda pada badai *error* di tengah jalan.

### Windows (WSL 2 Backend)
- **OS:** Windows 10/11 64-bit: Home atau Pro versi 21H2 atau lebih baru.
- **Hardware:** RAM minimal 4 GB. CPU dengan dukungan Virtualisasi (wajib diaktifkan di BIOS).

### macOS
- **Intel Mac:** macOS versi terbaru (minimal 2 versi mayor ke belakang). RAM minimal 4 GB.
- **Apple Silicon (M1/M2/M3):** Secara umum didukung sempurna, pastikan saja macOS Anda mutakhir.

### Linux
- **Distro:** Ubuntu, Debian, CentOS, Fedora, atau Raspberry Pi OS (64-bit).
- **Kernel:** Versi 3.10 ke atas.

> 💡 **PRO TIP:** 
> Untuk pengguna Windows, sangat disarankan menggunakan arsitektur **WSL 2 (Windows Subsystem for Linux)** alih-alih Hyper-V lawas. WSL 2 memberikan performa _file system_ yang jauh lebih cepat dan konsumsi RAM yang lebih hemat!

---

## 🪟 Instalasi di Windows (Docker Desktop)

Bagi pengguna Windows, Docker Desktop adalah cara paling elegan untuk memulai. Ia membungkus semua kompleksitas konfigurasi ke dalam satu aplikasi visual yang rapi.

1. **Aktifkan Virtualisasi:** Pastikan fitur *Virtualization* di Task Manager (tab Performance) berstatus *Enabled*.
2. **Unduh Installer:** Kunjungi [Dokumentasi Resmi Docker Windows](https://docs.docker.com/desktop/install/windows/) dan unduh `Docker Desktop Installer.exe`.
3. **Mulai Instalasi:** Jalankan installer. Saat muncul jendela konfigurasi, pastikan opsi **"Use WSL 2 instead of Hyper-V"** dicentang (biasanya ini adalah opsi default).
4. **Restart Komputer:** Setelah instalasi selesai, sistem biasanya akan meminta *restart*. Silakan *restart* komputer Anda.
5. **Konfirmasi Lisensi:** Buka Docker Desktop untuk pertama kalinya dan setujui *License Agreement*. 

> ⚠️ **PERINGATAN:**
> Jika Docker macet di status "Starting..." dalam waktu yang tidak wajar, biasanya ini disebabkan oleh WSL 2 yang belum diperbarui. Buka Command Prompt sebagai Admin, ketik `wsl --update`, lalu restart kembali Docker Anda.

---

## 🍎 Instalasi di macOS (Docker Desktop)

Apple membuat semuanya sederhana, begitu pula dengan prosedur instalasi Docker di ekosistem mereka.

1. **Kenali Chip Anda:** Pilih installer yang sesuai dengan arsitektur Mac Anda. (Pilih **Apple Silicon** jika Mac Anda menggunakan chip seri M, atau **Intel** jika menggunakan prosesor Intel lawas). Kunjungi [Halaman Resmi Docker Mac](https://docs.docker.com/desktop/install/mac-install/).
2. **Unduh & Geser:** Unduh file `.dmg`. Buka file tersebut dan cukup "drag-and-drop" ikon Docker ke dalam folder Applications.
3. **Akses Root:** Saat pertama kali dibuka, Docker membutuhkan akses istimewa (*privilege access*) untuk memasang komponen jaringannya. Masukkan kata sandi Mac Anda saat diminta.

Bagus! Anda baru saja melewati bagian yang sering menjadi momok bagi pemula. Mari kita selesaikan persiapan ini dengan sempurna.

---

## 🐧 Instalasi di Linux (Docker Engine)

Di Linux, kita secara native menggunakan *Docker Engine CLI* secara langsung karena performanya jauh lebih ringan, stabil, dan memberikan kendali penuh (*powerful*).

Berikut adalah mantra instalasi (menggunakan keluarga Debian/Ubuntu) yang secara elegan mengambil skrip rilis resmi dari Docker:

```bash
# 1. Bersihkan versi lama (jika ada) agar pondasi kita benar-benar bersih
sudo apt-get remove docker docker-engine docker.io containerd runc

# 2. Update repository lokal Anda
sudo apt-get update

# 3. Unduh dan jalankan skrip instalasi resmi dari Docker
# Skrip ini akan secara ajaib mengenali distro Anda dan memasang versi termutakhir!
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

**Post-Installation Steps (Langkah Krusial di Linux)**
Agar Anda tidak perlu bersusah payah mengetikkan `sudo` setiap kali memerintah Docker, tambahkan *user* Anda ke dalam grup khusus docker:

```bash
# Tambahkan user saat ini ke grup docker
sudo usermod -aG docker $USER

# Terapkan kepemilikan grup baru secara instan tanpa perlu log out
newgrp docker
```

---

## 🎯 Uji Coba: Verifikasi Pelabuhan Anda

Tidak peduli OS apa yang Anda gunakan, langkah validasi ini adalah ritual wajib untuk memastikan semuanya berjalan semestinya sebelum kita melangkah lebih jauh.

Buka Terminal (Mac/Linux) atau PowerShell/Command Prompt (Windows) Anda, dan ketikkan perintah ini:

```bash
# Meminta Docker menjalankan container percobaan untuk pertama kali
docker run hello-world
```

Jika terminal Anda menampilkan pesan yang diawali dengan **"Hello from Docker!"**, selamat! Pelabuhan Anda sudah beroperasi penuh dan siap menerima kapal kontainer pertama kita di bab selanjutnya. 🎉
