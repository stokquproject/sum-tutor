![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Concept: Core](https://img.shields.io/badge/Konsep-Krusial-orange?style=for-the-badge)

# 🌿 Dunia Paralel: Menguasai Branch & Merge

Bayangkan Anda sedang mengerjakan website toko online. Tiba-tiba, klien Anda menelepon panik: ada *bug* kritis di halaman pembayaran yang harus diperbaiki dalam 1 jam.

Masalahnya — Anda sedang di tengah-tengah mengerjakan fitur baru "Wishlist" yang belum selesai dan belum siap diluncurkan. Kode Anda berantakan di mana-mana.

**Tanpa Branch**: Anda panik. Anda terpaksa memilih antara menyelesaikan bug dulu (dan meninggalkan kode Wishlist yang setengah jadi) atau menunda perbaikan bug (dan klien marah).

**Dengan Branch**: Anda tenang. Anda buat cabang baru untuk *bug fix*, perbaiki masalahnya, selesaikan, gabungkan ke kode utama — semua itu tanpa menyentuh setitik pun kode Wishlist yang sedang Anda kerjakan. Sihir.

## 📋 Daftar Isi
- [Apa Itu Branch? (Analogi Linimasa Paralel)](#-apa-itu-branch-analogi-linimasa-paralel)
- [git branch — Melihat & Membuat Cabang](#-git-branch--melihat--membuat-cabang)
- [git checkout / git switch — Berpindah Linimasa](#-git-checkout--git-switch--berpindah-linimasa)
- [git merge — Menyatukan Dunia Paralel](#-git-merge--menyatukan-dunia-paralel)
- [Menangani Merge Conflict (Jangan Panik!)](#-menangani-merge-conflict-jangan-panik)
- [Strategi Branch yang Dipakai Tim Profesional](#-strategi-branch-yang-dipakai-tim-profesional)

---

## 🌌 Apa Itu Branch? (Analogi Linimasa Paralel)

Dalam dunia Marvel, ada konsep *multiverse* — dimana keputusan berbeda menciptakan linimasa yang berbeda, berjalan secara paralel tanpa saling mengganggu satu sama lain.

**Branch di Git bekerja persis seperti itu.**

Secara teknis, branch adalah sebuah *pointer* ringan yang menunjuk ke satu *commit* tertentu. Ketika Anda membuat branch baru dan mulai membuat *commit* di dalamnya, Anda membangun sejarah yang berbeda tanpa mengganggu branch `main` (linimasa utama) Anda.

```
Linimasa Utama (main):
    A ── B ── C ─────────────── G (merge)
                 \             /
                  D ── E ── F   (branch: fitur-wishlist)
```

Commit `A, B, C` ada di branch `main`. Pada titik `C`, Anda membuat branch baru `fitur-wishlist` dan membuat commit `D, E, F` di dalamnya. Kode di `main` tetap bersih di `C`. Saat fitur siap, `D, E, F` digabungkan menjadi commit `G` di `main`.

---

## 🌿 git branch — Melihat & Membuat Cabang

```bash
# Lihat semua branch yang ada (branch aktif ditandai tanda *)
git branch

# Buat branch baru (tapi TIDAK berpindah ke sana)
git branch nama-branch-baru

# Contoh nyata:
git branch fitur-halaman-kontak
git branch bugfix-form-login
git branch eksperimen-dark-mode
```

**Konvensi penamaan branch yang profesional:**
```
fitur/halaman-kontak      → untuk fitur baru
bugfix/form-login-error   → untuk perbaikan bug
hotfix/payment-crash      → untuk bug kritis di production
release/v1.2.0            → untuk persiapan rilis
```

> 💡 **PRO TIP:**
> Gunakan nama branch yang deskriptif. Branch bernama `coba2` atau `test` adalah tanda tanya besar bagi seluruh tim. Nama seperti `fitur/dark-mode` atau `bugfix/harga-diskon-salah-hitung` langsung memberi tahu semua orang apa yang sedang Anda kerjakan.

---

## 🚪 git checkout / git switch — Berpindah Linimasa

Membuat branch baru tidak otomatis memindahkan Anda ke sana. Gunakan perintah ini untuk berpindah:

```bash
# Cara modern (Git 2.23+) — lebih jelas dan direkomendasikan
git switch nama-branch

# Cara lama yang masih valid (banyak tutorial lama pakai ini)
git checkout nama-branch

# SHORTCUT FAVORIT: Buat branch baru DAN langsung pindah ke sana
git switch -c fitur-halaman-kontak
# atau dengan cara lama:
git checkout -b fitur-halaman-kontak
```

Shortcut di atas (`-c` atau `-b`) adalah kombinasi `git branch` + `git switch` dalam satu perintah. Ini yang paling sering Anda gunakan dalam praktik sehari-hari.

**Cara mengetahui Anda sedang di branch mana:**
```bash
git branch
# Output:
#   main
# * fitur-halaman-kontak   ← tanda * menunjukkan branch aktif Anda

# Atau lihat di git status:
git status
# On branch fitur-halaman-kontak
```

---

## 🔀 git merge — Menyatukan Dunia Paralel

Setelah fitur Anda selesai di branch terpisah dan sudah diuji dengan baik, saatnya menggabungkannya kembali ke branch utama.

```bash
# Langkah 1: Kembali ke branch tujuan (biasanya main)
git switch main

# Langkah 2: Gabungkan branch yang ingin dimasukkan
git merge fitur-halaman-kontak
```

**Output untuk merge yang mulus (Fast-Forward):**
```
Updating 7b2e904..a3f8c12
Fast-forward
 kontak.html | 45 +++++++++++++++++++++
 style.css   |  8 ++++
 2 files changed, 53 insertions(+)
```

Setelah merge berhasil, branch `fitur-halaman-kontak` tidak lagi dibutuhkan. Hapus untuk menjaga kebersihan repositori:

```bash
git branch -d fitur-halaman-kontak
```

---

## ⚔️ Menangani Merge Conflict (Jangan Panik!)

*Merge conflict* terjadi ketika dua branch mengubah **baris yang sama persis** pada file yang sama, dan Git tidak bisa memutuskan versi mana yang harus dipertahankan.

Ini terdengar menakutkan, tapi sebenarnya ini adalah Git sedang *berlaku jujur* kepada Anda: "Hei, ada dua versi berbeda di sini. Tolong beritahu aku mana yang benar."

**Saat conflict terjadi, output Git akan terlihat seperti:**
```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

**Buka file yang conflict (`index.html`), dan Anda akan menemukan tanda seperti ini:**

```html
<<<<<<< HEAD
<h1>Selamat Datang di Toko Kami</h1>
=======
<h1>Selamat Datang di Toko Online Kita!</h1>
>>>>>>> fitur-halaman-kontak
```

**Cara membacanya:**
- `<<<<<<< HEAD` — ini adalah versi dari branch aktif Anda (`main`)
- `=======` — pemisah antara dua versi
- `>>>>>>> fitur-halaman-kontak` — ini adalah versi dari branch yang sedang di-merge

**Cara menyelesaikannya:**
1. Edit file tersebut secara manual. Hapus semua tanda `<<<<<<<`, `=======`, `>>>>>>>` dan pilih (atau gabungkan) teks yang benar.
2. Simpan file.
3. Jalankan `git add` pada file yang sudah diperbaiki.
4. Jalankan `git commit` untuk menyelesaikan merge.

```bash
# Setelah Anda selesai mengedit file conflict
git add index.html
git commit -m "Selesaikan merge conflict di index.html"
```

> 💡 **PRO TIP: Gunakan VS Code untuk Resolve Conflict**
> VS Code punya antarmuka visual yang luar biasa untuk menyelesaikan *merge conflict*. Ia akan menampilkan tombol "Accept Current Change", "Accept Incoming Change", dan "Accept Both Changes" langsung di atas setiap blok konflik. Jauh lebih mudah daripada mengedit teks mentah.

---

## 🏛️ Strategi Branch yang Dipakai Tim Profesional

Untuk proyek serius, tim profesional biasanya menggunakan strategi branch yang terstruktur. Berikut yang paling populer dan ramah pemula:

**GitHub Flow** (Simpel, cocok untuk deployment cepat):

```
main           ← Kode yang selalu siap production
  │
  ├── fitur/a  ← Kerjakan fitur di sini
  ├── fitur/b  ← Kerjakan fitur lain di sini
  └── hotfix/c ← Perbaiki bug kritis di sini
```

Aturannya sederhana:
1. `main` selalu stabil dan siap diluncurkan.
2. Setiap pekerjaan baru (fitur, bugfix) dibuat di branch terpisah.
3. Setelah selesai dan diulas, branch digabungkan ke `main` via *Pull Request* di GitHub.

---

Anda baru saja menguasai salah satu konsep paling powerful dalam dunia rekayasa perangkat lunak. Branch adalah alasan mengapa tim besar seperti tim engineering Google atau Netflix bisa mengerjakan ratusan fitur secara paralel tanpa chaos.

Satu langkah besar tersisa: selama ini semua yang kita kerjakan masih hidup di laptop lokal Anda. Saatnya kita hubungkan mesin waktu lokal ini ke **GitHub** dan kirimkan karya kita ke cloud — agar bisa diakses dari mana saja dan berkolaborasi dengan siapa saja. 🚀

---
*Sebelumnya: [Part 3 — Perintah Dasar Git](Part-03-Perintah-Dasar-Git.md)*
*Selanjutnya: [Part 5 — Menghubungkan ke GitHub: Push, Pull & Clone](Part-05-Push-Pull-Clone-GitHub.md)*
