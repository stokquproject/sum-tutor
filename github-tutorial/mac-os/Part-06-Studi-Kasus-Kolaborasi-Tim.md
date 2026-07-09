![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 40 Mins](https://img.shields.io/badge/Durasi-40_Menit-blue?style=for-the-badge)
![Type: Study Case](https://img.shields.io/badge/Tipe-Studi_Kasus_Nyata-purple?style=for-the-badge)

# 🎬 Studi Kasus: Sehari Penuh Bekerja Seperti Developer macOS Profesional

Lima bab sudah dilalui. Semua alat sudah dikuasai. Sekarang kita satukan semuanya dalam satu simulasi nyata — dari pagi hingga sore, tepat seperti yang terjadi di studio-studio kreatif dan perusahaan teknologi yang menggunakan Mac sebagai senjata utama mereka.

**Skenario**: Anda adalah Frontend Developer di sebuah agensi digital. Tim menggunakan macOS, VS Code, dan GitHub sebagai pusat kolaborasi. Hari ini Anda punya dua tugas: menyelesaikan halaman profil user, dan merespons hotfix mendesak dari klien.

**Karakter**:
- **Anda** — Frontend Developer, menggunakan MacBook Pro M3
- **Tara** — UI/UX Developer, mengerjakan komponen desain di branch berbeda
- **Bagas** — Tech Lead, yang meng-approve Pull Request

Mari mulai.

## 📋 Daftar Isi
- [Babak 1: Pagi — Setup dan Mulai Sprint](#-babak-1-pagi--setup-dan-mulai-sprint)
- [Babak 2: Mengerjakan Fitur dengan Fokus](#-babak-2-mengerjakan-fitur-dengan-fokus)
- [Babak 3: Sinkronisasi dengan Pekerjaan Tim](#-babak-3-sinkronisasi-dengan-pekerjaan-tim)
- [Babak 4: Membuat Pull Request yang Berbicara](#-babak-4-membuat-pull-request-yang-berbicara)
- [Babak 5: Code Review — Seni Menerima Feedback](#-babak-5-code-review--seni-menerima-feedback)
- [Babak 6: Hotfix Mendadak di Tengah Pekerjaan](#-babak-6-hotfix-mendadak-di-tengah-pekerjaan)
- [Babak 7: Merge Conflict dan Resolusinya](#-babak-7-merge-conflict-dan-resolusinya)
- [Cheat Sheet: Referensi Lengkap Git untuk macOS](#-cheat-sheet-referensi-lengkap-git-untuk-macos)

---

## 🌅 Babak 1: Pagi — Setup dan Mulai Sprint

Pukul 09.00. Anda membuka MacBook. Buka Terminal (atau VS Code yang sudah terbuka dari kemarin).

Sebelum menyentuh satu baris kode pun, ritual pagi dimulai:

```zsh
# Masuk ke folder proyek
cd ~/Developer/agensi-website-klien

# Pastikan kita di branch utama
git switch main

# Tarik semua perubahan yang masuk semalam
git pull
```

**Output:**
```
From git@github.com:tim-agensi/website-klien
   c8f3a21..f4d2b91  main -> origin/main
Updating c8f3a21..f4d2b91
Fast-forward
 src/components/Header.jsx  | 24 ++++++++++++++++++------
 src/styles/global.css      |  8 ++++----
 2 files changed, 22 insertions(+), 10 deletions(-)
```

Tara sudah push perubahan semalam — komponen Header sudah diperbarui. Bagus, Anda mulai dari base yang terbaru.

```zsh
# Lihat apa yang berubah untuk konteks
git log --oneline -5
# f4d2b91 (HEAD -> main) Refactor Header — pisahkan navigasi mobile dan desktop
# c8f3a21 Perbaiki warna button CTA sesuai brand guideline
# ...
```

Sekarang buat branch untuk tugas hari ini:

```zsh
git switch -c fitur/halaman-profil-user
# Switched to a new branch 'fitur/halaman-profil-user'
```

Prompt Oh My Zsh langsung menunjukkan:
```
➜  agensi-website-klien git:(fitur/halaman-profil-user) ✗
```

---

## 💻 Babak 2: Mengerjakan Fitur dengan Fokus

Anda membuka VS Code (`code .`) dan mulai bekerja. Beberapa jam berlalu — Anda membuat komponen, mengerjakan styling, menambahkan logika.

Simpan progress secara bertahap — jangan tunggu sampai selesai semua:

```zsh
# Setelah selesai membuat struktur komponen dasar
git status
# modified: src/pages/Profile.jsx (baru dibuat)
# modified: src/styles/profile.css (baru dibuat)

git add src/pages/Profile.jsx
git commit -m "Tambah struktur dasar halaman profil user"

# Setelah menambahkan form edit profil
git add src/pages/Profile.jsx
git commit -m "Tambah form edit nama, bio, dan foto profil"

# Setelah styling selesai
git add src/styles/profile.css
git commit -m "Styling halaman profil — layout responsif untuk mobile dan desktop"

# Push branch ke GitHub untuk backup dan visibilitas tim
git push -u origin fitur/halaman-profil-user
```

> 💡 **PRO TIP: Push Awal untuk Backup**
> Jangan tunggu sampai fitur 100% selesai untuk push. Push setiap hari — minimal sebelum menutup laptop. MacBook tiba-tiba mati? Kopi tumpah ke keyboard? GitHub sudah punya backup pekerjaan Anda.

---

## 🔄 Babak 3: Sinkronisasi dengan Pekerjaan Tim

Setelah istirahat makan siang, Bagas mengirim notifikasi di Slack:

> *"Tara baru merge PR komponen Avatar ke main. Kalau lo lagi bikin halaman profil, pastiin sync dulu biar ga conflict."*

```zsh
# Ambil update terbaru dari GitHub tanpa merge dulu
git fetch origin

# Lihat seberapa jauh branch Anda dari main yang terbaru
git log --oneline main..fitur/halaman-profil-user
# a3f8c12 Styling halaman profil — responsif
# 7b2e904 Tambah form edit profil
# 1d9c331 Tambah struktur dasar halaman profil

git log --oneline fitur/halaman-profil-user..origin/main
# e9f4d21 Tambah komponen Avatar dengan size variants (commit Tara)
```

Satu commit di `main` yang belum ada di branch Anda. Integrasikan sekarang — lebih baik konflik kecil sekarang daripada konflik besar saat PR:

```zsh
# Rebase branch Anda di atas main terbaru
git rebase origin/main
```

**Output jika berjalan mulus:**
```
Successfully rebased and updated refs/heads/fitur/halaman-profil-user.
```

Branch Anda sekarang sudah memiliki komponen Avatar dari Tara. Bahkan bisa langsung menggunakannya:

```zsh
# Tambahkan komponen Avatar ke halaman profil yang Anda buat
# ... edit Profile.jsx di VS Code ...

git add src/pages/Profile.jsx
git commit -m "Integrasikan komponen Avatar Tara ke halaman profil"

# Push ulang (perlu --force-with-lease setelah rebase)
git push --force-with-lease origin fitur/halaman-profil-user
```

---

## 📋 Babak 4: Membuat Pull Request yang Berbicara

Fitur halaman profil sudah lengkap dan teruji. Saatnya minta review.

```zsh
# Pastikan semua sudah di-push
git push origin fitur/halaman-profil-user
```

Buka GitHub, buat Pull Request:

**Title**: `feat: halaman profil user dengan edit dan avatar — closes #23`

**Description**:
```markdown
## 📋 Ringkasan
Implementasi halaman profil user lengkap dengan fitur edit data diri.

## ✨ Perubahan
- `src/pages/Profile.jsx` — halaman profil dengan form edit
- `src/styles/profile.css` — styling responsif (mobile & desktop)
- Menggunakan komponen `Avatar` dari Tara (#21)

## 📱 Screenshot

| Mobile | Desktop |
|--------|---------|
| [screenshot mobile] | [screenshot desktop] |

## ✅ Checklist Testing
- [x] Form edit nama, bio, dan foto berfungsi
- [x] Avatar tampil dengan benar di semua ukuran
- [x] Layout responsif di iPhone SE hingga 4K monitor
- [x] Tidak ada console error di DevTools

## 🔗 Related
- Closes #23
- Menggunakan komponen dari #21 (Avatar by Tara)
```

Di sidebar:
- **Reviewers**: Bagas
- **Labels**: `enhancement`, `ui`

> 💡 **PRO TIP: Screenshot di PR adalah Investasi Waktu**
> Untuk perubahan UI, screenshot adalah cara paling efisien untuk mempercepat review. Reviewer tidak perlu checkout branch Anda untuk melihat hasilnya. Di macOS, `⌘+Shift+4` untuk screenshot area tertentu — seret langsung ke kotak description PR.

---

## 👀 Babak 5: Code Review — Seni Menerima Feedback

Bagas membuka PR Anda dan meninggalkan dua komentar:

**Komentar 1** (pada baris di `Profile.jsx`):
> *"Tolong pakai `useCallback` untuk fungsi `handleSubmit` — kalau tidak, dia akan di-recreate setiap render dan bisa menyebabkan performance issue di form yang kompleks."*

**Komentar 2** (pada `profile.css`):
> *"Warna `#e8e8e8` ini tidak ada di design token kita. Pakai variabel CSS `--color-border-light` yang sudah ada di `global.css`."*

Anda membaca, memahami alasannya, dan mengimplementasikan:

```zsh
# Masih di branch yang sama
git branch
# * fitur/halaman-profil-user

# Edit sesuai feedback Bagas
# ... buka VS Code, perbaiki dua hal tersebut ...

git add src/pages/Profile.jsx src/styles/profile.css
git commit -m "Revisi PR: useCallback untuk handleSubmit, ganti warna ke design token"

git push
```

Commit baru otomatis masuk ke PR yang sama. Bagas mereview ulang dan menulis:

> *"Mantap! ✅ Approved. Merge kalau sudah siap."*

---

## 🚨 Babak 6: Hotfix Mendadak di Tengah Pekerjaan

Pukul 15.30. PR Anda belum di-merge, Anda sedang menambahkan satu detail terakhir di kode — belum siap commit. Tiba-tiba pesan masuk dari Bagas:

> *"Alert! Menu navigasi di mobile hilang total di production setelah merge Header Tara. Klien sudah telepon. Bisa tolong lihat sekarang?"*

Anda perlu berpindah ke `main` segera, tapi kode yang sedang Anda kerjakan belum siap di-commit.

**Solusi: git stash**

```zsh
# Simpan pekerjaan setengah jadi ke "laci darurat"
git stash push -m "WIP: tambah tooltip untuk field bio — belum selesai"

# Working tree sekarang bersih
git status
# nothing to commit, working tree clean

# Pindah ke main dan ambil versi terbaru
git switch main
git pull

# Buat branch hotfix dari main yang bersih
git switch -c hotfix/mobile-nav-hilang
```

Anda investigasi — menemukan bahwa refactor Header dari Tara tidak sengaja menghapus conditional rendering menu mobile. Perbaiki:

```zsh
# Edit Header.jsx — kembalikan conditional rendering yang terhapus
# ... buka VS Code ...

git add src/components/Header.jsx
git commit -m "Hotfix: kembalikan conditional rendering menu navigasi mobile

Commit f4d2b91 tidak sengaja menghapus pengecekan viewport width
untuk menampilkan/menyembunyikan menu burger di mobile.

Dilaporkan oleh: Bagas via Slack — klien sudah konfirmasi issue"

git push -u origin hotfix/mobile-nav-hilang
```

Buat PR hotfix, Bagas approve dalam 3 menit, merge. Production kembali normal.

```zsh
# Bersihkan branch hotfix
git switch main
git pull
git branch -d hotfix/mobile-nav-hilang
git push origin --delete hotfix/mobile-nav-hilang

# Kembali ke branch fitur Anda
git switch fitur/halaman-profil-user

# Ambil kembali pekerjaan yang tadi disimpan
git stash pop
# On branch fitur/halaman-profil-user
# Changes not staged for commit:
#   modified: src/pages/Profile.jsx
```

Persis di titik yang ditinggalkan. Tidak ada yang hilang.

---

## ⚔️ Babak 7: Merge Conflict dan Resolusinya

Saat Anda ingin merge PR halaman profil, GitHub menampilkan:

```
⚠️ This branch has conflicts that must be resolved
```

Hotfix yang baru saja Anda merge juga menyentuh `src/styles/global.css` — di baris yang sama dengan perubahan Anda.

```zsh
git switch main
git pull

git switch fitur/halaman-profil-user
git rebase origin/main
```

**Output:**
```
CONFLICT (content): Merge conflict in src/styles/global.css
error: could not apply 7c3f001... Styling halaman profil — responsif
```

Buka `src/styles/global.css` di VS Code. Anda melihat conflict — tapi VS Code menampilkannya dengan indah:

```css
/* VS Code menampilkan: */
<<<<<<< HEAD (Current Change)
/* Tambahan dari hotfix Tara */
.nav-mobile {
  display: none;
}

@media (max-width: 768px) {
  .nav-mobile {
    display: block;
  }
}
=======
/* Tambahan Anda untuk halaman profil */
.profile-card {
  border: 1px solid var(--color-border-light);
  border-radius: 12px;
}
>>>>>>> 7c3f001 (Styling halaman profil — responsif)
```

Klik **"Accept Both Changes"** di VS Code — kedua blok CSS ini tidak saling bertentangan, keduanya harus dipertahankan.

```zsh
git add src/styles/global.css
git rebase --continue
# Editor terbuka untuk pesan commit — simpan dan tutup (⌘+S lalu ⌘+W di VS Code)

git push --force-with-lease origin fitur/halaman-profil-user
```

GitHub: ✅ **No conflicts**. Bagas merge PR Anda.

```zsh
# Ritual penutup hari
git switch main
git pull

# Sejarah hari ini terdokumentasi rapi
git log --oneline -8
# m7b3e91 (HEAD -> main) Merge PR #24: halaman profil user
# f9c4d21 Merge PR #25: hotfix mobile nav
# f4d2b91 Merge PR #21: komponen Avatar
# ...
```

---

## 📜 Cheat Sheet: Referensi Lengkap Git untuk macOS

```zsh
# ══════════════════════════════════════════
# HOMEBREW & INSTALASI
# ══════════════════════════════════════════
brew install git                              # Install Git via Homebrew
brew upgrade git                              # Update Git ke versi terbaru
git --version                                 # Cek versi

# ══════════════════════════════════════════
# KONFIGURASI
# ══════════════════════════════════════════
git config --global user.name "Nama"          # Set nama
git config --global user.email "email@x.com"  # Set email
git config --global init.defaultBranch main   # Default branch = main
git config --global core.editor "code --wait" # Editor = VS Code
git config --global pull.rebase true          # Pull pakai rebase
git config --global core.excludesfile \
  ~/.gitignore_global                         # Global gitignore
git config --list                             # Lihat semua konfigurasi

# ══════════════════════════════════════════
# SSH + KEYCHAIN
# ══════════════════════════════════════════
ssh-keygen -t ed25519 -C "email@x.com"        # Generate SSH key
ssh-add --apple-use-keychain ~/.ssh/id_ed25519 # Simpan ke Keychain
pbcopy < ~/.ssh/id_ed25519.pub                 # Salin public key ke clipboard
ssh -T git@github.com                          # Test koneksi SSH ke GitHub

# ══════════════════════════════════════════
# MEMULAI REPOSITORI
# ══════════════════════════════════════════
git init                                       # Init repo baru
git clone git@github.com:user/repo.git         # Clone via SSH

# ══════════════════════════════════════════
# SIKLUS KERJA HARIAN
# ══════════════════════════════════════════
git status                                     # Cek kondisi
git diff                                       # Perubahan yang belum di-staging
git diff --staged                              # Perubahan yang sudah di-staging
git add <file>                                 # Staging file tertentu
git add .                                      # Staging semua perubahan
git add -p                                     # Staging interaktif per hunk
git commit -m "pesan"                          # Commit
git commit -am "pesan"                         # Add tracked + commit

# ══════════════════════════════════════════
# MELIHAT SEJARAH
# ══════════════════════════════════════════
git log --oneline                              # Log ringkas
git log --oneline --graph --all --decorate     # Log dengan grafik branch
git log --oneline -5                           # 5 commit terbaru
git log --oneline --author="Nama"              # Filter by author
git log --oneline -- src/file.jsx              # Commit yang menyentuh file ini
git show <hash>                                # Detail satu commit

# ══════════════════════════════════════════
# BRANCH
# ══════════════════════════════════════════
git branch                                     # Lihat branch lokal
git branch -a                                  # Lihat semua branch
git switch <nama>                              # Pindah branch
git switch -c <nama>                           # Buat + pindah ke branch baru
git switch -                                   # Kembali ke branch sebelumnya
git branch -d <nama>                           # Hapus branch (sudah di-merge)
git branch -D <nama>                           # Hapus paksa
git branch -m <nama-baru>                      # Rename branch aktif

# ══════════════════════════════════════════
# MERGE & REBASE
# ══════════════════════════════════════════
git merge <branch>                             # Merge ke branch aktif
git merge --abort                              # Batalkan merge
git rebase origin/main                         # Rebase di atas main terbaru
git rebase --continue                          # Lanjut setelah resolve conflict
git rebase --abort                             # Batalkan rebase

# ══════════════════════════════════════════
# STASH — LACI DARURAT
# ══════════════════════════════════════════
git stash push -m "deskripsi"                  # Simpan pekerjaan sementara
git stash list                                 # Lihat semua stash
git stash pop                                  # Ambil stash terbaru
git stash apply stash@{0}                      # Ambil tanpa hapus dari list
git stash clear                                # Hapus semua stash

# ══════════════════════════════════════════
# REMOTE & GITHUB
# ══════════════════════════════════════════
git remote add origin git@github.com:u/r.git  # Tambah remote SSH
git remote -v                                  # Lihat remote
git remote set-url origin <url>                # Ubah URL remote
git push -u origin <branch>                    # Push pertama kali
git push                                       # Push selanjutnya
git push --force-with-lease                    # Push paksa (aman)
git push origin --delete <branch>              # Hapus branch di remote
git pull                                       # Pull (fetch + rebase/merge)
git fetch origin                               # Ambil tanpa merge

# ══════════════════════════════════════════
# PEMBATALAN & DARURAT
# ══════════════════════════════════════════
git restore <file>                             # Batalkan perubahan unstaged
git restore --staged <file>                    # Keluarkan dari staging
git commit --amend -m "pesan baru"             # Edit commit terakhir (pre-push!)
git revert <hash>                              # Batalkan commit (aman, buat commit baru)
git reset --soft HEAD~1                        # Batalkan commit, keep staging
git reset --mixed HEAD~1                       # Batalkan commit, keep working tree

# ══════════════════════════════════════════
# KHUSUS macOS
# ══════════════════════════════════════════
pbcopy < ~/.ssh/id_ed25519.pub                 # Salin SSH public key ke clipboard
ls -la | grep .DS_Store                        # Cek .DS_Store yang tidak sengaja masuk
⌘ + Shift + .                                  # Toggle hidden files di Finder
```

---

## 🏆 Penutup: Selamat Datang di Tim

Selamat. Anda baru saja menyelesaikan seri tutorial paling lengkap tentang Git di macOS.

Tapi lebih dari itu — Anda telah menjalani pola pikir seorang developer profesional:

- ✅ Memahami Git dan GitHub sebagai ekosistem yang saling melengkapi
- ✅ Menginstal Git dengan benar via Homebrew, siap untuk update seumur hidup
- ✅ Menguasai siklus merekam sejarah: `init → status → add → commit → log`
- ✅ Bekerja dalam dunia paralel dengan Branch, Merge, dan Stash
- ✅ Mengkonfigurasi SSH + Keychain untuk autentikasi yang aman dan permanen
- ✅ Mensimulasikan satu hari penuh: PR, code review, hotfix, merge conflict

macOS adalah platform yang sempurna untuk perjalanan ini. Terminal yang powerful, Keychain yang aman, Homebrew yang elegan, dan ekosistem tools developer yang kaya.

Sekarang buka MacBook Anda, buka Terminal, ketik `git init`, dan mulailah merekam sejarah kode Anda sendiri. Commit pertama selalu yang paling berkesan. 🍎🚀

---
*Sebelumnya: [Part 5 — SSH + Keychain ke GitHub](Part-05-SSH-Keychain-Push-Pull-Clone.md)*

---
> 💡 **Langkah Selanjutnya:**
> - **GitHub Actions** — otomasi CI/CD yang berjalan di cloud saat Anda push kode
> - **Git Hooks** — script yang berjalan otomatis di Mac Anda saat event Git terjadi
> - **Conventional Commits** — standar penulisan pesan commit yang diadopsi tim-tim besar
> - **Open Source** — mulai berkontribusi, cari issue berlabel `good first issue` di GitHub
