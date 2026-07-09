![Difficulty: Beginner](https://img.shields.io/badge/Tingkat-Pemula-brightgreen?style=for-the-badge)
![Time: 25 Mins](https://img.shields.io/badge/Durasi-25_Menit-blue?style=for-the-badge)
![Practice: Hands-On](https://img.shields.io/badge/Metode-Hands--On_Practice-red?style=for-the-badge)

# 📸 Mulai Merekam Sejarah: Perintah Dasar Git yang Wajib Dikuasai

Sudah cukup teori. Saatnya tangan kita kotor dan kita rasakan sendiri bagaimana Git bekerja.

Di bab ini, kita akan membangun sebuah proyek kecil dari nol dan merekam setiap perkembangannya menggunakan Git. Pada akhir bab ini, Anda tidak hanya hafal perintah-perintahnya — Anda akan benar-benar *mengerti* mengapa setiap perintah itu ada.

## 📋 Daftar Isi
- [Siklus Kerja Git (The Big Picture)](#-siklus-kerja-git-the-big-picture)
- [git init — Menyalakan Mesin Waktu](#-git-init--menyalakan-mesin-waktu)
- [git status — Kaca Spion Ajaib](#-git-status--kaca-spion-ajaib)
- [git add — Memilih Objek untuk Difoto](#-git-add--memilih-objek-untuk-difoto)
- [git commit — Mengambil Foto & Menyimpan Sejarah](#-git-commit--mengambil-foto--menyimpan-sejarah)
- [git log — Membuka Buku Sejarah](#-git-log--membuka-buku-sejarah)
- [git diff — Melihat Apa yang Berubah](#-git-diff--melihat-apa-yang-berubah)
- [Praktik Langsung: Rekam Proyek Pertama Anda](#-praktik-langsung-rekam-proyek-pertama-anda)

---

## 🗺️ Siklus Kerja Git (The Big Picture)

Sebelum kita mengetik satu perintah pun, pahami dulu alur ini. Semua perintah di bab ini berputar pada tiga "area" berikut:

```
┌─────────────────────────────────────────────────────────┐
│                     KOMPUTER ANDA                        │
│                                                         │
│  ┌──────────────┐   git add   ┌─────────────┐           │
│  │  Working     │ ──────────► │   Staging   │           │
│  │  Directory   │             │    Area     │           │
│  │  (File Anda) │ ◄────────── │  (Ruang     │           │
│  │              │  git restore│   Tunggu)   │           │
│  └──────────────┘             └──────┬──────┘           │
│                                      │ git commit        │
│                                      ▼                   │
│                               ┌─────────────┐           │
│                               │  Repository │           │
│                               │  (.git)     │           │
│                               │  (Sejarah)  │           │
│                               └─────────────┘           │
└─────────────────────────────────────────────────────────┘
```

- **Working Directory**: Folder biasa tempat Anda menulis kode.
- **Staging Area**: "Ruang tunggu" — tempat Anda memilih perubahan mana yang akan dimasukkan ke dalam foto berikutnya.
- **Repository (.git)**: Tempat semua foto (*commit*) tersimpan secara permanen.

Analogi dunia nyata: Anda sedang memotret ruang tamu untuk dijual. **Working Directory** = ruang tamu aslinya. **Staging Area** = saat Anda memilih sudut dan objek yang ingin masuk ke frame. **Commit** = saat Anda menekan tombol rana dan foto tersimpan.

---

## 🔧 git init — Menyalakan Mesin Waktu

Perintah ini mengubah folder biasa menjadi repositori Git. Cukup dijalankan **sekali** di awal proyek.

```bash
# Buat folder proyek baru
mkdir proyek-pertama-saya

# Masuk ke dalam folder tersebut
cd proyek-pertama-saya

# Nyalakan mesin waktu Git di folder ini!
git init
```

**Output yang akan Anda lihat:**
```
Initialized empty Git repository in C:/Users/Anda/proyek-pertama-saya/.git/
```

Git diam-diam membuat folder tersembunyi bernama `.git` di dalam proyek Anda. Folder inilah yang menyimpan seluruh sejarah, konfigurasi, dan "otak" dari mesin waktu Anda. **Jangan pernah menghapus folder `.git` secara manual**, kecuali Anda memang ingin menghancurkan seluruh sejarah proyek.

> 💡 **PRO TIP:**
> Ingin melihat folder `.git` yang tersembunyi? Di Git Bash, ketik `ls -la`. Flag `-a` menampilkan file tersembunyi. Di Windows Explorer, aktifkan "Show hidden items" di tab View.

---

## 👁️ git status — Kaca Spion Ajaib

Ini adalah perintah yang akan Anda ketik paling sering. `git status` memberitahu Anda kondisi terkini dari ketiga area di atas — apa yang berubah, apa yang belum di-*staging*, apa yang sudah siap di-*commit*.

```bash
git status
```

Biasakan diri untuk menjalankan `git status` **sebelum dan sesudah** setiap operasi Git. Jadikan ini refleks Anda.

**Output di repositori yang baru saja di-init:**
```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

---

## 📦 git add — Memilih Objek untuk Difoto

Setelah Anda membuat atau mengubah file, Git akan *mendeteksinya* tapi **tidak otomatis menyimpannya**. Anda harus secara eksplisit memilih perubahan mana yang ingin Anda masukkan ke dalam *commit* berikutnya.

```bash
# Tambahkan satu file spesifik ke staging area
git add nama-file.html

# Tambahkan semua file yang berubah sekaligus (paling sering dipakai)
git add .

# Tambahkan semua file dengan ekstensi tertentu
git add *.css
```

> ⚠️ **PERINGATAN: Jebakan `git add .`**
> Perintah `git add .` menambahkan **semua** file yang berubah — termasuk file yang seharusnya tidak masuk ke dalam repositori, seperti file `.env` (berisi password!), folder `node_modules/` (berisi ribuan file), atau file sementara editor.
>
> Selalu buat file **`.gitignore`** di awal proyek untuk mendaftarkan file/folder yang ingin Anda abaikan. Kita akan bahas ini lebih dalam di section berikutnya.

---

## 📸 git commit — Mengambil Foto & Menyimpan Sejarah

Ini adalah inti dari segalanya. `git commit` mengambil semua yang ada di *staging area* dan menyimpannya sebagai satu "foto" permanen dalam sejarah repositori Anda.

```bash
# Format standar — flag -m untuk menulis pesan langsung di terminal
git commit -m "Pesan commit yang deskriptif di sini"
```

**Contoh pesan commit yang baik vs buruk:**

| ❌ Pesan yang Buruk | ✅ Pesan yang Baik |
|---|---|
| `update` | `Tambah validasi form login` |
| `fix bug` | `Perbaiki error kalkulasi harga saat diskon 100%` |
| `asdfgh` | `Hapus file .env yang tidak sengaja ter-commit` |
| `final` | `Rilis versi 1.2.0 — tambah fitur export PDF` |

> 💡 **PRO TIP: Aturan Emas Commit Message**
> Pesan commit yang baik harus bisa melengkapi kalimat ini:
> *"Jika commit ini diterapkan, maka ia akan..."*
>
> "...Tambah validasi form login." ✅
> "...update." ❌ (Update apa? Tidak informatif sama sekali)
>
> Anda mungkin berpikir ini lebay untuk proyek pribadi. Tapi bayangkan Anda membuka sejarah kode 6 bulan dari sekarang dan melihat deretan pesan `update`, `fix`, `final2`, `final_beneran`. Kepada siapa Anda akan menyalahkan diri sendiri? 😄

---

## 📖 git log — Membuka Buku Sejarah

Setelah beberapa *commit*, gunakan perintah ini untuk melihat seluruh sejarah yang telah terekam:

```bash
# Tampilkan log lengkap (tekan Q untuk keluar)
git log

# Versi ringkas yang lebih nyaman dibaca — SANGAT DIREKOMENDASIKAN
git log --oneline

# Tampilkan log dengan grafik branch (berguna setelah belajar branching)
git log --oneline --graph --all
```

**Contoh output `git log --oneline`:**
```
a3f8c12 (HEAD -> main) Tambah halaman kontak
7b2e904 Perbaiki layout header di mobile
1d9c331 Inisialisasi proyek — tambah index.html dan style.css
```

Setiap baris adalah satu *commit*. Kode acak di kiri (`a3f8c12`) adalah **hash** — ID unik dari setiap commit. `HEAD -> main` menunjukkan posisi Anda saat ini.

---

## 🔍 git diff — Melihat Apa yang Berubah

Sebelum men-*staging* atau men-*commit*, kadang Anda ingin melihat persis perubahan apa yang terjadi baris per baris:

```bash
# Lihat perubahan yang belum di-staging
git diff

# Lihat perubahan yang sudah di-staging (sudah git add, belum git commit)
git diff --staged
```

Output `git diff` menggunakan format:
- Baris diawali `+` (hijau) = **baris baru** yang ditambahkan
- Baris diawali `-` (merah) = **baris lama** yang dihapus

---

## 🧪 Praktik Langsung: Rekam Proyek Pertama Anda

Teori sudah cukup. Mari lakukan semuanya dari awal sampai akhir:

```bash
# 1. Buat dan masuk ke folder proyek
mkdir latihan-git
cd latihan-git

# 2. Inisialisasi repositori
git init

# 3. Buat file pertama
echo "# Proyek Latihan Git Saya" > README.md

# 4. Cek status — Git sudah mendeteksi file baru
git status
# Output: Untracked files: README.md

# 5. Masukkan file ke staging area
git add README.md

# 6. Cek status lagi — file sudah hijau (siap di-commit)
git status
# Output: Changes to be committed: new file: README.md

# 7. Simpan sebagai commit pertama
git commit -m "Inisialisasi proyek — tambah README.md"

# 8. Lihat hasilnya!
git log --oneline
# Output: abc1234 (HEAD -> main) Inisialisasi proyek — tambah README.md
```

Sekarang ubah isi `README.md` (buka dengan Notepad atau VS Code, tambahkan teks apapun), lalu ulangi siklus `git add` → `git commit` dan rasakan sendiri bagaimana sejarah mulai terbentuk.

---

## 🎁 Bonus: Membuat .gitignore

File `.gitignore` adalah daftar hitam — Git akan mengabaikan semua file dan folder yang Anda daftarkan di sini.

Buat file `.gitignore` di root folder proyek Anda:

```bash
# Buat file .gitignore
touch .gitignore
```

Lalu isi dengan pola yang ingin diabaikan:

```gitignore
# File environment (JANGAN PERNAH di-commit ke GitHub!)
.env
.env.local

# Folder dependencies (ukurannya bisa ratusan MB)
node_modules/
vendor/

# File cache dan build
.cache/
dist/
build/

# File sistem operasi
.DS_Store        # Mac
Thumbs.db        # Windows

# File editor
.vscode/
.idea/
*.swp
```

> 💡 **PRO TIP: gitignore Generator**
> Tidak perlu buat dari nol. Kunjungi **[gitignore.io](https://www.toptal.com/developers/gitignore)**, masukkan teknologi yang Anda pakai (misal: "Laravel", "Node", "Windows"), dan situs ini akan otomatis membuat `.gitignore` yang komprehensif untuk Anda.

---

Luar biasa! Anda baru saja menguasai inti dari workflow Git sehari-hari: **init → status → add → commit → log**. Ini adalah siklus yang akan Anda ulang ratusan kali dalam karier Anda.

Tapi Git punya senjata rahasia paling powerful yang belum kita sentuh: kemampuan untuk bercabang dan membuat dunia paralel. Di bab berikutnya, kita akan menguasai **Branch** dan **Merge** — fitur yang mengubah Git dari sekadar "undo button" menjadi mesin kolaborasi kelas dunia. 🌿

---
*Sebelumnya: [Part 2 — Instalasi Git di Windows](Part-02-Instalasi-Git-di-Windows.md)*
*Selanjutnya: [Part 4 — Mengenal Branch & Merge: Dunia Paralel](Part-04-Branch-dan-Merge.md)*
