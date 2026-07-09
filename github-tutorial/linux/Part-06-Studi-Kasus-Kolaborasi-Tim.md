![Difficulty: Intermediate](https://img.shields.io/badge/Tingkat-Menengah-yellow?style=for-the-badge)
![Time: 40 Mins](https://img.shields.io/badge/Durasi-40_Menit-blue?style=for-the-badge)
![Type: Study Case](https://img.shields.io/badge/Tipe-Studi_Kasus_Nyata-purple?style=for-the-badge)

# 🎬 Studi Kasus: Satu Sprint Penuh Bersama Tim di Linux

Di lima bab sebelumnya, kita sudah menguasai semua alat. Sekarang kita satukan semuanya dalam simulasi yang mencerminkan cara kerja tim software engineering sesungguhnya.

Tidak ada latihan buatan. Setiap langkah di sini adalah cerminan dari apa yang terjadi di tim startup, agensi digital, dan perusahaan teknologi setiap harinya.

**Skenario**: Anda bergabung sebagai Backend Developer baru di tim yang sedang membangun REST API untuk aplikasi manajemen tugas. Server menggunakan Ubuntu. GitHub adalah pusat kolaborasi tim.

**Karakter**:
- **Anda** — developer baru yang baru onboarding
- **Rina** — senior developer, lead teknis
- **Dimas** — frontend developer yang akan konsumsi API Anda

Ambil kopi. Buka terminal. Mulai sprint. ☕

## 📋 Daftar Isi
- [Babak 1: Onboarding — Setup Hari Pertama](#-babak-1-onboarding--setup-hari-pertama)
- [Babak 2: Mengerjakan Tugas di Branch Terpisah](#-babak-2-mengerjakan-tugas-di-branch-terpisah)
- [Babak 3: Menjaga Branch Tetap Sinkron](#-babak-3-menjaga-branch-tetap-sinkron)
- [Babak 4: Membuat Pull Request yang Profesional](#-babak-4-membuat-pull-request-yang-profesional)
- [Babak 5: Code Review — Menerima & Memberikan Feedback](#-babak-5-code-review--menerima--memberikan-feedback)
- [Babak 6: Menyelesaikan Merge Conflict](#-babak-6-menyelesaikan-merge-conflict)
- [Babak 7: Hotfix — Memperbaiki Bug di Production](#-babak-7-hotfix--memperbaiki-bug-di-production)
- [Cheat Sheet: Semua Perintah Git dalam Satu Halaman](#-cheat-sheet-semua-perintah-git-dalam-satu-halaman)

---

## 🔨 Babak 1: Onboarding — Setup Hari Pertama

Rina mengirimkan pesan di Slack:

> *"Selamat bergabung! SSH key lo sudah gue tambahkan sebagai deploy key. Link repo: `git@github.com:tim-api/task-manager-api.git`. Tugas pertama lo ada di Issue #7: tambahkan endpoint `GET /api/tasks/:id`. Pakai branch convention kita ya: `fitur/issue-<nomor>-<deskripsi>`"*

```bash
# 1. Clone repositori tim menggunakan SSH
git clone git@github.com:tim-api/task-manager-api.git

# 2. Masuk ke direktori proyek
cd task-manager-api

# 3. Eksplorasi struktur proyek
ls -la
# routes/
# controllers/
# models/
# tests/
# .gitignore
# README.md
# package.json

# 4. Lihat branch yang ada
git branch -a
# * main
#   remotes/origin/main
#   remotes/origin/fitur/issue-5-auth-middleware   ← branch Rina
#   remotes/origin/fitur/issue-6-task-list-filter  ← branch Dimas

# 5. Lihat sejarah proyek untuk konteks
git log --oneline -10
# c8f3a21 (HEAD -> main, origin/main) Tambah middleware autentikasi JWT
# 7b2e904 Setup endpoint POST /api/tasks
# 3d9c445 Inisialisasi proyek Express.js
```

Anda sudah punya gambaran lengkap. Waktunya bekerja.

---

## 🌿 Babak 2: Mengerjakan Tugas di Branch Terpisah

```bash
# 1. Pastikan main lokal up-to-date
git switch main
git pull

# 2. Buat branch sesuai konvensi tim
git switch -c fitur/issue-7-get-task-by-id

# 3. Konfirmasi posisi
git status
# On branch fitur/issue-7-get-task-by-id
# nothing to commit, working tree clean
```

Anda mulai coding. Buka editor dan tambahkan endpoint baru:

```bash
# Buka file di editor pilihan Anda
nano routes/tasks.js   # atau code . untuk VS Code
```

Setelah menambahkan route dan controller, simpan progress Anda secara bertahap:

```bash
# Cek apa yang berubah
git status
# modified: routes/tasks.js
# modified: controllers/taskController.js
# new file:  tests/task.test.js

# Review perubahan sebelum staging
git diff routes/tasks.js

# Staging dan commit bertahap — pisahkan logika yang berbeda
git add routes/tasks.js controllers/taskController.js
git commit -m "Tambah endpoint GET /api/tasks/:id dengan validasi parameter"

git add tests/task.test.js
git commit -m "Tambah unit test untuk endpoint GET /api/tasks/:id"
```

> 💡 **PRO TIP: Atomic Commits**
> Commit yang baik adalah commit yang *atomic* — setiap commit mewakili satu perubahan logis yang utuh dan bisa di-*revert* secara independen. Jangan campur perubahan yang tidak berkaitan dalam satu commit. Ini membuat `git log`, `git bisect`, dan `git revert` jauh lebih mudah digunakan.

```bash
# Push branch ke GitHub untuk backup dan visibility
git push -u origin fitur/issue-7-get-task-by-id
```

---

## 🔄 Babak 3: Menjaga Branch Tetap Sinkron

Saat Anda coding, Rina sudah merge PR-nya ke `main`. Branch Anda sekarang tertinggal beberapa commit. Ini adalah situasi normal — dan ada cara yang benar untuk menanganinya.

```bash
# Ambil semua perubahan terbaru dari GitHub (tanpa merge dulu)
git fetch origin

# Lihat seberapa jauh branch Anda dengan main
git log --oneline --graph fitur/issue-7-get-task-by-id..origin/main
# Menampilkan commit di main yang belum ada di branch Anda

# Opsi 1: Merge main ke branch Anda (membuat merge commit)
git merge origin/main

# Opsi 2: Rebase branch Anda di atas main (history lebih linear — LEBIH DIREKOMENDASIKAN)
git rebase origin/main
```

**Keunggulan `git rebase` dalam skenario ini:**

```
Sebelum rebase:
  main:    A─B─C─D (D = commit baru Rina)
  fitur:   A─B─C─E─F (E,F = commit Anda)

Sesudah rebase:
  main:    A─B─C─D
  fitur:   A─B─C─D─E─F (E,F sekarang "duduk di atas" D)
```

Branch Anda seolah-olah baru dicabang dari `main` yang terbaru. History lebih bersih saat PR di-merge nantinya.

```bash
# Setelah rebase, push dengan force (diperlukan karena history ditulis ulang)
# Gunakan --force-with-lease, bukan --force biasa — lebih aman!
git push --force-with-lease origin fitur/issue-7-get-task-by-id
```

> ⚠️ **PERINGATAN:**
> Gunakan `git rebase` **hanya pada branch pribadi Anda sendiri** yang belum di-review orang lain. Jangan pernah rebase branch yang sudah dipakai orang lain — ini akan mengacaukan history mereka.

---

## 📋 Babak 4: Membuat Pull Request yang Profesional

Fitur sudah selesai dan teruji. Saatnya minta direview.

```bash
# Pastikan branch terbaru sudah di-push
git push origin fitur/issue-7-get-task-by-id
```

Buka GitHub dan buat Pull Request dengan konten berikut:

**Title**: `feat: tambah endpoint GET /api/tasks/:id — closes #7`

**Description**:
```markdown
## Ringkasan
Implementasi endpoint untuk mengambil satu task berdasarkan ID.

## Perubahan
- `routes/tasks.js` — tambah route `GET /api/tasks/:id`
- `controllers/taskController.js` — tambah fungsi `getTaskById`
- `tests/task.test.js` — 4 test case baru

## Test Coverage
- ✅ Return 200 + data task jika ID valid
- ✅ Return 404 jika task tidak ditemukan
- ✅ Return 400 jika format ID bukan integer
- ✅ Return 401 jika token tidak disertakan

## Cara Review
1. `git checkout fitur/issue-7-get-task-by-id`
2. `npm install && npm test`
3. Test manual: `curl -H "Authorization: Bearer <token>" localhost:3000/api/tasks/1`

## Catatan
Validasi ID menggunakan `parseInt()` + `isNaN()` — sama dengan pattern yang sudah ada di endpoint lain.
```

**Di sidebar PR:**
- **Reviewers**: tambahkan Rina
- **Labels**: `enhancement`, `ready for review`
- **Linked issues**: `#7` (GitHub otomatis akan close issue #7 saat PR di-merge)

---

## 👀 Babak 5: Code Review — Menerima & Memberikan Feedback

Rina membuka PR Anda dan meninggalkan komentar:

> *"Logic-nya bagus! Tapi untuk error handling, sebaiknya kita gunakan helper `createError()` dari `utils/errors.js` yang sudah ada, bukan throw Error biasa. Consistent sama codebase kita yang lain."*

Anda menerima feedback itu dan langsung perbaiki:

```bash
# Anda masih di branch yang sama
git branch
# * fitur/issue-7-get-task-by-id

# Edit file sesuai saran Rina
nano controllers/taskController.js

# Staging dan commit
git add controllers/taskController.js
git commit -m "Refactor: gunakan createError() helper untuk konsistensi error handling"

# Push — commit ini otomatis masuk ke PR yang sama
git push
```

Rina mereview commit terbaru Anda:

> *"Sempurna! ✅ Approved."*

---

## ⚔️ Babak 6: Menyelesaikan Merge Conflict

Tepat saat Rina ingin merge PR Anda, GitHub menampilkan:

```
⚠️ This branch has conflicts that must be resolved
```

Ternyata Dimas baru merge PR-nya ke `main`, dan ia juga memodifikasi `controllers/taskController.js` untuk menambahkan filtering — di baris yang sama dengan yang Anda ubah.

```bash
# 1. Update main lokal
git switch main
git pull

# 2. Kembali ke branch Anda
git switch fitur/issue-7-get-task-by-id

# 3. Rebase di atas main terbaru untuk mendapat conflict di sini (bukan di main)
git rebase origin/main
```

**Output:**
```
Auto-merging controllers/taskController.js
CONFLICT (content): Merge conflict in controllers/taskController.js
error: could not apply a3f8c12... Refactor: gunakan createError() helper
hint: Resolve all conflicts manually, use "git add <conflicted_files>"
hint: and then run "git rebase --continue".
```

```bash
# 4. Cek file yang conflict
git status
# both modified: controllers/taskController.js

# 5. Buka dan selesaikan conflict
nano controllers/taskController.js
```

Di dalam file, Anda temukan:

```javascript
<<<<<<< HEAD (commit Dimas di main)
const { createError } = require('../utils/errors');
const { filterTasks } = require('../utils/filters');

exports.getTaskById = async (req, res, next) => {
  try {
    const id = parseInt(req.params.id);
    if (isNaN(id)) throw new Error('Invalid ID format');
=======
const { createError } = require('../utils/errors');

exports.getTaskById = async (req, res, next) => {
  try {
    const id = parseInt(req.params.id);
    if (isNaN(id)) return next(createError(400, 'ID harus berupa angka'));
>>>>>>> a3f8c12 (Refactor: gunakan createError() helper)
```

Setelah menganalisis: Anda perlu **kedua perubahan** — import `filterTasks` dari Dimas, dan pengunaan `createError` dari Anda.

```javascript
// Hasil setelah conflict diselesaikan — menggabungkan keduanya
const { createError } = require('../utils/errors');
const { filterTasks } = require('../utils/filters');  // dari Dimas

exports.getTaskById = async (req, res, next) => {
  try {
    const id = parseInt(req.params.id);
    if (isNaN(id)) return next(createError(400, 'ID harus berupa angka'));  // versi Anda
```

```bash
# 6. Selesaikan rebase
git add controllers/taskController.js
git rebase --continue
# Editor akan terbuka untuk pesan commit — simpan dan tutup

# 7. Push dengan force-with-lease
git push --force-with-lease origin fitur/issue-7-get-task-by-id
```

GitHub sekarang menampilkan: ✅ **"This branch has no conflicts"**

Rina merge PR Anda.

---

## 🚨 Babak 7: Hotfix — Memperbaiki Bug di Production

Satu jam setelah PR Anda di-merge, Dimas laporan:

> *"Endpoint `/api/tasks/:id` return 500 kalau ID-nya string (bukan angka) di production. Bisa hotfix sekarang?"*

Ini situasi darurat. Kode sudah di `main` dan sedang dipakai user.

```bash
# 1. Pastikan main lokal mencerminkan production
git switch main
git pull

# 2. Buat branch hotfix dari main (BUKAN dari branch fitur apapun)
git switch -c hotfix/500-error-invalid-task-id

# 3. Perbaiki bug — ternyata perlu tambahkan early return
nano controllers/taskController.js

# 4. Test lokal
npm test

# 5. Commit
git add controllers/taskController.js
git commit -m "Hotfix: perbaiki 500 error saat ID task bukan angka

Sebelumnya: parseInt('abc') = NaN tidak ditangkap dengan benar
Sesudah: tambahkan guard clause di awal fungsi sebelum query DB

Dilaporkan oleh: Dimas via Slack"

# 6. Push dan buat PR — minta Rina approve cepat
git push -u origin hotfix/500-error-invalid-task-id
```

> 💡 **PRO TIP: Pesan Commit Hotfix yang Baik**
> Untuk hotfix, tambahkan konteks sebanyak mungkin di body commit: apa yang rusak, kenapa rusak, dan bagaimana Anda memperbaikinya. Commit ini akan muncul di sejarah dan berguna saat post-mortem.

Rina approve, merge. Done. Production aman.

```bash
# Bersihkan branch hotfix
git switch main
git pull
git branch -d hotfix/500-error-invalid-task-id
git push origin --delete hotfix/500-error-invalid-task-id
```

---

## 📜 Cheat Sheet: Semua Perintah Git dalam Satu Halaman

```bash
# ═══════════════════════════════════════
# INSTALASI & KONFIGURASI
# ═══════════════════════════════════════
sudo apt install git -y                          # Install (Ubuntu/Debian)
git config --global user.name "Nama"             # Set identitas
git config --global user.email "email@mail.com"  # Set email
git config --global init.defaultBranch main      # Default branch = main
git config --global core.editor nano             # Set editor default
git config --global pull.rebase true             # Pull pakai rebase
git config --list                                # Lihat semua konfigurasi

# ═══════════════════════════════════════
# SSH KEY
# ═══════════════════════════════════════
ssh-keygen -t ed25519 -C "email@mail.com"        # Generate SSH key
cat ~/.ssh/id_ed25519.pub                        # Tampilkan public key
ssh -T git@github.com                            # Test koneksi SSH ke GitHub

# ═══════════════════════════════════════
# MEMULAI REPOSITORI
# ═══════════════════════════════════════
git init                                         # Init repo baru
git clone git@github.com:user/repo.git           # Clone via SSH

# ═══════════════════════════════════════
# SIKLUS KERJA HARIAN
# ═══════════════════════════════════════
git status                                       # Cek kondisi
git diff                                         # Lihat perubahan unstaged
git diff --staged                                # Lihat perubahan staged
git add <file>                                   # Staging file tertentu
git add .                                        # Staging semua perubahan
git commit -m "pesan"                            # Commit
git commit -am "pesan"                           # Add tracked files + commit

# ═══════════════════════════════════════
# MELIHAT SEJARAH
# ═══════════════════════════════════════
git log --oneline                                # Log ringkas
git log --oneline --graph --all --decorate       # Log dengan grafik branch
git log --oneline -5                             # 5 commit terbaru
git log --oneline --grep="kata kunci"            # Cari di pesan commit
git show <hash>                                  # Detail satu commit

# ═══════════════════════════════════════
# BRANCH
# ═══════════════════════════════════════
git branch                                       # Lihat branch lokal
git branch -a                                    # Lihat semua branch
git branch -v                                    # Lihat branch + commit terakhir
git switch <nama>                                # Pindah branch
git switch -c <nama>                             # Buat + pindah ke branch baru
git switch -                                     # Kembali ke branch sebelumnya
git branch -d <nama>                             # Hapus branch (sudah di-merge)
git branch -D <nama>                             # Hapus branch paksa
git branch -m <nama-baru>                        # Rename branch aktif

# ═══════════════════════════════════════
# MERGE & REBASE
# ═══════════════════════════════════════
git merge <branch>                               # Merge ke branch aktif
git merge --abort                                # Batalkan merge
git rebase origin/main                           # Rebase di atas main terbaru
git rebase --continue                            # Lanjutkan setelah resolve conflict
git rebase --abort                               # Batalkan rebase

# ═══════════════════════════════════════
# STASH
# ═══════════════════════════════════════
git stash push -m "deskripsi"                    # Simpan pekerjaan sementara
git stash list                                   # Lihat semua stash
git stash pop                                    # Ambil stash terbaru + hapus
git stash apply stash@{0}                        # Terapkan stash tanpa hapus

# ═══════════════════════════════════════
# REMOTE & GITHUB
# ═══════════════════════════════════════
git remote add origin git@github.com:user/repo.git  # Tambah remote
git remote -v                                    # Lihat remote
git remote set-url origin <url-baru>             # Ubah URL remote
git push -u origin <branch>                      # Push pertama kali
git push                                         # Push selanjutnya
git push --force-with-lease                      # Push paksa (aman)
git push origin --delete <branch>               # Hapus branch di remote
git pull                                         # Pull (fetch + merge/rebase)
git fetch origin                                 # Ambil tanpa merge

# ═══════════════════════════════════════
# PEMBATALAN & DARURAT
# ═══════════════════════════════════════
git restore <file>                               # Batalkan perubahan unstaged
git restore --staged <file>                      # Keluarkan dari staging area
git commit --amend -m "pesan baru"               # Edit commit terakhir (pre-push!)
git revert <hash>                                # Batalkan commit dengan commit baru
git reset --soft HEAD~1                          # Batalkan commit, keep staging
git reset --mixed HEAD~1                         # Batalkan commit, keep working tree
git bisect start/good/bad                        # Cari commit penyebab bug
```

---

## 🏆 Penutup: Dari Nol ke Siap Industri

Selamat. Anda telah menyelesaikan perjalanan lengkap — bukan sekadar belajar perintah, tapi menjalani pola pikir seorang developer profesional:

- ✅ Memahami filosofi Git dan mengapa ia lahir di ekosistem Linux
- ✅ Menginstal dan mengkonfigurasi Git secara optimal di berbagai distro
- ✅ Menguasai siklus `init → status → add → commit → log`
- ✅ Menggunakan branch, merge, dan rebase untuk workflow paralel
- ✅ Mengkonfigurasi autentikasi SSH yang aman dan permanen
- ✅ Menjalani simulasi sprint tim nyata: PR, code review, conflict, hotfix

Git adalah alat yang tumbuh bersama Anda. Semakin banyak Anda menggunakannya, semakin banyak pola dan shortcut yang akan Anda temukan sendiri. Setiap `git log --oneline` yang Anda baca adalah sejarah yang Anda tulis sendiri.

Sekarang buka terminal, buat repositori baru, dan mulailah menulis sejarahmu. Commit pertama selalu yang paling berkesan. 🐧🚀

---
*Sebelumnya: [Part 5 — SSH, Push, Pull & Clone ke GitHub](Part-05-SSH-Push-Pull-Clone-GitHub.md)*

---
> 💡 **Langkah Selanjutnya:**
> - Pelajari **GitHub Actions** untuk CI/CD otomatis di Linux server
> - Pelajari **Git Hooks** — script yang berjalan otomatis saat event Git terjadi (pre-commit, post-merge)
> - Eksplorasi **Git Bisect** untuk mencari commit penyebab bug secara binary search
> - Kontribusi ke proyek open source — mulai dari issue berlabel `good first issue`
