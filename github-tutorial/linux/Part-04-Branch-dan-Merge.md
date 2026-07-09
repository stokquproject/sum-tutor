![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Concept: Core](https://img.shields.io/badge/Konsep-Krusial-orange?style=for-the-badge)

# 🌿 Dunia Paralel: Menguasai Branch & Merge di Linux

Skenario yang sudah pasti akan Anda hadapi:

Anda sedang mengerjakan fitur baru di aplikasi — kode setengah jalan, belum stabil. Tiba-tiba Anda menerima laporan: ada *bug* kritis di production yang harus diperbaiki dalam 30 menit.

Kode yang setengah jadi itu tidak bisa diluncurkan. Tapi *bug* harus ditangani sekarang.

Tanpa Branch: Anda dalam masalah besar.
Dengan Branch: Anda parkir pekerjaan fitur Anda, buat "jalur darurat" terpisah untuk memperbaiki *bug*, selesaikan, rilis — lalu kembali lagi ke fitur yang tadi, tepat di titik Anda berhenti.

## 📋 Daftar Isi
- [Apa Itu Branch? (Model Mental yang Benar)](#-apa-itu-branch-model-mental-yang-benar)
- [git branch — Mengelola Cabang](#-git-branch--mengelola-cabang)
- [git switch — Berpindah Antar Dunia](#-git-switch--berpindah-antar-dunia)
- [git merge — Menyatukan Dua Jalur](#-git-merge--menyatukan-dua-jalur)
- [Menangani Merge Conflict](#-menangani-merge-conflict)
- [git stash — Menyimpan Pekerjaan Sementara](#-git-stash--menyimpan-pekerjaan-sementara)
- [Strategi Branch untuk Tim Profesional](#-strategi-branch-untuk-tim-profesional)

---

## 🌌 Apa Itu Branch? (Model Mental yang Benar)

Secara teknis, **branch** adalah sebuah pointer ringan — hanya sebuah file teks kecil di dalam `.git/refs/heads/` yang menyimpan hash dari satu commit.

Tapi secara konseptual, anggap branch sebagai **jalur rel kereta yang bercabang**:

```
Jalur Utama (main):
○ ── ○ ── ○ ─────────────────── ○ (merge point)
              \                 /
               ○ ── ○ ── ○ ── ○   (branch: fitur/dark-mode)
```

Setelah titik percabangan, commit di `main` dan commit di `fitur/dark-mode` berjalan secara terpisah, tidak saling mempengaruhi. Saat fitur siap, kedua jalur digabungkan kembali di titik *merge*.

**Yang membuat Branch di Git luar biasa ringan:**
- Membuat branch baru = operasi instan, hanya membuat satu file kecil.
- Berpindah branch = operasi cepat, Git mengupdate working tree Anda.
- Tidak ada duplikasi file. Branch hanya menyimpan *perbedaannya* saja.

---

## 🌿 git branch — Mengelola Cabang

```bash
# Lihat semua branch lokal (tanda * = branch aktif)
git branch

# Lihat semua branch termasuk yang ada di remote GitHub
git branch -a

# Lihat branch beserta commit terakhir masing-masing
git branch -v

# Buat branch baru (TIDAK berpindah ke sana)
git branch nama-branch

# Hapus branch yang sudah di-merge
git branch -d nama-branch

# Hapus branch paksa (meski belum di-merge) — hati-hati!
git branch -D nama-branch

# Rename branch yang aktif
git branch -m nama-baru
```

**Konvensi penamaan branch yang dipakai tim profesional:**

```bash
# Format: <tipe>/<deskripsi-singkat-dengan-tanda-hubung>

git branch fitur/sistem-autentikasi
git branch fitur/halaman-profil-user
git branch bugfix/crash-saat-upload-kosong
git branch hotfix/sql-injection-form-login
git branch release/v2.3.0
git branch chore/update-dependensi
```

Konvensi ini bukan hanya estetika — banyak tool CI/CD dan GitHub Actions menggunakan pola nama branch untuk memicu workflow yang berbeda secara otomatis.

---

## 🚪 git switch — Berpindah Antar Dunia

Sejak Git 2.23, perintah resmi untuk berpindah branch adalah `git switch` (menggantikan `git checkout` yang overloaded dengan terlalu banyak fungsi).

```bash
# Pindah ke branch yang sudah ada
git switch main
git switch fitur/sistem-autentikasi

# SHORTCUT FAVORIT: Buat branch baru + langsung pindah
git switch -c fitur/halaman-kontak

# Kembali ke branch sebelumnya (seperti `cd -` di shell)
git switch -

# Verifikasi posisi Anda
git branch          # tanda * menunjukkan branch aktif
git status          # baris pertama menampilkan "On branch ..."
```

> 💡 **PRO TIP: `git switch -` adalah favorit tersembunyi**
> Sama seperti `cd -` di terminal Linux yang kembali ke direktori sebelumnya, `git switch -` membawa Anda kembali ke branch yang baru saja Anda tinggalkan. Sangat berguna saat berpindah bolak-balik antara `main` dan branch fitur.

---

## 🔀 git merge — Menyatukan Dua Jalur

Setelah fitur selesai dikerjakan dan diuji di branch terpisah, gabungkan kembali ke `main`:

```bash
# Langkah 1: Kembali ke branch tujuan (penerima merge)
git switch main

# Langkah 2: Pastikan main Anda up-to-date
git pull   # (jika sudah terhubung ke GitHub)

# Langkah 3: Merge branch fitur ke main
git merge fitur/halaman-kontak
```

**Dua jenis merge yang mungkin terjadi:**

**1. Fast-Forward Merge** (kondisi ideal — tidak ada commit baru di main sejak branching):
```
Sebelum:  main: A─B─C
                     \
          fitur:      D─E─F

Sesudah:  main: A─B─C─D─E─F
```
```
Fast-forward
Updating c8f3a21..f4c2b81
index.html | 12 ++++++++++++
1 file changed, 12 insertions(+)
```

**2. Recursive/3-Way Merge** (ada commit baru di main sejak branching):
```
Sebelum:  main: A─B─C─G
                     \
          fitur:      D─E─F

Sesudah:  main: A─B─C─G─M (M = merge commit baru)
                     \ /
                      D─E─F
```
Git secara otomatis membuat "merge commit" `M` yang menyatukan dua jalur.

**Bersihkan branch setelah merge:**
```bash
# Hapus branch lokal yang sudah tidak dibutuhkan
git branch -d fitur/halaman-kontak
```

---

## ⚔️ Menangani Merge Conflict

*Merge conflict* terjadi ketika dua branch mengubah **baris yang sama** pada file yang sama. Git tidak bisa memutuskan versi mana yang benar, jadi ia meminta Anda memutuskan.

**Deteksi conflict:**
```bash
git merge fitur/halaman-about
# Auto-merging index.html
# CONFLICT (content): Merge conflict in index.html
# Automatic merge failed; fix conflicts and then commit the result.
```

**Cek file mana yang conflict:**
```bash
git status
# both modified: index.html   ← ini file yang perlu diselesaikan
```

**Buka file conflict — Anda akan melihat marker ini:**

```html
<<<<<<< HEAD
<!-- Versi dari branch main (HEAD = posisi Anda sekarang) -->
<title>Website Portofolio - Ahmad</title>
=======
<!-- Versi dari branch yang di-merge -->
<title>Portfolio Ahmad Fauzi | Backend Developer</title>
>>>>>>> fitur/halaman-about
```

**Tiga pilihan penyelesaian:**

```bash
# PILIHAN 1: Terima versi HEAD (main) — buang perubahan dari branch
git checkout --ours index.html

# PILIHAN 2: Terima versi branch yang di-merge — buang versi main
git checkout --theirs index.html

# PILIHAN 3: Edit manual (paling sering dibutuhkan)
# Buka file, hapus semua marker <<<<, ====, >>>>, 
# tulis versi final yang Anda inginkan, simpan.
nano index.html
```

**Selesaikan conflict:**
```bash
# Setelah selesai edit, staging file yang sudah diselesaikan
git add index.html

# Jika ada file conflict lain, selesaikan semua dulu, baru commit
git commit -m "Selesaikan merge conflict di index.html — gabungkan judul halaman"
```

**Batalkan merge jika terlalu rumit:**
```bash
# Kembali ke kondisi sebelum merge dimulai
git merge --abort
```

> 💡 **PRO TIP: Gunakan `git mergetool`**
> Linux punya banyak pilihan visual merge tool. Untuk melihat pilihan yang tersedia:
> ```bash
> git mergetool --tool-help
> ```
> Tool seperti `vimdiff`, `meld`, atau `kdiff3` menampilkan perbandingan tiga panel (base, ours, theirs) yang jauh lebih mudah dibaca daripada teks mentah. Install `meld` dengan `sudo apt install meld` dan set sebagai default: `git config --global merge.tool meld`

---

## 🗄️ git stash — Menyimpan Pekerjaan Sementara

Situasi: Anda sedang coding di tengah jalan, belum siap untuk commit, tapi perlu berpindah branch segera. `git stash` adalah solusinya.

Anggap `stash` seperti **laci darurat** — Anda menyembunyikan pekerjaan yang setengah jadi, berpindah ke tempat lain untuk mengerjakan hal mendesak, lalu kembali dan membuka laci untuk melanjutkan dari titik yang sama.

```bash
# Simpan semua perubahan yang belum di-commit ke stash
git stash

# Atau dengan label deskriptif (sangat direkomendasikan)
git stash push -m "WIP: form validasi login belum selesai"

# Sekarang working tree bersih — bisa berpindah branch
git switch main

# ... kerjakan hal mendesak, commit, lalu kembali ...

git switch fitur/sistem-autentikasi

# Ambil kembali pekerjaan dari stash
git stash pop

# Lihat semua stash yang tersimpan
git stash list
# stash@{0}: On fitur/sistem-autentikasi: WIP: form validasi login belum selesai

# Terapkan stash tanpa menghapusnya dari daftar
git stash apply stash@{0}

# Hapus semua stash
git stash clear
```

---

## 🏛️ Strategi Branch untuk Tim Profesional

**GitHub Flow** — Sederhana, cocok untuk deployment cepat:

```
main  ●────────────────────────────────●
       \          \                   /
        ●─●─●      ●─●─●─●           /
        (bugfix)   (fitur baru)      ●
                                  (merge via PR)
```

Aturan:
1. `main` selalu dalam kondisi stabil dan siap di-deploy.
2. Setiap pekerjaan — fitur baru, bugfix, hotfix — dikerjakan di branch terpisah.
3. Gabungkan ke `main` hanya melalui *Pull Request* yang sudah di-review.

**Git Flow** — Lebih terstruktur, cocok untuk software dengan siklus rilis:

```
main     ●────────────────────────────●  (hanya commit rilis resmi)
          \                          /
develop    ●──●──●──●──●──●──●──●──●   (integrasi semua fitur)
                \       \
                 ●─●─●   ●─●          (branch fitur)
```

Untuk pemula, mulai dengan **GitHub Flow**. Sederhana dan sudah digunakan oleh mayoritas tim modern.

---

Anda kini memiliki senjata yang digunakan oleh tim engineering di startup hingga perusahaan Fortune 500. Branch adalah fondasi dari setiap workflow kolaborasi profesional yang ada.

Satu hal besar tersisa: semua yang kita kerjakan masih hidup di mesin lokal Anda. Saatnya menghubungkannya ke dunia luar via GitHub — dan di sini, Linux punya senjata rahasia yang tidak dimiliki sistem lain: **SSH Key Authentication** yang elegan dan aman. 🔐

---
*Sebelumnya: [Part 3 — Perintah Dasar Git](Part-03-Perintah-Dasar-Git.md)*
*Selanjutnya: [Part 5 — Menghubungkan ke GitHub dengan SSH](Part-05-SSH-Push-Pull-Clone-GitHub.md)*
