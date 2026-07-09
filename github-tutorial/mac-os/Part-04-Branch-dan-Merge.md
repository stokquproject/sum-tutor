![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 20 Mins](https://img.shields.io/badge/Durasi-20_Menit-blue?style=for-the-badge)
![Concept: Core](https://img.shields.io/badge/Konsep-Krusial-orange?style=for-the-badge)

# 🌿 Dunia Paralel: Menguasai Branch & Merge di macOS

Satu skenario yang hampir pasti akan Anda alami:

Anda sedang membangun fitur baru untuk aplikasi klien — sudah setengah jalan, kode belum bersih. Tiba-tiba klien menelepon: ada halaman yang error di website yang sedang live, harus diperbaiki sekarang juga.

Tanpa Branch: Anda bingung. Kode setengah jadi tidak bisa diluncurkan, tapi klien tidak bisa menunggu.

Dengan Branch: Anda parkir pekerjaan Anda di "laci khusus", buat jalur darurat yang bersih untuk memperbaiki bug, selesaikan, luncurkan — lalu kembali ke laci Anda dan lanjutkan tepat dari titik yang ditinggalkan.

## 📋 Daftar Isi
- [Apa Itu Branch? (Model Mental yang Benar)](#-apa-itu-branch-model-mental-yang-benar)
- [git branch — Mengelola Cabang](#-git-branch--mengelola-cabang)
- [git switch — Berpindah Konteks Kerja](#-git-switch--berpindah-konteks-kerja)
- [git merge — Menyatukan Hasil Kerja](#-git-merge--menyatukan-hasil-kerja)
- [Menangani Merge Conflict](#-menangani-merge-conflict)
- [git stash — Laci Darurat macOS Anda](#-git-stash--laci-darurat-macos-anda)
- [Visualisasi Branch dengan Git Graph di VS Code](#-visualisasi-branch-dengan-git-graph-di-vs-code)

---

## 🌌 Apa Itu Branch? (Model Mental yang Benar)

Di balik layar, branch di Git hanyalah sebuah file kecil yang menyimpan hash dari satu commit. Tapi secara konseptual, anggap branch sebagai **tab di browser Anda**.

Sama seperti Anda membuka tab baru di Safari untuk mengerjakan sesuatu yang berbeda tanpa menutup tab yang sedang aktif — branch memungkinkan Anda "membuka konteks kerja baru" tanpa merusak konteks yang sudah ada.

```
main:             ●────●────●────────────────●
                                \            ↑
fitur/dark-mode:   \             ●────●────● (merge)
                    \
bugfix/footer:       ●────●  (hotfix cepat, sudah di-merge lebih dulu)
```

Setiap branch berjalan di jalurnya sendiri. Setiap commit hanya mempengaruhi branch yang aktif. Merger menggabungkan hasil akhir.

**Yang membuat Branch Git sangat efisien:**
- Membuat branch baru = instan (microsecond)
- Berpindah branch = cepat, Git memperbarui working tree
- Tidak ada duplikasi file — semua berjalan di `.git/` yang sama

---

## 🌿 git branch — Mengelola Cabang

```zsh
# Lihat semua branch lokal (tanda * = branch aktif)
git branch

# Lihat semua branch termasuk remote
git branch -a

# Lihat branch dengan info commit terakhir
git branch -v

# Buat branch baru (tidak langsung pindah)
git branch nama-branch

# Hapus branch yang sudah di-merge
git branch -d nama-branch

# Hapus branch paksa (hati-hati!)
git branch -D nama-branch

# Rename branch aktif
git branch -m nama-baru
```

**Konvensi penamaan branch yang rapi:**

```zsh
# Format: <tipe>/<deskripsi-singkat>
git branch fitur/halaman-checkout
git branch fitur/dark-mode-ui
git branch bugfix/harga-tidak-tampil
git branch hotfix/payment-gateway-timeout
git branch release/v3.0.0
```

---

## 🚪 git switch — Berpindah Konteks Kerja

Sejak Git 2.23, `git switch` adalah cara modern untuk berpindah branch (menggantikan `git checkout` yang fungsinya terlalu banyak):

```zsh
# Pindah ke branch yang sudah ada
git switch main
git switch fitur/dark-mode-ui

# SHORTCUT TERBAIK: Buat branch baru + langsung pindah ke sana
git switch -c fitur/halaman-checkout

# Kembali ke branch sebelumnya (seperti ⌘+Tab di macOS)
git switch -

# Verifikasi posisi Anda
git branch        # tanda * di branch aktif
git status        # baris pertama: "On branch ..."
```

> 💡 **PRO TIP: `git switch -` adalah `⌘+Tab`-nya Git**
> Sama seperti `⌘+Tab` di macOS yang berpindah ke aplikasi sebelumnya, `git switch -` membawa Anda kembali ke branch yang baru saja Anda tinggalkan. Gunakan ini saat bolak-balik antara `main` dan branch fitur.

---

## 🔀 git merge — Menyatukan Hasil Kerja

Setelah fitur selesai dan diuji di branch terpisah, gabungkan ke `main`:

```zsh
# 1. Kembali ke branch penerima
git switch main

# 2. Pastikan main Anda up-to-date (jika sudah terhubung ke GitHub)
git pull

# 3. Merge branch fitur ke main
git merge fitur/halaman-checkout
```

**Dua jenis merge:**

**Fast-Forward** (kondisi bersih — tidak ada commit baru di `main` sejak branching):
```
Sebelum:  main: A─B─C
                     \
          fitur:      D─E─F

Sesudah:  main: A─B─C─D─E─F
```
Tidak ada merge commit ekstra — rapi.

**3-Way Merge** (ada commit baru di `main`):
```
Sebelum:  main: A─B─C─G
                     \
          fitur:      D─E─F

Sesudah:  main: A─B─C─G─M
                     \ /
                      D─E─F
```
Git membuat "merge commit" `M` secara otomatis.

**Bersihkan branch setelah merge:**
```zsh
git branch -d fitur/halaman-checkout
```

---

## ⚔️ Menangani Merge Conflict

*Merge conflict* terjadi ketika dua branch mengubah baris yang sama di file yang sama. Situasi normal yang tidak perlu ditakuti.

```zsh
git merge fitur/dark-mode-ui
# CONFLICT (content): Merge conflict in src/App.css
# Automatic merge failed; fix conflicts and then commit the result.
```

**Cek file yang conflict:**
```zsh
git status
# both modified: src/App.css
```

**Buka file — temukan marker conflict:**
```css
<<<<<<< HEAD
/* Versi dari main */
body {
  background-color: #ffffff;
  color: #333333;
}
=======
/* Versi dari fitur/dark-mode-ui */
body {
  background-color: #1a1a2e;
  color: #e0e0e0;
}
>>>>>>> fitur/dark-mode-ui
```

**Tiga cara menyelesaikan di macOS:**

**Opsi 1 — Edit manual di VS Code (paling umum):**
VS Code menampilkan tombol "Accept Current Change", "Accept Incoming Change", "Accept Both Changes" tepat di atas setiap blok conflict. Klik yang sesuai, simpan.

**Opsi 2 — Terima salah satu versi via terminal:**
```zsh
# Terima versi main (HEAD)
git checkout --ours src/App.css

# Terima versi branch yang di-merge
git checkout --theirs src/App.css
```

**Opsi 3 — Gunakan visual merge tool:**
```zsh
# Lihat tool yang tersedia
git mergetool --tool-help

# Gunakan VS Code sebagai merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
git mergetool
```

**Selesaikan:**
```zsh
git add src/App.css
git commit -m "Selesaikan merge conflict di App.css — terapkan dark mode"
```

**Batalkan merge jika terlalu kompleks:**
```zsh
git merge --abort
```

---

## 🗄️ git stash — Laci Darurat macOS Anda

Situasi: Anda coding di tengah jalan, belum siap commit, tapi perlu berpindah branch segera. `git stash` adalah "laci darurat" Anda — sembunyikan pekerjaan setengah jadi, tangani urusan mendesak, kembali dan lanjutkan.

```zsh
# Simpan semua perubahan yang belum di-commit
git stash

# Dengan label yang deskriptif (sangat disarankan)
git stash push -m "WIP: animasi hover kartu produk belum selesai"

# Sekarang working tree bersih — bisa pindah branch dengan bebas
git switch main

# ... kerjakan hal mendesak ...

# Kembali dan ambil pekerjaan yang tadi disimpan
git switch fitur/animasi-kartu
git stash pop

# Lihat semua stash yang tersimpan
git stash list
# stash@{0}: On fitur/animasi-kartu: WIP: animasi hover belum selesai

# Ambil stash tanpa menghapusnya
git stash apply stash@{0}

# Hapus semua stash
git stash clear
```

---

## 🎨 Visualisasi Branch dengan Git Graph di VS Code

Untuk pengguna macOS yang bekerja dengan VS Code, ada cara visual yang indah untuk melihat history branch:

1. Install ekstensi **Git Graph** di VS Code (cari di Extensions: `Ctrl+Shift+X`)
2. Di sidebar VS Code, klik ikon Git Graph
3. Anda akan melihat visualisasi grafis dari seluruh history branch — jauh lebih intuitif dari output teks `git log --graph`

Alternatif lain yang populer di komunitas macOS:
- **[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)** — ekstensi VS Code paling powerful untuk Git
- **[Fork](https://git-fork.com)** — aplikasi GUI Git native macOS yang elegan
- **[Tower](https://www.git-tower.com)** — GUI Git premium paling populer di kalangan developer macOS

> 💡 **PRO TIP:**
> GUI tools seperti Fork dan Tower **tidak menggantikan** pemahaman Git via terminal — mereka melengkapinya. Gunakan terminal untuk operasi sehari-hari, gunakan GUI untuk visualisasi history yang kompleks atau saat menyelesaikan merge conflict yang rumit.

---

Branch adalah fitur yang mengubah Git dari sekadar "tombol Undo yang canggih" menjadi mesin kolaborasi kelas dunia.

Satu hal besar tersisa: semua yang kita kerjakan masih hidup di Mac Anda. Di bab berikutnya, kita hubungkan ke GitHub menggunakan **SSH Key** yang terintegrasi dengan **macOS Keychain** — autentikasi yang sekali dikonfigurasi, tidak perlu diulangi selamanya. 🔐

---
*Sebelumnya: [Part 3 — Perintah Dasar Git](Part-03-Perintah-Dasar-Git.md)*
*Selanjutnya: [Part 5 — Koneksi ke GitHub: SSH + Keychain](Part-05-SSH-Keychain-Push-Pull-Clone.md)*
