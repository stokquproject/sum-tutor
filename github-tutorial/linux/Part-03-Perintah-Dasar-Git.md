![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 25 Mins](https://img.shields.io/badge/Durasi-25_Menit-blue?style=for-the-badge)
![Practice: Hands-On](https://img.shields.io/badge/Metode-Hands--On_Practice-red?style=for-the-badge)

# 📸 Merekam Sejarah: Perintah Dasar Git di Terminal Linux

Terminal Linux dan Git adalah pasangan yang lahir untuk satu sama lain.

Tidak ada lapisan abstraksi. Tidak ada GUI yang menyembunyikan apa yang sebenarnya terjadi. Di sini, setiap perintah yang Anda ketikkan adalah instruksi langsung ke mesin Git — dan Anda akan melihat persis apa yang terjadi sebagai responsnya.

Inilah cara belajar Git yang sesungguhnya.

## 📋 Daftar Isi
- [Tiga Arena Git (Mental Model Wajib)](#-tiga-arena-git-mental-model-wajib)
- [git init — Menghidupkan Repositori](#-git-init--menghidupkan-repositori)
- [git status — Kompas Anda di Setiap Saat](#-git-status--kompas-anda-di-setiap-saat)
- [git add — Memilih Perubahan untuk Difoto](#-git-add--memilih-perubahan-untuk-difoto)
- [git commit — Mengabadikan Momen](#-git-commit--mengabadikan-momen)
- [git log — Membaca Kitab Sejarah](#-git-log--membaca-kitab-sejarah)
- [git diff — Melihat Perubahan Baris per Baris](#-git-diff--melihat-perubahan-baris-per-baris)
- [Bonus: .gitignore & Alias Terminal](#-bonus-gitignore--alias-terminal)
- [Praktik Langsung: Proyek Pertama Anda](#-praktik-langsung-proyek-pertama-anda)

---

## 🗺️ Tiga Arena Git (Mental Model Wajib)

Sebelum mengetik satu perintah pun, pahami tiga "arena" tempat file-file Anda berada. Hampir semua kebingungan tentang Git berakar dari tidak pahamnya konsep ini.

```
┌──────────────────────────────────────────────────────────────┐
│                      MESIN LOKAL ANDA                         │
│                                                              │
│  ┌─────────────────┐             ┌──────────────────┐        │
│  │  Working Tree   │  git add ►  │  Staging Area    │        │
│  │                 │             │  (Index)         │        │
│  │  File-file yang │ ◄ git restore│                  │        │
│  │  Anda edit      │             │  Perubahan yang  │        │
│  │  sehari-hari    │             │  siap di-commit  │        │
│  └─────────────────┘             └────────┬─────────┘        │
│                                           │ git commit        │
│                                           ▼                   │
│                                  ┌──────────────────┐        │
│                                  │  Repository      │        │
│                                  │  (.git/)         │        │
│                                  │                  │        │
│                                  │  Sejarah abadi   │        │
│                                  │  semua commit    │        │
│                                  └──────────────────┘        │
└──────────────────────────────────────────────────────────────┘
```

- **Working Tree**: Direktori kerja Anda. File-file nyata yang Anda buka di editor.
- **Staging Area (Index)**: Ruang tunggu. Tempat Anda *memilih* perubahan mana yang akan masuk ke foto berikutnya.
- **Repository**: Database permanen di dalam folder `.git/`. Setiap commit tersimpan di sini selamanya.

Analogi nyata: Anda fotografer yang akan memotret pameran seni. **Working Tree** = ruangan pameran. **Staging Area** = saat Anda mengatur objek-objek ke dalam frame bidikan. **Commit** = saat Anda menekan rana dan foto tersimpan ke memory card.

---

## 🔧 git init — Menghidupkan Repositori

Perintah ini mengubah direktori biasa menjadi repositori Git. Cukup dijalankan **sekali** di awal proyek.

```bash
# Buat folder proyek baru
mkdir ~/proyek/website-saya

# Masuk ke dalamnya
cd ~/proyek/website-saya

# Hidupkan repositori Git
git init
```

**Output:**
```
Initialized empty Git repository in /home/user/proyek/website-saya/.git/
```

Git membuat folder tersembunyi `.git/` di dalam direktori Anda. Inilah "otak" repositori — tempat semua sejarah, konfigurasi, dan metadata tersimpan.

```bash
# Lihat folder .git yang tersembunyi
ls -la
# Output:
# drwxrwxr-x 7 user user 4096 Jul  9 10:00 .git/
```

> ⚠️ **PERINGATAN:**
> Jangan pernah menghapus atau memodifikasi isi folder `.git/` secara manual. Melakukannya sama dengan menghancurkan seluruh sejarah proyek Anda. Jika Anda ingin "menghapus" Git dari sebuah folder, cukup hapus folder `.git/` itu saja: `rm -rf .git/`

---

## 👁️ git status — Kompas Anda di Setiap Saat

`git status` adalah perintah yang akan Anda ketik paling sering. Ia memberitahu Anda kondisi lengkap dari tiga arena di atas — apa yang berubah, apa yang di-staging, dan apa yang siap di-commit.

```bash
git status
```

Jadikan ini refleks. Ketik `git status` **sebelum dan sesudah** setiap operasi Git.

**Output di repo yang baru di-init:**
```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

**Output setelah membuat file baru:**
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	index.html
	style.css

nothing added to commit but untracked files present (use "git add" to track)
```

Perhatikan bagaimana Git bahkan memberi petunjuk tindakan apa yang harus dilakukan selanjutnya. Ramah sekali untuk pemula.

---

## 📦 git add — Memilih Perubahan untuk Difoto

Setelah membuat atau mengubah file, Git mendeteksinya — tapi **tidak otomatis menyertakannya** dalam commit berikutnya. Anda harus secara eksplisit memilih perubahan mana yang masuk.

```bash
# Tambahkan satu file spesifik
git add index.html

# Tambahkan beberapa file sekaligus
git add index.html style.css

# Tambahkan semua file dengan pola tertentu
git add *.html

# Tambahkan semua perubahan di direktori saat ini (paling umum)
git add .

# Tambahkan semua perubahan di seluruh repositori
git add -A
```

**Perbedaan `git add .` vs `git add -A`:**

| Perintah | Tambah file baru | Modifikasi | Hapus file |
|---|---|---|---|
| `git add .` | ✅ | ✅ | ✅ (di Git modern) |
| `git add -A` | ✅ | ✅ | ✅ |

Untuk Git versi 2.x ke atas (yang Anda gunakan), keduanya **berperilaku sama**. Gunakan `git add .` untuk kesederhanaan.

> ⚠️ **JEBAKAN `git add .`:**
> Perintah ini menambahkan **semua** yang berubah — termasuk file yang seharusnya tidak masuk repositori: file `.env` (berisi credentials!), direktori `node_modules/` (ratusan ribu file!), file log, file build, dsb.
>
> Selalu buat `.gitignore` di awal proyek. Kita akan bahas di section Bonus.

---

## 📸 git commit — Mengabadikan Momen

Ini adalah perintah terpenting. `git commit` mengambil semua yang ada di staging area dan menyimpannya sebagai satu snapshot permanen dalam sejarah repositori.

```bash
# Format standar — flag -m untuk menulis pesan langsung
git commit -m "Pesan commit yang deskriptif"

# Shortcut: staging semua file yang sudah di-track + commit dalam satu langkah
# (Tidak menyertakan file baru yang belum pernah di-add!)
git commit -am "Pesan commit"
```

**Anatomi pesan commit yang baik:**

```
Tambah validasi form kontak          ← Baris pertama: ringkasan singkat (max 72 karakter)
                                     ← Baris kosong (wajib jika ada body)
Validasi mencakup:                   ← Body opsional: penjelasan lebih detail
- Format email dengan regex
- Panjang pesan minimal 20 karakter
- Sanitasi input untuk mencegah XSS

Closes #42                           ← Footer opsional: referensi ke issue/ticket
```

Untuk commit harian, cukup satu baris dengan `-m`. Body hanya diperlukan untuk perubahan yang kompleks.

**Contoh pesan commit: Buruk vs Baik**

| ❌ Pesan Buruk | ✅ Pesan Baik |
|---|---|
| `fix` | `Perbaiki crash saat user upload foto > 5MB` |
| `update file` | `Update konfigurasi Nginx untuk support HTTP/2` |
| `wip` | `Tambah endpoint API GET /users/:id` |
| `asdf` | `Hapus file debug.log yang tidak sengaja ter-commit` |
| `final banget` | `Rilis v2.1.0 — fitur dark mode dan notifikasi push` |

> 💡 **ATURAN EMAS:**
> Pesan commit harus bisa melengkapi kalimat: *"Jika commit ini diterapkan, ia akan..."*
>
> "...Tambah validasi form kontak." ✅
> "...fix." ❌

---

## 📖 git log — Membaca Kitab Sejarah

Setelah beberapa commit, gunakan `git log` untuk menelusuri sejarah yang sudah terekam:

```bash
# Log lengkap dengan semua detail
git log

# Versi ringkas — satu baris per commit (PALING SERING DIPAKAI)
git log --oneline

# Tampilkan dengan grafik branch yang indah
git log --oneline --graph --all --decorate

# Log 5 commit terbaru saja
git log --oneline -5

# Cari commit berdasarkan kata kunci di pesan
git log --oneline --grep="validasi"

# Lihat siapa yang mengubah baris tertentu di sebuah file
git log -p -- index.html
```

**Contoh output `git log --oneline`:**
```
f4c2b81 (HEAD -> main) Tambah validasi form kontak
a1d9e22 Perbaiki layout mobile di halaman about
7c3f001 Tambah halaman about.html
9b2a445 Inisialisasi proyek — tambah index.html dan style.css
```

`HEAD -> main` menunjukkan posisi Anda saat ini: di branch `main`, di commit terbaru (`f4c2b81`).

---

## 🔍 git diff — Melihat Perubahan Baris per Baris

Sebelum meng-*add* atau meng-*commit*, gunakan `git diff` untuk melihat persis apa yang berubah:

```bash
# Lihat perubahan yang BELUM di-staging (antara working tree vs staging area)
git diff

# Lihat perubahan yang SUDAH di-staging (antara staging area vs commit terakhir)
git diff --staged

# Bandingkan dua commit tertentu
git diff a1d9e22 f4c2b81

# Lihat perubahan hanya pada file tertentu
git diff index.html
```

**Membaca output `git diff`:**
```diff
diff --git a/index.html b/index.html
index 7b2e904..a3f8c12 100644
--- a/index.html
+++ b/index.html
@@ -10,6 +10,8 @@ <body>
     <h1>Selamat Datang</h1>
+    <!-- Baris baru yang ditambahkan -->
+    <p class="subtitle">Website Portofolio Saya</p>
     <nav>
```

- Baris dengan `+` (hijau) = ditambahkan
- Baris dengan `-` (merah) = dihapus
- Baris tanpa tanda = tidak berubah (konteks)

---

## 🎁 Bonus: .gitignore & Alias Terminal

### Membuat .gitignore

File `.gitignore` mendaftarkan file/folder yang ingin Git abaikan sepenuhnya:

```bash
# Buat file .gitignore di root proyek
touch .gitignore
nano .gitignore
```

Isi contoh untuk proyek web:

```gitignore
# Credentials — JANGAN PERNAH di-commit!
.env
.env.local
*.key
*.pem

# Dependencies — bisa diinstall ulang kapanpun
node_modules/
vendor/
.venv/

# Build output
dist/
build/
*.min.js
*.min.css

# Cache
.cache/
__pycache__/
*.pyc

# Log files
*.log
logs/

# File sistem operasi Linux
.Trash-*
*~

# File editor
.vscode/
.idea/
*.swp
*.swo
```

> 💡 **PRO TIP:** Kunjungi **[gitignore.io](https://www.toptal.com/developers/gitignore)** dan masukkan stack teknologi Anda (misal: "Python, Django, Linux") untuk generate `.gitignore` yang komprehensif secara otomatis.

### Membuat Git Alias di Bash/Zsh

Ini adalah optimasi kecil yang akan menghemat ribuan penekanan tombol sepanjang karier Anda. Tambahkan ke `~/.bashrc` atau `~/.zshrc`:

```bash
# Buka file konfigurasi shell Anda
nano ~/.bashrc   # atau ~/.zshrc jika pakai Zsh

# Tambahkan baris-baris ini di bagian bawah:
alias gs='git status'
alias ga='git add'
alias gc='git commit -m'
alias gp='git push'
alias gl='git log --oneline --graph --all --decorate'
alias gd='git diff'

# Simpan dan terapkan perubahan
source ~/.bashrc
```

Sekarang `gs` = `git status`, `gl` = tampilan log yang indah, dan seterusnya.

---

## 🧪 Praktik Langsung: Proyek Pertama Anda

Lakukan ini dari awal hingga akhir. Rasakan sendiri bagaimana sejarah terbentuk.

```bash
# 1. Setup proyek
mkdir ~/latihan-git && cd ~/latihan-git
git init

# 2. Buat file pertama
echo "# Latihan Git di Linux" > README.md
echo "Proyek latihan untuk menguasai Git." >> README.md

# 3. Cek status
git status
# → README.md muncul sebagai "Untracked file"

# 4. Staging
git add README.md
git status
# → README.md sekarang "Changes to be committed" (hijau)

# 5. Commit pertama
git commit -m "Inisialisasi proyek — tambah README.md"

# 6. Tambah file kedua
echo '<html><body><h1>Hello, Git!</h1></body></html>' > index.html
git add index.html
git commit -m "Tambah index.html dengan struktur HTML dasar"

# 7. Edit file yang sudah ada
echo "## Cara Menjalankan" >> README.md
echo "Buka index.html di browser." >> README.md

# 8. Lihat apa yang berubah sebelum commit
git diff README.md

# 9. Staging dan commit
git add README.md
git commit -m "Tambah instruksi cara menjalankan di README"

# 10. Lihat sejarah yang terbentuk
git log --oneline
```

**Output akhir:**
```
c3f8a21 (HEAD -> main) Tambah instruksi cara menjalankan di README
7b2e904 Tambah index.html dengan struktur HTML dasar
1d9c331 Inisialisasi proyek — tambah README.md
```

Tiga commit. Tiga momen dalam sejarah proyek Anda. Semuanya terekam secara permanen, bisa dijelajahi kapanpun, dan bisa dikembalikan jika diperlukan.

---

Anda sudah menguasai inti dari workflow Git sehari-hari: **init → status → add → commit → log**. Ini adalah siklus yang akan Anda jalani ratusan kali setiap minggu.

Tapi kekuatan Git sesungguhnya belum kita sentuh — kemampuan menciptakan dunia-dunia paralel yang berjalan secara bersamaan tanpa saling mengganggu. Di bab berikutnya, kita kuasai **Branch & Merge**. 🌿

---
*Sebelumnya: [Part 2 — Instalasi Git di Linux](Part-02-Instalasi-Git-di-Linux.md)*
*Selanjutnya: [Part 4 — Branch & Merge: Dunia Paralel](Part-04-Branch-dan-Merge.md)*
