![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 25 Mins](https://img.shields.io/badge/Durasi-25_Menit-blue?style=for-the-badge)
![Practice: Hands-On](https://img.shields.io/badge/Metode-Hands--On_Practice-red?style=for-the-badge)

# 📸 Merekam Sejarah: Perintah Dasar Git di macOS

Terminal macOS dan Git adalah kombinasi yang terasa natural — Zsh yang ekspresif, autocomplete yang intuitif, dan performa yang responsif di chip Apple Silicon maupun Intel.

Saatnya kita manfaatkan semua itu. Di bab ini kita tidak hanya menghafal perintah — kita membangun sebuah proyek kecil dari nol dan merekam setiap langkahnya. Pada akhirnya, Anda akan benar-benar *merasakan* bagaimana sejarah kode terbentuk.

## 📋 Daftar Isi
- [Tiga Arena Git (Mental Model yang Harus Anda Miliki)](#-tiga-arena-git-mental-model-yang-harus-anda-miliki)
- [git init — Menyalakan Repositori](#-git-init--menyalakan-repositori)
- [git status — Sensor Kondisi Real-Time](#-git-status--sensor-kondisi-real-time)
- [git add — Memilih Momen untuk Diabadikan](#-git-add--memilih-momen-untuk-diabadikan)
- [git commit — Mengabadikan Sejarah](#-git-commit--mengabadikan-sejarah)
- [git log — Menelusuri Jejak Waktu](#-git-log--menelusuri-jejak-waktu)
- [git diff — Melihat Perbedaan Baris per Baris](#-git-diff--melihat-perbedaan-baris-per-baris)
- [Bonus: .gitignore & Zsh Git Prompt](#-bonus-gitignore--zsh-git-prompt)
- [Praktik Lengkap: Dari Nol ke Repositori Aktif](#-praktik-lengkap-dari-nol-ke-repositori-aktif)

---

## 🗺️ Tiga Arena Git (Mental Model yang Harus Anda Miliki)

Hampir semua kebingungan tentang Git berasal dari tidak pahamnya konsep tiga area ini. Pahami sekali, dan segalanya akan terasa logis.

```
┌──────────────────────────────────────────────────────────────┐
│                         MAC ANDA                              │
│                                                              │
│  ┌──────────────────┐             ┌───────────────────┐      │
│  │  Working Tree    │             │   Staging Area    │      │
│  │                  │  git add ►  │   (Index)         │      │
│  │  File yang Anda  │             │                   │      │
│  │  edit di VS Code │ ◄ git restore│  Perubahan yang  │      │
│  │  atau editor lain│             │  siap di-commit   │      │
│  └──────────────────┘             └─────────┬─────────┘      │
│                                             │ git commit      │
│                                             ▼                 │
│                                   ┌──────────────────┐       │
│                                   │  Repository      │       │
│                                   │  (.git/)         │       │
│                                   │                  │       │
│                                   │  Sejarah abadi   │       │
│                                   │  semua commit    │       │
│                                   └──────────────────┘       │
└──────────────────────────────────────────────────────────────┘
```

- **Working Tree**: Folder proyek Anda di Finder/Terminal. File-file nyata yang Anda edit.
- **Staging Area**: Ruang tunggu. Anda *memilih* perubahan mana yang akan masuk ke snapshot berikutnya.
- **Repository (.git/)**: Database permanen yang menyimpan semua commit untuk selamanya.

Analogi macOS: Anda sedang mengedit foto di Photos untuk dikirim. **Working Tree** = semua foto mentah. **Staging Area** = foto yang sudah Anda pilih dan masukkan ke album "Untuk Dikirim". **Commit** = saat Anda klik "Share" dan foto-foto itu tersimpan sebagai koleksi resmi.

---

## 🔧 git init — Menyalakan Repositori

Perintah ini mengubah folder biasa menjadi repositori Git. Cukup sekali di awal proyek.

```zsh
# Buat folder proyek baru
mkdir ~/Developer/proyek-pertama

# Masuk ke folder tersebut
cd ~/Developer/proyek-pertama

# Nyalakan repositori Git
git init
```

> 💡 **PRO TIP: Folder `~/Developer`**
> Convention yang banyak dipakai developer macOS adalah menyimpan semua proyek di `~/Developer/`. Folder ini bahkan punya ikon khusus di Finder (palu dan obeng). Buat foldernya sekali: `mkdir ~/Developer`

**Output:**
```
Initialized empty Git repository in /Users/NamaAnda/Developer/proyek-pertama/.git/
```

Git membuat folder tersembunyi `.git/` — inilah "otak" repositori.

```zsh
# Lihat folder tersembunyi di macOS
ls -la
# drwxr-xr-x  9 user  staff  288 .git/
```

> ⚠️ **PERINGATAN:**
> Jangan hapus folder `.git/` — itu berarti menghapus seluruh sejarah proyek. Jika di Finder tidak terlihat, itu karena macOS menyembunyikan file yang diawali titik. Aktifkan dengan shortcut `⌘ + Shift + .` di Finder untuk melihat file tersembunyi.

---

## 👁️ git status — Sensor Kondisi Real-Time

Perintah yang akan Anda ketik paling sering. `git status` menunjukkan kondisi lengkap ketiga arena — apa yang berubah, apa yang di-staging, apa yang siap di-commit.

```zsh
git status
```

Jadikan refleks: ketik `git status` **sebelum dan sesudah** setiap operasi Git.

**Output di repo baru yang kosong:**
```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

**Output setelah membuat file:**
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	index.html
	style.css

nothing added to commit but untracked files present
```

Perhatikan: Git bahkan memberikan petunjuk tindakan selanjutnya di dalam outputnya.

---

## 📦 git add — Memilih Momen untuk Diabadikan

Membuat atau mengubah file tidak otomatis memasukkannya ke snapshot berikutnya. Anda harus memilih secara eksplisit:

```zsh
# Tambahkan satu file
git add index.html

# Tambahkan beberapa file
git add index.html style.css

# Tambahkan semua file dengan pola tertentu
git add *.html

# Tambahkan semua perubahan (paling sering dipakai)
git add .

# Mode interaktif — pilih perubahan baris per baris (fitur canggih)
git add -p
```

**`git add -p` adalah fitur rahasia yang membedakan Anda:**

Dengan flag `-p` (patch), Git akan menampilkan setiap "hunk" (blok perubahan) satu per satu dan meminta konfirmasi. Anda bisa memilih untuk meng-*staging* hanya sebagian dari perubahan di satu file.

Ini sangat berguna saat Anda membuat dua perubahan berbeda di satu file secara bersamaan dan ingin memisahkannya menjadi dua commit yang berbeda untuk history yang lebih bersih.

> ⚠️ **JEBAKAN `git add .`:**
> Hati-hati dengan file yang tidak ingin masuk ke repositori: `.DS_Store` (sudah ditangani via global gitignore di Part 2), `node_modules/`, file `.env`, dan lain-lain. Pastikan `.gitignore` Anda sudah terkonfigurasi sebelum `git add .`

---

## 📸 git commit — Mengabadikan Sejarah

`git commit` mengambil semua yang ada di staging area dan menyimpannya sebagai snapshot permanen dengan ID unik (hash).

```zsh
# Format standar
git commit -m "Pesan commit yang deskriptif"

# Staging semua file yang sudah pernah di-track + commit sekaligus
# (Tidak berlaku untuk file baru yang belum pernah di-add)
git commit -am "Pesan commit"

# Buka editor untuk menulis pesan yang lebih panjang
git commit
```

**Panduan menulis pesan commit yang baik:**

```
Tambah fitur pencarian produk di halaman utama     ← Baris 1: ringkasan (max 72 karakter)
                                                    ← Baris kosong (wajib jika ada body)
Implementasi meliputi:                              ← Body opsional: detail lebih lengkap
- Search bar dengan debounce 300ms
- Filter berdasarkan kategori dan harga
- Highlight kata yang dicari di hasil

Closes #15
```

**Contoh nyata — Buruk vs Baik:**

| ❌ Pesan Buruk | ✅ Pesan Baik |
|---|---|
| `update` | `Update konfigurasi Nginx untuk support HTTP/2` |
| `fix` | `Perbaiki crash saat export file kosong ke PDF` |
| `done` | `Selesaikan halaman checkout dengan integrasi Midtrans` |
| `test commit` | `Tambah test untuk edge case input angka negatif` |

> 💡 **ATURAN EMAS:**
> Pesan commit terbaik adalah yang menjawab: *"Jika commit ini diterapkan, ia akan..."*
> - "...Tambah fitur pencarian produk." ✅
> - "...update." ❌

---

## 📖 git log — Menelusuri Jejak Waktu

Setelah beberapa commit, gunakan ini untuk membaca sejarah:

```zsh
# Log lengkap
git log

# Log ringkas satu baris — paling sering dipakai
git log --oneline

# Log dengan visualisasi branch (sangat berguna di proyek tim)
git log --oneline --graph --all --decorate

# 5 commit terbaru
git log --oneline -5

# Cari berdasarkan kata kunci di pesan commit
git log --oneline --grep="pencarian"

# Lihat perubahan yang dibuat oleh developer tertentu
git log --oneline --author="Nama Developer"

# Lihat commit yang menyentuh file tertentu
git log --oneline -- src/components/SearchBar.jsx
```

**Contoh output `git log --oneline`:**
```
f4c2b81 (HEAD -> main) Tambah fitur pencarian produk
a1d9e22 Perbaiki styling header di layar kecil
7c3f001 Tambah halaman about dan kontak
9b2a445 Setup proyek — struktur folder dan file awal
```

`HEAD -> main` = posisi Anda saat ini (branch `main`, commit terbaru).

---

## 🔍 git diff — Melihat Perbedaan Baris per Baris

Sebelum staging atau commit, gunakan ini untuk mereview perubahan:

```zsh
# Perubahan yang BELUM di-staging
git diff

# Perubahan yang SUDAH di-staging (siap di-commit)
git diff --staged

# Perubahan di file tertentu
git diff index.html

# Perbandingan antara dua commit
git diff a1d9e22 f4c2b81

# Perbandingan antara dua branch
git diff main fitur/dark-mode
```

**Membaca output:**
- `+` hijau = baris yang **ditambahkan**
- `-` merah = baris yang **dihapus**
- Tanpa tanda = konteks (tidak berubah)

---

## 🎁 Bonus: .gitignore & Zsh Git Prompt

### File .gitignore per Proyek

Selain global gitignore yang sudah dibuat di Part 2, setiap proyek biasanya butuh `.gitignore` yang lebih spesifik:

```zsh
# Di root folder proyek
touch .gitignore
```

Contoh isi `.gitignore` untuk proyek web Node.js di macOS:

```gitignore
# Khusus macOS (backup — sudah di global gitignore)
.DS_Store

# Dependencies
node_modules/
.npm

# Environment variables — JANGAN PERNAH di-commit!
.env
.env.local
.env.production

# Build output
dist/
build/
.next/
.nuxt/

# Cache
.cache/
.parcel-cache/

# Log
*.log
npm-debug.log*
yarn-debug.log*

# Editor
.vscode/settings.json
.idea/

# Testing
coverage/
```

### Zsh Git Prompt dengan Oh My Zsh

Jika Anda sudah menginstal **Oh My Zsh** (disebut di Part 2), prompt terminal Anda otomatis menampilkan informasi Git:

```
➜  proyek-pertama git:(main) ✗
│   │                │         └── Ada perubahan yang belum di-commit
│   │                └─────────── Nama branch aktif
│   └──────────────────────────── Nama folder
└──────────────────────────────── Status (hijau = bersih, merah = ada error)
```

Tidak perlu `git branch` untuk tahu posisi Anda — informasinya selalu ada di depan mata.

---

## 🧪 Praktik Lengkap: Dari Nol ke Repositori Aktif

Ikuti dari atas ke bawah — rasakan setiap langkahnya:

```zsh
# 1. Setup proyek
mkdir ~/Developer/latihan-git
cd ~/Developer/latihan-git
git init

# 2. Buat file pertama
echo "# Proyek Latihan Git di macOS" > README.md
echo "" >> README.md
echo "Belajar Git step by step di ekosistem Apple." >> README.md

# 3. Cek status — Git mendeteksi file baru
git status
# → README.md muncul sebagai "Untracked file"

# 4. Staging
git add README.md
git status
# → README.md sekarang "Changes to be committed" (hijau)

# 5. Commit pertama
git commit -m "Inisialisasi proyek — tambah README.md"

# 6. Tambah file kedua
cat > index.html << 'EOF'
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Latihan Git</title>
</head>
<body>
  <h1>Hello, Git! 🍎</h1>
</body>
</html>
EOF

git add index.html
git commit -m "Tambah index.html dengan struktur HTML dasar"

# 7. Modifikasi file yang sudah ada
echo "" >> README.md
echo "## Cara Menjalankan" >> README.md
echo "Buka \`index.html\` di browser." >> README.md

# 8. Review perubahan sebelum commit
git diff README.md

# 9. Staging dan commit
git add README.md
git commit -m "Tambah instruksi menjalankan proyek di README"

# 10. Lihat sejarah yang terbentuk
git log --oneline
```

**Output akhir:**
```
c3f8a21 (HEAD -> main) Tambah instruksi menjalankan proyek di README
7b2e904 Tambah index.html dengan struktur HTML dasar
1d9c331 Inisialisasi proyek — tambah README.md
```

Tiga titik waktu dalam sejarah proyek Anda. Semuanya tersimpan permanen dan bisa dijelajahi kapanpun.

---

Siklus `init → status → add → commit → log` sudah menjadi bagian dari cara berpikir Anda. Itu adalah fondasi yang tidak bisa digoyahkan.

Tapi developer yang benar-benar produktif tidak bekerja dalam satu garis lurus — mereka bekerja di banyak jalur secara bersamaan. Di bab berikutnya, kita kuasai **Branch & Merge** — senjata yang mengubah Anda dari developer solo menjadi pemain tim yang sesungguhnya. 🌿

---
*Sebelumnya: [Part 2 — Instalasi Git di macOS](Part-02-Instalasi-Git-di-macOS.md)*
*Selanjutnya: [Part 4 — Branch & Merge: Dunia Paralel](Part-04-Branch-dan-Merge.md)*
