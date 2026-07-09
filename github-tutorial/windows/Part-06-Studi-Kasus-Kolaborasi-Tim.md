![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 35 Mins](https://img.shields.io/badge/Durasi-35_Menit-blue?style=for-the-badge)
![Type: Study Case](https://img.shields.io/badge/Tipe-Studi_Kasus_Nyata-purple?style=for-the-badge)

# 🎬 Studi Kasus: Satu Hari Bekerja Seperti Developer Profesional

Ini bukan lagi tutorial tentang perintah-perintah Git.

Ini adalah **simulasi dunia nyata**. Kita akan menapaki satu skenario lengkap dari awal hingga akhir — persis seperti yang terjadi setiap hari di tim developer startup, agensi web, dan perusahaan teknologi di seluruh dunia.

Karakternya: **Anda** (developer baru), dan **Sari** (rekan satu tim Anda).

Proyeknya: Website portofolio tim yang sedang dikembangkan bersama.

Ambil kopi Anda. Saatnya bekerja. ☕

## 📋 Daftar Isi
- [Skenario: Bergabung dengan Tim yang Sudah Jalan](#-skenario-bergabung-dengan-tim-yang-sudah-jalan)
- [Babak 1: Setup Hari Pertama](#-babak-1-setup-hari-pertama)
- [Babak 2: Mengerjakan Fitur di Branch Terpisah](#-babak-2-mengerjakan-fitur-di-branch-terpisah)
- [Babak 3: Membuat Pull Request di GitHub](#-babak-3-membuat-pull-request-di-github)
- [Babak 4: Code Review & Revisi](#-babak-4-code-review--revisi)
- [Babak 5: Menyelesaikan Merge Conflict dengan Tenang](#-babak-5-menyelesaikan-merge-conflict-dengan-tenang)
- [Babak 6: Kode Anda Masuk ke Production](#-babak-6-kode-anda-masuk-ke-production)
- [Cheat Sheet: Referensi Perintah Git Lengkap](#-cheat-sheet-referensi-perintah-git-lengkap)

---

## 📖 Skenario: Bergabung dengan Tim yang Sudah Jalan

Anda baru saja bergabung sebagai developer di sebuah tim kecil. Manajer Anda, **Budi**, mengirimkan pesan:

> *"Halo! Selamat bergabung. Link repo GitHub proyek kita ada di sini: `https://github.com/tim-kita/website-portofolio`. Tugas pertama Anda: tambahkan section 'Tim Kami' di halaman utama. Jangan lupa pakai workflow branch ya, jangan langsung push ke main!"*

Anda buka laptop. Saatnya bekerja.

---

## 🔨 Babak 1: Setup Hari Pertama

Langkah pertama selalu sama: dapatkan salinan kode proyek di laptop Anda.

```bash
# 1. Clone repositori tim ke laptop Anda
git clone https://github.com/tim-kita/website-portofolio.git

# 2. Masuk ke folder proyek
cd website-portofolio

# 3. Lihat struktur yang sudah ada
ls -la

# 4. Lihat branch yang tersedia
git branch -a
# Output:
# * main
#   remotes/origin/HEAD -> origin/main
#   remotes/origin/main
#   remotes/origin/fitur/halaman-blog  ← branch milik Sari yang sedang jalan

# 5. Lihat sejarah commit yang sudah ada
git log --oneline
# Output:
# c8f3a21 (HEAD -> main, origin/main) Tambah section hero homepage
# 7b2e904 Setup awal — index.html, style.css, script.js
# 1d9c331 Inisialisasi repositori
```

Anda sudah punya gambaran lengkap tentang kondisi proyek. Sari sedang mengerjakan halaman blog di branch terpisah, dan kode utama sudah ada 3 commit. Bagus.

---

## 🌿 Babak 2: Mengerjakan Fitur di Branch Terpisah

**ATURAN EMAS yang tidak boleh dilanggar**: Jangan pernah coding langsung di branch `main`. Selalu buat branch baru untuk setiap tugas.

```bash
# 1. Pastikan main Anda up-to-date sebelum bercabang
git switch main
git pull

# 2. Buat branch baru dengan nama yang deskriptif
git switch -c fitur/section-tim-kami

# 3. Konfirmasi Anda sudah di branch yang benar
git branch
# Output:
#   main
# * fitur/section-tim-kami   ← ada tanda * di sini
```

Sekarang Anda sudah berada di "ruang kerja pribadi" Anda. Buka VS Code dan mulai coding.

**Anda mengedit `index.html` dan menambahkan section baru:**

```html
<!-- Section baru yang Anda tambahkan di index.html -->
<section id="tim-kami">
  <h2>Tim Kami</h2>
  <div class="grid-tim">
    <div class="kartu-anggota">
      <img src="foto/budi.jpg" alt="Foto Budi">
      <h3>Budi Santoso</h3>
      <p>Project Manager & Backend Developer</p>
    </div>
    <div class="kartu-anggota">
      <img src="foto/sari.jpg" alt="Foto Sari">
      <h3>Sari Dewi</h3>
      <p>Frontend Developer</p>
    </div>
  </div>
</section>
```

**Setelah selesai coding, simpan progress Anda secara bertahap:**

```bash
# Cek apa yang berubah
git status
# Output:
# On branch fitur/section-tim-kami
# Changes not staged for commit:
#   modified: index.html

# Lihat detil perubahannya
git diff index.html

# Staging
git add index.html

# Commit dengan pesan yang informatif
git commit -m "Tambah section 'Tim Kami' di homepage dengan 2 kartu anggota"
```

Anda terus coding, menambahkan CSS untuk section tersebut:

```bash
# Setelah mengupdate style.css
git add style.css
git commit -m "Tambah styling kartu anggota untuk section tim-kami"
```

Sekarang branch Anda punya 2 commit ekstra di atas `main`. Waktunya kirim ke GitHub.

```bash
# Push branch ini ke GitHub untuk pertama kali
git push -u origin fitur/section-tim-kami
```

---

## 🔁 Babak 3: Membuat Pull Request di GitHub

*Push* sudah berhasil. Tapi kode Anda belum masuk ke `main`. Untuk itulah kita butuh **Pull Request (PR)** — sebuah pengajuan resmi yang meminta kode Anda diperiksa dan disetujui sebelum digabungkan.

1. Buka repositori tim di **GitHub**.
2. GitHub biasanya langsung menampilkan banner kuning: *"fitur/section-tim-kami had recent pushes. Compare & pull request"* — klik tombol itu.
3. Isi formulir Pull Request:

**Title**: `Tambah section Tim Kami di homepage`

**Description**:
```
## Apa yang berubah?
- Menambahkan section baru `#tim-kami` di `index.html`
- Menambahkan styling kartu anggota di `style.css`

## Screenshot
[Tambahkan screenshot tampilan baru di sini]

## Cara mengetes
1. Buka `index.html` di browser
2. Scroll ke bawah hingga section "Tim Kami"
3. Pastikan dua kartu anggota tampil dengan benar

## Catatan
Data anggota tim sementara hardcode dulu. Nanti bisa dihubungkan ke database.
```

4. Di bagian kanan, tambahkan **Reviewers**: pilih nama Budi (manajer Anda).
5. Klik **"Create Pull Request"**.

> 💡 **PRO TIP: Pull Request yang Baik Adalah Surat Cinta untuk Reviewer**
> PR yang baik membuat pekerjaan reviewer semudah mungkin. Jelaskan *apa* yang berubah, *mengapa* berubah, dan *bagaimana* cara memverifikasinya. Reviewer yang bahagia = PR yang cepat disetujui.

---

## 👀 Babak 4: Code Review & Revisi

Budi membuka PR Anda dan meninggalkan komentar di baris tertentu:

> *"Bagus! Tapi gambar foto anggota belum ada di folder `foto/`. Untuk sementara, pakai foto placeholder dulu ya, biar tidak broken di browser. Bisa pakai `https://via.placeholder.com/150`?"*

Anda menerima masukan itu. Di laptop Anda, Anda tidak perlu buat branch baru — cukup tambahkan commit baru di branch yang sama:

```bash
# Pastikan Anda masih di branch yang benar
git branch
# * fitur/section-tim-kami ✅

# Edit index.html — ganti src foto ke placeholder
# ... (edit di VS Code) ...

git add index.html
git commit -m "Ganti foto anggota dengan placeholder sementara sesuai review Budi"

# Push commit tambahan ini — otomatis masuk ke PR yang sama
git push
```

PR Anda di GitHub secara otomatis terupdate. Budi melihat revisi Anda dan menyetujuinya dengan menambahkan label ✅ **Approved**.

---

## ⚔️ Babak 5: Menyelesaikan Merge Conflict dengan Tenang

Tepat ketika Budi ingin meng-*merge* PR Anda, GitHub menampilkan peringatan merah:

> *"This branch has conflicts that must be resolved"*

Ternyata, selama Anda mengerjakan section tim, **Sari** juga melakukan perubahan di `index.html` untuk menambahkan navigasi ke halaman blog-nya — dan perubahan itu sudah lebih dulu masuk ke `main`.

Jangan panik. Ini situasi normal dan ada solusinya.

```bash
# 1. Kembali ke main dan ambil versi terbaru
git switch main
git pull

# 2. Kembali ke branch Anda
git switch fitur/section-tim-kami

# 3. Gabungkan versi terbaru main ke branch Anda (bukan sebaliknya!)
git merge main
```

**Output:**
```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

Buka `index.html` di VS Code. Anda akan melihat tanda conflict:

```html
<<<<<<< HEAD
<!-- Kode Anda: section tim-kami -->
<section id="tim-kami">
  <h2>Tim Kami</h2>
  ...
</section>
=======
<!-- Kode Sari: link navigasi blog -->
<nav>
  <a href="blog.html">Blog Tim</a>
</nav>
>>>>>>> main
```

Dalam kasus ini, **kedua perubahan harus dipertahankan**. Anda cukup hapus tanda conflict dan gabungkan keduanya secara logis:

```html
<!-- Hasil setelah conflict diselesaikan — kedua perubahan dipertahankan -->
<nav>
  <a href="blog.html">Blog Tim</a>
</nav>

<section id="tim-kami">
  <h2>Tim Kami</h2>
  ...
</section>
```

```bash
# Simpan file, lalu selesaikan merge
git add index.html
git commit -m "Selesaikan merge conflict dengan branch main — gabungkan nav blog dan section tim"

# Push hasilnya ke GitHub
git push
```

GitHub kini menampilkan: ✅ *"This branch has no conflicts with the base branch"*. Budi bisa meng-*merge* PR Anda.

---

## 🎉 Babak 6: Kode Anda Masuk ke Production

Budi menekan tombol **"Merge pull request"** → **"Confirm merge"** di GitHub.

Selamat! Kode Anda resmi bergabung dengan branch `main`. 

Sekarang bersihkan sisa-sisa pekerjaan Anda:

```bash
# 1. Kembali ke main lokal
git switch main

# 2. Ambil versi terbaru (yang sudah menyertakan kode Anda)
git pull

# 3. Hapus branch yang sudah tidak dibutuhkan (lokal)
git branch -d fitur/section-tim-kami

# 4. Hapus branch dari GitHub juga
git push origin --delete fitur/section-tim-kami
```

```bash
# Lihat sejarah — kode Anda kini tercatat selamanya
git log --oneline
# Output:
# f4c2b81 (HEAD -> main, origin/main) Merge pull request #3: Tambah section Tim Kami
# a1d9e22 Selesaikan merge conflict dengan branch main
# 7c3f001 Ganti foto anggota dengan placeholder sementara
# 9b2a445 Tambah styling kartu anggota untuk section tim-kami
# e8f3c12 Tambah section 'Tim Kami' di homepage
# c8f3a21 Tambah section hero homepage  ← commit milik Sari
# ...
```

Setiap commit Anda terdokumentasi dengan jelas. Siapa yang mengubah apa, kapan, dan mengapa — semuanya terekam untuk selamanya.

---

## 📜 Cheat Sheet: Referensi Perintah Git Lengkap

Simpan ini. Tempel di dinding. Anda akan membutuhkannya.

```bash
# ═══════════════════════════════
# SETUP & KONFIGURASI
# ═══════════════════════════════
git config --global user.name "Nama Anda"      # Set identitas nama
git config --global user.email "email@anda.com" # Set identitas email
git config --list                               # Lihat semua konfigurasi

# ═══════════════════════════════
# MEMULAI REPOSITORI
# ═══════════════════════════════
git init                                        # Buat repo baru di folder saat ini
git clone <url>                                 # Salin repo dari GitHub

# ═══════════════════════════════
# SIKLUS KERJA HARIAN
# ═══════════════════════════════
git status                                      # Cek kondisi saat ini
git add <file>                                  # Staging satu file
git add .                                       # Staging semua perubahan
git commit -m "pesan"                           # Simpan snapshot
git diff                                        # Lihat perubahan yang belum di-staging
git diff --staged                               # Lihat perubahan yang sudah di-staging

# ═══════════════════════════════
# MELIHAT SEJARAH
# ═══════════════════════════════
git log                                         # Log lengkap
git log --oneline                               # Log ringkas (satu baris per commit)
git log --oneline --graph --all                 # Log dengan visualisasi branch

# ═══════════════════════════════
# BRANCH
# ═══════════════════════════════
git branch                                      # Lihat semua branch lokal
git branch -a                                   # Lihat semua branch (lokal + remote)
git branch <nama>                               # Buat branch baru
git switch <nama>                               # Pindah ke branch
git switch -c <nama>                            # Buat branch baru + langsung pindah
git branch -d <nama>                            # Hapus branch (yang sudah di-merge)
git branch -D <nama>                            # Hapus branch paksa

# ═══════════════════════════════
# MERGE
# ═══════════════════════════════
git merge <branch>                              # Gabungkan branch ke branch aktif
git merge --abort                               # Batalkan merge yang sedang konflik

# ═══════════════════════════════
# GITHUB (REMOTE)
# ═══════════════════════════════
git remote add origin <url>                     # Daftarkan remote GitHub
git remote -v                                   # Lihat remote yang terdaftar
git push -u origin <branch>                     # Push pertama kali (set upstream)
git push                                        # Push selanjutnya
git pull                                        # Ambil & gabungkan perubahan dari GitHub
git fetch                                       # Ambil perubahan dari GitHub (tanpa merge)
git push origin --delete <branch>               # Hapus branch dari GitHub

# ═══════════════════════════════
# DARURAT & PEMBATALAN
# ═══════════════════════════════
git restore <file>                              # Batalkan perubahan yang belum di-staging
git restore --staged <file>                     # Keluarkan file dari staging area
git commit --amend -m "pesan baru"              # Edit pesan commit TERAKHIR (sebelum push!)
git revert <hash>                               # Batalkan commit dengan membuat commit baru
```

---

## 🏆 Penutup: Anda Sudah Bukan Pemula Lagi

Selamat. Dengan selesainya seri tutorial ini, Anda telah menjalani perjalanan lengkap:

- ✅ Memahami filosofi Git dan perbedaannya dengan GitHub
- ✅ Menginstal dan mengkonfigurasi Git di Windows dengan benar
- ✅ Menguasai siklus `init → add → commit → log` untuk merekam sejarah kode
- ✅ Menggunakan `branch` dan `merge` untuk bekerja secara paralel tanpa chaos
- ✅ Menghubungkan proyek lokal ke GitHub via `push`, `pull`, dan `clone`
- ✅ Menyelesaikan simulasi kolaborasi tim nyata dengan Pull Request dan Merge Conflict

Git bukan alat yang dipelajari sekali lalu selesai. Ia adalah teman perjalanan yang akan semakin Anda pahami seiring waktu. Setiap kali Anda membuat sebuah commit, Anda sedang menulis sejarah kode Anda sendiri — satu halaman dalam satu waktu.

Sekarang buka VS Code, buat proyek baru, dan mulailah merekam sejarahmu. 🚀

---
*Sebelumnya: [Part 5 — Push, Pull & Clone ke GitHub](Part-05-Push-Pull-Clone-GitHub.md)*

---
> 💡 **Langkah Berikutnya yang Direkomendasikan:**
> - Pelajari **GitHub Actions** untuk otomatisasi testing dan deployment
> - Pelajari **Git Rebase** sebagai alternatif merge yang lebih bersih
> - Mulai berkontribusi ke proyek **open source** — cari issue berlabel `good first issue` di GitHub
