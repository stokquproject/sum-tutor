![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![OS: macOS](https://img.shields.io/badge/OS-macOS_Ventura_|_Sonoma_|_Sequoia-000000?style=for-the-badge&logo=apple&logoColor=white)

# 🍺 Instalasi Git di macOS: Cara yang Benar dengan Homebrew

Di macOS, ada tiga cara menginstal Git. Kita akan bahas ketiganya — tapi kita akan langsung tahu mana yang terbaik.

Bersiap untuk pertama kali bertemu dengan **Homebrew** — salah satu alat paling produktif yang akan pernah Anda instal di Mac Anda.

## 📋 Daftar Isi
- [Cek: Apakah Git Sudah Ada?](#-cek-apakah-git-sudah-ada)
- [Tiga Cara Install Git — Mana yang Terbaik?](#-tiga-cara-install-git--mana-yang-terbaik)
- [Instalasi Homebrew (Jika Belum Ada)](#-instalasi-homebrew-jika-belum-ada)
- [Instalasi Git via Homebrew](#-instalasi-git-via-homebrew)
- [Konfigurasi Identitas: Menandatangani Setiap Karya](#-konfigurasi-identitas-menandatangani-setiap-karya)
- [Konfigurasi Tambahan untuk macOS](#-konfigurasi-tambahan-untuk-macos)
- [Memilih Terminal: Terminal.app vs iTerm2 vs Warp](#-memilih-terminal-terminalapp-vs-iterm2-vs-warp)
- [Verifikasi Instalasi](#-verifikasi-instalasi)

---

## 🔍 Cek: Apakah Git Sudah Ada?

Buka **Terminal** (tekan `⌘ + Space`, ketik "Terminal", tekan Enter) dan jalankan:

```zsh
git --version
```

**Kemungkinan 1 — Git sudah ada (via Xcode CLT):**
```
git version 2.39.3 (Apple Git-145)
```
Perhatikan tanda `(Apple Git-xxx)` — ini adalah Git versi Apple yang dikompilasi khusus, biasanya tertinggal beberapa versi dari Git resmi. Fungsional, tapi tidak ideal.

**Kemungkinan 2 — macOS menawarkan instalasi Xcode:**
```
xcode-select: note: No developer tools were found, requesting install.
```
Sebuah dialog GUI akan muncul meminta Anda menginstal Xcode Command Line Tools. Anda bisa klik Install — tapi ikuti panduan Homebrew di bawah ini untuk hasil yang lebih baik.

**Kemungkinan 3 — Git belum ada sama sekali:**
```
zsh: command not found: git
```
Sempurna. Kita mulai dari nol dengan cara yang benar.

---

## 🤔 Tiga Cara Install Git — Mana yang Terbaik?

| Metode | Pro | Kontra | Rekomendasi |
|---|---|---|---|
| **Xcode Command Line Tools** | Built-in Apple, mudah | Versi tertinggal, update lambat | ❌ Tidak ideal |
| **Installer resmi git-scm.com** | Versi terbaru | Update manual, tidak terintegrasi | ⚠️ Bisa, tapi kurang elegan |
| **Homebrew** | Versi terbaru, update otomatis, kelola semua software Mac | Perlu install Homebrew dulu | ✅ **INI YANG TERBAIK** |

Homebrew adalah pilihan yang tepat — bukan hanya untuk Git, tapi untuk hampir semua software developer yang akan Anda butuhkan di Mac (Node.js, PHP, Python, PostgreSQL, Redis, dan seterusnya).

---

## 🍺 Instalasi Homebrew (Jika Belum Ada)

Cek apakah Homebrew sudah ada:

```zsh
brew --version
```

Jika hasilnya `zsh: command not found: brew`, instal Homebrew sekarang. Buka Terminal dan jalankan perintah resmi dari **[brew.sh](https://brew.sh)**:

```zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Proses ini akan:
1. Mengunduh dan menginstal **Xcode Command Line Tools** secara otomatis (jika belum ada)
2. Mengunduh dan menginstal Homebrew itu sendiri
3. Membutuhkan input password Mac Anda (untuk akses `sudo`)

Estimasi waktu: 5–15 menit tergantung kecepatan internet.

### Langkah Penting Setelah Instalasi Homebrew (Apple Silicon)

Jika Mac Anda menggunakan chip **M1/M2/M3/M4** (Apple Silicon), Homebrew diinstal di `/opt/homebrew/` — berbeda dari lokasi Intel Mac (`/usr/local/`). Anda perlu menambahkan Homebrew ke PATH.

Terminal akan menampilkan instruksi ini setelah instalasi. Jalankan perintah berikut:

```zsh
# Tambahkan Homebrew ke PATH untuk sesi saat ini
eval "$(/opt/homebrew/bin/brew shellenv)"

# Tambahkan ke ~/.zprofile agar otomatis aktif setiap kali Terminal dibuka
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```

Untuk Intel Mac, Homebrew sudah otomatis di PATH — tidak perlu langkah ini.

**Verifikasi Homebrew:**
```zsh
brew --version
# Homebrew 4.x.x
```

> 💡 **PRO TIP: Homebrew adalah Ekosistem, Bukan Hanya Installer**
> Setelah Homebrew terinstal, Anda punya akses ke ribuan software developer berkualitas tinggi:
> ```zsh
> brew install node          # Node.js
> brew install php           # PHP
> brew install postgresql    # PostgreSQL
> brew install redis         # Redis
> brew install wget          # wget (tidak ada di macOS default)
> ```
> Satu perintah, software terpasang, dan selalu bisa diupdate dengan `brew upgrade`.

---

## 📥 Instalasi Git via Homebrew

Dengan Homebrew siap, instalasi Git adalah satu perintah:

```zsh
brew install git
```

Homebrew akan mengunduh dan menginstal Git versi terbaru secara resmi.

**Setelah instalasi, pastikan Terminal menggunakan Git dari Homebrew (bukan Apple):**

```zsh
# Cek versi Git — seharusnya sudah tidak ada tulisan "(Apple Git-xxx)"
git --version
# git version 2.47.x  ← tanpa "(Apple Git-xxx)", artinya sudah dari Homebrew

# Konfirmasi lokasi Git yang digunakan
which git
# /opt/homebrew/bin/git   ← Apple Silicon
# /usr/local/bin/git      ← Intel Mac
```

Jika `which git` masih menunjuk ke `/usr/bin/git` (Apple Git lama), tutup dan buka ulang Terminal Anda — ini menyegarkan PATH dan biasanya menyelesaikan masalah.

**Update Git di masa depan semudah:**
```zsh
brew upgrade git
```

---

## 🪪 Konfigurasi Identitas: Menandatangani Setiap Karya

Langkah **wajib** setelah instalasi. Setiap commit yang Anda buat akan menyertakan informasi ini — nama dan email Anda akan terpampang di GitHub untuk setiap baris kode yang Anda kontribusikan.

```zsh
# Set nama — ini yang tampil di setiap commit di GitHub
git config --global user.name "Nama Anda"

# Set email — HARUS sama dengan email akun GitHub Anda
git config --global user.email "email.anda@contoh.com"
```

Flag `--global` menyimpan konfigurasi di `~/.gitconfig` — berlaku untuk semua repositori di Mac Anda, cukup dilakukan sekali.

**Verifikasi:**
```zsh
git config --list
# user.name=Nama Anda
# user.email=email.anda@contoh.com
```

---

## ⚙️ Konfigurasi Tambahan untuk macOS

Empat konfigurasi ini membuat pengalaman Git di macOS lebih optimal:

### 1. Default Branch: `main`

```zsh
git config --global init.defaultBranch main
```

Menyelaraskan `git init` lokal dengan standar default GitHub.

### 2. Editor Default

```zsh
# VS Code (paling populer di komunitas macOS developer)
git config --global core.editor "code --wait"

# Nano (ramah pemula di terminal)
git config --global core.editor "nano"
```

### 3. Abaikan File `.DS_Store` Secara Global

`.DS_Store` adalah file tersembunyi yang macOS buat otomatis di setiap folder untuk menyimpan metadata Finder (ukuran ikon, posisi, dsb). File ini **tidak boleh masuk** ke repositori Git — tidak relevan bagi siapapun selain Finder di Mac Anda.

Buat file `.gitignore` global yang berlaku untuk semua proyek:

```zsh
# Buat file gitignore global
touch ~/.gitignore_global

# Tambahkan pola yang akan diabaikan secara global
cat >> ~/.gitignore_global << 'EOF'
# macOS system files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
.AppleDouble
.LSOverride

# macOS Finder sidecar files
Icon

# Thumbnail cache files
ehthumbs.db
Thumbs.db
EOF

# Daftarkan ke konfigurasi Git global
git config --global core.excludesfile ~/.gitignore_global
```

> ⚠️ **PERINGATAN:**
> File `.DS_Store` di repositori adalah salah satu hal yang paling cepat membuat developer Mac dicap tidak profesional oleh rekan satu tim yang pakai Linux. Konfigurasi global ini mengatasinya sekali untuk selamanya — tanpa perlu menambahkan `.DS_Store` ke setiap `.gitignore` proyek.

### 4. Credential: Gunakan macOS Keychain

```zsh
# Simpan credential GitHub di macOS Keychain — aman dan permanen
git config --global credential.helper osxkeychain
```

Setelah ini, saat pertama kali Anda push ke GitHub via HTTPS, macOS akan menyimpan token Anda di **Keychain** secara terenkripsi. Push berikutnya tidak perlu input apapun.

---

## 💻 Memilih Terminal: Terminal.app vs iTerm2 vs Warp

macOS hadir dengan **Terminal.app** bawaan — fungsional dan cukup untuk sebagian besar kebutuhan. Tapi komunitas developer macOS punya beberapa pilihan favorit:

| Terminal | Kelebihan | Cocok untuk |
|---|---|---|
| **Terminal.app** | Built-in, ringan, zero setup | Pemula, kebutuhan dasar |
| **[iTerm2](https://iterm2.com)** | Split pane, search, profil warna, integrasi tmux | Power user, multi-session |
| **[Warp](https://www.warp.dev)** | Modern, AI assist, blok output, autocomplete | Developer yang suka UX modern |
| **VS Code Terminal** | Terintegrasi langsung dengan editor | Saat coding di VS Code |

Rekomendasi untuk memulai: gunakan **Terminal.app** dulu. Setelah nyaman, eksplorasi iTerm2 atau Warp jika dirasa perlu.

> 💡 **PRO TIP: Oh My Zsh**
> Jika Anda sering di terminal, instal **[Oh My Zsh](https://ohmyz.sh)** — framework konfigurasi Zsh yang menambahkan tema cantik, plugin Git (yang menampilkan branch aktif di prompt), dan ratusan shortcut produktif:
> ```zsh
> sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
> ```
> Setelah Oh My Zsh terinstal, prompt terminal Anda akan otomatis menampilkan nama branch Git yang sedang aktif — tidak perlu `git branch` lagi untuk tahu posisi Anda.

---

## ✅ Verifikasi Instalasi

Pastikan semua sudah sempurna sebelum lanjut:

```zsh
# 1. Cek versi Git dari Homebrew
git --version
# git version 2.47.x (tanpa tulisan Apple)

# 2. Konfirmasi lokasi
which git
# /opt/homebrew/bin/git  atau  /usr/local/bin/git

# 3. Lihat semua konfigurasi
git config --list
```

**Output `git config --list` yang ideal:**
```
user.name=Nama Anda
user.email=email.anda@contoh.com
init.defaultbranch=main
core.editor=code --wait
core.excludesfile=/Users/NamaUser/.gitignore_global
credential.helper=osxkeychain
```

Semua sudah hijau? Markas Anda di macOS sudah siap tempur.

---

## 🚑 Klinik Darurat

> [!WARNING]
> **`git` masih menunjuk ke Apple Git setelah install Homebrew**
>
> ```
> git version 2.39.3 (Apple Git-145)
> ```
>
> **Solusi**: Tutup dan buka ulang Terminal. Jika masih terjadi, periksa urutan PATH:
> ```zsh
> echo $PATH
> # Pastikan /opt/homebrew/bin (atau /usr/local/bin) muncul SEBELUM /usr/bin
> ```
> Jika tidak, tambahkan ke `~/.zprofile`:
> ```zsh
> export PATH="/opt/homebrew/bin:$PATH"
> source ~/.zprofile
> ```

> [!WARNING]
> **Homebrew berjalan sangat lambat atau error di Apple Silicon**
>
> **Penyebab**: Menjalankan Terminal dalam mode Rosetta (emulasi Intel).
>
> **Solusi**: Klik kanan Terminal.app di Finder → Get Info → pastikan **"Open using Rosetta"** tidak dicentang. Homebrew untuk Apple Silicon harus berjalan di mode native ARM.

> [!NOTE]
> **Pertanyaan: Apakah perlu Xcode penuh (bukan hanya CLT)?**
>
> **Tidak**, untuk kebutuhan Git dan pengembangan web/backend. Xcode Command Line Tools sudah cukup dan Homebrew akan menginstalnya otomatis. Xcode penuh (ukuran 10GB+) hanya diperlukan jika Anda mengembangkan aplikasi iOS atau macOS native.

---

Git terpasang via Homebrew, identitas terdaftar, dan `.DS_Store` tidak akan pernah mengotori repositori Anda lagi.

Di bab berikutnya, kita langsung masuk ke aksi — membuat repositori pertama dan merasakan siklus `add → commit → log` yang akan menjadi napas kerja Anda sehari-hari. 📸

---
*Sebelumnya: [Part 1 — Apa Itu Git & GitHub?](Part-01-Apa-Itu-Git-dan-GitHub.md)*
*Selanjutnya: [Part 3 — Perintah Dasar Git: Mulai Merekam Sejarah](Part-03-Perintah-Dasar-Git.md)*
